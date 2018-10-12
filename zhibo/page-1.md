<div class="three-fourth fr">
                <h1 id="toc_0">WEB SDK开发指南</h1><p>版本：2.5.0<br>
日期：2018年09月12日</p><ul><li><a href="#toc_0">WEB SDK开发指南</a><ul><li><a href="#toc_1">概述</a></li><li><a href="#toc_2">直播SDK</a><ul><li><a href="#toc_3">依赖库</a></li><li><a href="#toc_4">调用方法</a></li><li><a href="#toc_5">主动调用 API</a></li><li><a href="#toc_6">直播响应事件 API</a></li><li><a href="#toc_7">返回值说明</a></li><li><a href="#toc_8">关键代码示例</a></li><li><a href="#toc_9">备注与说明</a></li><li><a href="#toc_10">附录1. 表情和a链接解析处理方法</a></li><li><a href="#toc_11">附录2. demo使用方法</a></li></ul></li><li><a href="#toc_12">回放SDK</a><ul><li><a href="#toc_13">依赖库</a></li><li><a href="#toc_14">调用方法</a></li><li><a href="#toc_15">回放响应事件 API</a></li><li><a href="#toc_16">返回值说明</a></li><li><a href="#toc_17">跳转到指定时间播放</a></li><li><a href="#toc_18">获取当前播放时间</a></li><li><a href="#toc_19">获取视频总时长</a></li><li><a href="#toc_20">文档自适应</a></li><li><a href="#toc_21">PC端回放播放器API</a></li><li><a href="#toc_22">附录 demo使用方法</a></li></ul></li><li><a href="#toc_23">版本更新记录</a></li></ul></li></ul><h2 id="toc_1">概述</h2><p>利用WEB SDK可以与CC视频直播系统进行对接，灵活调用直播和回放的视频、文档、聊天、问答等模块，在您的网页中实现自定义样式界面展示直播和回放。</p><h2 id="toc_2">直播SDK</h2><h3 id="toc_3">依赖库</h3><p>直播SDK依赖于jQuery，请自行引入 jQuery 库，版本没有要求。</p><h3 id="toc_4">调用方法</h3><p><span class="impor">页面引入 jQuery：</span></p><pre><code>&lt;script src="//view.csslcloud.net/js/jquery-1.9.0.min.js" type="text/javascript"&gt;&lt;/script&gt;
</code></pre><p><span class="impor">页面引入 JS SDK：</span></p><pre><code>&lt;script src="//view.csslcloud.net/js/liveSDK.js" type="text/javascript"&gt;&lt;/script&gt;
</code></pre><p><span class="impor">视频模块：</span></p><pre><code>&lt;div id="livePlayer"&gt;&lt;/div&gt;
</code></pre><p><span class="impor">文档模块：</span></p><pre><code>&lt;div id="drawPanel"&gt;&lt;/div&gt;
</code></pre><p><span class="impor">初始化：</span></p><pre><code>&lt;script type="text/javascript"&gt;
    DWLive.init({
        userid: 'userid',
        roomid: 'roomid',
        viewername: 'name',
        viewertoken: 'password',
        viewercustomua: 'android',
        language: 'en',
        viewercustominfo: '{"exportInfos": [ {"key": "城市", "value": "北京"}, {"key": "姓名", "value": "哈哈"}]}',
        fastMode:true
    });
&lt;/script&gt;
</code></pre><table width="900px"><tbody><tr style="background:#F60;color:#FFF"><td>参数</td><td>说明</td></tr><tr><td>userid</td><td>用户 id，不可为空</td></tr><tr><td>roomid</td><td>直播间id，不可为空</td></tr><tr><td>viewername</td><td>用户名称，可为空</td></tr><tr><td>viewertoken</td><td>需要密码验证方式时，不可为空</td></tr><tr><td>viewercustomua</td><td>自定义UA参数，配合接口验证使用，可为空</td></tr><tr><td>language</td><td>en，英文版flash播放器，可为空</td></tr><tr><td>viewercustominfo</td><td>json格式字符串，可选，自定义用户信息，该信息会记录在用户访问记录中，用于统计分析使用（长度不能超过1000个字符，若直播间启用接口验证则该参数无效）
</td></tr><tr><td>fastMode</td><td>是否开启极速动画模式</td></tr></tbody></table><h3 id="toc_5">主动调用 API</h3><table width="900px"><tbody><tr style="background:#F60;color:#FFF"><td>API</td><td>说明</td></tr><tr><td>sendPublicChatMsg(msg)</td><td>发送公聊，msg:消息内容</td></tr><tr><td>sendPrivateChatMsg(touserid,tousername,msg)</td><td>发送私聊，
        touserid:接收者的viewerid，tousername:接收者的viewername，msg:消息内容</td></tr><tr><td>sendQuestionMsg(msg)</td><td>发送问题，msg:消息内容</td></tr><tr><td>barrage(msg, color)</td><td>发送弹幕，color为十六进制颜色值(0xffffff)，仅支持PC端</td></tr><tr><td>getLine()</td><td>获取线路</td></tr><tr><td>changeLine(num)</td><td>切换线路，num: getLine返回的值(0,1)</td></tr>
   <tr><td>onlyAudio()</td><td>只听音频</td></tr>
   <tr><td>setSound(num)</td><td>音量调节，num: 0-1</td></tr><tr><td>answerRollcall(rid, pid)</td><td>签到，rid:rollcallId，pid:publisherId</td></tr><tr><td>replyVote(voteid, option, pid)</td><td>答题，voteid:voteId，option:答题选项，pid:publisherId</td></tr><tr><td>docBarrage(msg, color)</td><td>文档弹幕，color为十六进制颜色值(0xffffff)，仅支持PC端</td></tr><tr><td>openBarrage(true/false)</td><td>弹幕开关，仅支持PC端</td></tr><tr><td>showControl(true/false)</td><td>控制条显示隐藏</td></tr><tr><td>requestInteraction</td><td>请求语音互动</td></tr><tr><td>hangupInteraction</td><td>挂断双向视频</td></tr><tr><td>enterInteractionRoom</td><td>进入互动房间</td></tr><tr><td>sendInteractionMessage</td><td>发送互动信息</td></tr><tr><td>docAdapt(true/false)</td><td>文档自适应，默认为false关闭自适应，仅支持PC端</td></tr><tr><td>showMarquee</td><td>视频显示跑马灯，仅支持PC端</td></tr><tr><td>showMarqueeDoc</td><td>文档显示跑马灯，仅支持PC端</td></tr><tr><td>logout</td><td>退出</td></tr><tr><td>playerBackgroundImageUri</td><td>获取播放器自定义背景图片</td></tr><tr><td>playerBackgroundHint</td><td>获取播放器自定义提示语</td></tr><tr><td>liveCountdown</td><td>直播倒计时</td></tr><tr><td>getPublishingQuestionnaire</td><td>直播中获取问卷</td></tr><tr><td>changeNickname(name)</td><td>修改用户昵称，name:昵称，长度小于20</td></tr></tbody></table><h3 id="toc_6">直播响应事件 API</h3><table width="900px"><tbody><tr style="background:#F60;color:#FFF"><td>API</td><td>说明</td></tr><tr><td>onLiveStart</td><td>开始直播</td></tr><tr><td>onLiveEnd</td><td>停止直播</td></tr><tr><td>onUserCountMessage</td><td>在线人数</td></tr><tr><td>onPublicChatMessage</td><td>收到公聊</td></tr><tr><td>onPrivateChatMessage</td><td>收到私聊</td></tr><tr><td>onPrivateAnswer</td><td>收到私聊回复</td></tr><tr><td>onQuestion</td><td>收到提问</td></tr><tr><td>onAnswer</td><td>收到回答</td></tr><tr><td>onInformation</td><td>收到通知</td></tr><tr><td>onKickOut</td><td>踢出</td></tr><tr><td>onAnnouncementShow</td><td>开始直播后显示公告</td></tr><tr><td>onAnnouncementRelease</td><td>发布和修改公告</td></tr><tr><td>onAnnouncementRemove</td><td>删除公告</td></tr><tr><td>onLoginError</td><td>登录出现错误时的回调</td></tr><tr><td>onLiveStarting</td><td>移动web端直播中的回调</td></tr><tr><td>onStartRollCall</td><td>开始签到</td></tr><tr><td>onStartLottery</td><td>开始抽奖</td></tr><tr><td>onWinLottery</td><td>中奖</td></tr><tr><td>onStopLottery</td><td>结束抽奖</td></tr><tr><td>onStartVote</td><td>开始答题（voteType:0/1; 0为单选题，1为多选题）</td></tr><tr><td>onStopVote</td><td>结束答题</td></tr><tr><td>onVoteResult</td><td>答题统计</td></tr><tr><td>window.on_cc_live_accept_interaction</td><td>讲师接受互动信息</td></tr><tr><td>window.on_cc_live_interaction_message</td><td>互动信息</td></tr><tr><td>window.on_cc_live_interaction_chatusers</td><td>已经在聊天的列表信息</td></tr><tr><td>window.on_cc_live_interaction_disconnect</td><td>挂断互动信息</td></tr><tr><td>showUserCount</td><td>是否显示在线人数（0为不显示，1为显示）</td></tr><tr><td>onLiveDesc</td><td>显示简介</td></tr><tr><td>onBroadcastMsg</td><td>广播消息回调</td></tr><tr><td>onQaPublish</td><td>发布问题</td></tr><tr><td>onRoomSetting</td><td>直播间布局配置</td></tr><tr><td>onQuestionnairePublish</td><td>发布问卷</td></tr><tr><td>onQuestionnairePublishStop</td><td>结束发布问卷</td></tr><tr><td>onOnlineTeachers</td><td>获取讲师列表</td></tr><tr><td>window.on_cc_swf_loading_completed</td><td>flash播放器加载完成</td></tr><tr><td>window._onStart</td><td>PC端直播中的回调</td></tr><tr><td>onExternalQuestionnairePublish</td><td>第三方问卷调查</td></tr><tr><td>onPageChange</td><td>翻页信息回调</td></tr><tr><td>onChangeNickname</td><td>修改用户昵称回调</td></tr><tr><td>onLiveTime</td><td>获取开始直播时间和直播时间（未开始直播返回 {liveStartTime: "", liveDuration: -1}）</td></tr></tbody></table><h3 id="toc_7">返回值说明</h3><pre><code>onPublicChatMessage:
{
    "userid":"4ccd73b2fb1a4b63be1043b6c4c225dc", // 发送者id
    "username":"name",   // 发送者名字
    "userrole":"student",   // 发送者身份
    "useravatar":"img",   // 发送者头像
    "msg":"rrr",   // 消息内容
    "time":"16:45:08",   // 发送时间
    "usercustommark": ""  // 聊天自定义参数
}

onPrivateChatMessage:
{
    "fromuserid":"7a4715874d504b8db78cb5b77d66b8c8",  // 发送者id
    "fromusername":"name",   // 发送者名字
    "touserid":"33ed40d2d7b746919219789733b5bdd4",  // 接收者id
    "tousername":"第三方士大夫",   // 接收者名字
    "msg":"发反反复复",   // 消息内容
    "time":"17:22:15"   // 发送时间
}

onPrivateAnswer:
{
    "fromuserid":"33ed40d2d7b746919219789733b5bdd4",  // 发送者id
    "fromusername":"第三方士夫",  // 发送者名字
    "fromuserrole":"student",   // 发送者身份
    "touserid":"7a4715874d504b8db78cb5b77d66b8c8",  // 接收者id
    "tousername":"name",   // 接收者名字
    "msg":"阿斯蒂芬",   // 消息内容
    "time":"17:26:24"  // 发送时间
}

onQuestion:
{
    "action":"question",  // 提问
    "time":-1,
    "value":
    {
        "userId":"C783F0F7CB77E1F3",  // 提问者id
        "userName":"name",   // 提问者名字
        "content":"123145",  // 提问内容
        "userAvatar":"img",     // 提问者头像
        "id":"1B5BBA4826FFE337"   // 问题id
    }
}

onAnswer:
{
    "action":"answer",   // 回答
    "time":-1,
    "value":
    {
        "content":"ghghjgug",   // 回答内容
        "isPrivate":0,    // 是否仅提问者可见
        "questionId":"1B5BBA4826FFE337",   // 问题id
        "questionUserId":"C783F0F7CB77E1F3",   // 提问者id
        "userId":"ebadb3d414c3471786d095c93bab8cb5",  // 回答者id
        "userName":"www",   // 回答者名字
        "userAvatar":"img",    // 回答者头像
        "userRole":"publisher"   // 回答者身份
    }
}

onPageChange:
{
    "docId": "xxxx",//当前页id
    "docName": "Java.pdf",//当前页name
    "docTotalPage": 105,//总页数
    "pageNum": 0    //当前页索引值
}

onBroadcastMsg:
{
    content: "大家好",//广播内容
    time: 205 //广播时间
}

userRole和fromuserrole对应关系表示如下:
    unknow: 未知角色;
    publisher: 主讲;
    teacher: 助教;
    host: 主持人;
    student: 学员（观众）;
</code></pre><h3 id="toc_8">关键代码示例</h3><pre><code>&lt;script type="text/javascript"&gt;

$(function(){

    // 开始直播
    DWLive.onLiveStart = function(j){
        console.log(j);
    }

    // 停止直播
    DWLive.onLiveEnd = function(j){
        console.log(j);
    }

    // 在线人数
    DWLive.onUserCountMessage = function(j){
        console.log(j);
    }

   // 开始直播后显示公告
    DWLive.onAnnouncementShow = function (j) {
        console.log(j);
    };

    // 修改公告,发布公告
    DWLive.onAnnouncementRelease = function (j) {
        console.log(j);
    };

    // 删除公告
    DWLive.onAnnouncementRemove = function (j) {
        console.log(j);
    };

    // 接收公聊
    DWLive.onPublicChatMessage = function(j){
        console.log(j);

        DWLive.barrage(j,'0xff0000'); // 发送弹幕
    }

    // 接收私聊
    DWLive.onPrivateChatMessage = function(j){
        console.log(j);
    }

    // 接收私聊回复
    DWLive.onPrivateAnswer = function(j){
        console.log(j);
    }

    // 提问
    DWLive.onQuestion = function(j){
        console.log(j);
    }

    // 接收回答
    DWLive.onAnswer = function(j){
        console.log(j);
    }

    // 直播间布局配置
    DWLive.onRoomSetting = function (data) {
        var t = data.layout_video_main;
        if (t === 'true') {
            Ui.toggleVideo(true);
        } else {
            Ui.toggleVideo(false);
        }
    };

    // 通知
    DWLive.onInformation = function(j){ // 禁言
        console.log(j);
    }

    $(".btnsend").click(function(){
        var msg = $(".chatinput").val();
        DWLive.sendPublicChatMsg(msg); // 发送公聊
    })

    $(".qasend").click(function(){
        var msg = $(".qainput").val();
        DWLive.sendQuestionMsg(msg); // 发送问题
    })
    
    $(".setsound").click(function(){
       DWLive.setSound(0.5);  // 设置音量(0-1)
    })
})

&lt;/script&gt;
</code></pre><h3 id="toc_9">备注与说明</h3><p>响应事件返回的默认都为字符串格式，请自行按需求转化为JSON对象。</p><h3 id="toc_10">附录1. 表情和a链接解析处理方法</h3><pre><code>function showEm(str) {
    if (!$.trim(str)) {
        return '';
    }
    str = str.replace(/\&lt;/g, '&amp;lt;');
    str = str.replace(/\&gt;/g, '&amp;gt;');
    str = str.replace(/\n/g, '&lt;br/&gt;');
    str = str.replace(/\[em_([0-9]*)\]/g, '&lt;img src="//view.csslcloud.net/img/em/$1.gif" border="0" /&gt;');
    str = str.replace(/\[em2_([0-9]*)\]/g, '&lt;img src="//view.csslcloud.net/img/em2/$1.png" border="0" /&gt;');

    var nmsg = '';
    $.each(str.split(' '), function (i, n) {
        n = $.trim(n);
        if (n.indexOf('[uri_') == 0 &amp;&amp; n.indexOf(']') == n.length - 1 &amp;&amp; n.length &gt; 6) {
            var u = n.substring(5, n.length - 1) + ' ';
            nmsg += '&lt;a target="_blank" style="color: #2f53ff" href="' + u + '"&gt;' + u + '&lt;/a&gt;' + ' ';
        } else {
            nmsg += n + ' ';
        }
    });

    return nmsg;
}
</code></pre><p>需要发送带链接的a标签时，格式如下：<code>[uri_http://www.xxx.com]</code>  （注意：前后都需要加空格）</p><p>在收发消息的时候，用showEm('消息内容')处理一下消息内容即可，原理就是匹配[em2_*]，让它变为对应的表情图片，匹配[uri _ *]，让它变为可点击的a链接。</p><h3 id="toc_11">附录2. demo使用方法</h3><p>demo下载地址：  <a href="http://dl.csslcloud.net/live/sdk/web/demo_v2.5.0.zip">http://dl.csslcloud.net/live/sdk/web/demo_v2.5.0.zip</a><br><br>
下载后解压，live.html和mobile.html为直播demo，demo中注释的地方是直播SDK核心代码。</p><pre><code>&lt;!-- 直播视频模块 --&gt;
&lt;div id="livePlayer"&gt;&lt;/div&gt;

&lt;!-- 直播文档模块 --&gt;
&lt;div id="drawPanel"&gt;&lt;/div&gt;


    // 直播SDK参数配置
    DWLive.init({
        userid: 'userid',
        roomid: 'roomid',
        viewername: 'name',
        viewertoken: 'password',
        viewercustomua: 'android',
        language: 'en',
        viewercustominfo: '{"exportInfos": [ {"key": "城市", "value": "北京"}, {"key": "姓名", "value": "哈哈"}]}'
    });
</code></pre><h2 id="toc_12">回放SDK</h2><h3 id="toc_13">依赖库</h3><p>回放SDK依赖于 jQuery，请自行引入 jQuery 库，版本没有要求。</p><h3 id="toc_14">调用方法</h3><p><span class="impor">页面引入 jQuery：</span></p><pre><code>&lt;script src="//view.csslcloud.net/js/jquery-1.9.0.min.js" type="text/javascript"&gt;&lt;/script&gt;
</code></pre><p><span class="impor">页面引入 JS SDK：</span></p><pre><code>&lt;script src="//view.csslcloud.net/js/playbackSDK.js" type="text/javascript"&gt;&lt;/script&gt;
</code></pre><p><span class="impor">视频模块：</span></p><pre><code>&lt;div id="playbackPlayer"&gt;&lt;/div&gt;
</code></pre><p><span class="impor">文档模块：</span></p><pre><code>&lt;div id="playbackPanel"&gt;&lt;/div&gt;
</code></pre><p><span class="impor">初始化：</span></p><pre><code>&lt;script type="text/javascript"&gt;
    $.DW.config({
       userId: 'userId',
       roomId: 'roomId',
       recordId: 'recordId',
       viewername: 'name',
       viewertoken: 'password',
       isH5play:true,
       fastMode:true
   });
&lt;/script&gt;
</code></pre><table width="900px"><tbody><tr style="background:#F60;color:#FFF"><td>参数</td><td>说明</td></tr><tr><td>userId</td><td>用户id，不可为空</td></tr><tr><td>roomId</td><td>直播间id，不可为空</td></tr><tr><td>recordId</td><td>回放id，不可为空</td></tr><tr><td>viewername</td><td>观看者名字，可为空，接口验证时必填</td></tr><tr><td>viewertoken</td><td>观看密码，可为空，接口验证时必填</td></tr><tr><td>isH5play</td><td>PC端是否启用H5播放器，可选，默认为false使用Flash播放器，true为启用，false为不启用（不支持H5的浏览器，该参数无效，默认使用Flash播放器）</td></tr><tr><td>fastMode</td><td>是否开启极速动画模式</td></tr></tbody></table><h3 id="toc_15">回放响应事件 API</h3><table width="900px"><tbody><tr style="background:#F60;color:#FFF"><td>API</td><td>说明</td></tr><tr><td>on_cc_live_chat_msg</td><td>显示全部聊天信息</td></tr><tr><td>on_cc_live_chat_msg_sync</td><td>同步显示聊天信息</td></tr><tr><td>on_cc_live_broadcast_msg</td><td>显示全部广播信息</td></tr><tr><td>on_cc_live_broadcast_msg_sync</td><td>同步显示广播信息</td></tr><tr><td>on_cc_live_qa_question</td><td>显示提问信息</td></tr><tr><td>on_cc_live_qa_answer</td><td>显示回答信息</td></tr><tr><td>on_cc_callback_pages</td><td>返回文档信息对象</td></tr><tr><td>on_cc_callback_pagechange</td><td>翻页信息回调</td></tr><tr><td>on_cc_login_error</td><td>登录失败回调</td></tr><tr><td>on_cc_live_player_load</td><td>播放器加载完成，仅支持pc端</td></tr><tr><td>on_player_start</td><td>播放开始，仅支持pc端</td></tr><tr><td>on_spark_player_pause</td><td>播放暂停，仅支持pc端</td></tr><tr><td>on_spark_player_resume</td><td>恢复播放，仅支持pc端</td></tr><tr><td>on_spark_player_end</td><td>播放停止，仅支持pc端</td></tr></tbody></table><h3 id="toc_16">返回值说明</h3><pre><code>on_cc_live_chat_msg:
{
    "//": "发送聊天信息的用户ID",
    "userid": "7f3a0c7c496a4a2b86d8e51e358193fd",
    "//": "发送聊天信息的用户名称",
    "username": "老张",
    "//": "发送时间",
    "time": 20,
    "//": "聊天内容",
    "msg": "Hello World.",
    "//": "发送者头像",
    "useravatar": "http://www.bokecc.com/static/cms/image/cc-video/navlogo-big.png",
    "//": "发送者角色，student：学生，teacher：助教，publisher：讲师",
    "userRole": "student",
    "//": "用户自定义参数",
    "usercustommark": ""
}

on_cc_live_broadcast_msg:
{
    content: "大家好",//广播内容
    time: 205 //广播时间
}

on_cc_live_qa_question:
{
    "action": "question",
    "value": {
        "//": "问题ID",
        "id": "49CE0XF718D5AA52",
        "//": "问题内容",
        "content": "我从哪里来？",
        "//": "提问者ID",
        "userId": "92aa0c1965d842ec9b443270f5734124",
        "//": "提问者名称",
        "userName": "T",
        "//": "提问者头像",
        "userAvatar": "http://www.bokecc.com/static/cms/image/cc-video/navlogo-big.png",
        "//": "该问题是否已发布，1：已发布，0：未发布",
        "isPublish": 1
    }
}

on_cc_live_qa_answer:
{
    "action": "answer",
    "value": {
        "//": "问题ID",
        "questionId": "49CE0XF718D5AA52",
        "//": "回答内容",
        "content": "石头里",
        "//": "是否是私密回答，1：私密回答，0：公共回答",
        "isPrivate": 1,
        "//": "回答者用户ID",
        "userId": "71120e4cc905425f8da91945c7df2df6",
        "//": "回答者名称",
        "userName": "孙悟空",
        "//": "回答者头像"
        "userAvatar": "",
        "//": "回答者角色",
        "userRole": "回答者角色，teacher：助教，publisher：讲师"
    }
}

on_cc_callback_pages:
{
    "time": 11,   // 图片时间
    "url": "http://image.csslcloud.net/image/3CD4C4DF4DF8E0CB9C33DC5901307461/73D088D5AC02E6B1/0.jpg",  // 图片地址
    "docId": "73D088D5AC02E6B1",  // 文档id
    "docName": "英语.pptx",  // 文档名称
    "docTotalPage": 11,  // 文档总页数
    "pageNum": 0,  // 当前页码
    "encryptDocId": "73D088D5AC02E6B1",  // 加密id
    "useSDK": false
}

on_cc_callback_pagechange:
{
    "docId": "xxxx",//当前页id
    "docName": "Java.pdf",//当前页name
    "docTotalPage": 105,//总页数
    "pageNum": 0    //当前页索引值
}

userRole和answerUserRole对应关系表示如下:
    unknow: 未知角色;
    publisher: 主讲;
    teacher: 助教;
    host: 主持人;
    student: 学员（观众）;

</code></pre><h3 id="toc_17">跳转到指定时间播放</h3><pre><code>&lt;script type="text/javascript"&gt;
     $.DW.seek(time);   // 跳转到指定时间播放，time单位为秒
&lt;/script&gt;
</code></pre><h3 id="toc_18">获取当前播放时间</h3><pre><code>&lt;script type="text/javascript"&gt;
     $.DW.getPlayerTime();   // 获取当前播放时间
&lt;/script&gt;
</code></pre><h3 id="toc_19">获取视频总时长</h3><pre><code>&lt;script type="text/javascript"&gt;
     
     window.on_cc_live_player_load = function () { // 播放器加载完毕
          console.log($.DW.getDuration()); // 获取视频总时长
     };
&lt;/script&gt;
</code></pre><h3 id="toc_20">文档自适应</h3><pre><code>$.DW.docAdapt(true); // true为打开自适应，false为关闭，默认为关闭，仅支持PC端
</code></pre><h3 id="toc_21">PC端回放播放器API</h3><table width="900px"><tbody><tr style="background:#F60;color:#FFF"><td>API</td><td>说明</td></tr><tr><td>$.DW.isShowBar(0)</td><td>隐藏视频播放控制条，0为打开，1为隐藏，默认为打开</td></tr><tr><td>$.DW.getBuffer()</td><td>获取buffer</td></tr><tr><td>$.DW.setVolume()</td><td>设置音量，0-1</td></tr><tr><td>$.DW.getVolume()</td><td>获取音量</td></tr><tr><td>$.DW.play()</td><td>播放暂停</td></tr><tr><td>$.DW.setZScale()</td><td>缩放视频画面，number（0-1），仅支持Flash播放器</td></tr><tr><td>$.DW.getZScale()</td><td>获取视频画面缩放比例，仅支持Flash播放器</td></tr><tr><td>$.DW.setScale()</td><td>设置视频窗口比例（"full", "scale43", "scale169", "original"），仅支持Flash播放器</td></tr><tr><td>$.DW.getScale()</td><td>获取视频窗口比例，仅支持Flash播放器</td></tr><tr><td>$.DW.openSettingPanel()</td><td>打开设置面板，仅支持Flash播放器</td></tr><tr><td>$.DW.playbackRate()</td><td>倍速播放,默认1.0 正常速度，倍速设置范围0.5～2倍速，仅支持H5播放器</td></tr></tbody></table><h3 id="toc_22">附录 demo使用方法</h3><p>demo下载地址：  <a href="http://dl.csslcloud.net/live/sdk/web/demo_v2.5.0.zip">http://dl.csslcloud.net/live/sdk/web/demo_v2.5.0.zip</a><br><br>
下载后解压，playback.html和playback-mobile.html为回放demo，demo中注释的地方是回放SDK核心代码。</p><pre><code>&lt;!-- 回放视频模块 --&gt;
&lt;div id="playbackPlayer"&gt;&lt;/div&gt;

&lt;!-- 回放文档模块 --&gt;
&lt;div id="playbackPanel"&gt;&lt;/div&gt;


// 回放SDK参数配置
$.DW.config({
       userId: 'userId',
       roomId: 'roomId',
       recordId: 'recordId',
       viewername: 'name',
       viewertoken: 'password',
       isH5play:true,
       fastMode:true
});
</code></pre><h2 id="toc_23">版本更新记录</h2><table><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td>更新日期</td><td>版本号</td><td>更新内容</td></tr><tr><td>2018-09-12</td><td>2.5.0</td><td>直播和回放文档支持极速动画模式<br>直播新增onLiveTime回调，返回直播开始时间和直播时长<br>优化demo</td></tr><tr><td>2018-07-04</td><td>2.4.1</td><td>直播新增viewercustominfo参数<br>回放PC端新增H5播放器及倍速播放<br>回放demo界面美化</td></tr><tr><td>2018-06-13</td><td>2.4.0</td><td>直播和回放新增翻页信息回调<br>直播支持观看直播时修改昵称<br>直播支持广播信息补推（最后一条广播）<br>回放增加直播中发布的广播信息的回调</td></tr><tr><td>2018-03-28</td><td>2.3.1</td><td>新增直播中获取问卷的方法</td></tr><tr><td>2018-02-27</td><td>2.3.0</td><td>支持第三方问卷<br>支持直播倒计时<br>支持文档显示模式<br>优化低延迟模式下文档视频同步性<br>回放Flash播放器API增加播放回调事件、面板设置、画面缩放、画面比例</td></tr><tr><td>2017-11-28</td><td>2.2.0</td><td>支持聊天记录补推<br>增加获取播放器背景图及提示语的方法<br>支持橡皮擦删除画笔<br>增加聊天自定义参数支持<br>回放Flash播放器API增加隐藏控制条、音量控制、播放控制、获取buffer</td></tr><tr><td>2017-10-10</td><td>2.1.0</td><td>新增用户退出功能<br>新增问卷功能<br>新增广播消息<br>新增web端布局切换事件<br>新增聊天获取讲师列表私聊<br>新增PC端直播中的状态事件<br>新增获取直播间简介<br>新增是否显示在线人数<br>新增跑马灯功能，并支持设置显示在文档还是视频Flash上<br>直播和回放新增增加自定义ua参数 viewercustomua<br>直播和回放新增flash播放器加载完成事件<br>回放登录参数 liveId 修改为recordId</td></tr><tr><td>2017-07-26</td><td>2.0.0</td><td>移动端支持画笔显示<br>PC和移动端支持ppt动画<br>PC端增加文档自适应窗口方法<br>移动端回放支持ppt同步翻页<br>移动端直播增加文档延迟保持和直播同步<br>回放增加登录失败回调方法</td></tr><tr><td>2017-06-28</td><td>1.8.4</td><td>支持连麦功能<br>回放支持获取时长</td></tr><tr><td>2017-01-18</td><td>1.8.3</td><td>支持https</td></tr><tr><td>2016-11-22</td><td>1.8.2</td><td>新增回放聊天同步显示接口</td></tr><tr><td>2016-11-18</td><td>1.8.1</td><td>新增弹幕开关<br>新增控制条隐藏<br>新增文档弹幕<br>直播聊天和问答返回角色信息<br>回放聊天和问答返回角色、头像信息</td></tr><tr><td>2016-11-08</td><td>1.8.0</td><td>新增签到<br>新增抽奖<br>新增答题卡<br>新增聊天中超链接发送说明<br>回放新增获取文档图片信息<br>回放新增获取当前播放时间</td></tr></tbody></table><br><br><br>                <!--文章内容分页 begin-->
                                <!--文章内容分页 end-->
            </div>