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
* ...

Element events MAY specify the type and number of inputs allowed. If desired, these MUST be included in a `in` tag, which is an ordered list of input types, for example:
`["in", "elem.h1", "elem.p", "data.string", "data.string", "data.number"]`

Example events:
```
{
id: 1111b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff8842
content: ""
tags: [["in", "heading:elem.h1", "body:elem.p", "_body:style", "_box:style"],
["out", "elem.div"],
["ord", "(DIV#_box(heading, body#_body)"]]
}

{
id: 22222b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff7777
content: ""
tags: [["in", "data.string"],
["out", "elem.h1"],
["ord", "(H1=0)"]]
}

{
id: 33333b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff1111
content: ""
tags: [["in", "data.string"],
["out", "elem.p"],
["ord", "(P=0)"]]
}


{
id: 44444b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff1111
content: ""
tags: [["border-style", "solid"], ["border-color", "FFFFFF"], ["max-width", "800px"]]
}

{
id: 555555b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff1111
content: ""
tags: [["text-align", "middle"]]
}
```

Using the events above, we can construct our first Composite event to create a framework:

```
{
id: 66666666b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff1111

content: "1111b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff8842(
22222b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff7777:heading,
33333b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff1111:body,
44444b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff1111,
555555b9ff8c19b537ba5cdb7a7809f2031eb34c033229117ecfe055f608ff1111
)"
tags: [["in", "heading:data.string", "body:data.string"], ["out", "DIV"]]
}
```

and then we can populate this composite event with data using a Function event that selects a heading and body based on some criteria:

