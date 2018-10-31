\# 关于fq		2018/10/3

1. 购买VPS（虚拟私有服务器）

   www.vultr.com

2. windows下使用x-shell连接服务器

   ssh命令

   ```
   ssh IP地址	
   ssh 用户名@IP地址 -p 端口号
   ```

3. 搭建shadowsocks(或ssr)

   ```bash
   git clone https://github.com/flyzy2005/ss-fly
   ss-fly/ss-fly.sh -i 登陆密码 端口号
   ```

4. 开启BBR加速

   ```bash
   ss-fly/ss-fly.sh -bbr
   ```

   判断BBR加速是否开启成功

   ```bash
   sysctl net.ipv4.tcp_available_congestion_control
   ```

5. 客户端使用

   - 登陆
   - 启用系统代理（系统代理模式：PAC）


参考：

http://blog.51cto.com/13756513/2118075