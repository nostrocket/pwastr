# PWASTR

### Problem
Building frontend apps is more annoying than it could be.

### Solution
Compose frontend apps from nostr events. Anyone can re-use anyone else's events to compose an application. PWAs become composed of chains of events. Chains can follow different pathways based on user input.

### Architecture
- Events MAY contain exactly one Function, Style, or Element. 
- Events MAY specify a Lightning address to recieve zaps for usage.

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

#### State
PWASTR apps MUST NOT retain any local state, but MAY cache events.
