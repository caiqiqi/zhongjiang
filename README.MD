今天在空间里看到一个所谓的""抽奖网站，想去看看是个什么情况，能诱导几个同学分享了它们的页面。[这](http://choujiang.dgyfsd.com/zhuanpan/)是它们的网站首页。看了一下，整个页面能给用户看到的就是一张图片而已(好吧，可能人家是专为手机用户设计的呢，知道晚上那么晚了看这个的应该是用手机吧)，</br>
![千万红包](https://github.com/caiqiqi/zhongjiang/blob/master/img/%E5%8D%83%E4%B8%87%E7%BA%A2%E5%8C%85.jpg)</br>
不管点这个页面的哪里，都是那张图片，而这张图片都指向[这里](http://choujiang.dgyfsd.com/zhuanpan/haoyunlai.html)，即同目录下的`haoyunlai.html`,大概是这么个样子![送你三次抽奖机会](https://github.com/caiqiqi/zhongjiang/blob/master/img/%E8%BF%98TMD%E9%80%81%E4%BD%A0%E4%B8%89%E6%AC%A1%E6%9C%BA%E4%BC%9A-%E6%98%8E%E6%98%8E%E4%BB%A3%E7%A0%81%E9%87%8C%E5%86%99%E6%AD%BB%E4%BA%86%E5%B0%8F%E4%BA%8E%E4%B8%89%E6%AC%A1%E5%B0%B1%E4%B8%8D%E4%BC%9A%E4%B8%AD%E7%9A%84.PNG) ![抽奖按钮](https://github.com/caiqiqi/zhongjiang/blob/master/img/%E6%8D%95%E8%8E%B7%E6%8C%89%E9%92%AE.PNG)</br>
放心，前两次一定不会中，因为代码里已经写死了。</br>
好,来看看为什么前两次不会中，第三次肯定中。</br>

首先注意到中间的“抽奖”按钮的`onclick()`属性，
```html
<div style="width: 369.231px; height: 369.231px; margin-left: -184.615px; margin-top: -184.615px; cursor: pointer;" id="btn_run" onclick="choujiang();"><img src="%E5%A5%BD%E5%8F%8B%E9%80%81%E4%BD%A03%E6%AC%A1%E6%9C%BA%E4%BC%9A%EF%BC%81_files/TB2JXL8hXXXXXbtXXXXXXXXXXXX_75928067.png" alt="" style="width: 100%;height: 100%"></div>

```
你点击“抽奖”之后，执行`choujiang()`方法
```javascript
//用户点击“抽奖”之后，发生的逻辑
    function choujiang(){
        //让这个按钮不能再被点击了
        $("#btn_run").attr('disabled', true).css("cursor", "default");
        //在抽奖次数小于3的情况下
        if(getCookie('times')<3){
           if(powerby==0){
               powerby=1;
               choujiangcishu();
               //抽奖时播放的那段声音
               playVid();
               //然后进行判决是否中奖
               lottery();
           }
        }
    }
```
它从当前的cookie中获取"times"属性的值，如果小于3，就先给你放一段抽奖的声音，然后用`lottery()`方法判定是否中奖。
```javascript
//判定抽奖结果的方法
    function lottery() {
        var now_times=getCookie('times');
        if(now_times<3){
            buzhong();
        }else{
            zhong();
            di2();
        }
    }
```
可以看出，如果你“抽奖”的次数小于3，它就判定你不中奖，然后自己假装捣鼓一通之后，告诉你“嘿嘿真不巧，你没中奖诶”，然后终于第三次你点击“抽奖”，诶，捣鼓捣鼓之后，人给你返回“成功”，然后弹出对话框告诉你，“哎妈呀，你中奖了，但是你得分享到QQ空间之后才能真的收到奖品”，然后你一点那个“确定”按钮啊，人就给你构造好一个分享到QQ空间的url，然后你啥也不看就分享了，然后你就又给人做广告了，引诱更多的小伙伴进来帮它继续做广告。</br>
另外提一下，它判断你有没有分享到QQ空间的逻辑也挺逗，就看你点没点那个弹出的对话框上的“确定”按钮，点了就认为你分享到QQ空间了，然后就跳转到什么“手表”页面，然后那么扯的玩意儿就先不扯了。。。</br>
咳咳，最后徐说一下，我觉得年轻人， 诶，应该提高一下， 啊，这个，英文水平，特别是写前端的，你的代码是完全交给客户端的，不要像这个代码君，命名真逗。</br>

![命名](https://github.com/caiqiqi/zhongjiang/blob/master/img/%E5%90%8D%E5%AD%97.PNG)
