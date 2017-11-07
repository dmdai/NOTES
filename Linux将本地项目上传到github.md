---
title: Linux将本地项目上传到github
tags: github
grammar_cjkRuby: true
---



### 主要有以下几个步骤：  

- #### 登录github，新建一个项目new repository  

- #### 把当前目录变成git可以管理的仓库
  确认当前目录是自己的项目工程目录，在终端输入
`git init`
此时终端会显示“初始化空的Git仓库于/......git”
 
- #### 添加所有需要上传的文件和配置到git
  `git add FILE`添加确定的文件FILE
`git add . `添加当前目录下所有文件
 
- #### 查看当前提交状态
  `git status` 显示当前所有提交的状态
  ![git status][1]
  >> 可以看出当前的信息就是在master分支上，“初始提交”即表明初始化了commit命令，等待提交
  >>
  同样，我们也可以在这个时候选择删除不需要git的文件，在终端输入
`git rm FILE --cached(保留本地)`
`git rm FILE -f(强行删除)`
 
- #### 提交文件
  `git commit -m ’log message‘`
  ![git commit -m "log message"][2]
  >> 上述命令**必须添加**‘-m’及‘log message’，其中log message可以自己随便填写，否则是提交不成功的，在后面的**push操作**中会提示错误：“error:src refspec master does not match any”

至此，我们就已经**提交文件到本地仓库**了！
现在我们需要将上述本地仓库里的文件**添加到远程库**！

- #### 在github里添加origin
  `git remote add origin https://github.com/***.git` 
  >> 如果之前配置过一次，再次配置则会提示以下错误：
**ERROR**：远程 origin 已经存在。
说明远程仓库已经存在该origin，此时就如果我们需要将远程配置删除，再重新添加：
**`git remote rm origin`
`git remote add origin https://github.com/***.git`**
再次提交文件即可正常使用

- #### 上传文件
  `git push -u origin master`
执行此命令后，git会提示输入github账户的用户名和密码，验证通过后，进行文件上传！

### push常见问题及解决方案：
> **ERROR**：向github仓库推送时(Git push originmaster)，出现**当前分支 master 没有对应的上游分支**的错误。
**解决**：推送当前分支并建立与远程上游的跟踪
   `git push --set-upstream origin master`    


>  **ERROR**：更新被拒绝，因为远程版本库包含您本地尚不存在的提交。这通常是因为另外一个版本库已向该引用进行了推送。再次推送前，您可能需要先整合远程变更（如 'git pull...'）。详见 'git push -- help' 中的 'Note about fast-forwards'小节。
**解决：**`git push -u origin +master`
强制推送，但这样会删除github仓库中之前有的文件！

> **ERROR**：如果git没有commit就执行push操作会出现以下错误，"unable to access https://github.com/**.git/: Empty reply from server"
**解决**：只需要先commit 在 push即可



 
 


  [1]: ./images/2017-11-07%2011-10-20%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE.png "2017-11-07 11-10-20屏幕截图"
  [2]: ./images/1510024928732.jpg