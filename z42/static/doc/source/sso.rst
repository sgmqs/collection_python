单点登录系统 SSO

SSO 是公司项目公用的登录系统，通过 JSONP 实现跨域名登录支持

SSO 提供用户基础信息、登录历史的存储，应用服务器在存储这些数据时需要向 SSO 服务器发送请求以更新数据。

App 无需存储用户数据，用户数据存储在 SSO 上，App 只需要存储用户数据版本号。

App 可存储用户数据备份，仅作读取使用。


注册流程
=====================

用户在 App 网站调用 JS 弹窗登录，向 SSO 发起注册请求，如信息无问题则发起登录流程。


登录流程
=====================

1. 用户在应用网站上调用登录模块（JS 弹窗）向 SSO 服务器发送请求，如验证通过，则由 SSO 向 App 发出更新数据请求，
   参数包括：
   user_id、user_info_id 用于判断用户数据是否发生修改
   session 设置用户 session，可由 App 或者 SSO 设置
   sign 用于验证数据是否被修改
   time 用户验证请求是否已超时


2. App 服务器根据 user_id 和 user_info_id 判断用户数据是否更新

   2.1 数据发生更新。SSO 向应用服务器发起更新数据的请求。

   2.2 数据未更新。

3. APP 存储更新数据（如果有更新），向 Client 设置 cookie。



更新数据请求
=====================




应用服务器需要实现
=====================


2. 向 SSO 服务器端发送更新数据的接口

3. /auth/sync 同步用户数据

4. 解读 session 和 cookie
