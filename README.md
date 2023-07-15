# PWASTR
<img width="605" src="https://github.com/nostrocket/pwastr/assets/8143945/65e6bb7a-540d-4c2a-a71f-8d7a3cf63ccc" />

### Problem
Building frontend apps is more annoying than it could be, mostly relies on github, and code is repeated across many projects.

### Solution
Compose frontend apps from nostr events.

Anyone can re-use anyone else's events to compose an application. Think of these events as modular micro-libraries and micro-elements with standardized interfaces.

PWAs become composed from directed acyclic graphs of events. The route that is followed through the graph determines how the app is constructed for the end user. The route can be programmed but can also be driven by user action such that an application is constructed on-the-fly depending on what action the user takes.

For example, when tapping on a community, that community's functionality will be pulled in from events and rendered for the user. Different communities might have different functionality.

Instead of sending pull requests to a repository, developers simply publish events. Instead of asking a maintainer to merge a patch, the end user themselves can immediately try the newly created feature without any action by package maintainers.

Users can set an amount to zap each event in the chain of events they consume. Events (functions) that are more useful to users will end up getting zapped more. This would work much the same way as V4V works on fountain etc, but for code rather than audio.

### Architecture
- Events MUST contain exactly one Function, Style, Element, or Component. 
- Events MAY specify a Lightning address to recieve automatic V4V zaps for usage.

#### Function Events
- Function events take inputs and produce outputs
- Function events MUST NOT retain any internal state
- Function events MAY take other function events as input by passing in the event ID
- Function events MAY produce standard Typescript functions as outputs (to be executed by the browser)
- Function events MUST be composed of standard Typescript
- Function events MUST specify the Type and number of inputs and outputs using the tags `in` and `out`.

#### Element Events
Element events are Function events that produce exactly one DOM Element when executed.

- Element events MAY take JSON objects as inputs
- Element events MAY take other Element events as inputs by passing in the event ID
- Element events MAY take Style Events as inputs by passing in the event ID
- To produce complex elements, take multiple Element events as inputs and produce a single DOM Element as output

#### Style Events
Style events MUST contain at least one `property` and `value`.
Style events do not need to include a `selector`. Element Events should instead include the ID of the relevant Style event and use this ID as the class. CSS Properties and Values can then be injected, using the event ID as the selector.

#### Component Events
A Component Event contains Function, Element, Style, and other Component event IDs to be compiled into a PWA by pwastr.js
- Lisp style language

#### State
PWASTR apps MUST NOT retain any local state, but MAY cache events.
