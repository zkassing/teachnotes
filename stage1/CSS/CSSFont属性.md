# CSSFont属性
## 字体颜色属性color
* 取值方式  
1. 使用颜色关键字
    - 比如red，green , black,white ，highlight，brown，darkgreen，darkred，orange
2. 使用十六进制表示：比如#ff6700;
    - 十六进制基数组成： 0 1 2 3 4 5 6 6 7 9  a(10) b(11) c(12) d(13) e(14) f(15)   任意6个组成； 
    - 十六进制前导符号：# 
    - 比如：#ff8900   #aaa  
    *#ff8900是十六进制的全写形式，#aaa十六进制的简写形式*
3. 使用rgb()格式表示；比如：rgb(123,0,255);
*取值范围是0 - 255*
* 案例：  
```(html)
<h1>hello<h1>

<style>
    h1{
        color:red;
    }
</style>
```
## css字体属性font
**font简写属性在一个声明中设置所有字体属性。**
1. font-family:规定字体的系列
    - 案例：    
    ```
    p {
        font-family: Times, TimesNR, 'New Century Schoolbook',     Georgia, 'New York', serif;
     }
     p{
         font-family:"微软雅黑";
     }
    ```
    *只有当字体名中有一个或多个空格（比如 New York），或者如果字体名包括 # 或 $ 之类的符号，才需要在 font-family 声明中加引号。单双引号都可*
    *多个字体系列之间使用逗号隔开*
2. font-style属性：	规定字体样式  
    * 取值： 
        - normal： 默认值，浏览器显示一个标准的字体样式。
        - italic: 浏览器会显示一个斜体的字体样式
        - 案例：
    ```
    h1{
        font-style:italic;//定义斜体字体样式
    }
    ```
*所有浏览器都支持该属性*   
3. font-weight属性：font-weight 属性设置文本的粗细      
    *该属性用于设置显示元素的文本中所用的字体加粗。数字值 400 相当于 关键字 normal，700 等价于 bold*   
    * 取值：  
        - normal:默认值，定义标准字符；
        - bold:	定义粗体字符  
        - bolder:	定义更粗的字符
        - lighter:定义更细的字符。
        - 关键字：100 200 300 400 500 600 700 800 900
        - 案例：
    ```
    h1{
        font-weight:bold;//定义粗体字体      
    }
    h2{
          font-weight:500;
    }
    ```
4. font-size属性:设置字体大小
    * 取值：
        - font-size:20px;
        - font-size:2em;
        - font-size:2rem;  
*如果您没有规定字体大小，普通文本（比如段落）的默认大小是 16 像素 (16px=1em)。*
* 行高：line-height  
***基线到基线的距离，基线是小写字母x的下边界所在的线称为基线***
    - 取值：
        * line-height:20px;
        * line-height:3;//字体大小的倍数；比如字体是20px；则行高为20px*2=40px;
## font字体综合属性
- 语法：font:font-style font-weight font-size/line-height font-family;
- 案例：
    ```  
    p.ex2{
        font:italic bold 12px/20px arial,sans-serif;
    }    
    ```



