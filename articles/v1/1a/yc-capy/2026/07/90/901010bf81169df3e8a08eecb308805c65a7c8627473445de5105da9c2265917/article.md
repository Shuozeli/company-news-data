---
schema_version: "1.0.0"
document_id: "901010bf81169df3e8a08eecb308805c65a7c8627473445de5105da9c2265917"
company_key: "yc-capy"
company: "Capy"
source_id: "yc-capy-news-import-ccb8c20193bf"
canonical_url: "https://scrapybara.com/blog/unified-action-space"
published_at: null
first_seen_at: "2026-07-23T04:45:19.830543+00:00"
fetched_at: "2026-07-28T21:40:00.658555+00:00"
content_hash: "sha256:eafdf35d2aca5649d8a3d541d1880eae8eddf9ac0db61b6ac3baad9b3f93a34c"
---

# Unifying the Computer Use Action Space

## Computer use models are evolving rapidly—without a clear standard specification for computer control actions.


Since the launch of[Claude 3.5 Sonnet Computer Use Beta](https://www.anthropic.com/news/3-5-models-and-computer-use) in October 2024, we have seen dozens of computer use models launch from tech giants like ByteDance to university labs. What do all of these models have in common? At a high level, they can all generate functions calls that control graphical interfaces with mouse and keyboard commands. Here are some examples of commands in natural language:


*Left click at x = 100, y = 200* *Type "Hello, world!"* *Move mouse to x = 200, y = 300 and scroll down 100px*


Every computer use model has been trained on a set of action types (left click, type, move mouse, scroll) and parameters (coordinates, scroll amount). This means that the models are really only optimized to control computers in its native format. For some models, the action format is decently defined and documented: Anthropic's[Claude 3.7 Sonnet](https://docs.anthropic.com/en/docs/models/sonnet-3-5) only outputs structured tool calls strictly constrained by its tool definitions. For left clicks, it will always use *left_click* and output a coordinate array. Other models like ByteDance's[UI-TARS](https://github.com/bytedance/UI-TARS) , however, and put the onus on the developer to parse the command. These models often randomly output function arguments in different formats and units from iteration to iteration. With one prompt the model would output *command* to press the command hotkey on MacOS; with another, the same model acting in the same environment could output *meta* . In production environments, it is a nightmare to catch every edge case.


UI-TARS even has multiple action spaces!


Moreover, every single model release has introduced a new idiosyncratic action space. Claude's *left_click* is expected to behave like UI-TAR's *click* . Even incremental upgrades from the same lab have different action spaces. Anthropic's latest Claude 3.7 Sonnet completely revamped the action space from its predecessor, 3.5 Sonnet, introducing *left_mouse_down, scroll, wait* , and more action types. More unexpectedly, the primitive action of clicking at a coordinate is now one tool call instead of moving the mouse first and clicking. Accommodating more action types is simple, but it is a lot trickier to handle a change in the semantics of existing actions. At this point, we are fairly certain that computer use models are being trained at other labs. Who knows what other action spaces we will see in the future?


Claude 3.7 Sonnet's action space is a drastic departure from its predecessor


## Developing a new approach


As an infrastructure provider sitting at the intersection of computer use models and virtual execution environments, we have had the unique opportunity to explore multiple approaches to deploying agents under one endpoint.


We first started with a barebones integration with Anthropic's Python SDK, adding basic utility like *ToolCollection* that directly connected to our remote instances and executed commands one-to-one: our instances directly accepted the same action space as 3.5 Sonnet. But even simple tasks, like running a small sampling loop, required huge chunks of repetitive boilerplate code. To tackle this inefficiency, we developed the[Act SDK](https://docs.scrapybara.com/act-sdk) , effectively abstracting LLM handling away from the developer. At the same time, we developed a general message format that could support different models later down the road. However, computer use action execution remained the same on our instances.


Legacy Anthropic connector using Anthropic's action space


When we tried integrating open source models like UI-TARS, we ran into the action space problem. Our first approach was messy: we created a separate endpoint just for UI-TARS that would effectively execute the same actions with different inputs. We quickly realized that this approach would not scale, as more models = more endpoints. Yikes.


On our second attempt, we simply added more instance actions on the same endpoint. Suddenly, the input type accepted *left_click, click_left, click* which all meant the same thing! Parameters would be different as well: some models outputted coordinates as int arrays, others outputted x and y explicitly. Suddenly, we were back to square one and went back to the drawing board.


## A new standard


Today, we are excited to introduce a new unified action space, now available on our[/computer endpoint](https://docs.scrapybara.com/api-reference/instance/computer) . The Act SDK now translates model outputs to our action specification before executing corresponding actions on the instances.


To reconcile semantic differences between model outputs, we first broke down actions into their most basic forms: composable actions like move mouse, click mouse, drag mouse, scroll, press key, type text, and additional utility functions like wait, take screenshot, and get cursor position. For each action, we defined required parameters (move mouse must take coordinates) and optional parameters (click mouse does not necessarily need coordinates to click in place) for modularity and extensibility across different model types. The goal was simple: to support as many action types as possible while maintaining compatability with all models. We believe that our specification is a step in the right direction towards unifying model actions and urge developers and model makers to adopt it.


Here is the full specification as Pydantic models with validators:


```text
# Mouse Actions
class     MoveMouseAction  (  BaseModel  )  :
action  :   Literal  [  "move_mouse"  ]
coordinates  :   List  [  int  ]      # [x, y]
hold_keys  :   Optional  [  List  [  str  ]  ]     =     None


@field_validator  (  "coordinates"  )
@classmethod
def     check_coordinates_length  (  cls  ,   v  )  :
if     len  (  v  )     !=     2  :
raise   ValueError  (  "coordinates must be a list of exactly 2 integers [x, y]"  )
return   v


class     ClickMouseAction  (  BaseModel  )  :
action  :   Literal  [  "click_mouse"  ]
button  :   Literal  [  "left"  ,     "right"  ,     "middle"  ,     "back"  ,     "forward"  ]
click_type  :   Optional  [  Literal  [  "down"  ,     "up"  ,     "click"  ]  ]     =     "click"
coordinates  :   Optional  [  List  [  int  ]  ]     =     None      # [x, y], optional for up/down
num_clicks  :   Optional  [  int  ]     =     1      # Only relevant for full clicks
hold_keys  :   Optional  [  List  [  str  ]  ]     =     None


@field_validator  (  "num_clicks"  )
@classmethod
def     num_clicks_only_for_click  (  cls  ,   v  ,   info  )  :
click_type   =   info  .  data  .  get  (  "click_type"  )
if   click_type   is     not     None     and   click_type   !=     "click"     and   v   !=     1  :
raise   ValueError  (  "num_clicks should only be set for click_type='click'"  )
return   v


@field_validator  (  "coordinates"  )
@classmethod
def     check_coordinates_length  (  cls  ,   v  )  :
if   v   is     not     None     and     len  (  v  )     !=     2  :
return   v


class     DragMouseAction  (  BaseModel  )  :
action  :   Literal  [  "drag_mouse"  ]
path  :   List  [  List  [  int  ]  ]      # List of [x, y] points
hold_keys  :   Optional  [  List  [  str  ]  ]     =     None


@field_validator  (  "path"  )
@classmethod
def     check_path  (  cls  ,   v  )  :
if     len  (  v  )     <     2  :
raise   ValueError  (  "path must contain at least 2 points for a drag"  )
for   point   in   v  :
if     len  (  point  )     !=     2  :
raise   ValueError  (  "each point in path must be a list of 2 integers [x, y]"  )
return   v


class     ScrollAction  (  BaseModel  )  :
action  :   Literal  [  "scroll"  ]
coordinates  :   Optional  [  List  [  int  ]  ]     =     None     # [x, y], optional
delta_x  :   Optional  [  float  ]     =     0.0      # Horizontal scroll amount
delta_y  :   Optional  [  float  ]     =     0.0      # Vertical scroll amount
hold_keys  :   Optional  [  List  [  str  ]  ]     =     None


@field_validator  (  "coordinates"  )
@classmethod
def     check_coordinates_length  (  cls  ,   v  )  :
if   v   is     not     None     and     len  (  v  )     !=     2  :
return   v


@model_validator  (  mode  =  'after'  )
def     check_scroll_amount  (  self  )  :
if   self  .  delta_x   ==     0.0     and   self  .  delta_y   ==     0.0  :
raise   ValueError  (  "at least one of delta_x or delta_y must be non-zero"  )
return   self


# Keyboard Actions
class     PressKeyAction  (  BaseModel  )  :
action  :   Literal  [  "press_key"  ]
keys  :   List  [  str  ]      # Simultaneous key press
duration  :   Optional  [  float  ]     =     None      # Seconds, if None, quick press and release


@field_validator  (  "keys"  )
@classmethod
def     check_keys_not_empty  (  cls  ,   v  )  :
if     not   v  :
raise   ValueError  (  "keys list cannot be empty"  )
return   v


class     TypeTextAction  (  BaseModel  )  :
action  :   Literal  [  "type_text"  ]
text  :     str
hold_keys  :   Optional  [  List  [  str  ]  ]     =     None


@field_validator  (  "text"  )
@classmethod
def     check_text_not_empty  (  cls  ,   v  )  :
if     not   v  :
raise   ValueError  (  "text cannot be empty"  )
return   v


# Utility Actions
class     WaitAction  (  BaseModel  )  :
action  :   Literal  [  "wait"  ]
duration  :     float      # Seconds


@field_validator  (  "duration"  )
@classmethod
def     check_duration_positive  (  cls  ,   v  )  :
if   v   <=     0  :
raise   ValueError  (  "duration must be positive"  )
return   v


class     TakeScreenshotAction  (  BaseModel  )  :
action  :   Literal  [  "take_screenshot"  ]


class     GetCursorPositionAction  (  BaseModel  )  :
action  :   Literal  [  "get_cursor_position"  ]


# Direct union of all action types
ComputerRequest   =   Annotated  [
Union  [
MoveMouseAction  ,
ClickMouseAction  ,
DragMouseAction  ,
ScrollAction  ,
PressKeyAction  ,
TypeTextAction  ,
WaitAction  ,
TakeScreenshotAction  ,
GetCursorPositionAction  ,
]  ,
Field  (  discriminator  =  'action'  )
]
```


## Looking ahead


Our computer action space is a dynamic specification that will continue to evolve as computer use capabilities improve. You can find the latest specification in our[documentation](https://docs.scrapybara.com/ubuntu) . In the meantime, we will keep working with our developer community to maintain the specification and make it easier to use computer use models. We hope model makers can start adopting our specification for new computer use models. If you have feedback or are interested in contributing to the specification, please join our[Discord](https://discord.gg/s4bPUVFXqA) and follow us on[X](https://x.com/scrapybara) .


## GET STARTED TODAY


Visit our docs and join our Discord community to see what others are building with Scrapybara. We would love to hear your feedback and see what you build next!
