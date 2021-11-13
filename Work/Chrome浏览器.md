# Chrome 浏览器知识
## Network 面板
    - 控制器: 控制面板的外观与功能
    - 过滤器: 过滤请求列表中显示的资源
      - 按住 Command (Mac) 或 Ctrl (Window/Linux), 然后点击过滤器可以同时选择多个过滤器
    - 概览: 显示 HTTP 请求、响应的时间轴
    - 请求列表: 默认时间排序，可选择显示列
    - 概要: 请求总数、总数据量、总花费时间等
![Network 面板](/Users/lotsd/Pictures/图床/chrome/Chrome Network 面板.png)
![Chrome 控制器面板](/Users/lotsd/Pictures/图床/chrome/Chrome 控制器面板.png)
![Chrome 过滤器：按类型](/Users/lotsd/Pictures/图床/chrome/Chrome 过滤器(按类型).png)

过滤器：
* domain: 仅显示来自指定域的资源。您可以使用通配符字符(*)纳入多个域 
* has-response-header: 显示包含指定HTP响应标头的资源
* is: 使用 is: running 可以查找 Websocket 资源, is: from-cache 可查找缓存读出的资源
* larger-than: 显示大于指定大小的资源(以字节为单位)。将值设为1000等同于设置 为1k
* method: 显示通过指定HTTP方法类型检索的资源 
* mime-type:显示指定 MIME 类型的资源
* mixed-content: 显示所有混合内容资源(mixed-content: all),或者仅显示当前显示的资源(mixed-content:displayed)
* scheme:显示通过未保护 HTTP(scheme:http) 或受保护 HTTPS (scheme:https) 检索的资
原。
* set-cookie-domain: 显示具有 Set-Cookie 标头并且 Domain 属性与指定值匹配的资源。 
* set-cookie-name:显示具有 Set-Cookie标头并且名称与指定值匹配的资源。
* set-cookie-value: 显示具有 Set-Cookie 标头并且只与指定值匹配的资源。
* status-code: 仅显示 HTTP 状态代码与指定代码匹配的资源。
* 多属性通过空格实现 AND 操作

请求类标的排序：
* 时间排序，默认
* 按列排序
* 按活动时间排序
  - Start Time: 发出的第一个请求位于顶部
  - Response Time: 开始下载的第一个请求位于顶部
  - End Time: 完成的第一个请求位于顶部
  - Total Duration: 连接设置时间和请求/响应时间最短的请求位于顶部
  - Latency: 等待最短响应时间的请求位于顶部

请求列表：
* Name: 资源的名称
* Status: HTTP 状态代码
* Type: 请求的资源的 MIME 类型
Initiator: 发起请求的对象或进程。它可能有以下几种值:
- Parser(解析器): Chrome 的 HTML 解析器发起了请求
- 鼠标悬停显示 JS 脚本
- Redirect (重定向): HTTP 重定向启动了请求
- Script (脚本): 脚本启动了请求
- Other (其他): 一些其他进程或动作发起请求，例如用户点击链接调转到页面或在地址中输入网址
* Size: 服务器返回的响应大小（包括头部和包体），可显示解压后大小
* Time: 总持续时间，从请求的开始到接受响应中的最后一个字节
* Waterfall: 各请求相关活动的直观分析图
  
预览请求内容：
* 查看头部
* 查看 cookie
* 预览响应正文:查看图像用 查看响应正文
* 时间详细分布
* 导出数据为HAR格式
* 查看未压缩的资源大小: Use Large Request Rows
* 浏览器加载时间(概览、概要、请求列表)
  - DOMContentLoaded 事件的颜色设置为蓝色,而 load 事件设置为红色
* 将请求数据复制到剪贴版
  - Copy Link Address: 将请求的网址复制到剪贴板
  - Copy Response: 将响应包体复制到剪贴板
  - Copy as CURL: 以 cURL 命令形式复制请求
  - Copy All as CURL: 以一系列 cURL 命令形式复制所有请求
  - Copy All as HAR:以 HAR 数据形式复制所有请求
* 查看请求上下游:按住 shift 键悬停请求上,绿色是上游,红色是下游

浏览器加载时间：
* 触发流程
  - 解析HTML结构
  - 加载外部脚本和样式表文件
  - 解析并执行脚本代码 // 部分脚本会阻塞页面的加载
  - DOM 树构建完成// DOMContentLoaded 事件
* 加载图片等外部文件
* 页面加载完毕// load事件

请求时间详细分布：
* Queueing: 浏览器在以下情况下对请求排队
  - 存在更高优先级的请求
  - 此源已打开六个 TCP 连接,达到限值,仅适用于 HTTP/1.0 和 HTTP/1.1 
  - 浏览器正在短暂分配磁盘缓存中的空间
* Stalled: 请求可能会因 Queueing 中描述的任何原因而停止 
* DNS Lookup: 浏览器正在解析请求的 IP 地址
* Proxy Negotiation: 浏览器正在与代理服务器协商请求
* Request sent:正在发送请求
* ServiceWorker Preparation: 浏览器正在启动 Service Worker
* Request to ServiceWorker: 正在将请求发送到 Service Worker
* Waiting(TTFB): 浏览器正在等待响应的第一个字节。TTFB表示 Time TO First Byte
(至第一字节的时间)。此时间包括1次往返延迟时间及服务器准备响应所用的时间
* Content Download: 浏览器正在接收响应
* Receiving Push: 浏览器正在通过 HTTP/2 服务器推送接收此响应的数据
* Reading Push: 浏览器正在读取之前收到的本地数据