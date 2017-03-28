HtmlNative
========

[Chinese](README_ch.md)

HtmlNative，use Html+css to render  Android native widget. Furthermore if you need some logic inside of it, HtmlNative also support lua script.

This repo stands upon some basic idea：

Although we have react-native and Weex, which are very strong and excellent, to enable us use javascript to write mobile applications.

But in order to master them, you need to climb up a rather steep learning curve, which may not be so friendly for everybody.

But html seems a lauguage that everybody know, so why not try using html to render native widget.

If you have idea, just make it work. Then HtmlNative is born.

## Example:


```html
<html>
<head>
    <style>
        #text1{
            color: #000;
            font-size: 16;
            padding: 10
        }
    </style>
</head>
<body>
    <p id="text1">
        This is an example of ImageView
        <br />2 Images are shown.
    </p>
    <img src="http://n.sinaimg.cn/news/crawl/20170302/18ey-fycaahm6004808.jpg" />
    <img src="http://n.sinaimg.cn/news/crawl/20170312/VUL1-fychhvn8494769.jpg" />
    
    <button onClick="changeText1">clickme</button>
</body>
<script type="text/lua">
    -- Toast in Android
    alert("hello world")
    
    -- Define a global variable
    b = false

    -- Define a function which responde to click event on button
    function changeText1()
        -- 通过id找到view
        local v = view("text1")
        
        -- 设置下样式
        if(b) then
            v.style("background:red;color:#fff")
        else
            v.style("background:blue;color:red")
        end

        b = not(b)

    end
    
    -- register the function with a clickevent name.
    callback("changeText1", changeText1)
    
    -- Done.

</script>
</html>
```

After rendering:

![screen1](show.gif)

## In Android

All you have to do is :

```java

// get the html file somewhere
String htmlStr = ...

HNative.getInstance().loadView(context, mActivity.getAssets().open(fileName), new HNative.OnHNViewLoaded() {

    @Override
    public void onViewLoaded(View v) {
        // do what ever you want to deal with this view
    }

    @Override
    public void onError(Exception e) {
        // if anything went wrong, for example, there is syntax error in html.
    }

    @Override
    public void onHead(HNHead head) {
        // here you can receive the <head> element, deal with title, meta...
    }
});

```

### License

Copyright 2016 Hsllany. All rights reserved.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

