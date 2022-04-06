# 我的开发环境

## 视频教程

https://www.bilibili.com/video/BV1ZL4y1u7c4/

## 使用方法

1. 安装最新版 Docker 客户端
2. 打开 Docker 客户端的配置
    1. 找到 Docker Engine 选项卡，配置 registry-mirrors（自行搜索教程）
    2. 找到 Resources 选项卡，配置 Proxies（可跳过）
3. `git clone https://github.com/FrankFang/oh-my-env-1.git` 将 oh-my-env-1 下载到本地，重命名为 oh-my-env
4. 打开 Windows/Mac 的终端，运行 `docker network create network1`
5. 打开 VSCode
    1. 安装 Remote - Container 插件
    2. 打开 oh-my-env 目录
    3. 输入 Ctrl + Shift + P，然后输入 Reopen，回车，等待
6. 等上一步启动完毕之后，新建终端
    1. 运行 `nvm use system` 和 `node --version` 得到 node 运行环境
    2. 运行 `rvm use 3` 和 `ruby --version` 得到 ruby 运行环境
