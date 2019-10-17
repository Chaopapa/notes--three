## HTML5 简介

### 什么是HTML5

HTML5 将成为 HTML、XHTML 以及 HTML DOM 的新标准。

HTML 的上一个版本诞生于 1999 年。自从那以后，Web 世界已经经历了巨变。

HTML5 仍处于完善之中。然而，大部分现代浏览器已经具备了某些 HTML5 支持。

### HTML5是如何起步的？

HTML5 是 W3C 与 WHATWG 合作的结果。

**编者注：**W3C 指 World Wide Web Consortium，万维网联盟。

**编者注：**WHATWG 指 Web Hypertext Application Technology Working Group。

WHATWG 致力于 web 表单和应用程序，而 W3C 专注于 XHTML 2.0。在 2006 年，双方决定进行合作，来创建一个新版本的 HTML。

### 新特性

HTML5 中的一些有趣的新特性：

- 用于绘画的 canvas 元素
- 用于媒介回放的 video 和 audio 元素
- 对本地离线存储的更好的支持
- 新的特殊内容元素，比如 article、footer、header、nav、section
- 新的表单控件，比如 calendar、date、time、email、url、search

### 浏览器支持

最新版本的 Safari、Chrome、Firefox 以及 Opera 支持某些 HTML5 特性。Internet Explorer 9 将支持某些 HTML5 特性。

### HTML5网页代码

```html
<!DOCTYPE html>
<html>
  <head>
  	<title>文档的标题</title>
  </head>
  <body>
  	文档的内容......
  </body>
</html>
```



##HTML5标签

### 新增标签

##### 结构性标签

header

footer

main

section

aside

articel

nav

hgroup

dialog

figure & figcaption

details & summary

##### 多媒体标签

video

audio

source

track

canvas

embed

##### 状态标签

progress

meter

##### Menu

menu

menuitem

commond

##### 注释标签

ruby & rp & rt

##### 其他标签

mark

time



## HTML5 表单

##### HTML5 新的Input 类型

email

url

number

range

Date pickers (date, month, week, time, datetime, datetime-local)

search

color

##### HTML5 新的表单元素

output

datalist  (input & option)



## Embed

##### 基本用法

##### 属性设置

src="资源路径"   type="video/mp4"



## video

##### 定义和用法

##### 音频格式

mp4	webm	ogv

##### 标签属性

src

height

width

autoplay

controls

loop

preload

poster

muted

##### api

play()

pause()

duration

currentTime

src

currentSrc

volume

controls

muted

networkState

ended

loop

playbackRate

readyState

timeupdate

seeked

seeking

volumechange

requestFullscreen(webkitRequestFullscreen,  mozRequestFullScreen, msRequestFullScreen)

load

canplay

##### 案例



## audio

##### 定义和用法

##### 音频格式

ogg	mp3	wav

##### 标签属性

src

controls

autoplay

loop

muted

##### api

poster

play

pause

duration

currentTime

src

currentSrc

volume

controls

meted

networkState

ended

loop

playbackRate

readyState

timeupdate

seeked

seeking

volumechange

requestFullscreen

load

canplay

##### 案例



## HTML5 新的表单属性

##### 新的 form 属性：

autocomplete

novalidate

##### 新的 input 属性：

autocomplete

autofocus

form

form overrides (formaction, formenctype, formmethod, formnovalidate, formtarget)

height 和 width

list

min, max 和 step

multiple

pattern (regexp)

placeholder

required

## HTML5 全局属性

## HTML5事件

## Form 事件

## Mouse 事件

## Media 事件