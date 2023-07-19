Problem: we do not have any example events that can be used as test cases when rendering events in the browser.

### Element Event
Element events MUST specifiy exactly one element Type that will be produced as an output. This is the type of HTML element to be injected into the DOM. The element Type is to be indicated by {including it in a tag} {using a kind from the list below (e.g. 8801 = `div`)}

Element events MUST NOT contain any element types that are not in the following list:
* DIV
* P
* BR
* H1
* H2
* H3
* H4

Element events MAY specify the type and number of inputs allowed. If desired, these MUST be included in a `in` tag, which is an ordered list of input types, for example:
`["in", "elem.h1", "elem.p", "data.string", "data.string", "data.number"]`

Example event:
```
content: empty
tags: [
["in", "elem.h1", "elem.p", "data.string", "data.string", "data.number", "style", "style"],
["out", "elem.div"]
]

```
