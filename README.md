# Actions-OpenWrt

[![LICENSE](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&label=LICENSE)](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE)
![GitHub Stars](https://img.shields.io/github/stars/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Stars&logo=github)
![GitHub Forks](https://img.shields.io/github/forks/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Forks&logo=github)

Build OpenWrt using GitHub Actions

[Read the details in my blog (in Chinese) | 中文教程](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝

一键安装：bash <(curl -sL https://raw.githubusercontent.com/hijkpw/scripts/master/centos_install_v2ray2.sh)

其他
1. 查看v2ray运行状态 / 配置：bash <(curl -sL https://raw.githubusercontent.com/hijkpw/scripts/master/centos_install_v2ray2.sh) info

2. v2ray管理命令：启动：systemctl start v2ray，停止：systemctl stop v2ray，重启：systemctl restart v2ray；

3. nginx管理命令：测试配置文件有无错误：nginx -t，启动：systemctl start nginx，停止：systemct stop nginx，重启：systemctl restart nginx；

4. 更新v2ray到最新版：bash <(curl -sL https://raw.githubusercontent.com/hijkpw/scripts/master/goV2.sh)（提示“装不上daemon”不用管，systemctl restart v2ray重新启动v2ray就好了）

5. 查看SSL证书：certbot certificates，更新证书：systemctl stop nginx; certbot renew; systemctl restart nginx

6. 卸载： bash <(curl -sL https://raw.githubusercontent.com/hijkpw/scripts/master/centos_install_v2ray2.sh) uninstall；

静态网站
静态网站是最简单的网站，既可以上传个人作品/模板做展示站，也可以托管文件当ftp、网盘。

将小说站改成静态网站的操作非常简单：编辑 /etc/nginx/conf.d/你的域名.conf 文件(你的域名换成真实域名，例如hijk.art)，删除 proxy_pass  xxxx 这一行(第28行)，然后重启Nginx。

一键修改脚本：
domain=`cat /etc/v2ray/config.json | grep Host | cut -d: -f2 | tr -d \",' '`
confpath="/etc/nginx/conf.d/"
if [ ! -f $confpath${domain}.conf ]; then
  confpath="/www/server/panel/vhost/nginx/"
fi
sed -i '28d' ${confpath}${domain}.conf
nginx -s reload

接下来，将你的文件上传到 /usr/share/nginx/html 文件夹，就可以通过 https://你的域名/文件路径 的方式访问上传的网页或者文件了。文件上传操作可参考 Bitvise连接Linux服务器教程 或者 Mac电脑连接Linux教程。

反向代理网站
默认的小说站就是反向代理，如果你想换成其他网站，例如百度，把 /etc/nginx/conf.d/你的域名.conf 文件的 proxy_pass  xxxx 这一行(第28行)改成 proxy_pass http://www.baidu.com ，然后重启Nginx。

这种建站方式简单粗暴，实践时也有一些坑。例如Nginx不支持反向代理http2的网站，如果后端网站是h2，需要设置 proxy_http_version 1.1；后端网站的一些链接可能不是相对路径，需要用 proxy_redirect 替换。等等问题本文不再细说，请参考Nginx官方文档。

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝


## Usage

- Click the [Use this template](https://github.com/P3TERX/Actions-OpenWrt/generate) button to create a new repository.
- Generate `.config` files using [Lean's OpenWrt](https://github.com/coolsnowwolf/lede) source code. ( You can change it through environment variables in the workflow file. )
- Push `.config` file to the GitHub repository.
- Select `Build OpenWrt` on the Actions page.
- Click the `Run workflow` button.
- When the build is complete, click the `Artifacts` button in the upper right corner of the Actions page to download the binaries.

## Tips

- It may take a long time to create a `.config` file and build the OpenWrt firmware. Thus, before create repository to build your own firmware, you may check out if others have already built it which meet your needs by simply [search `Actions-Openwrt` in GitHub](https://github.com/search?q=Actions-openwrt).
- Add some meta info of your built firmware (such as firmware architecture and installed packages) to your repository introduction, this will save others' time.

## Acknowledgments

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [c-hive/gha-remove-artifacts](https://github.com/c-hive/gha-remove-artifacts)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © P3TERX
