#### 自学Python一个月写出来的第一个爬虫，往代码里填入自己的账号密码就可以使用


## 2020年2月3日更新(1.1)：
- 改用愚蠢的手动拆分成4段代码给4个线程，意外的比以前更高效，不知道有没有简便的写法

- 有些图片分辨率过大导致超时，可以复制失败url到 download_again.py 再下一遍，或者手动点击链接进网站右键保存

## 2020年2月3日更新(1.2):
- 代码更简洁了

## 2020年2月3日更新(1.3):

- 会新建文件夹了

## 2020年2月4日更新(1.4):
- 在多页批量下载的时候，下载到中途会出现各种报错，大概一半的图片会受影响而下载失败（10060，10054等我看不懂的错误）

- 暂不清楚是我的网络问题还是网站有反爬虫

- 建议一次下载100张图以内

- download_again 新加多线程下载

## 2020年2月9日更新(1.5):
- 优化了代码，并显示线程名

## 2020年2月12日更新(1.6):
- 代码更简洁了，用线程池代替线程模块

## 2020年2月12日更新(1.7):
- 优化代码

## 2020年2月14日更新(1.8):
- 爬完过去一年的toplist前30页之后我开始爬过去6个月的toplist，准备了一份url文本，用以剔除大量重复内容
- 新增 delete_same_file 用以删除文件夹里的重复图片

## 2020年2月14日更新(1.9):
- 改用8线程
- 终于想起来用 try...except... 来捕获异常，能正确提取失败url了

## 2020年2月17日更新(2.0):
- 与其自己手动复制失败的url，不如再写个循环让失败的url在主程序里继续跑，省事多了，但也更耗时了
- 不清楚下载失败的具体原因，猜测是网络问题，因为有的第一遍下不来第二遍第三遍就能下得动
- 为了解决大量重复图片的问题，现在程序会生成一个文本文件用以储存已经爬过的url，在代码中新增delete_url()函数，在get_img()里面新增一行判断，用以避免重复下载
- 需要注意的是文本没有用'[]'括起来，所以还需用完手动添加，用前手动删除

## 2020年2月17日更新(2.1):
- 删除delete_url()函数
- 删除重复代码
- 重写write_url()函数，现在无需手动改文本文件，能顺利读取和新增url
- 新增write_fail_url()函数，记录那些死活下不动的url

## 2020年2月19日更新(3.0):
- 重大更新！
- 重写部分用到 beautifulsoup 的代码，更简洁
- 终于发现了之前频繁下载失败的原因：当我开多个线程去解析网页获取图片url的时候就会失败，线程开得越多失败率越高
- 不清楚是代码问题还是网站问题
- 总之我把解析网页这部分单独拎出来顺序执行，执行完再开8线程进行下载，这样失败就只剩下图片太大下不来这一种可能

## 2020年2月19日更新(3.1):
- 掌握beautifulsoup，可以不用etree了

## 2020年2月20日更新(4.0):
- 重大更新之后的重大更新！
- 用异步IO库：asyncio, aiohttp重构几乎全部代码！
- 下载速度比旧版线程有了质的飞越
- 现存问题：解析网页无论是异步并行还是多线程，都会导致解析失败，可能是网站的限制
- 无奈我限制只能并行1个异步，这里成了最耗时的部分