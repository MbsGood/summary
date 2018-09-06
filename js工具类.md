#### 图片懒加载

```
//图片没加载出来时用一张图片代替
aftLoadImg: function (obj, url, errorUrl,cb) {
    var oImg = new Image(), _this = this;
    oImg.src = url;
    oImg.onload = function () {
        obj.src = oImg.src;
        if (cb && _this.istype(cb, 'function')) {
            cb(obj);
        }
    }
    oImg.onerror=function () {
        obj.src=errorUrl;
        if (cb && _this.istype(cb, 'function')) {
            cb(obj);
        }
    }
},
//图片滚动懒加载
//@className {string} 要遍历图片的类名
//@num {number} 距离多少的时候开始加载 默认 0
//比如，一张图片距离文档顶部3000，num参数设置200，那么在页面滚动到2800的时候，图片加载。不传num参数就滚动，num默认是0，页面滚动到3000就加载
//html代码
//<p><img data-src="https://user-gold-cdn.xitu.io/2017/12/7/160319f12631736f" class="load-img" width='528' height='304' /></p>
//<p><img data-src="https://user-gold-cdn.xitu.io/2017/12/7/160319f12631736f" class="load-img" width='528' height='304' /></p>
//<p><img data-src="https://user-gold-cdn.xitu.io/2017/12/7/160319f12631736f" class="load-img" width='528' height='304' /></p>....
//data-src储存src的数据，到需要加载的时候把data-src的值赋值给src属性，图片就会加载。
//详细可以查看testLoadImg.html
//window.onload = function() {
//    loadImg('load-img',100);
//    window.onscroll = function() {
//        loadImg('load-img',100);
//        }
//}
loadImg: function (className, num, errorUrl) {
    var _className = className || 'ec-load-img', _num = num || 0, _this = this,_errorUrl=errorUrl||null;
    var oImgLoad = document.getElementsByClassName(_className);
    for (var i = 0, len = oImgLoad.length; i < len; i++) {
        //如果图片已经滚动到指定的高度
        if (document.documentElement.clientHeight + document.documentElement.scrollTop > oImgLoad[i].offsetTop - _num && !oImgLoad[i].isLoad) {
            //记录图片是否已经加载
            oImgLoad[i].isLoad = true;
            //设置过渡，当图片下来的时候有一个图片透明度变化
            oImgLoad[i].style.cssText = "transition: ''; opacity: 0;"
            if (oImgLoad[i].dataset) {
                this.aftLoadImg(oImgLoad[i], oImgLoad[i].dataset.src, _errorUrl, function (o) {
                    //添加定时器，确保图片已经加载完了，再把图片指定的的class，清掉，避免重复编辑
                    setTimeout(function () {
                        if (o.isLoad) {
                            _this.removeClass(o, _className);
                            o.style.cssText = "";
                        }
                    }, 1000)
                });
            } else {
                this.aftLoadImg(oImgLoad[i], oImgLoad[i].getAttribute("data-src"), _errorUrl, function (o) {
                    //添加定时器，确保图片已经加载完了，再把图片指定的的class，清掉，避免重复编辑
                    setTimeout(function () {
                        if (o.isLoad) {
                            _this.removeClass(o, _className);
                            o.style.cssText = "";
                        }
                    }, 1000)
                });
            }
            (function (i) {
                setTimeout(function () {
                    oImgLoad[i].style.cssText = "transition:all 1s; opacity: 1;";
                }, 16)
            })(i);
        }
    }
}
 

```

#### 关键词加标签/高亮

```
//这两个函数多用于搜索的时候，关键词高亮
//创建正则字符
//createKeyExp([前端，过来])
//result:(前端|过来)/g

createKeyExp: function (strArr) {
    var str = "";
    for (var i = 0; i < strArr.length; i++) {
        if (i != strArr.length - 1) {
            str = str + strArr[i] + "|";
        } else {
            str = str + strArr[i];
        }
    }
    return "(" + str + ")";
}

//关键字加标签（多个关键词用空格隔开）
//findKey('守侯我oaks接到了来自下次你离开快乐吉祥留在开城侯','守侯 开','i')
//"<i>守侯</i>我oaks接到了来自下次你离<i>开</i>快乐吉祥留在<i>开</i>城侯"

findKey: function (str, key, el) {
    var arr = null,
        regStr = null,
        content = null,
        Reg = null,
        _el = el || 'span';
    arr = key.split(/\s+/);
    //alert(regStr); //    如：(前端|过来)
    regStr = this.createKeyExp(arr);
    content = str;
    //alert(Reg);//        /如：(前端|过来)/g
    Reg = new RegExp(regStr, "g");
    //过滤html标签 替换标签，往关键字前后加上标签
    content = content.replace(/<\/?[^>]*>/g, '')
    return content.replace(Reg, "<" + _el + ">$1</" + _el + ">");
}

```

#### 数据类型判断

```
//istype([],'array')
//true
//istype([])
//'[object Array]'
istype: function (o, type) {
    if (type) {
        var _type = type.toLowerCase();
    }
    switch (_type) {
        case 'string':
            return Object.prototype.toString.call(o) === '[object String]';
        case 'number':
            return Object.prototype.toString.call(o) === '[object Number]';
        case 'boolean':
            return Object.prototype.toString.call(o) === '[object Boolean]';
        case 'undefined':
            return Object.prototype.toString.call(o) === '[object Undefined]';
        case 'null':
            return Object.prototype.toString.call(o) === '[object Null]';
        case 'function':
            return Object.prototype.toString.call(o) === '[object Function]';
        case 'array':
            return Object.prototype.toString.call(o) === '[object Array]';
        case 'object':
            return Object.prototype.toString.call(o) === '[object Object]';
        case 'nan':
            return isNaN(o);
        case 'elements':
            return Object.prototype.toString.call(o).indexOf('HTML') !== -1
        default:
            return Object.prototype.toString.call(o)
    }
}

```

#### 手机类型判断

```
browserInfo: function (type) {
    switch (type) {
        case 'android':
            return navigator.userAgent.toLowerCase().indexOf('android') !== -1
        case 'iphone':
            return navigator.userAgent.toLowerCase().indexOf('iphone') !== -1
        case 'ipad':
            return navigator.userAgent.toLowerCase().indexOf('ipad') !== -1
        case 'weixin':
            return navigator.userAgent.toLowerCase().indexOf('micromessenger') !== -1
        default:
            return navigator.userAgent.toLowerCase()
    }
}
 

```

#### 函数节流

```
//多用于鼠标滚动，移动，窗口大小改变等高频率触发事件
// var count=0;
// function fn1(){
//     count++;
//     console.log(count)
// }
// //100ms内连续触发的调用，后一个调用会把前一个调用的等待处理掉，但每隔200ms至少执行一次
// document.onmousemove=delayFn(fn1,100,200)

delayFn: function (fn, delay, mustDelay) {
    var timer = null;
    var t_start;
    return function () {
        var context = this, args = arguments, t_cur = +new Date();
        //先清理上一次的调用触发（上一次调用触发事件不执行）
        clearTimeout(timer);
        //如果不存触发时间，那么当前的时间就是触发时间
        if (!t_start) {
            t_start = t_cur;
        }
        //如果当前时间-触发时间大于最大的间隔时间（mustDelay），触发一次函数运行函数
        if (t_cur - t_start >= mustDelay) {
            fn.apply(context, args);
            t_start = t_cur;
        }
        //否则延迟执行
        else {
            timer = setTimeout(function () {
                fn.apply(context, args);
            }, delay);
        }
    };
}
 
```

