---
title: 'MD - Markdown'
date: 2024-02-05
draft:  false   
featured: false  
description: "MD - Markdown"
thumbnail: "/posts/markdown/images/markdown.png"
featureImage: "/posts/markdown/images/markdown.png" 
shareImage: "/posts/markdown/images/markdown.png"
author: "Angel Vyas"
math: true
enableEmoji: true
tags:
    - Markdown
categories:     
    - General
---

Markdown is a lightweight markup language that allows you to add formatting elements to plaintext text documents. Developed by John Gruber in 2004.
In md files we can use certain Html commands easily.

### HEADINGS

```md
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
```
**OUTPUT**
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5

### Text Styles

| BOLD | ITALIC | BOLD AND ITALIC |
|:--:|:--:|:--:|
| `**Angel Vyas**` | `*Angel Vyas*` | `**_Angel Vyas_**`|
|**Angel Vyas**|*Angel Vyas*| **_Angel Vyas_**|


### Text Formating
| Style| Code | Output|
|--|--|--|
| MONOSPACED | `<samp> Hi I'm Angel Vyas.</samp>` | <samp> Hi I'm Angel Vyas.</samp> |
| UNDERLINED | `<ins> Hi I'm Angel Vyas.</ins>` | <ins> Hi I'm Angel Vyas.</ins> |
| STRIKE-THROUGH | `~~Hi I'm Angel Vyas.~~` | ~~Hi I'm Angel Vyas.~~ |
| SUBSCRIPT | `log<sub>2</sub>(x)` | log<sub>2</sub>(x) |
| SUPERSCRIPT | `2 <sup>41-1</sup> and -2 <sup>41-1</sup>` | 2 <sup>41-1</sup> and -2 <sup>41-1</sup> |


### TEXT COLOR

```md
<style>
r { color: Red }
o { color: Orange }
g { color: Green }
</style>

- <r>TODO:</r> Hi
- <o>TODO:</o> Hi
- <g>DONE:</g> Hi
```

<style>
r { color: Red }
o { color: Orange }
g { color: Green }
</style>

- <r>TODO:</r> Hi
- <o>TODO:</o> Hi
- <g>DONE:</g> Hi

### TABLES in Markdown

#### Simple Table

```md
|A |B| C|
|--|--|--|
|1 |2| 3|
```
**Output**
|A |B| C|
|--|--|--|
|1 |2| 3|

#### Breakline in Table 

```md
|A |B| C|
|-- |--| --|
|1| |2 <br>3</br> 4| 5|
```

**Output**
|A |B|C|
|--|--|--|
|1|2 <br>3<br/> 4| 5|

#### Alignment in Table
```md
| Default    | Left align | Center align | Right align |
| ---------- | :--------- | :----------: | ----------: |
| 1111111111 | 1111111111 | 111111111    | 1111111111  |
| 111111111  | 111111111  | 111111111    | 111111111   |
| 11111111   | 11111111   | 11111111     | 11111111    |
| 1111111    | 1111111    | 1111111      | 1111111     |
```
| Default    | Left align | Center align | Right align |
| ---------- | :--------- | :----------: | ----------: |
| 1111111111 | 1111111111 | 1111111111   | 1111111111  |
| 111111111  | 111111111  | 111111111    | 111111111   |
| 11111111   | 11111111   | 11111111     | 11111111    |
| 1111111    | 1111111    | 1111111      | 1111111     |

### Blockquotes
> Hi my name is Angel Vyas.

> Hello,
>> Hi my name is Angel Vyas.

>Hi
>>I'm
>>>Angel Vyas.


### Collapsable

<details>
  <summary>Markdown</summary>
-  <kbd>[Markdown Editor](https://binarytree.dev/me)</kbd>
-  <kbd>[Table Of Content](https://binarytree.dev/toc)</kbd>
-  <kbd>[Markdown Table Generator](https://binarytree.dev/md_table_generator)</kbd>

</details>

### Horizontal lines
```md
---
***
___
```
**Output**
---
***
___
<br>

