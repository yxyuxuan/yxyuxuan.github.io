---
title: block，inline和inline-block概念和区别
date: 2016-07-27 23:50:48
tags: CSS
---

## 总体概念
1.block和inline这两个概念是简略的说法，完整确切的说应该是 block-level elements (块级元 素) 和 inline elements (内联元素)。block元素通常被现实为独立的一块，会单独换一行；inline元素则前后不会产生换行，一系列inline元素都在一行内显示，直到该行排满。

2.大体来说HTML元素各有其自身的布局级别（block元素还是inline元素）：

-  常见的块级元素有 DIV, FORM, TABLE, P, PRE, H1~H6, DL, OL, UL 等。
-  常见的内联元素有 SPAN, A, STRONG, EM, LABEL, INPUT, SELECT, TEXTAREA, IMG, BR 等。

3.block元素可以包含block元素和inline元素；但inline元素只能包含inline元素。

要注意的是这个是个大概的说法，每个特定的元素能包含的元素也是特定的，所以具体到个别元素上，这条规律是不适用的。比如 P 元素，只能包含inline元素，而不能包含block元素。

4.一般来说，可以通过display:inline和display:block的设置，改变元素的布局级别。

##block，inline和inlinke-block细节对比
-  display:block
 1.  block元素会独占一行，多个block元素会各自新起一行。默认情况下，block元素宽度自动填满其父元素宽度。
 2.  block元素可以设置width,height属性。块级元素即使设置了宽度,仍然是独占一行。
 3.  block元素可以设置margin和padding属性。

-  display:inline
 1.  inline元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行，其宽度随元素的内容而变化。

 2.  inline元素设置width,height属性无效。

 3.  inline元素的margin和padding属性，水平方向的padding-left, padding-right, margin-left, margin-right都产生边距效果；但竖直方向的padding-top, padding-bottom, margin-top, margin-bottom不会产生边距效果。

-  display:inline-block

 1.  简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性。

## 补充说明
-  一般我们会用display:block，display:inline或者display:inline-block来调整元素的布局级别，其实display的参数远远不止这三种，仅仅是比较常用而已。
-  IE（低版本IE）本来是不支持inline-block的，所以在IE中对内联元素使用display:inline-block，理论上IE是不识别的，但使用display:inline-block在IE下会触发layout，从而使内联元素拥有了display:inline-block属性的表象。