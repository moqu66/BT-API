# BT-API
宝塔API接口

我的博客: [LittleMO's blog](https://sm.link)

* 抓取的时候BTpanl版本为: 7.0.2
* 没有备注的选项不建议修改,除非你已经了解它的用途  
* 只写了发送参数,没有写返回数据格式. 按照官方文档demo发送一次数据,通过浏览器控制台就可以看到返回的数据格式

### 添加FTP  
```
URL地址: /ftp?action=AddUser  
参数:  
ftp_username: test02 //用户名  
ftp_password: n22TfaDwt4nBaA7X //密码  
path: /www/wwwroot/test02 //FTP目录  
ps: test02 //备注  
```
----
### 删除FTP  
```
URL地址: /ftp?action=DeleteUser  
参数:  
id: 2  
username: test02  
```
----
### 启用或停用FTP  
```
URL地址: /ftp?action=SetStatus  
参数:  
id: 2 //id  
username: test02 //用户名  
status: 0 // 0是停用,1是启用  
```
----
### 获取FTP列表  
```
URL地址: /data?action=getData  
参数:  
tojs: ftp.get_list  
table: ftps  
limit: 15  
p: 1  
search:   
order: id desc  
```
----

### 添加站点 
``` 
URL地址: /site?action=AddSite  
参数:  
例1: webname: {"domain":"test.com","domainlist":["test01.com","test02.com","test03.com"],"count":3}  
例2: webname: {"domain":"test.com","domainlist":[],"count":0}  
//domain是主域名,必填! domainlist是追加的域名,不需要就留空,如例2  count,追加的域名数量(如果和添加的实际数量不符,后果未知)  
ps: 测试备注 //站点备注  
path: /www/wwwroot/demo.com //站点目录  
ftp: true //是否添加FTP,不需要就填false  
ftp_username: demo_com //FTP用户名,如果上方ftp填了false,请删除此项  
ftp_password: KYMxFCY2NpCp7f8s //FTP密码,如果上方ftp填了false,请删除此项  
sql: MySQL //数据库类型,不需要就填false  
codeing: utf8 //数据库编码  
datauser: demo_com //数据库用户名,如果上方sql填了false,请删除此项  
datapassword: FhXrWHyLGtKm5KF4 //数据库密码,如果上方sql填了false,请删除此项  
type: PHP //程序类型  
version: 72 //PHP版本,00的纯静态,其他的如: 56 70 71 72 73 ,前提是你已经安装了对应的版本!!!  
type_id: 0  
port: 80  
```
----
### 删除站点
```
URL地址: /site?action=DeleteSite  
参数:  
id: 3 //站点id  
webname: demo.com //站点主域名  
ftp: 1 //是否删除FTP 1是,0否  
database: 1 //是否删除数据库 1是,0否  
path: 1 //是否删除目录 1是,0否  
```
----
### 启用或停用站点  
```
URL地址: /site?action=SiteStop  
参数:  
id: 2 //站点ID  
name: test.com //站点主域名  
```
----
### 站点到期时间设置  
```
URL地址: /site?action=SetEdate  
参数:  
id: 2 //站点ID  
edate: 2019-11-30 //到期时间,请验证参照此格式 0000-00-00  
```
----
### 站点备注设置  
```
URL地址: /data?action=setPs  
参数:  
table: sites  
id: 2 //站点ID  
ps: 测试 //内容  
```
----
### 获取站点列表  
```
URL地址: /data?action=getData  
参数:  
tojs: site.get_list  
table: sites  
limit: 15  
p: 1  
search:   
order: id desc  
type: -1  
```
----
### 获取站点绑定的域名列表  
```
URL地址: /data?action=getData  
参数:  
table: domain  
list: True  
search: 2 //站点ID  
```
----
### 向站点添加域名
```  
URL地址: /site?action=AddDomain  
参数:  
domain: demo.test.com //添加的新域名  
webname: test.com //站点主域名  
id: 2 //站点ID  
```
----
### 删除站点域名  
```
URL地址: /site?action=DelDomain  
参数:  
id: 2 //站点ID  
webname: test.com //站点主域名  
domain: demo.test.com //删除的域名  
port: 80 //端口,你添加域名时填的什么端口,删除时也需要一样吧  
```
----
### 设置站点流量控制 
``` 
URL地址: /site?action=SetLimitNet  
参数:  
id: 2 //站点ID  
perserver: 300 //并发限制  
perip: 25 //单IP限制  
limit_rate: 512 //流量限制 单位KB  
```
----
### 查看站点流量控制
```  
URL地址: /site?action=GetLimitNet  
参数:  
id: 2 //站点ID  
```
----
### 关闭站点流量控制
```  
URL地址: /site?action=CloseLimitNet  
参数:  
id: 2 //站点ID  
```
----
### 设置站点伪静态规则  
```
URL地址: /files?action=SaveFileBody  
参数:  
path: /www/server/panel/vhost/rewrite/test.com.conf //伪静态文件路径  
data: location / {  
	if (!-e $request_filename){  
		rewrite  ^(.*)$  /index.php?s=$1  last;   break;  
	}  
} //伪静态规则  
encoding: utf-8 //编码  
```
----
### 查看站点伪静态规则  
```
URL地址: /files?action=GetFileBody  
参数:
path: /www/server/panel/vhost/rewrite/test.com.conf //伪静态文件路径  
```
----
### 查看站点默认文档
```  
URL地址: /site?action=GetIndex  
参数:
id: 2 //站点ID  
```
----
### 设置站点默认文档  
```
URL地址: /site?action=SetIndex  
参数:  
id: 2 //站点ID  
Index: index.php,index.html,index.htm,default.php,default.htm,default.html,test.html //逗号分隔  
```
----
### 站点主配置  
```
URL地址: /files?action=GetFileBody  
参数:  
path: /www/server/panel/vhost/nginx/test.com.conf //配置文件路径  
```
----
### 获取站点PHP版本  
```
URL地址: /site?action=GetSitePHPVersion  
参数:  
siteName: test.com //站点主域名  
```
----
### 设置站点PHP版本  
```
URL地址: /site?action=SetPHPVersion  
参数:  
siteName: test.com //站点主域名  
version: 72 //PHP版本,估计应该是这样写 56 70 71 72 73  你懂的...  
```
----
### 获取已安装的PHP版本  
```
URL地址: /site?action=GetPHPVersion  
参数:  
action: GetPHPVersion  
```
----
### 设置301重定向  
```
URL地址: /site?action=Set301Status  
参数:  
siteName: test.com //主域名  
toDomain: http://baidu.com //目标链接  
srcDomain: test.com //需要重定向的域名,只能选择一个域名或整站域名,比如有3个域名,那就只可以选择跳转1个或所有,不能只跳转2个域名,一个不跳转  
type: 1 //是否开启301, 1是开启 0是关闭  
```
----
### 创建目录  
```
URL地址: /files?action=CreateDir  
参数:  
path: /www/wwwroot/test  //目录路径  
```
----
### 创建文件
```  
URL地址: /files?action=CreateFile  
参数:  
 path: /www/wwwroot/test.txt //文件路径  
```
----
### 读取文件内容 
``` 
URL地址: /files?action=GetFileBody  
参数:  
path: /www/wwwroot/test.txt //文件路径  
```
----
### 修改文件内容
> 你应该配合上方的读取文件内容,然后将读取的文件内容放入下方data项,然后再修改! 否则建议你慎用!!!)  
```
URL地址: /files?action=SaveFileBody  
参数:  
data: 测试内容 //修改的内容( 此处的内容会覆盖整个文件原有内容 )  
path: /www/wwwroot/test.txt //文件路径  
encoding: utf-8 //文件编码  
```
----
### 压缩文件  
```
URL地址: /files?action=Zip  
参数:  
sfile: test //需要压缩的目录或者文件  
dfile: /www/wwwroot/test.tar.gz //压缩文件保存路径  
z_type: tar.gz //压缩方式  
path: /www/wwwroot //需要压缩的文件所在目录  
```
----
### 删除文件 
``` 
URL地址: /files?action=DeleteFile  
参数:  
path: /www/wwwroot/test.txt //需要删除的文件路径  
```
----
### 删除目录  
```
URL地址: /files?action=DeleteDir  
参数:  
path: /www/wwwroot/test //需要删除目录的路径  
```
----
### 目录或文件权限设置  
```
URL地址: /files?action=SetFileAccess  
参数:  
filename: /www/wwwroot/demo.com //文件或者目录的路径  
user: www //所属用户  
access: 755 //权限值  
all: True //是否应用到子目录  
```
----
### 文件或目录重命名和剪切移动  
```
URL地址: /files?action=MvFile  
参数:  
sfile: /www/test0.txt //命名前路径  
dfile: /www/wwwroot/test1.txt //重命名后路径  
rename: true  
```
----
### 删除防火墙
```  
URL地址: /firewall?action=DelAcceptPort  
参数:  
id: 9 //编号  
port: 8080 //端口号  
```
----
### 开启或关闭谷歌身份认证  
```
URL地址: /config?action=set_two_step_auth  
参数:  
act: 1 //1是开启 0是关闭  
```
----
### 获取谷歌身份认证密匙  
```
URL地址: /config?action=get_key  
参数:  
action: get_key  
```
----
### 面板设置  
```
URL地址: /config?action=setPanel  
参数:  
webname: 宝塔面板 //面板别名  
port: 8888 //面板端口  
workers: 1 //并发线程  
session_timeout: 86400 //超时时间  
domain: //绑定域名  
limitip: //授权IP  
sites_path: /www/wwwroot //默认建站目录  
backup_path: /www/backup //默认备份目录  
address: 192.168.9.88 //服务器IP  
```
----
### 同步服务器时间 
``` 
URL地址: /config?action=syncDate  
参数:无  
```
----
### 面板安全入口设置  
```
URL地址: /config?action=set_admin_path  
参数:  
admin_path: /admin123 //入口  
```
----
### 设置BasicAuth  
```
URL地址: /config?action=set_basic_auth  
参数:  
open: True //True是开启 False 是关闭  
basic_user: admin //开启请填写,关闭请留空  
basic_pwd: 123456 //开启请填写,关闭请留空  
```
----
### 修改面板用户名  
```
URL地址: /config?action=setUsername  
username1: admin888 //用户名,确保两次输入一致  
username2: admin888 //用户名,确保两次输入一致  
```
----
### 修改面板密码 
``` 
URL地址: /config?action=setPassword  
password1: TijWytF7RbaG //密码,确认两次输入一致  
password2: TijWytF7RbaG //密码,确认两次输入一致  
```
