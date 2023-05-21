# 我的开发环境


## 视频教程

https://www.bilibili.com/video/BV1ZL4y1u7c4/

## 使用方法

1. 安装最新版 Docker 客户端
2. 打开 Docker 客户端的配置
    1. 找到 Docker Engine 选项卡，配置 registry-mirrors（自行搜索教程）
    2. 找到 Resources 选项卡，配置 Proxies（可跳过）
3. `git clone https://github.com/FrankFang/oh-my-env-1.git` 将 oh-my-env-1 下载到本地（也可以直接下载 zip），重命名为 oh-my-env
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

* 方法一：直接在 Docker 客户端里设置代理即可。
* 方法二：https://github.com/yuanlam/Clash-Linux#%E4%B8%89%E5%AE%89%E8%A3%85clash%E4%BD%BF%E7%94%A8yuanlam%E7%94%A8%E6%88%B7%E7%99%BB%E5%BD%95
