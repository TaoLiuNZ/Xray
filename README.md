# Xray

Original Repo: https://github.com/kirin10000/Xray-script

# Some changes need to be made
Allow beta version --beta\
Allow logs, remove --without logs\
Allow geodata, remove --without geodata\
Allow updating geodata\
Add updating geodata script\
Block cn/ir traffic\
Change script URL


# Manual steps

1. Certificates
bash <(curl -Ls https://raw.githubusercontent.com/TaoLiuNZ/Xray/main/install.sh)

// Add paths to node.js project and build
// Copy server.json to /usr/local/etc/xray/config.json

// Permission
chmod 755 /root/cert/fullchain.cer
chmod 755 /root/cert/ukmemory.online.cer

//注意：若还出现错误23,是因为权限没有设置对可以试一试这种方法

编辑文件 vi /etc/systemd/system/xray.service ,将User=nobody 修改为User=root\

找到 CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE这一行 前面加上# 注释掉\

systemctl daemon-reload 重新加载下\

2. Xray
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install -u root --beta

3. Nginx
// 证书安装必须在nginx之前，不然nginx会占用80端口
apt update && apt install nginx -y\
把伪装站点的文件全部上传到 /var/www/html\
Copy nginx config to /etc/nginx/nginx.conf\

4.开机启动

 systemctl enable xray\
 systemctl enable nginx\


5. Xray启动和常用命令

 systemctl start xray\
 systemctl status xray #查看状态\
 systemctl status nginx #查看ng状态\
 systemctl restart xray\
 systemctl reload nginx\
