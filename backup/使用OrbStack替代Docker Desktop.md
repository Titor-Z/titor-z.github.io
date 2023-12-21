

👉  在阅读此篇文章前，我假定你已经了解并使用过Docker，否则你应先对Docker相关知识有所了解。

## OrbStack是什么？

[OrbStack · Fast, light, simple Docker & Linux on macOS](https://orbstack.dev)

<aside>
💡 OrbStack是一个强大的Docker Desktop替代品。它提供了一种在本地环境中进行容器化开发的方式，无需担心Docker Desktop可能会带来的性能问题或高昂的许可费用。

OrbStack具有一些引人注目的特性，包括支持Windows, MacOS和Linux，强大的性能和稳定性，以及与主流容器编排工具的无缝集成。它的用户界面也非常直观，使得开发者可以轻松地管理和监控他们的容器。

通过使用OrbStack，开发者可以更加高效地进行容器化开发，同时还可以节省一些可能用于购买Docker Desktop许可的成本。这使得OrbStack成为了Docker Desktop的理想替代品。

</aside>

## 使用Docker UI界面的原因

日常在Linux上使用Docker，并没有什么性能问题，大家都是在CLI中使用指令，主要就是用来搭建容器环境，部署项目而已。而平时在本地开发项目时，需要的操作就会繁琐和复杂的多。比如：

- 为项目编写Dockerfile和docker-compose，测试实例能否正常启动。
- 删除、启动、停止多个Container和Image。
- 查看Container的配置信息，历史日志。
- 快速进入或启动一个Container实例，并进入实例的shell。

以上这些情况，通过CLI也可操作，但每次都需要敲击很多遍，才能完成。相反，通过Docker Desktop提供的UI界面，鼠标点击下就能完成很多批量操作，这无异于能够节省很多时间。

### **Docker Desktop 存在的意义**

# 提供了一套方便的UI界面。

- 能够方便查看，编辑、删除Image和Container。
- 它最有意思的点，应该就是能够在WSL中搭建Dev Container，通过VSCode提供的Remote-wsl直接进入容器。
- 还可以直接在UI界面中查看已启动容器的日志，直接进入容器实例内的CLI。
- 还可以查看CPU、RAM、Disk的每个Container和Image占用情况。
- 以及方便的对Docker进行设置。

但它的弊端，就是每次在本地使用Docker，都需要先启用Docker Desktop，如果有最新版本，还会要求更新，有时还会有评分反馈。但这些都还不算什么，它最大的问题，就是对宿主机的资源占用太大，启动Docker的速度太慢，尤其是在一些时间比较久的机器上，这种对资源的开销是不能忍受的。

而我日常是在一台比较久的Mac上做一些Demo，尽管已将vscode配置的很精简了，但同时打开浏览器，并启动Docker Desktop后，电脑性能还是会明显下降。因此需要一款性能更好的UI操作界面。

我曾尝试过使用Dockeg来操作，但它目前的UI界面还存在BUG，对于在服务器端做维护来说是一个很不错的选择，但对于本地环境来说，还是一款App界面操作来的更方便。直到后来刷视频看到别人分享了OrbStack，尝试下载使用了一下。而相较于Podman和Docker Desktop，确实更简单直接。

### OrbStack 使用情况

- 启动速度很快，从启动到运行都在2～5s以内。
- 界面干净简单，没有多余内容。操作习惯直接、方便。
- 基本的Container、Volume、Image、查看Container的状态、信息、Log、一键Container shell、这些功能都有。
- 还提供了容器编排的Pod、Service界面。
- 额外提供了一项Linux子容器界面。
- UI界面占用内存很小，目前看只有64MB，但Virtual Machine Service进程内存占用在340MB。

就目前UI操作界面的占用来说，它的内存占用已经很低，界面的使用比Docker Desktop精简，反应速度更快，初次使用，没有出现卡顿情况，具体情况，需要后期用户自己使用。但对于日常频繁使用的功能，都给予了提供，因此可以完全替代Docker Desktop在本地使用。

## 上干货，直接介绍如何安装

先问大家一个问题，有没有想过直接删掉Docker Desktop（它的内部包含了Docker Client、Engine和其他的一众捆绑）提供的环境，反而像Linux上一样直接从shell中访问，给Mac或Win提供一个纯粹的Docker环境。（答案，是有的，大家可自行搜索**Lima** & ****Colima****），这里，我将演示使用OrbStack提供一个轻量的Docker for Mac 环境。

## 卸载Mac的Docker环境

- 删除Docker Desktop for Mac应用
- 或执行以下命令

```bash
 /Applications/Docker.app/Contents/MacOS/uninstall
```

当删除环境之后，系统还会存在残存的文件信息，可通过以下指令清除：

```bash
rm -rf ~/Library/Group\ Containers/group.com.docker
rm -rf ~/Library/Containers/com.docker.docker
rm -rf ~/.docker
```

详情可参考官方文档：

[Uninstall Docker Desktop](https://docs.docker.com/desktop/uninstall/#uninstall-docker-desktop)

## 安装OrbStack & Docker for Mac 环境

1.  首先，需要使用 HomeBrew 安装 Docker CLI，为本地提供Docker Client服务

```bash
brew install docker
```

1. 下载 OrbStack
    - 官网下载：[https://orbstack.dev/download](https://orbstack.dev/download)
    - HomeBrew 安装
        
        ```bash
        brew install orbstack
        ```
        
    

以上便完成了安装，接下来启动 OrbStack后，便可以通过Terminal正常使用Docker指令。以上操作安装的Docker环境，每次使用Docker时，只需要启动OrbStack，不存在其他占用内存的消耗。

具体的Settings，比如 Docker源设定，和虚拟机资源占用，通过OrbStack的Settings配置即可。

## 卸载OrbStack环境

1. 删除OrbStack应用：打开Application目录，删除OrbStack.app
2. 如果是通过HomeBrew安装，则执行
    
    ```bash
    brew uninstall orbstack
    ```
    
3. 卸载Docker Cli
    
    ```bash
    brew uninstall docker
    ```
    

以上便是关于在Mac下配置Docker Desktop for Mac的轻量化替换产品OrbStack的说明。

<br>
<footer style="color: gray">
🫥 转载请注明并粘贴本篇文章的URL。
</footer>