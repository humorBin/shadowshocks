# shadowshocks
shadowshocks vpn agent

客户端下载地址：
<br>
https://github.com/shadowsocks/shadowsocks-windows/releases?after=2.5.1
<br>
https://www.flyzy2005.com/fan-qiang/shadowsocks/ss-clients-download/
<br>
http://www.jeyzhang.com/how-to-install-and-setup-shadowsocks-client-in-different-os.html
<br>
<br>
服务器下载地址：
<br>
https://www.librehat.com/three-minutes-to-set-up-shadowsocks-server-on-windows/
<br>
更多阅读：
<br>
https://blueboy.me/2016/10/26/tor-with-ss.html
<br>
结果校验
https://httpbin.org/headers
<br>

Windows下三分钟搭建Shadowoscks服务器端
之前在V2EX上有人问为啥没人做个在Windows上一键运行Shadowsocks服务器端的程序，我只想说……这是因为没人关注我的libQtShadowsocks项目啊！（脑补暴走漫画表情）

所以本文要来告诉这些想要帮别人的“小白”，轻轻松松只要三分钟，无痛@#@%#*（什么鬼？）让Shadowsocks服务端在你的Windows机器上跑起来！不用自己编译，不用安装什么Python、.Net的。


先上步骤，内情在后面再叙。

下载最新的shadowsocks-libqss（Fedora下软件包名为shadowsocks-libQtShadowsocks）
准备好config.json文件（范例文件点此，点Raw另存为config.json就能下载下来了），server字段填写”0.0.0.0″（如果走IPv6线路，填”::”），加密方式可以改成更新潮的”chacha20″（老旧的Shadowsocks客户端可能不支持chacha20加密）
要shadowsocks-libqss.exe以server mode运行需要加上-S参数，你可以从命令行提示符去运行。或者，更简单的，用我写好的bat脚本（点此查看，点Raw按钮另存为bat脚本即可）
将shadowsocks-server.bat与shadowsocks-libqss.exe, config.json放在同一个文件夹下，执行shadowsocks-server.bat即可
停止运行？关掉就可以了。下次再运行？执行shadowsocks-server.bat脚本就好了。修改配置文件？别用自带的记事本和写字板，去下载一个Notepad++吧，免得格式乱套了。

“内情”
使用的这个程序shadowsocks-libqss本身是libQtShadowsocks项目的一部分，最初始的目的是演示如何在Qt程序里调用libQtShadowsocks，后来则成为一个命令行式的客户端/服务端了。因为本身libQtShadowsocks就兼具客户端和服务端的功能，两者的区别很不大，如果拆成两个程序反而奇怪。

所以默认情况下shadowsocks-libqss会读取当前文件夹下的config.json文件，并以客户端模式启动。使用-c可以指定配置文件，而-S参数则使其以服务端模式运行。

配置文件config.json的格式和其他Shadowsocks版本一样，双向兼容~~（说了无痛>.<)

简单说一下相比其他文章提到的其他版本，shadowsocks-libqss的优势在哪里吧。shadowsocks-libev在Windows下编译比较麻烦，如果你下载第三方编译的版本，总是有点不放心不是？（当然，你下载的是我编译的shadowsocks-libqss，如果你不放心就别下拉倒）。shadowsocks-go已经很久没有实质更新了。shadowsocks-csharp-server支持的加密方式很少而且依赖.Net…主线的python版本依赖Python环境，而且要支持Salsa20和ChaCha20的话还要装libsodium，值得注意的还有shadowsocks-libqss的CPU、内存占用小。

最后，我的博客不是反映问题的地方，有问题请报到libQtShadowsocks的issues列表！

