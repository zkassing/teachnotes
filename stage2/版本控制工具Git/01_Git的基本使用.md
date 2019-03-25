# 安装 Git

最早 Git 是在 Linux 上开发的，很长一段时间内，Git 也只能在 Linux 和 Unix 系统上跑。不过，慢慢地有人把它移植到了 Windows 上。现在，Git 可以在 Linux、Unix、Mac 和 Windows 这几大平台上正常运行了。

### 在 Windows 上安装 Git

在 Windows 上使用 Git，可以从 Git 官网直接[下载安装程序](https://git-scm.com/downloads)，（网速慢的同学请移步[国内镜像](https://pan.baidu.com/s/1kU5OCOB#list/path=%2Fpub%2Fgit)），然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明 Git 安装成功！

![1546241218705](images/1546241218705.png)

![1546435573722](images/1546435573722.png)

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

因为 Git 是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和 Email 地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的 Git 仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和 Email 地址

# 创建版本库

什么是版本库呢？

> 版本库又名仓库，英文名**repository**，你可以简单理解成一个目录，这个目录里面的所有文件都可以被 Git 管理起来，每个文件的修改、删除，Git 都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

所以，创建一个版本库非常简单，

1. 选择一个合适的地方，创建一个空目录
2. 如果你使用 Windows 系统，为了避免遇到各种莫名其妙的问题，**请确保目录名（包括父目录）不包含中文**。
3. 通过`git init`命令把这个目录变成 Git 可以管理的仓库：

![1546241468812](images/1546241468812.png)

![1546435588352](images/1546435588352.png)

瞬间 Git 就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个`.git`的目录，这个目录是 Git 来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把 Git 仓库给破坏了。

![1546241530666](images/1546241530666.png)

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的

win7 的用户可以进行如下设置

![1546241605863](images/1546241605863.png)

也不一定必须在空目录下创建 Git 仓库，选择一个已经有东西的目录也是可以的。

### 把文件添加到版本库

首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如 TXT 文件，网页，所有的程序代码等等，Git 也不例外。

版本控制系统可以告诉你每次的改动，比如在第 5 行加了一个单词“Linux”，在第 8 行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从 100KB 改成了 120KB，但到底改了啥，版本控制系统不知道，也没法知道。

不幸的是，Microsoft 的 Word 格式是二进制格式，因此，版本控制系统是没法跟踪 Word 文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。(`git特别适合管理代码`)

因为文本是有编码的，比如中文有常用的 GBK 编码，日文有 Shift_JIS 编码，如果没有历史遗留问题，强烈建议使用标准的 UTF-8 编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

言归正传，现在我们编写一个`readme.txt`文件，内容如下：

```
Git is a version control system.
Git is free software.
```

和把大象放到冰箱需要 3 步相比，把一个文件放到 Git 仓库只需要两步。

1. `git add <file>`
2. `git commit -m <message>`

第一步，用命令`git add`告诉 Git，把文件添加到仓库：

```
$ git add readme.txt
```

执行上面的命令，没有任何显示，这就对了，Unix 的哲学是“没有消息就是好消息”，说明添加成功。

![1546435612600](images/1546435612600.png)

第二步，用命令`git commit`告诉 Git，把文件提交到仓库：

```
$ git commit -m "wrote a readme file"
```

![1546435625057](images/1546435625057.png)

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

嫌麻烦不想输入`-m "xxx"`行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。

**因为如果`提交记录`很多的话, 没有说明的`提交记录`, 几乎找不到, 而找不到的`提交记录`, 毫无意义...**

`git commit`命令执行成功后会告诉你，`1 file changed`：1 个文件被改动（我们新添加的 readme.txt 文件）；`2 insertions`：插入了两行内容（readme.txt 有两行内容）。

为什么 Git 添加文件需要`add`，`commit`一共两步呢？因为`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件，比如：

```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

### 小结

初始化一个 Git 仓库，使用`git init`命令。

添加文件到 Git 仓库，分两步：

1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m <message>`，完成

# 时光机穿梭

我们已经成功地添加并提交了一个 readme.txt 文件，现在，是时候继续工作了，于是，我们继续修改 readme.txt 文件，改成如下内容：

```
Git is a distributed version control system.
Git is free software.
```

现在，运行`git status`命令看看结果：

```
$ git status
```

![1546435647557](images/1546435647557.png)

`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。

虽然 Git 告诉我们`readme.txt`被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周, 从泰国回来，第一天上班时，已经记不清上次怎么修改的`readme.txt`，所以，需要用`git diff`这个命令看看：

```
$ git diff readme.txt
```

![1546321392281](images/1546321392281.png)

![1546435712102](images/1546435712102.png)

`git diff`顾名思义就是查看 difference，显示的格式正是 Unix 通用的 diff 格式，可以从上面的命令输出看到，我们在第一行添加了一个`distributed`单词。

知道了对`readme.txt`作了什么修改后，再把它提交到仓库就放心多了，提交修改和提交新文件是一样的两步，第一步是`git add`：

```
$ git add readme.txt
```

同样没有任何输出。在执行第二步`git commit`之前，我们再运行`git status`看看当前仓库的状态：

```
$ git status
```

![1546435725978](images/1546435725978.png)

`git status`告诉我们，将要被提交的修改包括`readme.txt`，下一步，就可以放心地提交了：

```
$ git commit -m "add distributed"
```

![1546435745281](images/1546435745281.png)

提交后，我们再用`git status`命令看看仓库的当前状态：

```
$ git status
```

![1546435765669](images/1546435765669.png)

Git 告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的。

### 小结

-   要随时掌握工作区的状态，使用`git status`命令。
-   如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容。

## 版本回退

现在，你已经学会了修改文件，然后把修改提交到 Git 版本库，现在，再练习一次，修改 readme.txt 文件如下：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

然后尝试提交：

```
$ git add readme.txt
```

![1546321604139](images/1546321604139.png)

![1546321697019](images/1546321697019.png)

像这样，你不断对文件进行修改，然后不断提交修改到版本库里，就好比玩 RPG 游戏时，每通过一关就会自动把游戏状态存盘，如果某一关没过去，你还可以选择读取前一关的状态。有些时候，在打 Boss 之前，你会手动存盘，以便万一打 Boss 失败了，可以从最近的地方重新开始。Git 也是一样，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在 Git 中被称为`commit`。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个`commit`恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

现在，我们回顾一下`readme.txt`文件一共有几个版本被提交到 Git 仓库里了：

版本 1：wrote a readme file

```
Git is a version control system.
Git is free software.
```

版本 2：add distributed

```
Git is a distributed version control system.
Git is free software.
```

版本 3：append GPL

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
```

当然了，在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容，不然要版本控制系统干什么。版本控制系统肯定有某个命令可以告诉我们历史记录，在 Git 中，我们用`git log`命令查看：

```
$ git log
commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:06:15 2018 +0800

    append GPL

commit e475afc93c209a690c39c13a46716e8fa000c366
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 21:03:36 2018 +0800

    add distributed

commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Fri May 18 20:59:18 2018 +0800

    wrote a readme file
```

![1546321774061](images/1546321774061.png)

`git log`命令显示从最近到最远的提交日志，我们可以看到 3 次提交，最近的一次是`append GPL`，上一次是`add distributed`，最早的一次是`wrote a readme file`。

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：

```
$ git log --pretty=oneline
1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
```

![1546321811785](images/1546321811785.png)

需要友情提示的是，你看到的一大串类似`7f1b0d8...`的是`commit id`（版本号），和 SVN 不一样，Git 的`commit id`不是 1，2，3……递增的数字，而是一个 SHA1 计算出来的一个非常大的数字，用十六进制表示，而且你看到的`commit id`和我的肯定不一样，以你自己的为准。为什么`commit id`需要用这么一大串数字表示呢？因为 Git 是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用 1，2，3……作为版本号，那肯定就冲突了。

每提交一个新版本，实际上 Git 就会把它们自动串成一条时间线。如果使用可视化工具查看 Git 历史，就可以更清楚地看到提交历史的时间线：

![1546321873595](images/1546321873595.png)

好了，现在我们启动时光穿梭机，准备把`readme.txt`回退到上一个版本，也就是`add distributed`的那个版本，怎么做呢？

首先，Git 必须知道当前版本是哪个版本，在 Git 中，用`HEAD`表示当前版本，也就是最新的提交`7f1b0d8...`（注意我的提交 ID 和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上 100 个版本写 100 个`^`比较容易数不过来，所以写成`HEAD~100`。

现在，我们要把当前版本`append GPL`回退到上一个版本`add distributed`，就可以使用`git reset`命令：

```
$ git reset --hard HEAD^
```

![1546321976984](images/1546321976984.png)

`--hard`参数有啥意义？这个后面再讲，现在你先放心使用。

看看`readme.txt`的内容是不是版本`add distributed`：

```
$ cat readme.txt
```

![1546322015660](images/1546322015660.png)

果然被还原了。

还可以继续回退到上一个版本`wrote a readme file`，不过且慢，然我们用`git log`再看看现在版本库的状态：

```
$ git log
```

![1546322088866](images/1546322088866.png)

最新的那个版本`append GPL`已经看不到了！好比你从 21 世纪坐时光穿梭机来到了 19 世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个`append GPL`的`commit id`是`7f1b0...`，于是就可以指定回到未来的某个版本：

```
$ git reset --hard 7f1b0
```

![1546322163872](images/1546322163872.png)

版本号没必要写全，前几位就可以了，Git 会自动去找。当然也不能只写前一两位，因为 Git 可能会找到多个版本号，就无法确定是哪一个了。

再小心翼翼地看看`readme.txt`的内容：

```
$ cat readme.txt
```

![1546322188847](images/1546322188847.png)

果然，我胡汉三又回来了。

Git 的版本回退速度非常快，因为 Git 在内部有个指向当前版本的`HEAD`指针，当你回退版本的时候，Git 仅仅是把 HEAD 从指向`append GPL`：

![1546922573841](images/1546922573841.png)

改为指向`add distributed`：

![1546922583813](images/1546922583813.png)

然后顺便把工作区的文件更新了。所以你让`HEAD`指向哪个版本号，你就把当前版本定位在哪。

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的`commit id`怎么办？

在 Git 中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`add distributed`版本时，再想恢复到`append GPL`，就必须找到`append GPL`的 commit id。Git 提供了一个命令`git reflog`用来记录你的每一次命令：

```
$ git reflog
```

![1546322261943](images/1546322261943.png)

终于舒了口气，从输出可知，`append GPL`的 commit id 是`7f1b0d8`，现在，你又可以乘坐时光机回到未来了。

### 小结

现在总结一下：

-   `HEAD`指向的版本就是当前版本，因此，Git 允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
-   穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
-   要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

## 工作区和暂存区

Git 和其他版本控制系统如 SVN 的一个不同之处就是有暂存区的概念。

![1546922221020](images/1546922221020.png)

-   Workspace：工作区
-   Index / Stage：暂存区
-   Repository：仓库区（或本地仓库）
-   Remote：远程仓库

#### 工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的`ai`文件夹就是一个工作区：

![1546322815786](images/1546322815786.png)

#### 版本库（Repository）

工作区有一个隐藏目录`.git`，这个不算工作区，而是 Git 的版本库。

Git 的版本库里存了很多东西，其中最重要的就是称为 stage（或者叫 index）的暂存区，还有 Git 为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

![1546922236772](images/1546922236772.png)

分支和`HEAD`的概念我们以后再讲。

前面讲了我们把文件往 Git 版本库里添加的时候，是分两步执行的：

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建 Git 版本库时，Git 自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对`readme.txt`做个修改，比如加上一行内容：

```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```

然后，在工作区新增一个`LICENSE`文本文件（内容随便写）。

![1546322988738](images/1546322988738.png)

先用`git status`查看一下状态：

```
$ git status
```

![1546323024777](images/1546323024777.png)

Git 非常清楚地告诉我们，`readme.txt`被修改了，而`LICENSE`还从来没有被添加过，所以它的状态是`Untracked`。

现在，使用两次命令`git add`，把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下:

![1546323114567](images/1546323114567.png)

现在，暂存区的状态就变成这样了：

![1546922250947](images/1546922250947.png)

所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。

```
$ git commit -m "understand how stage works"
```

![1546323209487](images/1546323209487.png)

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

```
$ git status
```

![1546323243255](images/1546323243255.png)

现在版本库变成了这样，暂存区就没有任何内容了：

![1546922264546](images/1546922264546.png)

### 小结

**暂存区是 Git 非常重要的概念，弄明白了暂存区，就弄明白了 Git 的很多操作到底干了什么。**

## 管理修改

现在，假定你已经完全掌握了暂存区的概念。下面，我们要讨论的就是，为什么 Git 比其他版本控制系统设计得优秀，因为 Git 跟踪并管理的是修改，而非文件。

![1546435931506](images/1546435931506.png)

你会问，什么是修改？比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。

为什么说 Git 管理的是修改，而不是文件呢？我们还是做实验。第一步，对 readme.txt 做一个修改，比如加一行内容：

![1546323354927](images/1546323354927.png)

然后，添加：

```
$ git add readme.txt
$ git status
```

![1546323398022](images/1546323398022.png)

然后，再修改 readme.txt：

![1546323426907](images/1546323426907.png)

提交：

```
$ git commit -m "git tracks changes"
```

![1546323482188](images/1546323482188.png)

提交后，再看看状态：

```
$ git status
```

![1546323505665](images/1546323505665.png)

咦，怎么第二次的修改没有被提交？

别激动，我们回顾一下操作过程：

第一次修改 -> `git add` -> 第二次修改 -> `git commit`

你看，我们前面讲了，Git 管理的是修改，当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

提交后，用`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别：

```
$ git diff HEAD -- readme.txt
```

![1546323553753](images/1546323553753.png)

可见，第二次修改确实没有被提交。

那怎么提交第二次修改呢？你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了：

第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

![1546325763644](images/1546325763644.png)

### 小结

现在，你又理解了 Git 是如何跟踪修改的，每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。

## 撤销修改

自然，你是不会犯错的。不过现在是凌晨两点，你正在赶一份工作报告，你在`readme.txt`中添加了一行：

![1546325790293](images/1546325790293.png)

在你准备提交前，一杯咖啡起了作用，你猛然发现了`stupid boss`可能会让你丢掉这个月的奖金！

既然错误发现得很及时，就可以很容易地纠正它。你可以删掉最后一行，手动把文件恢复到上一个版本的状态。如果用`git status`查看一下：

```
$ git status
```

![1546326010297](images/1546326010297.png)

你可以发现，Git 会告诉你，`git checkout -- file`可以丢弃工作区的修改：

```
$ git checkout -- readme.txt
```

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

![1546326148079](images/1546326148079.png)

现在，看看`readme.txt`的文件内容：

![1546326117481](images/1546326117481.png)

文件内容果然复原了。

`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。

现在假定是凌晨 3 点，你不但写了一些胡话，还`git add`到暂存区了：

![1546326175030](images/1546326175030.png)

![1546326191723](images/1546326191723.png)

庆幸的是，在`commit`之前，你发现了这个问题。用`git status`查看一下，修改只是添加到了暂存区，还没有提交：

![1546326221103](images/1546326221103.png)

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   readme.txt
```

Git 同样告诉我们，用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区：

![1546326583352](images/1546326583352.png)

`git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。

再用`git status`查看一下，现在暂存区是干净的，工作区有修改：

![1546435542840](images/1546435542840.png)

还记得如何丢弃工作区的修改吗？

```
$ git checkout -- readme.txt
```

整个世界终于清静了！

![1546326673024](images/1546326673024.png)

现在，假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得[版本回退](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节吗？可以回退到上一个版本。不过，这是有条件的，就是你还没有把自己的本地版本库推送到远程。还记得 Git 是分布式版本控制系统吗？我们后面会讲到远程版本库，一旦你把`stupid boss`提交推送到远程版本库，你就真的惨了……

### 小结

又到了小结时间。

场景 1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景 2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景 1，第二步按场景 1 操作。

场景 3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节，不过前提是没有推送到远程库
