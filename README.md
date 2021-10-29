## 超星学习通自动签到
超星学习通自动签到脚本，原作者是[sanyue3](https://github.com/sanyue3/ChaoXingSign)，我只对代码做了一点简单的修改  
本README.md的撰写参考文档：【[1](https://github.com/yuban10703/chaoxingsign/blob/master/README.md)】【[2](https://github.com/exqlnet/chaoxing_sign/blob/master/README.md)】【[3](https://github.com/sanyue3/ChaoXingSign/blob/main/README.md)】(我也是第一次写这玩意，如有错误，多多包涵，欢迎指正)

## 特别鸣谢：信科学长czy的指导、我舍友cmr的辅助测试

## 前言
该脚本能够让你抛弃学习通签到的干扰，努力学习，专心听课

## 使用前必读（使用条款）：
本脚本适用对象：来上课但是懒得签到的同学（因为每次都会来，所以签到就会显得很无聊），这样就可以专心听课（或者课前背一背托福单词🐶），而不用盯着手机生怕错过签到。  
所以，在往下看之前，请保证你会去上课。  
再次重申一遍：本脚本不是用来逃课的，如果你想这么做，请另寻代码。当然，我也拦不住你用我这个，但是，这都是你自己的选择，你需要对自己的选择负责，别到时候挂了，怪我这个脚本没让你去上课。  
对于那些真心想逃课的人，我相信就算没有我这个脚本，他照样能找到替代品（甚至更好的），不管怎样，这取决于你。  

## 功能特点
1. 只支持普通签到、拍照签到、位置签到、手势签到，不支持抢答等功能

2. 因为作者是让程序在启动的时候解析所有课程，所有运行期间不会自动获取新的课程，如果在程序运行期间新增了课程，则需要重启程序

3. **目前只支持单人，不支持多人**

4. 腾讯云函数和server酱是可以白嫖的，免费额度应该够用，正常使用应该不用出钱（最起码目前情况是这样的，但是为了防止善变资本家的剥削，我还是建议你经常关注免费额度使用情况，以免被割韭菜）

## 修改部分
1. 删除了企业微信推送功能（考虑到大多数人不用企业推送）
2. 添加了sever酱推送功能
3. 对代码进行优化（新增了一个云函数的主函数），使其能部署到腾讯云函数上
4. 修改了签到完成退出方式，以适应腾讯云函数退出方式
5. 修改了一些注释

## 配置部分
打开main.py文件，上面的注释都很清楚，按着提示来配置就行，把那几个必填的填了就行，别忘了保存。（经纬度不知道的用这个：[百度地图坐标拾取系统](https://api.map.baidu.com/lbsapi/getpoint/index.html)）（[Server酱注册地址](https://sct.ftqq.com/)）

## 配置完成后建议本地运行一遍，缺啥包就安装啥包（这个不难，本地运行相对来说很简单，不会的自行百度，可以叫上你的舍友开一门签到课，帮忙测试一下）

## 部署到腾讯云上
[云函数参考食用方法](https://yuban10703.xyz/archives/527)
1. 按照上述网站的提示创建好云函数任务（建议使用香港服务器，反正我目前用的好好的），把main.py上传到云函数上（注意：环境选择`Python 3.6`,
内存最低实测最多用了五十几M，所以你设置成64M应该就够了，但是我为了以防万一，设置的128M，别贪多，设置的越多，免费额度消耗得越快.）
2. 关键步：执行方法改为：main.main_function   然后触发器别把时间写错了就行
3. 静待花开，自动签到

#### 关于Cron设定
我们先来看一个例子

```
0 */10 8-12,14-18 * * 1-5
```

云函数的Cron跟Linux Cron非常相似,不过左边多了一个秒.  
以上Cron可以解释为: 

```
0 */10 8-12,14-18 * * 1-5
| |    |          | |  |
| |    |          | |  .------- 在周几     (周一到周五)
| |    |          | .---------- 在哪个月   (所有)  
| |    |          .------------ 在哪一天   (所有)
| |    .----------------------- 在几点     (8-12和14-18) 
| .---------------------------- 在第几分钟 (每隔10分钟)
.------------------------------ 在第几秒   (第0秒)
```
这是比较符合现在上课的情况的Cron,各位也可以根据这个列表进行自定义
作者目前用的是这个：0 0 8,9,10 * * MON-FRI *

## 祝大家学得开心，学业有成！











