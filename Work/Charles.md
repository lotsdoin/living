1. charles不能抓包
在mac上面,一般使用 charles进行抓包,方便开发iOS进行 debug和调试。近期, charles不能 抓取mac上面的网络请求,这让笔者的开发很麻烦。
2. charles proxy设置
遇到mac的网络请求不能抓包,首先确认 charlese的proy选项设置, Proxy-> macos Proxy,勾 选上 macos Proxy,再试一试能否抓取mac的网络请求包。
3.信任 Charles根证书
有时候不能抓包是 charles的根证书没有被开发者信任,通过如下方式信任根证书,选择 charles 菜单,help-> SSL Proxying-> Install Charles Root Certificate,此时会打开mac的钥匙串 访问程序,右键选择证书列表中的 charles/根证书,将该证书选择永久信任。需要注意的是,永 久信任的选项隐藏比较深,找的时候注意点
再试一试能否抓包。
4.代理冲突导致不能抓包
这是笔者遇到的问题,因为笔者使用的是代理上网方式,这可能根 charles的代理有所冲突,解 决方法是,设置->网络->Wifi->高级->代理,在左侧的配置协议列表中取消勾选"自动发现 代理"和“自动代理配置"。
重启 charles,再尝试一下,看能否 charles抓取mac的网络请求包。