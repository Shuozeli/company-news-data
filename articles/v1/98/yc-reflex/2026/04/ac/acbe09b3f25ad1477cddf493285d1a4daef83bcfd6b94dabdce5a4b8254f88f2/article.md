---
schema_version: "1.0.0"
document_id: "acbe09b3f25ad1477cddf493285d1a4daef83bcfd6b94dabdce5a4b8254f88f2"
company_key: "yc-reflex"
company: "Reflex"
source_id: "yc-reflex-news-import-a39f8c531c08"
canonical_url: "https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9/"
published_at: "2026-04-30T00:00:00+00:00"
first_seen_at: "2026-07-22T23:16:11.777394+00:00"
fetched_at: "2026-07-28T21:45:24.644708+00:00"
content_hash: "sha256:675fda09879a3d42e8d14e9e7d2c7bac161f70303287317446341ff03c6d35a4"
---

# Upgrading Reflex Apps from 0.8 to 0.9

[Upgrading Reflex Apps from 0.8 to 0.9](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#upgrading-reflex-apps-from-0.8-to-0.9)


[v0.9.0](https://github.com/reflex-dev/reflex/releases/tag/v0.9.0) moves event processing to the backend, makes database support an optional extra, collapses production into a single port, and turns off auto-generated state setters by default. Here's what to change.


[TL;DR](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#tl;dr) Change


What to do


Database deps are now an extra


` pip install 'reflex\[db\]~=0.9.0'` and set


` db_url` explicitly


` state_auto_setters` defaults to


` False` Define


` set_*` event handlers explicitly, or opt back in temporarily


Production runs on a single port


Access


` --env prod` apps on


` --frontend-port` (default


` 3000` )


` App.overlay_component` removed


Use


` extra_app_wraps`


` rx.Base` and


` PydanticV1` removed


Migrate to dataclasses or Pydantic V2


` App.process_background` removed


Use


` app.event_processor`


` codeblock` in


` rx.markdown` removed


Use


` pre`


` reflex-enterprise` users


Upgrade to


` >= 0.7.0.post1`


[1. Install with the right extras](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#1.-install-with-the-right-extras)


` pydantic` ,


` sqlmodel` , and


` alembic` are no longer base dependencies. If you use


` rx.Model` or any database helpers, install the


` db` extra:


Or in


` pyproject.toml` :


[2. Set db_url explicitly](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#2.-set-db_url-explicitly)


` db_url` no longer defaults to a local SQLite file. Declare it in


` rxconfig.py` :


[3. Define your own setters](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#3.-define-your-own-setters)


` state_auto_setters` defaults to


` False` , so Reflex no longer generates


` set_count` for you.


**Before:**


**After:**


If a state field has many call sites, you can opt back in temporarily:


This is deprecated and emits a warning. Don't reach for it as a long-term solution — define explicit handlers and remove the flag before v1.0.


[4. Production runs on a single port](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#4.-production-runs-on-a-single-port)


The


` --single-port` flag is gone —


` --env prod` now always serves frontend and backend on one port.


The frontend is served by Starlette


` StaticFiles` . Default ports depend on the running mode:


- **Fullstack** (frontend + backend, the default): both share


` --frontend-port` (


` 3000` )


- **Frontend only** :


` --frontend-port` (


` 3000` )


- **Backend only** :


` --backend-port` (


` 8000` )


Update any reverse proxy or load balancer that split traffic across separate frontend and backend ports.


If you call


` prerequisites.check_running_mode()` in tooling, it now returns a single


` RunningMode` enum (


` FRONTEND_ONLY` ,


` BACKEND_ONLY` ,


` FULLSTACK` ) instead of a


` (frontend, backend)` tuple.


[5. Replace removed APIs](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#5.-replace-removed-apis)


**` App.overlay_component` → ` extra_app_wraps` :**


` extra_app_wraps` is a


` dict\[tuple\[int, str\], Callable\[\[bool\], Component | None\]\]` — keyed by a


` (priority, name)` tuple, with a callable that receives a


` stateful: bool` and returns the wrapper component (or


` None` ). Wrappers must render their


` children` , so use


` rx._x.memo` to declare one:


**` rx.Base` and ` PydanticV1` are gone.** Migrate model classes to dataclasses or Pydantic V2.


` rx.State` is unaffected — it moved off Pydantic in 0.8.


**` codeblock` in ` rx.markdown` → ` pre` :**


**` App.process_background` → ` app.event_processor` .**


` App._background_tasks` becomes


` App.event_processor._tasks` .


**` _substate_key` / ` _split_substate_key` are deprecated.** Use


` rx.BaseStateToken` to address state from outside an event handler — for example with


` app.modify_state` :


**Other internal renames:**


- ` State.class_substates` →


` State.get_substates()`
- ` Event.token` removed — the token lives on


` EventContext`
- ` Event.substate_token` →


` Event.state_cls`
- ` StateManager.create(state=...)` no longer takes a


` state=` kwarg


- ` fix_events()` and


` get_hydrate_event()` removed


- ` AppHarness` lost


` state_manager` ,


` get_state()` ,


` set_state()` ,


` modify_state()` ,


` poll_for_clients()` ,


` _reset_backend_state_manager()` — drive state through events in tests instead


[6. Bump reflex-enterprise](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#6.-bump-reflex-enterprise)


[7. New APIs worth a look](https://reflex.dev/blog/upgrading-reflex-0-8-to-0-9#7.-new-apis-worth-a-look)


- **` rx.upload_files_chunk`** (


[#6190](https://github.com/reflex-dev/reflex/pull/6190) ) — streams chunks instead of buffering whole files


- **` @rx._x.memo`** (


[#6192](https://github.com/reflex-dev/reflex/pull/6192) , experimental) — JS-level memoization for components and pure functions


- **` backend_path` config** (


[#6338](https://github.com/reflex-dev/reflex/pull/6338) ) — prefix backend routes for path-based proxies


- **In-memory state expiration** (


[#6201](https://github.com/reflex-dev/reflex/pull/6201) ) and a


**Redis state-expiry event** (


[#6194](https://github.com/reflex-dev/reflex/pull/6194) )


- **Recharts ` Defs`** (


[#6322](https://github.com/reflex-dev/reflex/pull/6322) ) and


**dropdown cells** in the data editor (


[#6139](https://github.com/reflex-dev/reflex/pull/6139) )


See the


[roadmap](https://github.com/reflex-dev/reflex/issues/2727) for what's coming next.
