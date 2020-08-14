# TNT_WB

1. 时代少年团官博出道以来微博转赞评数据及内容->tnt.excel&tnt.csv
2. 数据抓取代码->TNT_weibo.ipynb

2019年11月23日-2020年8月13日。

统计时间2020年8月13日晚9点。

## 环境

Jupyter Notebook

python3.7

## 没有环境的看这里

**免安装试用体验**一下，[戳这里](https://link.jianshu.com/?t=https%3A%2F%2Ftry.jupyter.org%2F)

1. 点这里![tnt](https://github.com/gulico/TNT_WB/blob/master/fig/2.jpg)
2. 将文件拖动到页面上。
3. 点击运行按钮即可逐块运行了。

![tnt](https://github.com/gulico/TNT_WB/blob/master/fig/3.jpg)

4. 生成的CSV文件右键下载

![tnt](https://github.com/gulico/TNT_WB/blob/master/fig/4.png)

5. excel直接打开CSV文件，另存为选择excel格式即可。

## 自定义修改

1. 首先用chrome浏览器打开https://m.weibo.cn登陆自己的微博。

2. 搜索你想要了解的用户，进入他的主页，点击chrome右上角工具栏->更多工具->开发者工具。

3. 如图选择NETWORK选项卡、XHR过滤器

   右侧数据列表中选择getIndex?uid=用户id

   左侧选择Preview选项卡

   ![tnt](https://github.com/gulico/TNT_WB/blob/master/fig/1.jpg)

4. 下方内容展开data->cards->0->mblog，即可寻找你需要的内容了。

5. ```python
   #uid 你所要爬取的微博的ID，在响应的参数列表中可以得到，图中可以找到
   uid = 6620842908
   #p 爬取的页数
   p = 30
   ```

   这里修改用户id和需要获取的页数

6. ```python
   def parse_json(json):
       items = json.get('data').get('cards')
   
   
       for item in items:
           item = item.get('mblog')
           weibo = {}
           weibo['发表时间'] = item.get('created_at')
           #weibo['手机类型'] = item.get('source')
           weibo['转发数量'] = item.get('reposts_count')
           weibo['内容'] = py(item.get('text')).text()
           #weibo['图片链接'] = item.get('bmiddle_pic')
           weibo['点赞数'] = item.get('attitudes_count')
           weibo['评论数'] = item.get('comments_count')
           yield weibo
   ```

   

## 参考资料

[Jupyter Notebook介绍、安装及使用教程](https://www.jianshu.com/p/91365f343585)

[Python帮你了解你喜欢的人！爬取她的微博内容信息！（Ajax数据爬取）](https://blog.csdn.net/zc666ying/article/details/104635850)

