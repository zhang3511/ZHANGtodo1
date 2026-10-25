旧手机变 NAS 完全指南（中文版）

目标：把抽屉里那台闲置安卓手机，变成一台像"飞牛 OS"一样的家用小服务器。 不需要 root，不需要拆机，安卓 8.0 以上就能玩。

一、先说清楚：飞牛 OS 装不进手机

飞牛 OS 是给电脑和开发板做的完整系统，手机有锁死的启动器和专属芯片驱动， 不能像装 APP 那样装进手机。GitHub 上也没有人做过这件事。

但是——把手机变成飞牛那样的 NAS，已经有人做好现成方案了。 我们用的项目叫 Pocket Cloud（https://github.com/huzefdev/pocket-cloud ）， 装好后手机上会同时有下面三个功能：

飞牛 OS 里的东西手机上变成怎么打开文件管理器FileBrowser浏览器输 http://手机IP:8080飞牛影视（看电影）Jellyfin浏览器输 http://手机IP:8096相册自动备份Syncthing浏览器输 http://手机IP:8384

二、准备工作（5 分钟）

在那台闲置手机上做：

装 Termux（这是一个在安卓里跑 Linux 命令的 APP）

必须从这个网址下，别去应用商店： https://f-droid.org/packages/com.termux/

下载安装后打开，会请求存储权限，点允许。

关闭电池杀后台（非常重要，否则手机几分钟后就把服务杀掉）

手机 设置 → 电池 → 找到 Termux → 选 "不限制 / 无优化"

关掉安卓 12 以上的进程限制

设置 → 关于手机 → 连点版本号 7 次，打开"开发者选项"

进去找 "关闭幽灵进程 / 禁止子进程限制"，打开

手机长期插着充电器，当服务器用。

三、安装（照着敲，一共就两行）

打开 Termux，逐行输入（一行一回车）：

termux-setup-storage

回车后手机会弹权限框，点允许。

pkg install -y git && git clone https://github.com/huzefdev/pocket-cloud.git && cd pocket-cloud && bash install.sh

然后会发生这些事，全部一路回车就行：

它先更新系统、装一堆工具（几分钟）

问 Deploy FileBrowser? (Y/n) → 直接回车

问 Deploy Syncthing? (Y/n) → 直接回车

问 Deploy Jellyfin? (Y/n) → 直接回车（这一步要下约 500MB，耐心等 10~20 分钟）

最后问 Start all services now? (Y/n) → 直接回车

装完屏幕上会显示三个网址，类似：

FileBrowser : http://192.168.1.50:8080 Syncthing : http://192.168.1.50:8384 Jellyfin : http://192.168.1.50:8096

四、怎么用

用家里另一台设备（你的主力手机或电脑），连同一个 WiFi：

浏览器打开 http://192.168.1.50:8080

账号：admin

密码：admin

进去就能上传、下载、管理手机里的文件，跟飞牛的文件管理一样。

浏览器打开 http://192.168.1.50:8096

这是 Jellyfin，影音库。

第一次进去按提示选中文，添加媒体文件夹，就能在电视/电脑上串流看手机里的电影。

http://192.168.1.50:8384 是 Syncthing，用来跟别的电脑/手机自动同步照片， 具体用法以后需要再单独说。

五、以后每次开机

手机重启后，所有服务不会自己起来。 打开 Termux，敲一句：

bash ~/start-services.sh

三个服务就全部启动，屏幕上会再显示一次那三个网址。

六、常见问题

Q：Termux 哪里下？应用商店搜不到。 A：必须从 F-Droid 官网下：https://f-droid.org/packages/com.termux/

Q：装到一半卡住/报错怎么办？ A：把 Termux 里红色的报错文字截图发给我。

Q：手机锁屏后就连不上了？ A：电池优化没关，回第二节第 2 步再检查一遍。

Q：能在外网（不在家）访问吗？ A：现在只能家里 WiFi 用。外网访问需要加 Tailscale 或 frp，等你玩顺了再说。

Q：这个安全吗？ A：代码我逐行读过，就是装官方的 FileBrowser、Syncthing、Jellyfin，没有奇怪的东西。 初始密码 admin/admin，进去后记得改掉。

七、备选方案（连命令都不想敲）

如果不想装 Termux，还有个中文 APK 直接装： PocketNAS-Pro：https://github.com/Hjilin/PocketNAS-Pro 装好 APP 就是文件管理 + 影音 + FTP/WebDAV，开箱即用。 缺点是项目很新，没上面这个成熟。

整理人：豆包 ｜ 整理日期：2026-10-25

# ZHANGtodo1
