# Markdown grammar

## SPACE & NEW LINE

Space: \&nbsp;  
NewLine: \</br>

## HEADERS

> \# This is an \<h1\> tag
>
> \#\# This is an \<h2\> tag
>
> \#\#\#\#\#\# This is an \<h6\> tag

## EMPHASIS

> \*This text will be italic\*
>
> *This text will be italic*

> \_This will also be italic\_
>
> _This will also be italic_

> \*\*This text will be bold\*\*
>
> **This text will be bold**

> \_\_This will also be bold\_\_
>
> __This will also be bold__

> \*You \*\*can\*\* combine them\*
>
> *You **can** combine them*

## BLOCKQUOTES

As Grace Hopper said:

\> I’ve always been more interested

\> in the future than in the past.

As Grace Hopper said:
> I’ve always been more interested
> in the future than in the past.

## LISTS

#### Unordered

\* Item1  
\* Item2  
&nbsp;&nbsp;\* Item2a  
&nbsp;&nbsp;\* Item2b

>* Item1
>* Item2
>   * Item2a
>   * Item2b

#### Ordered

1. Item1  
2. Item2  
\* Item2a  
\* Item2b

>1. Item1
>2. Item2
>* Item2a
>* Item2b

## IMAGES

>\!\[GitHub Logo](/images/logo.png)
>
>![GitHub Logo](/images/logo.png)  
>
>Format: \!\[Alt Text](url)
>
>Format: ![Alt Text](url)

## LINKS

>http://github.com - automatic!  
>\[GitHub](http://github.com)  
>[GitHub](http://github.com)

## FENCED CODE BLOCKS

Markdown coverts text with four leading spaces into a code block; with GFM you can
wrap your code with ``` to create a code block without the leading spaces. Add an
optional language identifier and your code will get syntax highlighting.
>\```javascript
>function test() {
> console.log("look ma’, no spaces");
>}
>\```
```javascript
function test() {
 console.log("look ma’, no spaces");
}
```

## TASK LISTS

>\- [x] this is a complete item
>\- [ ] this is an incomplete item
>\- [x] @mentions, #refs, \[links](),
\*\*formatting\*\*, and \<del\>tags\</del\>
supported
\- [x] list syntax required (any
unordered or ordered list
supported)

- [x] this is a complete item
- [ ] this is an incomplete item
- [x] @mentions, #refs, [links](),
**formatting**, and <del>tags</del>
supported
- [x] list syntax required (any
unordered or ordered list
supported)

## TABLES

You can create tables by assembling
a list of words and dividing them
with hyphens - (for the first row),
and then separating each column
with a pipe | :

>First Header \| Second Header
------------ \| -------------
Content cell 1 \| Content cell 2
Content column 1 \| Content column 2

First Header | Second Header
------------ | -------------
Content cell 1 | Content cell 2
Content column 1 | Content column 2