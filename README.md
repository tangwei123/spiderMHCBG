# spiderMHCBG
目前发现，藏宝阁的接口数据已经加密，现这个版本的爬虫已经无法使用，暂时仅供开发爬虫的小伙伴学习！会尽快，开发解析页面数据的版本，请耐心等待！
python scrapy 扒取梦幻藏宝阁的上架的账号信息，然后分析出符合我要求的账号，发送带账号网址的链接地址到我的邮箱。

在cbg163.py文件中，Cbg163Spider类为爬虫类，爬虫开始运行的入口为方法start_requests，为啥写了个循环只要前20页的数据呢？首先，我修改了cbg接口的每页显示的
个数，其次是，玩梦幻的都知道都到20页了，再往后面的肯定性价比不高，所以我也就不要了！

在middlewares.py文件中，cbgDownloaderMiddleware这个类，是自动化处理代理IP，思路为：如果当前内存中的可以代理IP低于50个，那么就从数据库中取最多200个IP，
然后开线程去验证数据库中的每个IP是否可用，如果可用，那么就保存到内存中，如果不能用就从数据库中删掉。如果数据库中没有可用的，那么就去请求代理IP的接口上拉
一把，把拉到IP开线程验证，验证能用的写入数据库并放到内存中供爬虫使用！为了确保有足够的代理IP，用一个循环去验证，直到有足够的代理IP可以使用！
其中：
  spider_cbg163_backup1
  spider_cbg163_backup2
  spider_cbg163_backup3
  这些是之前写的爬虫，只是发现有些地方暂时行不通，故改道为之的历程！
  
在items.py文件中，mhCbgAccountItem这个类，做为爬虫请求与响应再请求再响应的一个持久化数据的存放地，保存这个爬虫从开始到完成工作所必要数据的记录，当然这
儿我并没有写入数据库的操作，因为存入数据库本就不在我的计划范围内！（我的打算就是符合要求的账号发邮件给我）如需存入数据库，只要yield某个item，然后
在pipelines.py做存库的操作即可！

整个爬虫，我目前只分析了账号的技能、神器、坐骑、锦衣、法宝、装备、修炼的信息，价格估算值进行到坐骑、锦衣、技能、修炼、召唤兽，并未对召唤兽装备、
账号准备等进行估价处理，如果有志同道合朋友欢迎加我微信18168820608，一起探讨，完善这个爬虫项目！

