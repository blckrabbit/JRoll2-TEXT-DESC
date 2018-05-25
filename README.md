JRoll 2 使用文档（史上最强大的下拉刷新，滚动，无限加载插件）


标签：scroller   方便   专业   duration   电脑   parent   margin   status   上线   

概述

说明

JRoll，一款能滚起上万条数据，具有滑动加速、回弹、缩放、滚动条、滑动事件等功能，兼容CommonJS/AMD/CMD模块规范，开源，免费的轻量级html5滚动插件。

JRoll第二版是在JRoll第一版基础上重写JRoll滑动算法，基于时间运动，解决帧频降低时滑动缓慢的问题，更改垂直水平方向判断方法，使捕获垂直水平方向更准确灵敏。

JRoll第二版增减了一些api不完全兼容JRoll第一版。

先睹为快

技术分享

http://www.chjtx.com/JRoll/demos/

 

运行示例

请先安装 git 和 nodejs


#克隆仓库 Clone repository
git clone https://github.com/chjtx/JRoll.git

#进入项目 Go into project
cd JRoll

#安装express Install express
npm install -g express

#如果用苹果电脑，需要加sudo
#If on mac, use sudo
sudo npm install -g express

#运行 Run
node server.js
然后在浏览器打开 localhost:3020/demos/

 

兼容性

[√] IOS 6+
[√] Android 4.0+
[√] Chrome
[√] Firefox
[√] IE 9+
注意：JRoll专为移动应用度身设计，对PC浏览器的兼容只为方便开发调试，没作过多处理，因此强烈建议使用谷歌浏览器模拟器进行开发，在移动端使用。

在UC浏览器上表现较差，作者已将UC浏览器定义为资讯类应用，非专业浏览器，不会专门去兼容它

引入

普通方式引入
                    
<script src=‘jroll.js‘></script>
                    
CommonJS规范引入
                    
var JRoll = require(‘jroll‘);
                    
AMD规范引入（requireJS）
                    
require([‘jroll‘], function(JRoll) {
    ...
});
                    
CMD规范引入（seaJS）
                    
seajs.use(‘jroll‘, function(JRoll) {
    ...
});
                    
简单例子

html代码

                    
<div id="wrapper">
    <ul id="scroller">
        <li>有一美人兮，见之不忘。</li>
        <li>一日不见兮，思之如狂。</li>
        <li>凤飞翱翔兮，四海求凰。</li>
        <li>无奈佳人兮，不在东墙。</li>
        <li>将琴代语兮，聊写衷肠。</li>
        <li>何日见许兮，慰我彷徨。</li>
        <li>愿言配德兮，携手相将。</li>
        <li>不得於飞兮，使我沦亡。</li>
    </ul>
</div>
                    
css代码

                    
ul {margin: 0; padding: 0;}
li {line-height: 24px; margin-left: 24px;}
#wrapper {width: 200px; height: 100px; border: 1px solid;}
                    
js代码

                    
new JRoll("#wrapper");
                    
 

使用

如何使用

            
var jroll = new JRoll(selector [, options]);
            
selector是容器，可以是id选择器字符串#wrapper，也可以是dom对象document.getElementById(‘wrapper‘)，第二个参数是可选对象，该参数内容决定了创建一个怎样的JRoll对象

例：创建一个带垂直滚动条的对象
            
var jroll = new JRoll("#wrapper", {scrollBarY:true});
            
保存了JRoll对象后，可动态对部分可选参数进行修改

例：禁止回弹
            
jroll.options.bounce = false;
            
可选参数

可选值	默认值	说明
id	[随机生成]	id，jroll对象的唯一标记，建议手动提供id，方便在全局JRoll.jrollMap访问指定jroll对象，不提供时系统自动创建。
scrollX	false	使能水平滑动可动态修改
scrollY	true	使能垂直滑动可动态修改
scrollFree	false	使能自由滑动，默认情况下，x方向在滑动时，y方向不能滑动，相反亦然，如果应用于对图片进行放大滑动，可将此参数设为true可动态修改
minX	0	向左滑动的边界值可动态修改
maxX	[负scroller的宽]	向右滑动的边界值可动态修改
minY	0	向下滑动的边界值可动态修改
maxY	[负scroller的高]	向上滑动的边界值可动态修改
zoom	false	使能缩放可动态修改
zoomMin	1.0	最小缩放倍数可动态修改
zoomMax	4.0	最大缩放倍数可动态修改
bounce	true	允许回弹可动态修改
scrollBarX	false	开启水平滚动条
scrollBarY	false	开启垂直滚动条
scrollBarFade	false	滚动条使用渐隐模式
preventDefault	true	禁止touchmove默认事件
momentum	true	开启滑动加速，惯性过渡可动态修改
autoStyle	true	自动为wrapper和scroller添加样式
adjustTop	190	从JRoll v2.2.0版本开始，JRoll删除了adjustTop选项，自动调整安卓机输入框位置的功能抽离到jroll-fixedinput.js里。安卓手机弹出软键盘时自动调整输入框位置，作者不建议使用该项，如遇软键盘遮挡输入框的情况，建议重新设计表单页面。参考：WebAPP输入框被软键盘遮挡肿么办？
scroller	[wrapper的第一个子元素]	指定scroller，不可动态更改，可以是id选择器字符串#scroller，也可以是dom对象document.getElementById(‘scroller‘)
属性

id
JRoll对象的唯一标识符。

var jroll = new JRoll("#wrapper");
console.log(jroll.id);
                
jrollMap
对象，JRoll对象集合，保存了当前页面的所有JRoll对象。

console.log(JRoll.jrollMap);
                
方法

refresh支持链式调用
当scroller或wrapper的高度发生变化时，需要用此方法对JRoll对象进行刷新

var jroll = new JRoll("#wrapper");
    //do something，例：动态修改scroller的内容，使scroller的高度发生变化
    jroll.refresh();
                
scrollTo支持链式调用
该方法用于移动scroller，共五个参数，第一个参数是x偏移量（必填），第二个是y偏移量（必填），第三个是滑动时间（可选，单位ms)，第四个是是否允许超出边界（可选，true/false），第五个回调方法（可选）。如果想获取当前x,y偏移量，可直接输出jroll.x和jroll.y

jroll.scrollTo(x, y, duration [, bool, callback])
        

var jroll = new JRoll("#wrapper");
    //200ms内滑动到0px, -100px位置
    jroll.scrollTo(0, -100, 200);
    //允许超出边界
    jroll.scrollTo(100, 100, 0, true);
    //回调
    jroll.scrollTo(0, 100, 400, false, function() {
        //滑动结束后执行
    });
                
enable支持链式调用
使能滑动，使用disable禁止滑动后可用该方法重新开启

jroll.enable();
                
disable支持链式调用
使不能滑动

jroll.disable();
                
destroy
销毁jroll对象

jroll.destroy();
                
scale支持链式调用
缩放，只接受一个整型/浮点型参数

//放大1.5倍
jroll.scale(1.5);
                
call
在滑动时中转移对象，返回转移给的对象。适合于嵌套滑动时内层滑动到末尾开始滑动外层的场景。

/* 例：
 * jroll1在外层，包裹jroll2
 * jroll2在滑动到达指定条件时将滚动权交给jroll1
 */
var pos;
var jroll1 = new JRoll("#wrapper", {bounce:true});
var jroll2 = new JRoll("#inner", {bounce:true});
    jroll2.on("scrollStart", function() {
        pos = this.y;
    });
    jroll2.on("scroll", function(e) {
        if ((this.y-pos > 0 && pos === 0) || (this.y-pos < 0 && pos === this.maxScrollY)) {
            jroll2.call(jroll1, e); //返回jroll1
        }
    });
                
事件

JRoll一共提供8个事件，每个事件都可多次添加行为。事件里的this指向jroll对象。

scrollStart
滑动开始时执行

jroll.on("scrollStart", function() {
    console.log(this.x); //输出当前x偏移量，this指向jroll对象
});
                
scroll
滑动过程中执行

jroll.on("scroll", function() {
    //该干嘛干嘛去...
});
                
scrollEnd
滑动结束时执行

jroll.on("scrollEnd", function() {
    //该干嘛干嘛去...
});
                
touchEnd
用户释放手指时执行，早于scrollEnd晚于scroll事件

jroll.on("touchEnd", function() {
    //该干嘛干嘛去...
});
                
zoomStart
开始缩放时执行

jroll.on("zoomStart", function() {
    //该干嘛干嘛去...
});
                
zoom
缩放过程中执行

jroll.on("zoom", function() {
    //该干嘛干嘛去...
});
                
zoomEnd
缩放结束后执行

jroll.on("zoomEnd", function() {
    //该干嘛干嘛去...
});
                
refresh
使用jroll.refresh()刷新后执行

jroll.on("refresh", function() {
    //该干嘛干嘛去...
});
                
 

进阶

使用this.s判断当前滑动状态


var jroll = new JRoll("#wrapper");
jroll.on("scroll", function() {
    if (this.s === "scrollY") {
        //干点你想干的事情
    } else {
        //或者干点别的事情
    }
})
    
jroll.s中的s表示status，6种可能取值

1. null初始状态，未进行任何滑动操作
2. preScroll准备开始滑动
3. preZoom准备开始缩放
4. scrollX正在进行横向滑动
5. scrollY正在进行竖向滑动
6. scrollFree正在进行横竖方向滑动
注意：JRoll v2.3.0以下版本的min压缩文件的jroll.s值用1、2、3、4、5表示preScroll、preZoom、scrollX、scrollY、scrollFree。在JRoll v2.3.0版本开始与未压缩版保持一致，当初真不应该为了节省那丁点字节取用数字压缩的。

判断是否滑动到底部


var jroll = JRoll("#wrapper");
jroll.on("scrollEnd", function() {
    if (this.y === this.maxScrollY) {
        console.log("已滑动到底部");
    }
});
    
有关jroll对象更多的属性请自行在浏览器控制台输出jroll对象查看。

自定义滚动条样式

只要scrollBarX/scrollBarY的值为字符串，即为开启自定义滚动条，需要自己写样式。

滚动条对样式定位有些特殊要求，自定义滚动条大小、颜色时需要先将默认样式拷贝下来，再对 .jroll-ybar/.jroll-xbar 和 .jroll-ybtn/.jroll-xbtn 进行修改。


var jroll = new JRoll("#wrapper", {
        scrollBarY: "custom",
        scrollBarFade: true
    });
    
解决某些安卓机无法滑动非播放状态的<video>

如果您的页面需要播放视频，在某些安卓机下无法滑动<video>，可用以下方法解决。

非播放状态的<video>其表现像controls一样无法捕获touchstart等事件，因此无法使用JRoll滑动，可使用透明div解决。


<div id="parent">
    <video id="video" controls="controls">
        <source src="./video.ogg" type="video/ogg">
    </video>
    <div class="fixed-video-scroll"></div>
</div>
<script>
var video = document.getElementById("video");
document.addEventListener("click", function(e) {
    if (e.target.className === "fixed-video-scroll") {
        if (video.paused) {
            video.play();
        } else {
            video.pause();
        }
    }
})
</script>
    
1. 使#parent为相对定位，video的宽度为100%，高度可自动也可自己计算
2. div.fixed-video-scroll绝对定位，覆盖video，高度为video的高度减去44px，确保不会遮挡controls
3. 添加事件，点击div.fixed-video-scroll时执行播放或暂停操作
关于被软键盘遮挡input输入框的问题

评论框贴在底部随着软键盘升起而升起的功能似乎很受客户青睐，这一需求使用H5技术实现很是力不从心，fixed定位失效，第三方输入法不改变window高度致使input被遮挡，IOS自动移动input到错误位置等等问题成了最大的阻力。

现时比较可行的解决方案有：

1. 点击评论时弹出浮动窗，使输入框位于上半屏。
2. 切换到新页面进行输入操作。
这两种设计方案都巧妙地避开了输入框被软键盘遮挡的情况，可参考这篇文章WebAPP输入框被软键盘遮挡肿么办？

JRoll使用translate3d滑动页面，可监听input聚焦事件，使用scrollTo方法将输入框移动到可见位置，在Android机上可解决被遮挡的问题，详见jroll-fixedinput组件

 

下载

建议：下载文件后将文件名版本号去掉，这样在JRoll有更新时只需要更新jroll.js文件，不需要更新引用jroll的文件。

jroll.2.3.2.js(30k)
jroll.2.3.2.min.js(14k)
jroll.2.3.0.js(28k)
jroll.2.3.0.min.js(14k)
jroll.2.2.1.js(27k)
jroll.2.2.1.min.js(13k)
jroll.2.2.0.js(27k)
jroll.2.2.0.min.js(13k)
jroll.2.1.0.js(28k)
jroll.2.1.0.min.js(13k)
jroll.2.0.0.beta(25k)
jroll.2.0.0.min.beta(12k)
版本日志

v2.3.2（2016-10-23）
兼容IE 9+。
优化滑动体验，bounce为false滑动到最大/最小值时重置计算开始点和结束点。
添加仿QQ列表侧滑删除案例
v2.3.0（2016-10-16）
支持PC浏览器（只为方便开发调试使用，并未在PC上作大量测试）。
解决wrapper的padding和scroller的margin造成maxWidth/maxHeight计算错误的问题。
v2.2.1（2016-07-29）
优化滑动。
utils工具添加IOS判断。
v2.2.0（2016-07-24）
防止按停滑动时误触a链接。
废除adjustTop选项。
抽离focusin/out到jroll-fixedinput组件。
滑动时例input/textarea失焦。
调整滑动数值。
v2.1.0（2016-07-01）
正式版!!!
修复若干bug。
调整滑动数值。
使用requestAnimationFrame执行回弹，解决IOS在大量dom时使用transition回弹卡顿问题。
textarea不出现滚动条时允许滚动JRoll实例。
scrollTo方法添加第五个参数->回调方法。
滚动条长度限制最小为8px。
删除了g可选项，分阶段使用不同的系数值。
v2.0.0（2016-06-19）
上线!!!
重写滑动算法，基于时间运动，解决帧频降低时滑动缓慢的问题。
更改垂直水平方向判断方法，使捕获垂直水平向更准确灵敏。
添加minX、maxX、minY、maxY选项。
添加touchEnd事件。
修改滚动条样式。
删除scroll选项。
 

插件

jroll-pulldown.js 下拉组件

下载：jroll-pulldown.js(9k) jroll-pulldown.min.js(6k)

说明：jroll-pulldown 使用文档

jroll-infinite.js 无限加载组件

下载：jroll-infinite.js(7k) jroll-infinite.min.js(4k)

详情：jroll-infinite 使用文档

jroll-fixedinput.js 固定输入框

下载：jroll-fixedinput.js(2k) jroll-fixedinput.min.js(1k)

详情：jroll-fixedinput 使用文档

 

JRoll 2 使用文档（史上最强大的下拉刷新，滚动，无限加载插件）
