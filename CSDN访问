# coding:utf-8
import lxml.html
import random
import time
import requests

 
class CsdnSpider():
    USER_AGENTS = [
        'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.95 Safari/537.36 OPR/26.0.1656.60',
        'Opera/8.0 (Windows NT 5.1; U; en)',
        'Mozilla/5.0 (Windows NT 5.1; U; en; rv:1.8.1) Gecko/20061208 Firefox/2.0.0 Opera 9.50',
        'Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; en) Opera 9.50',
        'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:34.0) Gecko/20100101 Firefox/34.0',
        'Mozilla/5.0 (X11; U; Linux x86_64; zh-CN; rv:1.9.2.10) Gecko/20100922 Ubuntu/10.10 (maverick) Firefox/3.6.10',
        'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/534.57.2 (KHTML, like Gecko) Version/5.1.7 Safari/534.57.2',
        'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.71 Safari/537.36',
        'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.11 (KHTML, like Gecko) Chrome/23.0.1271.64 Safari/537.11',
        'Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US) AppleWebKit/534.16 (KHTML, like Gecko) Chrome/10.0.648.133 Safari/534.16',
        'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.11 TaoBrowser/2.0 Safari/536.11',
        'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.1 (KHTML, like Gecko) Chrome/21.0.1180.71 Safari/537.1 LBBROWSER',
        'Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident/5.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; LBBROWSER)',
        'Mozilla/5.0 (Windows NT 5.1) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.84 Safari/535.11 SE 2.X MetaSr 1.0',
        'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; Trident/4.0; SV1; QQDownload 732; .NET4.0C; .NET4.0E; SE 2.X MetaSr 1.0)',
        'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/38.0.2125.122 UBrowser/4.0.3214.0 Safari/537.36'
    ]
    url_list = [
        "https://blog.csdn.net/qq_37416933/article/details/93923051",
        "https://blog.csdn.net/qq_37416933/article/details/95159938",
        "https://blog.csdn.net/qq_37416933/article/details/92850922",
        "https://blog.csdn.net/qq_37416933/article/details/95353196",
        "https://me.csdn.net/qq_37416933",
        "https://me.csdn.net/download/qq_37416933",
        "https://me.csdn.net/bbs/qq_37416933"
        "https://blog.csdn.net/qq_24347541/article/details/88737370",
        "https://blog.csdn.net/qq_24347541/article/details/88734308",
        "https://blog.csdn.net/qq_24347541/article/details/88709917",
    ]
    def __init__(self):
        self.page = 0
        self.proxy = []
    def get_proxy(self):
        self.page+=1
        headers = {"User-Agent" : "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_0) AppleWebKit/535.11 (KHTML, like Gecko) Chrome/17.0.963.56 Safari/535.11"}
        request = requests.get("https://www.kuaidaili.com/free/inha/"+str(self.page), headers=headers)
        html = request.content
        etree = lxml.html.etree
        content = etree.HTML(html)
        #print html
        ip = content.xpath('//td[@data-title="IP"]/text()')
        port = content.xpath('//td[@data-title="PORT"]/text()')
        # 将对应的ip和port进行拼接
        for i in range(len(ip)):
            for p in range(len(port)):
                if i == p:
                    if ip[i] + ':' + port[p] not in self.proxy:
                        self.proxy.append(ip[i] + ':' + port[p])
        # print self.proxy
        if self.proxy:
            print ("this use" + str(self.page) + "page IP")
            self.spider()
 
    def spider(self):
        num = 0 # 用于访问计数
        err_num = 0 #用于异常错误计数
        while True:
            # 从列表中随机选择UA和代理
            user_agent = random.choice(self.USER_AGENTS)
            proxy = random.choice(self.proxy)

            referer = random.choice(self.url_list) #随机选择访问url地址
            headers = {
                "Host": "blog.csdn.net",
                "Connection": "keep-alive",
                "Cache-Control": "max-age=0",
                "Upgrade-Insecure-Requests": "1",
                "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8",
                "Referer": "https://blog.csdn.net/qq_24347541",
                "User-Agent": user_agent,
                "Accept-Language": "zh-CN,zh;q=0.9",
				"Cookie": "smidV2=2018061109563875e1d84afd822e152ccb71c406cf4e44009bb058182434650; uuid_tt_dd=10_37292961410-1553592218451-585832; UN=RUSH00000; Hm_ct_6bcd52f51e9b3dce32bec4a3997715ac=6525*1*10_37292961410-1553592218451-585832!5744*1*RUSH00000; acw_tc=2760824015580561068492252e3b68add4b06393ed45927064f907a6c5015c; __yadk_uid=szPOcQVFaUokWOOM2tzYYKteKJO5RAK6; acw_sc__v3=5ce219647dc08d09158df14c726ba51f46249bfd; acw_sc__v2=5ce21963f50279c4296b98184746d6a85a5f877d; dc_session_id=10_1558321509369.910879; Hm_lvt_6bcd52f51e9b3dce32bec4a3997715ac=1558054651,1558321511; SESSION=25351c44-6b87-48dc-b04b-a336aab6db77; UserName=RUSH00000; UserInfo=338ce29d15c840c98dbe43f5da028079; UserToken=338ce29d15c840c98dbe43f5da028079; UserNick=RUSH00000; AU=AAC; BT=1558321532133; dc_tos=prs8ld; Hm_lpvt_6bcd52f51e9b3dce32bec4a3997715ac=1558321538"
            }
            try:
                # 构建一个Handler处理器对象，参数是一个字典类型，包括代理类型和代理服务器IP+PROT
                request = requests.get(referer,headers=headers,proxies={"http": proxy})
                html = request.content
                etree = lxml.html.etree
                content = etree.HTML(html)
                # 使用xpath匹配阅读量
                read_num = content.xpath('//span[@class="read-count"]/text()')
                # 将列表转为字符串
                new_read_num = ''.join(read_num)
                # 通过xpath匹配的页面为blog.csdn.net/qq_41782425/article/details/84934224所以匹配其他页面返回的为空
                if len(new_read_num) != 0:
                    print (new_read_num)
 
                num += 1
                print ('The' + str(num) + 'few visits')
                print (request.url + "proxy ip: " + str(proxy))
                # print request.headers
                time.sleep(6)
                # 当访问数量达到100时，退出循环，并调用get_proxy方法获取第二页的代理
                if num > 100:
                    break
            except Exception as result:
                err_num+=1
                print ("error message(%d):%s"%(err_num,result))
                # 当错误信息大于等于30时，初始化代理页面page，重新从第一页开始获取代理ip，并退出循环
                if err_num >=30:
                    self.__init__()
                    break
        # 当退出循环时，看就会执行get_proxy获取代理的方法
        print ("Re acquiring agent proxy IP")
        self.get_proxy()
 
 
if __name__ == "__main__":
    CsdnSpider().get_proxy()
    
    
