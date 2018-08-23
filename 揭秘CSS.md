### 一.CSS编码技巧
1. 尽量减少代码重复。
 
-   1> 当某些值互相依赖时，把它们的相互关系用代码表示。
        （字号和其他尺寸能够跟父级的字号相关联，用em.若是这些字号和根级字号（即html元素的字号）相关联，用rem）  
        
-    2> currentColor inherit

 2. 响应式网页设计
      

-      1>合理使用媒体查询。
-      2>使用百分比长度来取代固定宽度
-      3> 在较大分辨率下得到固定宽度时，使用max-width
-      4>不要忘记为替换元素（如img、object、video、iframe等）设置max-width
-      5>背景图片需要完整地铺满一个容器，不管容器的尺寸如何变化，使用background-size:cover
-      6>当图片（或其他元素）以列式进行布局时，让视口的宽度来决定列的数量。可使用弹性布局或者display:inline-block加上常规的文本折行行为，都可以实现这一点。
-      7>在使用多列文本时，指定column-width。

3. 合理使用简写
### 二.背景与边框

   1. 半透明边框:
   
```
   border: 10px solid hsla(0,0%,100%,0.5);
   background:white;
   background-clip:padding-box;

```

   2. 多重边框：
   
```
  法一：
  box-shadow
  法二：
    outline（只适用双层“边框”的场景）
    
```
   3.灵活的背景定位：
   
```

  法一： background-position
  
   background-position:right 20px bottom 10px;
   
  法二：background-origin
  
   background-position以padding-box为准，background-origin的默认值时padding-box.
   
   background-origin:content-box;
  
  法三：calc()
  
    
```
   
  4.边框内圆角：
  
```

  outline box-shadow(扩张值为约为圆角半径的一半)
  
 
```

  5.条纹背景：
  i
```
   repeating-linear-gradient()  
```

6.复杂的背景图案：

```
   radial-gradient
   
```
### 三.形状：

1.自适应的椭圆：

```
border-radius:水平半径/垂直半径（用百分数表示，会基于元素的尺寸进行解析）

```
2.平行自边形：（变形元素而不变形它的内容）

```
法一：嵌套元素

容器： transform:skewX(-45deg);     
内容：transform:skewX(45deg); 

```

```
法二：伪元素
 16           .aa::before{
 17           content:'';
 18           position:absolute;
 19           top:0;
 20           left:0;
 21           right:0;
 22           bottom:0;
 23           /*把它的堆叠层次推到宿主元素之后*/
 24           z-index:-1;
 25           background:blue;
 26           transform:skewX(-45deg);
 27           }


```

3.菱形图片：
```


菱形基于变形的方案（==如果图片不是正方形，基于变形的方案会严重崩坏）==

==裁切路径方案：（推荐:可以很好地适应非正方形图片，而且也不需要额外的html标签）==

clip-path 裁切路径 

polygon() 多边形函数          



```
线性渐变方案：linear-gradient(); (代码冗长，改变时改动地方多。好处：允许文字溢出并超出切角区域)

内联SVG与border-image方案：border-image  background-clip:padding-box（避免背景色蔓延到边框区域）

裁切路径方案：（不完全支持；内边距不够时会裁掉文本；好处:可使用任意类型的背景，甚至可对替换元素进行裁切，支持动画效果）


5.梯形标签页：

```
22           .aa::before{
 23                    content: '';          
 24                    top:0;
 25                    right:0;
 26                    bottom:0;
 27                    left:0;
 28                    z-index:-1;
 29                    background:blue;
 30                    position:absolute;
 31                    transform:scaleY(1.3) perspective(.5em) rotateX(5deg);                                                                 
 32                    transform-origin:bottom;
 33           }
 
 
```
6.简单的饼图：

```
  1 <!DOCTYPE html>                                                                                                                           
  2 <html>
  3      <head>
  4            <title>简单的饼图</title>
  5           <style>
  6               svg{
  7                  width:100px;
  8                  height:100px;
  9                  transform:rotate(-90deg);
 10                  background:yellowgreen;
 11                  border-radius:50%;
 12               }
 13               circle{
 14               fill:yellowgreen;
 15               stroke:#655;
 16               stroke-width:32;
 17               stroke-dasharray:20 100;
 18               }
 19           </style>    
 20      </head>
 21      <body class="content">
 22           <svg viewBox="0 0 32 32">
 23               <circle r="16" cx="16" cy="16" />
 24           </svg>
 25      </body>
 26 </html>
           
```
### 四.视觉效果：

1.投影：

```
  1 <!DOCTYPE html>
  2 <html>
  3      <head>
  4            <title>投影</title>
  5           <style>
  6                .aa{
  7                width:100px;
  8                height:50px;
  9                background:yellowgreen;
 10                /*单侧投影*/
 11                /*负的扩张半径，值等于模糊半径*/
 12                /*box-shadow: 0 5px 4px -4px black;*/
 13 
 14 
 15 
 16                /*邻边投影*/
 17               
 18                /*负的扩张半径，值等于模糊半径的一半*/
 19               /* box-shadow: 5px 5px 4px -2px black;*/
 20 
 21               /*双侧投影*/
 22               box-shadow: 5px 0 4px -4px black,
 23                          -5px 0 4px -4px black;
 24                }
 25           </style>    
 26      </head>
 27      <body class="content">
 28      <div class="aa">
 29         
 30      </div>
 31      </body>
 32 </html>   
```

2.毛玻璃效果：

```
  1 <!DOCTYPE html>
  2 <html>
  3      <head>
  4            <title>毛玻璃效果</title>
  5           <style>
  6                 body,main::before{
  7                  background:url("bear.jpg") 0 / cover fixed;
  8                 }
  9                 main{
 10                   position:relative;
                      /*把多余的模糊区域裁切掉*/
 11                   overflow:hidden;
 12                   background:hsla(0,0%,100%,0.3);
 13 
 14                 }
 15                 main::before{
 16                 content: '';
 17                 position:absolute;
 18                 top:0;
 19                 bottom:0;
 20                 left:0;
 21                 right:0;
 22                 filter:blur(20px);
 23                 margin:-30px;
 24                 }
 25          </style>  
 26      </head>
 27      <body>
 28          <main>
 29               小熊
 30          </main>     
 31     </body>
 32 </html> 
```
### 五.字体排印：

1.连字符断行：

```
 hyphens:auto;
```
2.插入换行：

```
使用伪元素：before
内容为换行:  content:"\A";
保留源代码中的空白符和换行： white-space：pre;

```
3.文本行的斑马条纹：



```
padding：0.5em;
line-height:1.5;
background:beige;
background-size: auto 3em; //每个背景贴片需要覆盖两行，所以为3em
background-origin:content-box;
background-image:linear-gradient(rgba(0,0,0,0.2) 50%, transparent 0);
```
4.调整tab的宽度：

```
tab-size
```
5.连字：

```
font-variant-ligatures: common-ligatures //通用字
                        discretionary-ligatures
                        historical-ligatures;
                        
```
6.华丽的&字符：

```
@font-size{
    font-family:Ampersand;
    src:local("Baskerville-italic"),
        local("BookAntiqua-Italic");
}
```

7.自定义下划线：

```
background:linear-gradient(gray,gray) no-repeat;
background-size:100% 1px;
background-position:0 1.15em;
text-shadow: .05em 0 white,-0.05em 0 white;
(通过色标的百分比位置值来微调虚实比例，通过background-size来改变虚线的疏密)

```
8.现实中的文字效果：

```
   1.凸版印刷效果：

     当我们在浅色背景上使用深色文字时，在底部加上浅色投影通常效果最佳。
     例如：
     background:hsl(210,13%,60%);
     color:hsl(210,13%,30%);
     text-shadow:0 1px 1px hsla(,0%,100%,0.8);

```


```
  2.空心字效果：
  
  法一：使用多个text-shadow,分别给这些投影加上不同方向的少量偏移。
  法二：使用多个text-shadow，重叠多层轻微模糊的投影来模拟描边，不需要设置偏移量。
  法三：SVG
```

```
  3.文字外发光效果：
  
    方法一：几层重叠的text-shadow即可，不需要考虑偏移量，颜色也只需跟文字保持一致。
    （以来text-shadow来实现文字显示的做法无法实现平稳退化）
    
    方法二：CSS滤镜：
    
    a{
        background：#203；
        color:white;
        transtion:1s;
    }
    a:hover{
        
        filter:blur(.1em);
    }
    
```

```
4.文字凸起效果：

  使用一长串累加的投影，不设模糊并以1px的跨度逐渐错开，使颜色逐渐变暗，最后在底部加一层强烈模糊的暗投影。
  background：#58a;
  color:white;
  text-shadow: 0 1px hsl(0,0%,85%),
               0 2px hsl(0,0%,80%),
               0 3px hsl(0,0%,75%),
               0 4px hsl(0,0%,70%),
               0 5px hsl(0,0%,65%);
               0 5px 10px black;
               
               
如果把所有的投影都设为黑色，并且去掉最底层的投影，可以模拟出一种在复古标志牌中常见的文字效果。               
               
             
```

### 六.用户体验

```
1.选用合适的鼠标光标：

  例如：提示禁用状态： cursor:not-allowed;
        隐藏鼠标光标： cursor:none;
        

```

```
2.扩大可点击区域：

   使用伪元素：
    button{
        
        position:relative;
    }
    button::before{
        content: '';
        position:absolute;
        top:-10px;
        right:-10px;
        bottom:-10px;
        left:-10px;
        
    }
```

```
3.自定义复选框：

<input type="checkbox" id="awesome">
<label for="awesome" >Awesome!</label>

input[type="chckbox"]+label::before{
    
    content:'\a0'; /*不换行空格*/
    display:inline-block;
    vertical-align:0.2em;
    width:.8em;
    height:.8em;
    margin-rght:.2em;
    border-radius:.2em;
    background:silver;
    text-indent:.15em;
    line-height:.65;
 
    
}
input[type="checkbox"]:checked+label::before{
    content:'\2713';
    background:yellowgreen;
}
/*把原来的复选框以一种不损失可访问性的方式隐藏起来*/
input[type="checkbox"]{

    position:absolute;
    clip:rect(0,0,0,0);
}


```

```
4.通过阴影来弱化背景：
 
 方法一：伪元素方案：
  
   body.dimmed::before{
       position:fixed;
       top:0;
       left:0;
       right:0;
       bottom:0;
       z-index:1;
       background:rgba(0,0,0,0);
   }
   
   方法二：box-shadow
   box-shadow:0 0 0 999px rgba(0,0,0,0.8);
   (无法在较大的屏幕分辨率下正常工作)
   box-shadow:0 0 0 50vmax rgba(0,0,0,.8);
   
   方法三: backdrop方案：
   
   dialog::backdrop{
   
       background:rgba(0,0,0,.8);
   }
  (不完全支持)
  
```


```
 5.通过模糊来弱化背景：
 
 filter:blur(3px) contrast(.8) brightness(.8);
 

```

### 七.结构与背景：

```
1.精确控制表格列宽:

  例如：
  table{
      
      table-layout:fixed;
      width:100%;
  }
```

```
 2.根据兄弟元素的数量来设置样式：
 
  只有一个列表项:  :only-child
  数量范围： :nth-child()括号中的参数可以使具体数字，也可以是范围： n+b(选中从b个开始的所有元素  
  
               -n+b(选中开头的b个元素))
   
   命中所有列表项： li:first-child:nth-last-child(参数)，
   li:first-child:nth-last-child(参数)~li{}
   
```

```
3.满幅的背景，定宽的内容：

 footer{
     padding:1em;
     padding:1em calc(50%-450px);
     background:#333;
 }
```

```
4.垂直居中：

方法一：基于绝对定位：
  main{
      position：absolute;
      top:50%;
      left:50%;
      margin-top: -3em;
      margin-left: -9em;
      width:18em;
      height:6em;
      
  }
  或者：
  main{
      position：absolute;
      top:calc(50%-3em);
      left:calc(50%-9em);
      width:18em;
      height:6em; 
  }
  或者
      main{
      position：absolute;
      top:50%;
      left:50%;
      transform:translate(-50%,-50%);
  }
  
  方法二：基于视口单位：
  
  main{
  
      width:18em;
      padding:1em 1.5em;
      margin:50vh auto 0;
      transform:translateY(-50%);
  }
  
  方法三：基于Flexbox：
  
  body{
      display:flex;
      min-height:100vh;
      margin:0;
  }
  main{
margin:auto;
  }
  
  同时让内部的文本也居中;
  main{
      display:flex;
      align-items:center;
      justify-content:center;
      width:18em;
      height:10em;
  }
```











