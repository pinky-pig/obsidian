## 从 GitHub 模板 template 引用项目开发后，再次合并模板的最新代码到新分支上

要从现有的 `master` 分支创建新分支并将模板的内容合并到新分支中，可以按照以下步骤操作：

1. 确保您的本地主分支是最新的，使用以下命令拉取更新并切换到主分支：
    
    git checkout master  
    git pull origin master
    
2. 创建并切换到新分支：
    
    git checkout -b new_branch
    
3. 添加模板项目作为远程源，并拉取它：
    
    git remote add template https://github.com/antfu/vitesse-nuxt3.git  
    git fetch template
    
4. 将模板分支合并到新分支中：
    
    git merge template/main --allow-unrelated-histories
    
    如果有冲突需要解决，按照提示进行。
    
5. 推送新分支到远程：
    
    git push origin new_branch
    

现在，您已经成功地创建了一个新分支，并将模板项目合并到其中。您可以继续开发这个新分支，而不会影响现有代码。