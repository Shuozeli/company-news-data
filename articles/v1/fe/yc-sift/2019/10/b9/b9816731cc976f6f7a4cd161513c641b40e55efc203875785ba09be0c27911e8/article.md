---
schema_version: "1.0.0"
document_id: "b9816731cc976f6f7a4cd161513c641b40e55efc203875785ba09be0c27911e8"
company_key: "yc-sift"
company: "Sift"
source_id: "yc-sift-news-import-56a09e055dd6"
canonical_url: "https://engineering.sift.com/introducing-resourcerer-declarative-react-data-fetching-for-rest-apis/"
published_at: "2019-10-17T21:30:30+00:00"
first_seen_at: "2026-07-24T13:26:21.656972+00:00"
fetched_at: "2026-07-28T21:33:49.818370+00:00"
content_hash: "sha256:47648d4cdc10f2142f883dc5a6f2b0c1bc23b5419cea886a6ffd77f74daceb62"
---

# Introducing Resourcerer: Declarative React Data-Fetching for REST APIs

Post category:


[Articles](https://engineering.sift.com/articles/)


# [Introducing Resourcerer: Declarative React Data-Fetching for REST APIs](https://engineering.sift.com/introducing-resourcerer-declarative-react-data-fetching-for-rest-apis/)


Sift


• October 17, 2019


We are excited to announce the public release of a package we’ve been using internally at Sift to handle our client-side data fetching for over two years now:[resourcerer](https://github.com/SiftScience/resourcerer) . Resourcerer contains a React[higher-order component](https://reactjs.org/docs/higher-order-components.html) (HOC) called` withResources` that allows you to easily and declaratively manage your components’ data flows, while also handling loading states and app-wide resource caching.


Here’s what it looks like:


```text
import ErrorState from 'components/error_state/error_state.jsx';
import Loader from 'components/loader/loader.jsx';
import React from 'react';
import {withResources} from 'resourcerer';


@withResources((props, ResourceKeys) => ({
// string<ResourceKey>: object<ResourceOptions>
[ResourceKeys.TODOS]: {}
}))
class TodosComponent extends React.Component {
render() {
return (
<div classname='TodosComponent'>
{this.props.isLoading ? <Loader /> : null}


// don't forget about your graceful error states!
{this.props.hasErrored ? <ErrorState message='An error occurred.' /> : null}


{this.props.hasLoaded ? (
<ul>
{this.props.todosCollection.map((todoModel) => (
<li key={todoModel.id}>{todoModel.get('name')}</li>
))}
</ul>
) : null}
</div>
);
}
}


```


The` ResourceKeys.TODOS` string, representing our TODOS resource, is available in the executor function after[adding it to a configuration file](https://github.com/SiftScience/resourcerer#tutorial) .


Easy enough! And if you have another component on the page that uses` withResources` for the same resource, only a single request will be made, and both components will get access to the same resource object.


But we can also pass a wide array of options as part of the` resourceOptions` object, for example:


```text
import React from 'react';
import {withResources} from 'resourcerer';


@withResources((props, {TODOS, USERS}) => ({
[TODOS]: {
// this get stringified as request query parameters
data: {user_id: props.userId},
// re-renders the components if the collection updates
listen: true,
// pass down the specific status code of the request, for example, for
// handling a 404 or 202
status: true
}
}))
class TodosComponent extends React.Component {}


```


Here our resource depends on the` userId` prop. If, say, the user clicks on a link and changes the value of` props.userId` , our` TodosComponent` will automatically go back into a loading state (` this.props.isLoading === true` ) as the new user resource gets requested. When that new resource returns,` TodosComponent` will go back into a loaded state. If the user decides to then go back to the original` props.userId` , the previous collection will still be in the cache (within a certain grace period) and available immediately, without re-requesting.


## Critical vs. Noncritical Resources


One thing to stress is how important it is to separate your critical from your non-critical resources, where we only wait to render content until our critical resources return and allow non-critical ones to render as they come.` resourcerer` makes this a cinch:


```text
import React from 'react';
import {withResources} from 'resourcerer';


@withResources((props, {TODOS, USERS}) => ({
[TODOS]: {data: {user_id: props.userId}, listen: true, measure: true},
[USERS]: {
// noncritical resources do not contribute to overall loading state.
noncritical: true
}
}))
class TodosComponent extends React.Component {}


```


Imagine in our example above that below the user’s to-dos, we also render a list of available users as links. This is less important content than our current user’s to-dos, so we don’t want to block rendering on the` USERS` resource that powers it. By denoting it as` noncritical` , the` isLoading` /` hasLoaded` /` hasErrored` props depend only on the` TODOS` resource (and any other critical resource we might add to the component). We can then use resource-specific loading states provided by` withResources` to render our noncritical content when ready:


```text
import React from 'react';
import {hasLoaded} from 'resourcerer/utils';
import {withResources} from 'resourcerer';


@withResources((props, {TODOS, USERS}) => ({
[TODOS]: {data: {user_id: props.userId}, listen: true, measure: true},
[USERS]: {noncritical: true}
}))
class TodosComponent extends React.Component {
render() {
return (
<div classname='TodosComponent'>
{this.props.isLoading ? <Loader /> : null}


{this.props.hasErrored ? <ErrorState message='An error occurred.' /> : null}


{this.props.hasLoaded ? (
<ul>
{this.props.todosCollection.map((todoModel) => (
<li key={todoModel.id}>{todoModel.get('name')}</li>
))}
</ul>
) : null}


{hasLoaded(this.props.usersLoadingState) ? (
<ul>{this.props.usersCollection.map(...)}</ul>
) : null}
</div>
);
}
}


```


Here’s a real-life example in the Sift Console where we don’t want to wait on dynamic Workflow run counts to render our static Workflow configuration cards:


When the run counts return, we get:


## Dependent Requests


We can also use` resourcerer` to build out *dependent* (serial) requests. In the following example, imagine we have a queue of items to process. But within each queue item is a user that we need information about. At a path of` /queues/{queue_id}/items/{item_id}` , we know the item id—but we can’t fetch the user resource until we know the user id. With` withResources` , we can automatically link resources via` provides` /` dependsOn` options:


```text
@withResources((props, {QUEUE_ITEM, USER}) => ({
[QUEUE_ITEM]: {
data: {id: props.itemId}
// this object will provide a new prop equal to the object key as a result of
// running its resource through the object value, a transform function
provides: {userId: getUserIdFromItem}
},
[USER]: {
options: {userId: props.userId},
// this resource will not get requested until props.userId exists
dependsOn: ['userId']
}
}))
export default class QueueItemPage extends React.Component {}


function getUserIdFromItem(queueItemModel) {
// the return value here gets set as props.userId
return queueItemModel.get('userId');
}


```


Upon returning, the` QUEUE_ITEM` resource **provides**` props.userId` with a value equal to the return value of the transform function` getUserIdFromItem` , while the` USER` resource **depends on**` props.userId` to be defined before its request will be made.


## Prefetching Resources


Now let’s say a user makes a search request in your app and sees the first 10 results listed. When they click on the ‘next’ button, you can request the next batch by, for example, incrementing` props.page` . But you may also want to, in anticipation of them clicking ‘next,’ prefetch the next batch of results so that they are immediately available when requested. Easy-peasy with the` prefetches` option:


```text
const REQUESTS_PER_PAGE = 10;


@withResources((props, {TODOS_SEARCH}) => ({
[TODOS_SEARCH]: {
data: {
from: props.page * REQUESTS_PER_PAGE,
limit: REQUESTS_PER_PAGE,
sort_field: props.sortField
},
// each entry represents _changed_ props used to assemble a new request
prefetches: [{page: props.page + 1}]
}
}))
class TodosSearchPage extends React.Component {}


```


Each entry in the` prefetches` array, which represents *changed* props, is merged with existing props to generate a new request. This request gets placed in the cache but is not passed down as props and is not taken into account in loading states; it’s simply fetched optimistically. When the current props are changed to reflect an entry in` prefetches` (in this case, when` props.page` is equal to 1 after the user clicks the ‘next’ button), the prefetched model is already in the cache and returned immediately! The following page is then prefetched accordingly.


## Give it a Spin


By utilizing critical, noncritical, prefetched, and dependent resources via a declarative syntax, we can easily orchestrate component data flows within our app to deliver the best user experiences possible! But this is actually just scratching the surface of what is available in the` withResources` HOC. Head over to[github](https://github.com/SiftScience/resourcerer) to check out the full documentation on how to get started!


## Author


-


[Sift](https://engineering.sift.com/author/emily/)
