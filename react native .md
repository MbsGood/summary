react native 开发例子</br>
极光推送：https://github.com/jpush/jpush-react-native </br>
emoji表情：https://github.com/omnidan/node-emoji</br>
高德定位：https://github.com/qiuxiang/react-native-amap-geolocation</br>
录音：https://github.com/jsierles/react-native-audio</br>
模糊视图：https://github.com/react-native-community/react-native-blur</br>
相机：https://github.com/react-native-community/react-native-camera</br>
热更新：https://github.com/Microsoft/react-native-code-push</br>
通讯录：https://github.com/rt2zz/react-native-contacts</br>
element-ui：https://github.com/react-native-training/react-native-elements</br>
文件传输：https://github.com/wkh237/react-native-fetch-blob</br>
iap：https://github.com/dooboolab/react-native-iap</br>
图片选择器，这里有两个，各有特点：</br>
1.https://github.com/react-community/react-native-image-picker</br>
2.https://github.com/ivpusic/react-native-image-crop-picker</br>
图片缓存：https://github.com/wcandillon/react-native-img-cache</br>
进度条：https://github.com/oblador/react-native-progress</br>
二维码生成：https://github.com/cssivision/react-native-qrcode</br>
二维码扫描：https://github.com/moaazsidat/react-native-qrcode-scanner</br>
滚动tab：https://github.com/happypancake/react-native-scrollable-tab-view</br>
音频播放：https://github.com/zmxv/react-native-sound</br>
视频播放器：https://github.com/easyui/react-native-ezplayer</br>
加载动画：https://github.com/maxs15/react-native-spinkit</br>
启动白屏解决：https://github.com/crazycodeboy/react-native-splash-screen</br>
icon：https://github.com/oblador/react-native-vector-icons</br>
视频播放：https://github.com/react-native-community/react-native-video</br>
本地视频压缩（目前好像只支持IOS，安卓有报错）：https://github.com/shahen94/react-native-video-processing</br>
微信SDK：https://github.com/yorkie/react-native-wechat</br>
很不错的UI库：https://github.com/rilyu/teaset</br>
聊天UI：https://github.com/FaridSafi/react-native-gifted-chat</br>
自定义下拉刷新插件：https://github.com/react-native-studio/react-native-SmartRefreshLayout</br>
https://bolan9999.github.io/react-native-spring-scrollview/#/?id=react-native-spring-scrollview%E6%98%AF%E4%BB%80%E4%B9%88%EF%BC%9F</br>
适配工具类：https://bbs.reactnative.cn/topic/5727/react-native-%E9%80%82%E9%85%8D%E5%B7%A5%E5%85%B7%E7%B1%BB</br>
可拖动排序的标签组件：https://github.com/bolan9999/react-native-drag-to-sort-tags</br>
TabBar中间按钮，播放旋转动画 ： https://github.com/afresh/tadpole</br>
SectionList 多级列表下拉刷新 ：https://github.com/bolan9999/react-native-largelist</br>
高德地图react-native：https://gitee.com/1148030615/rn-AmapLocation</br>
缓存管理：https://www.npmjs.com/package/react-native-http-cache</br>
弹幕插件：https://github.com/react-native-studio/react-native-android-danmaku</br>
自定义字体：https://bbs.reactnative.cn/topic/204/%E8%AE%BE%E7%BD%AEreact-native%E8%87%AA%E5%AE%9A%E4%B9%89%E5%AD%97%E4%BD%93/3</br>





## 一些比较的好的js工具类，可以直接引用来封装</br>

### 去除字符串空格

```
//去除空格  type 1-所有空格  2-前后空格  3-前空格 4-后空格
//trim('  1235asd',1)
//result：1235asd
//这个方法有原生的方案代替，但是考虑到有时候开发PC站需要兼容IE8，所以就还是继续保留

trim: function (str, type) {
    switch (type) {
        case 1:
            return str.replace(/\s+/g, "");
        case 2:
            return str.replace(/(^\s*)|(\s*$)/g, "");
        case 3:
            return str.replace(/(^\s*)/g, "");
        case 4:
            return str.replace(/(\s*$)/g, "");
        default:
            return str;
    }
}
```



### 字母大小写切换

```
/*type
 1:首字母大写
 2：首页母小写
 3：大小写转换
 4：全部大写
 5：全部小写

- */
  //changeCase('asdasd',1)
  //result：Asdasd

changeCase: function (str, type) {
    function ToggleCase(str) {
        var itemText = ""
        str.split("").forEach(
            function (item) {
                if (/^([a-z]+)/.test(item)) {
                    itemText += item.toUpperCase();
                } else if (/^([A-Z]+)/.test(item)) {
                    itemText += item.toLowerCase();
                } else {
                    itemText += item;
                }
            });
        return itemText;
    }
    switch (type) {
        case 1:
            return str.replace(/\b\w+\b/g, function (word) {
                return word.substring(0, 1).toUpperCase() + word.substring(1).toLowerCase();
            });
        case 2:
            return str.replace(/\b\w+\b/g, function (word) {
                return word.substring(0, 1).toLowerCase() + word.substring(1).toUpperCase();
            });
        case 3:
            return ToggleCase(str);
        case 4:
            return str.toUpperCase();
        case 5:
            return str.toLowerCase();
        default:
            return str;
    }
}
```



### 字符串循环复制

```
//repeatStr(str->字符串, count->次数)
//repeatStr('123',3)
//"result：123123123"

repeatStr: function (str, count) {
    var text = '';
    for (var i = 0; i < count; i++) {
        text += str;
    }
    return text;
}
```



### 字符串替换

```
//replaceAll('这里是上海，中国第三大城市，广东省省会，简称穗，','上海','广州')
//result："这里是广州，中国第三大城市，广东省省会，简称穗，"

replaceAll: function (str, AFindText, ARepText) {
    raRegExp = new RegExp(AFindText, "g");
    return str.replace(raRegExp, ARepText);
}
```



### 字符串替换*

```
//字符替换*
//replaceStr(字符串,字符格式, 替换方式,替换的字符（默认*）)
//replaceStr('18819322663',[3,5,3],0)
//result：188*****663
//replaceStr('asdasdasdaa',[3,5,3],1)
//result：***asdas***
//replaceStr('1asd88465asdwqe3',[5],0)
//result：*****8465asdwqe3
//replaceStr('1asd88465asdwqe3',[5],1,'+')
//result："1asd88465as+++++"

replaceStr: function (str, regArr, type, ARepText) {
    var regtext = '',
        Reg = null,
        replaceText = ARepText || '*';
    //repeatStr是在上面定义过的（字符串循环复制），大家注意哦
    if (regArr.length === 3 && type === 0) {
        regtext = '(\\w{' + regArr[0] + '})\\w{' + regArr[1] + '}(\\w{' + regArr[2] + '})'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[1]);
        return str.replace(Reg, '$1' + replaceCount + '$2')
    }
    else if (regArr.length === 3 && type === 1) {
        regtext = '\\w{' + regArr[0] + '}(\\w{' + regArr[1] + '})\\w{' + regArr[2] + '}'
        Reg = new RegExp(regtext);
        var replaceCount1 = this.repeatStr(replaceText, regArr[0]);
        var replaceCount2 = this.repeatStr(replaceText, regArr[2]);
        return str.replace(Reg, replaceCount1 + '$1' + replaceCount2)
    }
    else if (regArr.length === 1 && type === 0) {
        regtext = '(^\\w{' + regArr[0] + '})'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
    else if (regArr.length === 1 && type === 1) {
        regtext = '(\\w{' + regArr[0] + '}$)'
        Reg = new RegExp(regtext);
        var replaceCount = this.repeatStr(replaceText, regArr[0]);
        return str.replace(Reg, replaceCount)
    }
}
```



### 检测字符串

```
//检测字符串
//checkType('165226226326','phone')
//result：false
//大家可以根据需要扩展

checkType: function (str, type) {
    switch (type) {
        case 'email':
            return /^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$/.test(str);
        case 'phone':
            return /^1[3|4|5|7|8][0-9]{9}$/.test(str);
        case 'tel':
            return /^(0\d{2,3}-\d{7,8})(-\d{1,4})?$/.test(str);
        case 'number':
            return /^[0-9]$/.test(str);
        case 'english':
            return /^[a-zA-Z]+$/.test(str);
        case 'text':
            return /^\w+$/.test(str);
        case 'chinese':
            return /^[\u4E00-\u9FA5]+$/.test(str);
        case 'lower':
            return /^[a-z]+$/.test(str);
        case 'upper':
            return /^[A-Z]+$/.test(str);
        default:
            return true;
    }
}
```



### 检测密码强度

```
//checkPwd('12asdASAD')
//result：3(强度等级为3)

checkPwd: function (str) {
    var nowLv = 0;
    if (str.length < 6) {
        return nowLv
    }
    if (/[0-9]/.test(str)) {
        nowLv++
    }
    if (/[a-z]/.test(str)) {
        nowLv++
    }
    if (/[A-Z]/.test(str)) {
        nowLv++
    }
    if (/[\.|-|_]/.test(str)) {
        nowLv++
    }
    return nowLv;
}
```



### 随机码（toString详解）

```
//count取值范围0-36
//randomWord(10)
//result："2584316588472575"
//randomWord(14)
//result："9b405070dd00122640c192caab84537"
//randomWord(36)
//result："83vhdx10rmjkyb9"

randomWord: function (count) {
    return Math.random().toString(count).substring(2);
}
```



### 查找字符串出现次数

```
//过滤字符串(html标签，表情，特殊字符)
//字符串，替换内容（special-特殊字符,html-html标签,emjoy-emjoy表情,word-小写字母，WORD-大写字母，number-数字,chinese-中文），要替换成什么，默认'',保留哪些特殊字符
//如果需要过滤多种字符，type参数使用,分割，如下栗子
//过滤字符串的html标签，大写字母，中文，特殊字符，全部替换成*,但是特殊字符'%'，'?'，除了这两个，其他特殊字符全部清除
//var str='asd    654a大蠢sasdasdASDQWEXZC6d5#%^*^&*^%^&*$\\"\'#@!()*/-())_\'":"{}?<div></div><img src=""/>啊实打实大蠢猪自行车这些课程';
// filterStr(str,'html,WORD,chinese,special','*','%?')
//result："asd    654a**sasdasd*********6d5#%^*^&*^%^&*$\"'#@!()*/-())_'":"{}?*****************"

filterStr: function (str, type, restr, spstr) {
    var typeArr = type.split(','), _str = str;
    for (var i = 0, len = typeArr.length; i < len; i++) {
        //是否是过滤特殊符号
        if (typeArr[i] === 'special') {
            var pattern, regText = '$()[]{}?\|^*+./\"\'+';
            //是否有哪些特殊符号需要保留
            if (spstr) {
                var _spstr = spstr.split(""), _regText = "[^0-9A-Za-z\\s";
                for (var j = 0, len1 = _spstr.length; j < len1; j++) {
                    if (regText.indexOf(_spstr[j]) === -1) {
                        _regText += _spstr[j];
                    }
                    else {
                        _regText += '\\' + _spstr[j];
                    }
                }
                _regText += ']'
                pattern = new RegExp(_regText, 'g');
            }
            else {
                pattern = new RegExp("[^0-9A-Za-z\\s]", 'g')
            }
        }
        var _restr = restr || '';
        switch (typeArr[i]) {
            case 'special':
                _str = _str.replace(pattern, _restr);
                break;
            case 'html':
                _str = _str.replace(/<\/?[^>]*>/g, _restr);
                break;
            case 'emjoy':
                _str = _str.replace(/[^\u4e00-\u9fa5|\u0000-\u00ff|\u3002|\uFF1F|\uFF01|\uff0c|\u3001|\uff1b|\uff1a|\u3008-\u300f|\u2018|\u2019|\u201c|\u201d|\uff08|\uff09|\u2014|\u2026|\u2013|\uff0e]/g, _restr);
                break;
            case 'word':
                _str = _str.replace(/[a-z]/g, _restr);
                break;
            case 'WORD':
                _str = _str.replace(/[A-Z]/g, _restr);
                break;
            case 'number':
                _str = _str.replace(/[0-9]/g, _restr);
                break;
            case 'chinese':
                _str = _str.replace(/[\u4E00-\u9FA5]/g, _restr);
                break;
        }
    }
    return _str;
}
```



### 格式化处理字符串

```
//formatText('1234asda567asd890')
//result："12,34a,sda,567,asd,890"

//formatText('1234asda567asd890',4,' ')
//result："1 234a sda5 67as d890"

//formatText('1234asda567asd890',4,'-')
//result："1-234a-sda5-67as-d890"

formatText: function (str, size, delimiter) {
    var _size = size || 3, _delimiter = delimiter || ',';
    var regText = '\\B(?=(\\w{' + _size + '})+(?!\\w))';
    var reg = new RegExp(regText, 'g');
    return str.replace(reg, _delimiter);
}
```



### 找出最长单词

```
//longestWord('Find the Longest word in a String')
//result：7

//longestWord('Find|the|Longest|word|in|a|String','|')
//result：7

longestWord: function (str, splitType) {
    var _splitType = splitType || /\s+/g,
        _max = 0,_item='';
    var strArr = str.split(_splitType);
    strArr.forEach(function (item) {
        if (_max < item.length) {
            _max = item.length
            _item=item;
        }
    })
    return {el:_item,max:_max};
}
```



### 现金额转大写

 * ```
    /**
    
    - 
    - @desc   现金额转大写
    - @param  {Number} n 
    - @return {String}
      */
      function digitUppercase(n) {
      var fraction = ['角', '分'];
      var digit = [
          '零', '壹', '贰', '叁', '肆',
          '伍', '陆', '柒', '捌', '玖'
      ];
      var unit = [
          ['元', '万', '亿'],
          ['', '拾', '佰', '仟']
      ];
      var head = n < 0 ? '欠' : '';
      n = Math.abs(n);
      var s = '';
      for (var i = 0; i < fraction.length; i++) {
          s += (digit[Math.floor(n * 10 * Math.pow(10, i)) % 10] + fraction[i]).replace(/零./, '');
      }
      s = s || '整';
      n = Math.floor(n);
      for (var i = 0; i < unit[0].length && n > 0; i++) {
          var p = '';
          for (var j = 0; j < unit[1].length && n > 0; j++) {
              p = digit[n % 10] + unit[1][j] + p;
              n = Math.floor(n / 10);
          }
          s = p.replace(/(零.)*零$/, '').replace(/^$/, '零') + unit[0][i] + s;
      }
      return head + s.replace(/(零.)*零元/, '元')
          .replace(/(零.)+/g, '零')
          .replace(/^整$/, '零元整');
      };
    ```

    





## 数组操作

#### 数组去重

```
removeRepeatArray: function (arr) {
    return arr.filter(function (item, index, self) {
        return self.indexOf(item) === index;
    });
}
 
```

 

####  数组顺序打乱

```
upsetArr: function (arr) {
    return arr.sort(function () {
        return Math.random() - 0.5
    });
},
```

####  数组最大值最小值

```
//数组最大值
maxArr: function (arr) {
    return Math.max.apply(null, arr);
},
//数组最小值
minArr: function (arr) {
    return Math.min.apply(null, arr);
}
 
```

#### 数组求和，平均值

```
//这一块的封装，主要是针对数字类型的数组
//求和
sumArr: function (arr) {
    return arr.reduce(function (pre, cur) {
        return pre + cur
    })
}
//数组平均值,小数点可能会有很多位，这里不做处理，处理了使用就不灵活！
covArr: function (arr) {
    return this.sumArr(arr) / arr.length;
},
 
```

####  从数组中随机获取元素 

```
//randomOne([1,2,3,6,8,5,4,2,6])
//2

randomOne: function (arr) {
    return arr[Math.floor(Math.random() * arr.length)];
}

```

#### 回数组字符串一个元素出现的次数

```
//getEleCount([1,2,3,4,5,66,77,22,55,22],22)
//result：2

getEleCount: function (obj, ele) {
    var num = 0;
    for (var i = 0, len = obj.length; i < len; i++) {
        if (ele === obj[i]) {
            num++;
        }
    }
    return num;
}

```

#### 数组/字符串出现最多的几次元素和出现次数

```
//arr, rank->长度，默认为数组长度，ranktype，排序方式，默认降序
//返回值：el->元素，count->次数
//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2])
//默认情况，返回所有元素出现的次数
//result：[{"el":"2","count":6},{"el":"1","count":4},{"el":"3","count":2},{"el":"4","count":1},{"el":"5","count":1},{"el":"6","count":1}]

//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],3)
//传参（rank=3），只返回出现次数排序前三的
//result：[{"el":"2","count":6},{"el":"1","count":4},{"el":"3","count":2}]

//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],null,1)
//传参（ranktype=1,rank=null），升序返回所有元素出现次数
//result：[{"el":"6","count":1},{"el":"5","count":1},{"el":"4","count":1},{"el":"3","count":2},{"el":"1","count":4},{"el":"2","count":6}]

//getCount([1,2,3,1,2,5,2,4,1,2,6,2,1,3,2],3,1)
//传参（rank=3，ranktype=1），只返回出现次数排序（升序）前三的
//result：[{"el":"6","count":1},{"el":"5","count":1},{"el":"4","count":1}]

getCount: function (arr, rank, ranktype) {
    var obj = {},
        k, arr1 = []
    //记录每一元素出现的次数
    for (var i = 0, len = arr.length; i < len; i++) {
        k = arr[i];
        if (obj[k]) {
            obj[k]++;
        } else {
            obj[k] = 1;
        }
    }
    //保存结果{el-'元素'，count-出现次数}
    for (var o in obj) {
        arr1.push({el: o, count: obj[o]});
    }
    //排序（降序）
    arr1.sort(function (n1, n2) {
        return n2.count - n1.count
    });
    //如果ranktype为1，则为升序，反转数组
    if (ranktype === 1) {
        arr1 = arr1.reverse();
    }
    var rank1 = rank || arr1.length;
    return arr1.slice(0, rank1);
}

```

#### 得到n1-n2下标的数组 

```
//getArrayNum([0,1,2,3,4,5,6,7,8,9],2) //不传第二个参数,默认返回从n1到数组结束的元素
//result：[2, 3, 4, 5, 6, 7, 8, 9]

getArrayNum: function (arr, n1, n2) {
    return arr.slice(n1, n2);
}

```

#### 筛选数组

```
/删除值为'val'的数组元素
//removeArrayForValue(['test','test1','test2','test','aaa'],'test',')
//result：["aaa"]   带有'test'的都删除

//removeArrayForValue(['test','test1','test2','test','aaa'],'test')
//result：["test1", "test2", "aaa"]  //数组元素的值全等于'test'才被删除

removeArrayForValue: function (arr, val, type) {
    return arr.filter(function (item) {
        return type ? item.indexOf(val) === -1 : item !== val
    })
}

```

#### 获取对象数组某些项

```
//var arr=[{a:1,b:2,c:9},{a:2,b:3,c:5},{a:5,b:9},{a:4,b:2,c:5},{a:4,b:5,c:7}]
//getOptionArray(arr,'a,c')
//result：[{a:1,c:9},{a:2,c:5},{a:5,c:underfind},{a:4,c:5},{a:4,c:7}]

//getOptionArray(arr,'b')
//result：[2, 3, 9, 2, 5]

getOptionArray: function (arr, keys) {
    var newArr = []
    if (!keys) {
        return arr
    }
    var _keys = keys.split(','), newArrOne = {};
    //是否只是需要获取某一项的值
    if (_keys.length === 1) {
        for (var i = 0, len = arr.length; i < len; i++) {
            newArr.push(arr[i][keys])
        }
        return newArr;
    }
    for (var i = 0, len = arr.length; i < len; i++) {
        newArrOne = {};
        for (var j = 0, len1 = _keys.length; j < len1; j++) {
            newArrOne[_keys[j]] = arr[i][_keys[j]]
        }
        newArr.push(newArrOne);
    }
    return newArr
}

```

####  排除对象数组某些项

```
//var arr=[{a:1,b:2,c:9},{a:2,b:3,c:5},{a:5,b:9},{a:4,b:2,c:5},{a:4,b:5,c:7}]
//filterOptionArray(arr,'a')
//result：[{b:2,c:9},{b:3,c:5},{b:9},{b:2,c:5},{b:5,c:7}]
//filterOptionArray(arr,'a,c')
//result：[{b:2},{b:3},{b:9},{b:2},{b:5}]
filterOptionArray: function (arr, keys) {
    var newArr = []
    var _keys = keys.split(','), newArrOne = {};
    for (var i = 0, len = arr.length; i < len; i++) {
        newArrOne = {};
        for (var key in arr[i]) {
            //如果key不存在排除keys里面,添加数据
            if (_keys.indexOf(key) === -1) {
                newArrOne[key] = arr[i][key];
            }
        }
        newArr.push(newArrOne);
    }
    return newArr
}
```

#### 对象数组排序

```
//var arr=[{a:1,b:2,c:9},{a:2,b:3,c:5},{a:5,b:9},{a:4,b:2,c:5},{a:4,b:5,c:7}]
//arraySort(arr,'a,b')a是第一排序条件，b是第二排序条件
//result：[{"a":1,"b":2,"c":9},{"a":2,"b":3,"c":5},{"a":4,"b":2,"c":5},{"a":4,"b":5,"c":7},{"a":5,"b":9}]

arraySort: function (arr, sortText) {
    if (!sortText) {
        return arr
    }
    var _sortText = sortText.split(',').reverse(), _arr = arr.slice(0);
    for (var i = 0, len = _sortText.length; i < len; i++) {
        _arr.sort(function (n1, n2) {
            return n1[_sortText[i]] - n2[_sortText[i]]
        })
    }
    return _arr;
}
 
```

#### 判断两个数组是否相等

```
/**
 * 
 * @desc 判断两个数组是否相等
 * @param {Array} arr1 
 * @param {Array} arr2 
 * @return {Boolean}
 */
function arrayEqual(arr1, arr2) {
    if (arr1 === arr2) return true;
    if (arr1.length != arr2.length) return false;
    for (var i = 0; i < arr1.length; ++i) {
        if (arr1[i] !== arr2[i]) return false;
    }
    return true;
}
```

