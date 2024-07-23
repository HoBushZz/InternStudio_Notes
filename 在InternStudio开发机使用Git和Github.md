# 在InternStudio开发机将文件提交到指定项目分支

## 准备好Git环境

```shell
sudo apt update
sudo apt install git
```

并且准备好相关VSCode插件：

![image-20240724011347553](D:\桌面\InternStudioNotes\在InternStudio开发机使用Git和Github.assets\image-20240724011347553.png)

## Fork的相关基础

首先明确fork不是Git操作，而是一个Github操作。Fork之后的仓库包含了原来的仓库（即upstream repository，上游仓库）所有内容，如分支、Tag、提交。如果想将你的修改合并到原项目中时，可以通过的 Pull Request 把你的提交贡献回原仓库。总结：

- 从Github单纯clone一个仓库，除非自己是这个仓库的贡献者，否则无法向其pull request，只能取最新代码（git fetch），能本地的仓库与源仓库同步。
- 如果fork一个仓库后，再clone fork的仓库，就可以随意拉取(fetch)和推送(pull)，并且可以通过pull request向upstream 仓库贡献代码

## 本地分支与远程分支

- 远程分支其实就是**远程代码仓库当中的分支**，比如我们的repo如果是存在github的，那么这个远程仓库就是github。在使用git clone的时候，git会自动地**将这个远程的repo命名为origin**，拉取它所有的数据之后，创建一个指向它master的指针，命名为origin/master，之后会在本地创建一个指向同样位置的指针，命名为master，和远程的master作为区分。一句话总结，origin指的是远程仓库名

假设你在一个 Git 仓库中，运行以下命令：

`git branch -a`

你会看到类似以下的输出：

```bash
* main
 feature-branch
 remotes/origin/HEAD -> origin/main
 remotes/origin/main
 remotes/origin/feature-branch
```

- `* main`：当前所在的本地分支。
- `feature-branch`：其他本地分支。
- `remotes/origin/HEAD -> origin/main`：远程仓库 `origin` 的默认分支。
- `remotes/origin/main`：远程分支 `origin/main`。
- `remotes/origin/feature-branch`：远程分支 `origin/feature-branch`。

## **流程**

### Fork目标项目

[目标项目地址](https://github.com/InternLM/Tutorial)

启动开发机，在VsCode终端输入：

```bash
git clone https://github.com/XXX/Tutorial.git # 修改为自己frok的仓库
cd Tutorial/
git branch -a #查看当前分支内容
```

![image-20240724022542438](D:\桌面\InternStudioNotes\在InternStudio开发机使用Git和Github.assets\image-20240724022542438.png)

本地分支camp3，远程默认分支为origin/camp3，图中可以知道只有一个远程分支camp3。

### 自定义新分支

```bash
git checkout -b camp3_2282 # 自定义一个新的分支，#2282是自己的ID名
```

### 创建文件

```bash
touch ./data/Git/task/camp3_2282.md ##2282是自己的ID名
```

在VSCode中编辑内容

### 提交更改到分支

提交前需要设置好本地Git**用户信息**，可以是全局设置也可以是本地设置。

局部设置例子，在目标文件夹下：

```bash
git config --local user.name "Your Name"
git config --local user.email "your.email@example.com"
```

提交更改：

```bash
git add .
git commit -m "add git_2282_introduction" # 提交信息记录
```

### push更改到fork的repo

```bash
git push origin camp3_2282 #2282是自己的ID名
```

- 本地分支 `camp3_2282` 的所有提交将被推送到远程仓库 `origin` 的 `camp3_2282` 分支。
- 如果远程仓库中不存在 `camp3_2282` 分支，则会创建一个新的分支 `camp3_2282`

### 查看提交

到fork的Github链接上查看：
![image-20240724023950624](D:\桌面\InternStudioNotes\在InternStudio开发机使用Git和Github.assets\image-20240724023950624.png)

### 在 github 页面将修改的内容 PR 到 Tutorial

