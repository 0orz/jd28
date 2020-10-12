## github action使用教程说明
 - Fork [此仓库项目](https://github.com/lxk0301/scripts) > 点击右上角fork按钮即可, [再不会可看此图](icon/fork.png)
 - 然后参考github@ruicky写的特别详细的小白教程[@ruicky教程](https://ruicky.me/2020/06/05/jd-sign/)

### 注意几个地方就行

- 如果actions出现没有定时执行情况，就修改一下`README.md`文件(enter键回车添加一个空格)，再提交(或者随便找个文件修改一下)。之后再观察一下，不出意外应该是会执行定时任务了。
    
    - 不知怎么修改README.md文件的看[这个图](icon/action3.png);
    
- 使用action的时候其中京东的ck,不要放到 [jdCookie.js](https://raw.githubusercontent.com/lxk0301/scripts/master/jdCookie.js) 里面，要放到Secrets里面, 添加 JD_COOKIE的时候。 多账号的cookie， 使用`&`隔开，比如 `账号一cookie&账号二cookie&账号三cookie`，再多账号就依次类推即可
    - 下面给个示例 ``pt_key=xxx1;pt_pin=xxx1;&pt_key=xxx2;pt_pin=xxx2;&pt_key=xxx3;pt_pin=xxx3;`` , 注:后面的英文引号`;`不可缺失
    - 京东cookie获取看这里
       - [浏览器获取京东cookie教程](https://github.com/lxk0301/scripts/blob/master/backUp/GetJdCookie.md) 或者 [插件获取京东cookie教程](https://github.com/lxk0301/scripts/blob/master/backUp/GetJdCookie2.md)
       - IOS代理软件(Surge, Quantumult X, Loon)等用户有使用过BoxJs的,可在BoxJs里面提取京东cookie(打开BoxJs -> 底部中间的 `应用` -> NobyDa脚本订阅 -> 京东(多合一签到) -> 点击会话右上方的三个点点 -> 修改会话 -> 全选复制即可)，再不会看此[图文教程](icon/jd8.png)
       - (新增兼容多个京东cookie可以换行)目前多个账号的cookie，可以使用按`Enter`键换行隔开
           ```
            这里给下三个账号的示例：
            pt_key=bbbbbbbbbbbbbb;pt_pin=aaaaaaa;
            pt_key=cccccccc;pt_pin=dddddddd;
            pt_key=eeeeeeeee;pt_pin=ffffffff;
           ```
- server酱的推送通知服务, 是可选项, 如果需要 自行申请SCKEY,再填入Secrets里面(Name选项输入 `PUSH_KEY` ,Value选项输入申请的 SCKEY)

- cron时间是按国际标准时间来的， 和北京时间不同，github action写16点才表示北京时间0点，具体可参考下面两个链接写cron

  -  [参考链接一](https://datetime360.com/cn/utc-beijing-time/) ， [参考链接二](http://www.timebie.com/cn/universalbeijing.php)

  - 根据使用经验发现github action 会有延迟现象，一般会延迟15分钟左右吧。比如action设置`北京时间16:00`运行，action其实要`16:15左右`才会执行脚本的。
  
- 上面 [@ruicky教程](https://ruicky.me/2020/06/05/jd-sign/) 获取ck的方法不对。参考上面两种获取京东cookie的方式才对.

- 如何查看action运行情况
    - [查看运行状态](https://raw.githubusercontent.com/lxk0301/scripts/master/icon/action1.png)
    
    - [查看运行日志](https://raw.githubusercontent.com/lxk0301/scripts/master/icon/action2.png)  

- fork过后，如果没有看到action运行，是因为`/.github/workflows/`路径里面的`.yml`后缀文件里面的cron时间未到，如需立马看到效果

  - 方法：在自己仓库，手动点击仓库的右上角`star图标按钮`即可，稍后就能看到运行 
  - 注：之后如果想单独运行某一个脚本(此处的前提条件是执行过上面的方法)，手动点击 Run workflow [根据此图片示例操作](https://user-images.githubusercontent.com/21308593/93980945-e28ab000-fdb1-11ea-977c-c50705e79ac3.png) ，再次点一下`Actions`图标即可看到效果(或者等待10秒左右也可) 

- 自动同步Fork后的代码(此部分内容由tg@wukongdada和tg@goukey提供) 注：此项目里面提供的配置文件是方案A  
  
  - 方案A - 强制远程分支覆盖自己的分支
  
      1. 参考tg@wukongdada这篇教程 [保持自己github的forks自动和上游仓库同步的教程](https://github.com/lxk0301/scripts/blob/master/backUp/gitSync.md) ， 安装[pull插件](https://github.com/apps/pull) 并确认此项目已在pull插件的作用下（参考@twukongdada这篇教程文中1-d）
      
      2. 确保.github/pull.yml文件正常存在，yml内上游作者填写正确(此项目已填好，无需更改)。
      
      3. 确保pull.yml里面是`mergeMethod: hardreset`(默认就是`hardreset`)。
      
      4. ENJOY!上游更改三小时左右就会自动发起同步。
      
  - 方案B - 保留自己仓库已修改过的文件
    
    > 上游变动后pull插件会自动发起pr，但如果有冲突需要自行**手动**确认。
    > 如果上游更新涉及workflow里的文件内容改动，需要自行**手动**确认。
    
    1. 参考tg@wukongdada这篇教程 [保持自己github的forks自动和上游仓库同步的教程](https://github.com/lxk0301/scripts/blob/master/backUp/gitSync.md) ， 安装[pull插件](https://github.com/apps/pull) 并确认此项目已在pull插件的作用下（参考@twukongdada这篇教程文中1-d）
    2. 确保.github/pull.yml文件正常存在，yml内上游作者填写正确(此项目已填好，无需更改)。
    3. 将pull.yml里面的`mergeMethod: hardreset`修改为`mergeMethod: merge`保存。
    4. ENJOY!上游更改三小时左右就会自动发起同步。
  
- 下方提供使用到的 **Secrets全集合**

    | Name                    |   归属   | 属性   | 说明                                                         |
    | :---------------------: | :----------: | --------- | ------------------------------------------------------------ |
    | `JD_COOKIE`             |   京东   | 必须   | 京东cookie,多个账号的cookie使用`&`隔开或者换行。具体获取参考[浏览器获取京东cookie教程](https://github.com/lxk0301/scripts/blob/master/backUp/GetJdCookie.md) 或者 [插件获取京东cookie教程](https://github.com/lxk0301/scripts/blob/master/backUp/GetJdCookie2.md) |
    | `JD_DEBUG`              |   脚本打印log   | 非必须   | 运行脚本时，是否显示log,默认显示。改成false表示不显示，注重隐私的人可以在设置secret -> `Name:JD_DEBUG,Value:false` |
    | `PUSH_KEY`              |   微信推送   | 非必须 | cookie失效推送[server酱的微信通知](http://sc.ftqq.com/3.version) |
    | `BARK_PUSH`             |   BARK推送   | 非必须 | cookie失效推送BARK这个APP,填写内容是app提供的`设备码`，例如：https://api.day.app/123 ，那么此处的设备码就是`123`，再不懂看 [这个图](icon/bark.jpg) |
    | `BARK_SOUND`            |   BARK推送   | 非必须 | bark推送声音设置，例如`choo`,具体值请在`bark`-`推送铃声`-`查看所有铃声` |
    | `TG_BOT_TOKEN`          |   telegram推送   | 非必须 | tg推送,填写自己申请[@BotFather](https://t.me/BotFather)的Token,如`10xxx4:AAFcqxxxxgER5uw` , [具体教程](https://github.com/lxk0301/scripts/pull/37#issuecomment-692415594) |
    | `TG_USER_ID`            |   telegram推送   | 非必须 | tg推送,填写[@getuseridbot](https://t.me/getuseridbot)中获取到的纯数字ID, [具体教程](https://github.com/lxk0301/scripts/pull/37#issuecomment-692415594) |
    | `DD_BOT_TOKEN`          |   钉钉推送   | 非必须 | 钉钉推送[官方文档](https://ding-doc.dingtalk.com/doc#/serverapi2/qf2nxq) ,只需`https://oapi.dingtalk.com/robot/send?access_token=XXX` 等于符号后面的XXX， 注：如果钉钉推送只填写`DD_BOT_TOKEN`，那么安全设置需勾选`自定义关键词`，内容输入输入`账号`即可，其他安全设置不要勾选 |
    | `DD_BOT_SECRET`         |   钉钉推送   | 非必须 | 密钥，机器人安全设置页面，加签一栏下面显示的SEC开头的字符串,填写了`DD_BOT_TOKEN`和`DD_BOT_SECRET`，钉钉机器人安全设置只需勾选`加签`即可，其他选项不要勾选 |
    | `PET_NOTIFY_CONTROL`    | 推送开关  | 非必须 | 控制京东萌宠是否静默运行,`false`为否(发送推送通知消息),`true`为是(即：不发送推送通知消息)              |
    | `FRUIT_NOTIFY_CONTROL`  | 推送开关  | 非必须 | 控制京东农场是否静默运行,`false`为否(发送推送通知消息),`true`为是(即：不发送推送通知消息)              |
    | `JD_JOY_REWARD_NOTIFY`  | 推送开关  | 非必须 | 控制jd_joy_reward.js脚本是否静默运行,`false`为否(发送推送通知消息),`true`为是(即：不发送推送通知消息)              |
    | `JOY_FEED_COUNT`        | 宠汪汪喂食数量  | 非必须 | 控制jd_joy_feedPets.js脚本喂食数量  ,可以填的数字10,20,40,80 , 其他数字不可.              |
    | `MARKET_COIN_TO_BEANS`  | 京小超兑换京豆数量  | 非必须 | 控制jd_blueCoin.js兑换京豆数量,可输入值为1到20或者1000的数字，其他数字不可.              |
    | `FruitShareCodes`       |  东东农场互助码  | 非必须 | 填写规则请看 [jdFruitShareCodes.js](https://github.com/lxk0301/scripts/blob/master/jdFruitShareCodes.js) 里面的说明 |
    | `PETSHARECODES`         |  东东萌宠互助码  | 非必须 | 填写规则请看 [jdPetShareCodes.js](https://github.com/lxk0301/scripts/blob/master/jdPetShareCodes.js) 里面的说明 |
    | `PLANT_BEAN_SHARECODES` |  种豆得豆互助码  | 非必须 | 填写规则请看 [jdPlantBeanShareCodes.js](https://github.com/lxk0301/scripts/blob/master/jdPlantBeanShareCodes.js) 里面的说明 |
    | `SUPERMARKET_UPGRADE`   |  京小超自动升级  | 非必须 | 自动升级,顺序:解锁升级商品、升级货架,true表示自动升级,false表示关闭自动升级 |
    | `BUSINESS_CIRCLE_JUMP`  |  京小超自动更换商圈  | 非必须 | 小于对方300热力值自动更换商圈队伍,true表示运行,false表示禁止 |
    
    ##### 互助码的填写规则
    ```
    同一个京东账号的好友互助码用@隔开,不同京东账号互助码用&或者换行隔开,下面给一个文字示例和具体互助码示例说明
    两个账号各两个互助码的文字示例：
    京东账号1的shareCode1@京东账号1的shareCode2&京东账号2的shareCode1@京东账号2的shareCode2
    
    两个账号各两个互助码的真实示例： 
    0a74407df5df4fa99672a037eec61f7e@dbb21614667246fabcfd9685b6f448f3&6fbd26cc27ac44d6a7fed34092453f77@61ff5c624949454aa88561f2cd721bf6&6fbd26cc27ac44d6a7fed34092453f77@61ff5c624949454aa88561f2cd721bf6
    ```
    ##### 关于脚本推送通知(微信server酱推送通知，bark app推送通知，telegram机器人推送通知，钉钉机器人推送通知)
    - 如果你填写了上面四种推送通知方式中的某一个通知所需secret，那么脚本通知情况如下：
    
          目前默认只有jd_fruit.js,jd_pet.js,jd_bean_sign.js三个脚本每次运行后都通知(其中jd_fruit.js,jd_pet.js的通知频率可设置新的secret来控制，具体详情见sendNotify.js文件的说明)
          jd_plantBean.js是每周一收集京豆后通知一次，
          jd_joy_reward.js是每次兑换到了京豆通知一次，
          其余的脚本平常运行都是不通知，只有在京东cookie失效后，才会推送通知    
    

    
##### 参考文献
[GitHub Actions 手动触发方式进化史](https://p3terx.com/archives/github-actions-manual-trigger.html)
    
[GitHub Actions 入门教程](https://p3terx.com/archives/github-actions-started-tutorial.html)

[github@ruicky教程](https://ruicky.me/2020/06/05/jd-sign/)
