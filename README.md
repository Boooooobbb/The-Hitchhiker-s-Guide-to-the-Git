# Git 文档

## Git 使用指南

>Git 是一款主流的分布式**版本控制系统** (VCS, Version Control System)，主要用于管理和记录对于文件的修改。本指南旨在为快速入门使用 Git Bash 进行文件的版本控制提供帮助。 

### 什么是版本控制

- 每有新的修改时，都会创造新的版本  
- 版本控制可以查看各版本中的**修改都有哪些**
- 也可以查看是**谁**在什么**时间**进行了这些修改
- 更可以**回退**到任何之前的版本  

---

### 使用 Git 的三种形式

- **Git Bash**：Linux 风格的命令行（✅ 推荐使用，使用指南以这种形式为主体）
- **Git CMD**：Windows 风格的命令行
- **Git GUI**：图形界面的 Git

---

### Linux 命令行基本用法（使用 Bash 的基础）

[Linux 命令行基本用法](Linux%20文档.md#Linux%20命令行基本用法)

---

### Git 使用必要配置（⚠一定要配置⚠）

1. 配置 name（请将 `<your-name>` 部分换成你的用户名，可以自己任取，注意不要忘记双引号） ^quote-of-name
    ```bash
    git config --global user.name "<your-name>"
    ``` 
2. 配置 email（请将 `<your-email>` 部分换成你的邮箱，最好使用自己的邮箱）
    ```bash
    git config --global user.email <your-email>
    ```
3. 检查配置是否已完成
    ```bash
    git config --global --list
    ```

---

### 创建本地仓库

1. 进入需要作为本地 Git 仓库的目录  
2. 在右键菜单中点击 “Open Git Bash here”  
	![Git%20使用指南-创建仓库-创建本地仓库-1](images/Git%20使用指南-创建仓库-创建本地仓库-1.png)
	
3. 在 Git Bash 中输入以下命令**创建本地仓库**`init` = **Init**ialization
    ```bash
    git init
    ```
4. 如果创建成功，当前目录下会有一个名为 `.git` 的隐藏文件夹  （ps. 如果不知道在 Windows 下如何查看隐藏文件夹，不妨自行探索一下 :P）
	
	![Git 使用指南-创建仓库-创建本地仓库-2](images/Git%20使用指南-创建仓库-创建本地仓库-2.png)
---

### Git 基本操作

#### 文件的三种状态

![Git 使用指南-Git 基本操作-文件的三种状态](images/Git%20使用指南-Git%20基本操作-文件的三种状态.png)
- **未跟踪** or **未暂存**——文件位于工作目录下（还记得在执行 `git init`后，有一个隐藏的`.git`文件的目录吗，这就是工作目录 :D）
    - **未跟踪**：文件未被纳入版本控制
    - **未暂存**：文件被修改后，新的修改未提交到暂存区
- **已暂存**：修改后的文件或新文件已被提交至暂存区（暂存区类似于一个临时仓库）
- **已提交**：所有暂存区内的文件被提交成一个新的正式版本（临时仓库内的所有货物📦被转运至正式仓库储存，并被给予一个正式的批次标记🏷️）

#### 状态间的转换

##### 添加工作区至暂存区（add）

- 添加**未跟踪的新文件**至版本控制 or 提交**修改后的文件**到暂存区：
	- `git add .`：将当前工作目录下所有文件（包括工作目录下文件夹内的所有文件）都提交到暂存区
	- `git add <filename>`：将工作目录下文件名为`filename`的文件提交到暂存区
		- 例：`git add DocsForGit.md` 将`DocsForGit.md`提交到暂存区

##### 提交暂存区至本地仓库（commit）

- 将暂存区内所有修改提交到**本地仓库**
- `git commit -m "<message>"`：`<message>`为附加信息（类似于注释），一般简要地描述一下本次提交的暂存区的修改有哪些 ^quote-of-commit-message


#### 状态的查看（status）

- 查看工作目录下文件的状态：
	```bash
	git status
	````
- 文件未跟踪（新文件未提交到暂存区）：
	
	![状态的查看（status）-1](images/Git%20使用指南-Git%20基本操作-状态的查看（status）-1.png)
	
- 文件未暂存（文件修改后未提交到暂存区）：
	
	![状态的查看（status）-2](images/Git%20使用指南-Git%20基本操作-状态的查看（status）-2.png)
	
- 文件未提交（暂存区文件未提交到**本地仓库**）：
	
	![状态的查看（status）-3](images/Git%20使用指南-Git%20基本操作-状态的查看（status）-3.png)
	

#### 查看提交日志（log）

- 查看每次`commit`的记录：
	```bash
	git log
	```
- 命令行中会显示每次`commit`的<u>身份证commitID</u>（一个唯一的标识符）以及<u>是谁干的</u>（[怎么判断是谁——配置的name](#^quote-of-name)）、<u>什么时候干的</u>、<u>留下的附加信息是什么</u>（[忘记什么是附加信息了？](#^quote-of-commit-message)）
	
	![Git 使用指南-Git 基本操作-查看提交日志（log）](images/Git%20使用指南-Git%20基本操作-查看提交日志（log）.png)
	
- 一些`log`命令的选项（(((φ(◎ロ◎;)φ)))晕头转向？下有终极解决方案）
	1. `--all`：显示所有分支
	2. `--pretty=oneline`：将每次`commit`的记录信息合并到一行显示
	3. `--abbrev-commit`：精简显示每次`commit`的标识符（只取前7位）
	4. `--graph`：以图的形式显示`commit`记录
- 给`git log  --all --pretty=oneline --abbrev-commit --graph`配置别名`git-log`（[如何为长命令配置别名？](Linux%20文档#为长命令配置别名)）
	```
	alias git-log='git log  --all --pretty=oneline --abbrev-commit --graph'
	```
	
#### 版本回退

- 回退到之前`commit`的版本：
	```bash
	git reset --hard <commitID>
	```
	- 例：`git reset --hard c8f6cb1` 回退到commit ID（输入commit ID的前七位或完整版皆可）为c8f6cb1的版本
- 查看**所有操作**的ID（回退版本后找不到一些commit ID时使用）：
	```bash
	git reflog
	```

#### 忽略列表

- 符合忽略列表中制定的规则的文件都不会被纳入版本控制
- 创建忽略列表（该文件名是固定的！！！）：
	```bash
	touch .gitignore
	```
- 如何撰写忽略列表：文件通配符（常用通配符见下表）

| 通配符  |           作用           |       示例        |                      说明                       |
| :--: | :--------------------: | :-------------: | :-------------------------------------------: |
| `*`  | 匹配**任意长度**的任意字符（包括空字符） |     `*.txt`     |                匹配所有 `.txt` 文件                 |
|      |                        |     `doc*`      |                匹配以 `doc` 开头的文件                |
|      |                        |   `*report*`    |             匹配文件名中包含 `report` 的文件             |
| `?`  |      匹配**单个**任意字符      |   `file?.txt`   | 匹配 `file1.txt`、`fileA.txt`（但不匹配 `file10.txt`） |
| `[]` |   匹配**括号内指定范围**的单个字符   | `file[1-3].txt` |    匹配 `file1.txt`、`file2.txt`、`file3.txt`     |
|      |                        |   `[aeiou]*`    |                 匹配以元音字母开头的文件                  |
|      |                        |    `[!0-9]*`    |           匹配**不以数字开头**的文件（`!` 表示排除）           |

---

### Git 分支
#### 什么是分支

分支就是由主干引申出的枝干。把正在进行的工作想象成一棵树，当你和你的伙伴需要同时针对主干开发不同的功能时，你们可以创建几个枝干（即分支），并在各自的枝干上完成自己的任务。之后再将各自的成果合并到主干，从而使主干不断完善。

#### 查看、创建本地分支（branch）

- 查看本地分支（看一看树上有哪些枝干）：
	```bash
	git branch
	```
- 创建本地分支（创建一个枝干）：
	```bash
	git branch <branch-name>
	```
- 示例：
	1. 创建一个名为`dev`的分支：
		```bash
		git branch dev
		```
	2. 查看本地分支：
		```bash
		git branch
		```
		
		![Git 使用指南-Git 分支-查看、创建本地分支（branch）](images/Git%20使用指南-Git%20分支-查看、创建本地分支（branch）.png)

#### 切换分支（checkout）

- 切换分支（从一个枝干跳到另一个枝干上）：
	```bash
	git checkout <branch-name>
	```
- 示例：
	1. 切换分支前：
		
		![Git 使用指南-Git 分支-切换分支（checkout）-1](images/Git%20使用指南-Git%20分支-切换分支（checkout）-1.png)
		
	2. 切换至`dev`分支：
		```bash
		git checkout dev
		```
		
		![Git 使用指南-Git 分支-切换分支（checkout）-2](images/Git%20使用指南-Git%20分支-切换分支（checkout）-2.png)
		
- ⭐⭐⭐实用用法：创建分支并切换到该分支 
	```bash
	git checkout -b <branch-name>
	```
	- 例：
		```bash
		git checkout -b feature/01
		```
		
		![Git 使用指南-Git 分支-切换分支（checkout）-3](images/Git%20使用指南-Git%20分支-切换分支（checkout）-3.png)

#### 合并分支（merge）

- 把一个分支里的成功合并到主分支（`master`）或其他分支
- 合并分支的步骤
	1. 利用`git checkout`切换到目标分支（一般为主分支`master`）
		![Git 使用指南-Git 分支-合并分支（merge）-1](images/Git%20使用指南-Git%20分支-合并分支（merge）-1.png)
	2. 利用`merge`命令将其他分支合并到当前所在分支（`merge`命令会默认把命令中指定的分支`<branch-to-merge>`合并到当前所在分支）
		```bash
		git merge <branch-to-merge>
		```
	3. 一般情况下，合并分支后即可利用以下命令将该分支删除
		```bash
		git branch -d <branch-to-delete>
		```
	- 注：未进行合并的分支需要使用以下命令进行删除（之所以命令中是`D`，主要是为了防止误删除未合并的分支）
		```bash
		git branch -D <branch-to-delete>
		```
- 解决合并过程中分支间的冲突（两个分支都针对同一数据进行了修改，且修改的结果不同）的一般步骤 ^quote-of-conflict
	1. 合并出现冲突时的提示
		
		![Git 使用指南-Git 分支-合并分支（merge）-2](images/Git%20使用指南-Git%20分支-合并分支（merge）-2.png)
		
	2. Git 会自动保留冲突的部分，需要你手动处理出现冲突的地方（在冲突的部分所在的文件中，删掉不需要的，按需求修改内容）
		
		![Git 使用指南-Git 分支-合并分支（merge）-3](images/Git%20使用指南-Git%20分支-合并分支（merge）-3.png)
		
	3. 再重新`add`、`commit`一下有冲突的文件

---

### Git 远程仓库

#### 配置公钥连接远程仓库

1. 生成 SSH 公钥：输入以下命令，并不断回车
	```bash
	ssh-keygen -t rsa
	```
2. 查看生成的公钥
	```bash
	cat ~/.ssh/id_rsa.pub
	```
3. 将公钥（图中黄色方框中的部分）复制（[在 Git Bash 中如何进行复制?](Linux%20文档#^quote-of-copy)）到远程仓库平台的SSH设置中
	![Git 使用指南-Git 远程仓库-配置公钥连接远程仓库-1](images/Git%20使用指南-Git%20远程仓库-配置公钥连接远程仓库-1.png)
	Github 中的 SSH 设置：
	![Git 使用指南-Git 远程仓库-配置公钥连接远程仓库-2](images/Git%20使用指南-Git%20远程仓库-配置公钥连接远程仓库-2.png)
	Gitee 中的 SSH 设置：
	![Git 使用指南-Git 远程仓库-配置公钥连接远程仓库-3](images/Git%20使用指南-Git%20远程仓库-配置公钥连接远程仓库-3.png)
4. 输入以下命令验证是否配置成功(如果是 Gitee，则换成`git@gitee.com`)
	```bash
	ssh -T git@github.com
	```
5. 显示以下内容即为配置成功
	![Git 使用指南-Git 远程仓库-配置公钥连接远程仓库-4](images/Git%20使用指南-Git%20远程仓库-配置公钥连接远程仓库-4.png)
#### 添加远程仓库

1. 进入需要连接远程仓库的本地仓库
2. 通过以下命令添加远程仓库（请将`<name-of-remote>`换成给需要连接的远程仓库起的名字，一般用`origin`，`<SSH>`换成远程仓库的路径）
	```bash
	git remote add <name-of-remote> <SSH>
	```
	例：`git remote add origin git@github.com:Boooooobbb/The-Hitchhiker-s-Guide-to-the-Git.git`
3. 可以通过以下命令查看远程仓库
	```bash
	git remote
	```
	
	![Git 使用指南-Git 远程仓库-添加远程仓库](images/Git%20使用指南-Git%20远程仓库-添加远程仓库.png)

#### 推送本地分支到远程仓库（push）

-  推送本地的`master`分支到远程仓库的`master`分支
	```bash
	git push origin master
	```
- `push`命令的完全体：
	```bash
	git push -f --set-upstream <name-of-remote> <name-of-local-branch>:<name-of-remote-branch>
	```
	- `-f`：当本地推送的修改内容和远程仓库的修改冲突时，强制用本地推送的修改内容覆盖远程仓库
	- `--set-upstream`：将本地分支与远程分支关联
		- ⭐⭐⭐关联之后，使用`git push`即可将本地分支的修改推送到关联的远程分支中
	- `<name-of-remote>`：远程仓库名
	- `<name-of-local-branch>`：本地分支名
	- `:<name-of-remote-branch>`：远端分支名； 当远端分支名与本地分支名相同时，可以省略`: <name-of-remote-branch>`
- 注：可以通过以下命令查看本地分支和远程分支的对应关系
	```bash
	git branch -vv
	```

#### 从远程仓库克隆（clone）

1. 在 Github 或 Gitee 上找到需要克隆的仓库的 URL 
	
	![Git 使用指南-Git 远程仓库-从远程仓库克隆（clone）-1](images/Git%20使用指南-Git%20远程仓库-从远程仓库克隆（clone）-1.png)
	
2. 在 Git Bash 中进入需要存放克隆仓库的目录  
3.  输入以下命令**克隆远程仓库**  （请将 `<URL>` 部分换成需要克隆的仓库的 URL；Github 克隆太慢时，可以将`<URL>`中`https://github.com`部分替换为`https://gitclone.com/github.com`
	```bash
    git clone <URL>
    ```
4. 克隆成功后可在目录下看到克隆到本地的仓库
	
	![Git 使用指南-Git 远程仓库-从远程仓库克隆（clone）-2](images/Git%20使用指南-Git%20远程仓库-从远程仓库克隆（clone）-2.png)

#### 从远程仓库抓取（fetch）和拉取（pull）

- 将远程仓库中的所有更新抓取到本地，**不会进行合并（merge）**
	```bash
	git fetch 
	```
- 将远程仓库中的更新抓取到本地，**并合并（merge）当前所在的分支**
	```bash
	git pull 
	```
- 当`pull`发生冲突时，解决方法与[合并分支发生冲突时的解决方法](#^quote-of-conflict)相同