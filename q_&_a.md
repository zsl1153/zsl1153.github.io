# Q & A

## 1. PSD -> 网页

其实这个过程做的多了就会变成一个机械的思想了。

### Step 1

首先拿到一个psd第一个会想到的就是整个大页面的框架的布局。按照经验无非就是 `header` (`banner` + `nav`) + `main` (`aside` + `article`) + `footer` 或者 `header` + `main` (`nav` / `aside` + `article`) + `footer` 这两种，基本上传统的设计都是这样的框架，所以第一个会想到的肯定是把这些大的不同部分的容器构建好。比如下面这样：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div class="wrap">

    <div class="header">
      <div class="banner"></div>
      <div class="nav"></div>
    </div>

    <div class="main">
      <div class="aside"></div>
      <div class="article"></div>
    </div>

    <div class="footer"></div>

  </div>
</body>
</html>
```

或者这样：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div class="wrap">

    <div class="header">
      <div class="banner"></div>
    </div>

    <div class="main">
      <div class="nav"></div>
      <div class="article"></div>
    </div>

    <div class="footer"></div>

  </div>
</body>
</html>
```

把这些骨架搭建好之后就可以根据设计图的尺寸写好这些骨架的css了。

理论上大部分传统的网页都是用这种传统的布局方式的，除非遇到很潮的设计师，不然大部分情况这两种模板都能套的上去的。

### Step 2

写完骨架之后个人习惯是把剩下的html和css填完，就是根据设计图，按照骨架的顺序一个个部位把设计图里面的东西实现，暂时写的也只是html + css，js的部分在这一步里面还没有加入。基本上也没什么别的经验的啦，就是按着psd做就是了。

### Step 3

把整个静态的网页都重构完之后就可以开始写js了，之所以要先全部html先写好，是为了写js的时候更有条理，因为可以知道每个部分都有什么，哪个部分跟哪个部分会有关联，这样在写js的时候就可以避免前面写了后面又要加，更有条理。也方便js的安排，比较容易确定每个部分中的每个元素在什么时候会触发什么事件执行什么函数实现什么效果。

基本上个人来讲从psd到页面的思路大概就是这样了。

## 2. 响应式

其实响应式的概念，个人理解就是基于同一套UI主题（比如配色什么的）和UI组件，根据不同的分辨率改变各种组件的布局方式，达到在不同分辨率的终端上有符合不同终端用户习惯的浏览效果。它跟做pc + mobile两个版本这种兼容方式的最大区别其实就是在于页面中的组件，它不需要重新写一套，早期的pc + mobile双版页面的时代通常都是pc上一套html + css，然后mobile上是另一套html + css，就是两个网页。而响应式的页面就是只需一套html + 一套css就可以实现在不同终端自动匹配布局方式，而这个匹配的过程，虽说是在一套css里面，但是因为还是需要基于不同的media来写不同的布局，所以理论上还是算是对不同终端单独做适配的，但是由于html和css中ui组件样式是同一套，所以表现上和体验上会更加的统一。

然后呢，要不要做响应式也完全是看需求的。而做响应式的时候关于单位和浮动这种属性还是有它的规范的。

首先是单位。因为移动端屏幕分辨率很多，所以固定死每个元素的长宽显然没有办法适配不同的分辨率。而且由于屏幕分辨率不同，所以屏幕的dpi也不同，虽然 `viewport` 这个属性可以解决这个问题。所以移动端中大部分时候都需要用到相对单位还有 `auto` 这种自动属性又或者 `calc` 这种bug级方法。比如上面讲到的骨架部分，通常来讲它们的长宽最好是用百分比来做单位，然后里面的元素再进行相对定位。

然后是浮动。比如在移动端中，由于屏幕是竖直方向的，所以在水平方向上安排很多内容显然是不合理的，而且这么挤的空间显然也不可能安排很多内容。所以在响应式设计的移动端部分，大部分的内容都是排列在竖直方向上的。比如bootstrap的navbar-collapse就是自动在屏幕变窄时把横向的导航栏变成下拉菜单。所以基本上在响应式的移动端部分，是很少需要用到浮动的，基本上所有内容自上而下线性排列会是比较好的实现。而在pc端中就可以放心地左右乱浮了，毕竟屏幕宽度是足够在水平方向上放很多内容的。值得注意的一点是，在写html的时候顺序最好采用移动端中线性出现的顺序，然后在不同的 `media-query` 里面再设置对应的浮动，这样无论是从逻辑上还是在便捷上都会比较合适。

That's All, Thx For Reading...