# 我的开发环境


## 视频教程

https://www.bilibili.com/video/BV1ZL4y1u7c4/

## 使用方法

1. 安装最新版 Docker 客户端
2. 打开 Docker 客户端的配置
    1. 找到 Docker Engine 选项卡，配置 registry-mirrors（自行搜索教程）
    2. 找到 Resources 选项卡，配置 Proxies（可跳过）
3. `git clone https://github.com/FrankFang/oh-my-env-1.git` 将 oh-my-env-1 下载到本地（也可以直接下载 zip），重命名为 oh-my-env
    1. mac M1 用户请将 `.devcontainer/Dockerfile` 文件中的 `oh-my-docker:mangosteen` 改为 `oh-my-docker-m1:mangosteen`（会遇到兼容性问题，不推荐这么做）
4. 打开 Windows/Mac 的终端，运行 `docker network create network1`
5. 打开 VSCode
    1. 安装 Dev Containers 插件
    2. 将 oh-my-env 目录拖入 VSCode
    3. 输入 Ctrl + Shift + P，然后输入 Reopen，回车，等待
6. 等上一步启动完毕之后，新建终端
    1. 运行 `nvm use system` 和 `node --version` 得到 node 运行环境
    2. 运行 `rvm use 3` 和 `ruby --version` 得到 ruby 运行环境

## 如何升级



1. 删掉本地的旧镜像

    ```bash
    docker rmi frankfang128/oh-my-docker:mangosteen
    # 如果你是 M1 用户，那么你可以把 oh-my-docker 改为 oh-my-docker-m1（但是 m1 会遇到很多兼容性问题，所以我不推荐你这么做）
    ```
2. 删除之前的 oh-my-env 目录，下载最新的 oh-my-env，然后用 VSCode 打开，输入 Ctrl + Shift + P，然后输入 Reopen，回车，等待
    1. 如果你之前是用 `git clone` 下载的 oh-my-env-1，那么你也可以用 `git pull` 命令来更新代码
    
## 数据备份

```
# 首次备份
# 可选 find ~/repos -name .git -print0 | xargs -0 rm -rf
# 可选 find ~/repos -name cache -print0 | xargs -0 rm -rf
cp -r ~/repos /workspaces/oh-my-env/repos
# 后续增量备份
rsync -avz --delete  ~/repos  /workspaces/oh-my-env/repos
```

## 如何使用宿主机的代理

你的 docker 环境里访问外网会发现无法连接或者下载速度很慢，怎么才能用上宿主机的代理呢？步骤如下：

1. 在 Docker 终端运行 `code /workspaces/oh-my-env/.devcontainer/devcontainer.json`
2. 搜索 `--network`，找到这一行并注释掉或者删掉
3. 在 VSCode 中 rebuild 当前环境
4. 获取宿主机的 IP，以 Clash 为例，点击 General 面板中的 Allow LAN 文字旁边的图标，就能获取 WSL 的 Address：172.29.xxx.x
5. 回到 Docker 终端运行 `export all_proxy="socks5://172.29.xxx.x:1080"`，然后终端里的其他命令就能网速飞快地运行了
6. 运行完了之后，把第 2 步里注释掉的 `--network` 改回来，重新 rebuild（此时代理就不能用了）

这个方法略显麻烦，因为一旦你启用了 network，就不能访问宿主机；但不启用 network，开发又不是那么方便。

## 如何 trojan

1. 运行 `code ~/.config/trojan.conf`，将你自己购买的 trojan 服务器的 JSON 配置复制进去，保存文件
2. 运行命令 `fq`
    * 这是我写在 bashrc 里的 alias，会去运行 `trojan` 命令
    * 这个命令会在后台运行，运行日志在 /tmp/trojan.log
    * 如果你想关闭它，可以运行 `killall trojan` 命令
4. 如果你的本地代理端口不是 1080， 那么你需要运行 `code ~/.config/proxychains.conf`，将 1080 改为你的端口，然后保存文件
5. 在你的任意命令前加 pc 即可，例如：
    1. pc git clone git@xxxxx
    2. pc curl -L https://twitter.com

