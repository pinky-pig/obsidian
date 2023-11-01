

## 合并 commit
### Squash 

***VSCode Terminal***

```bash
# 开始
git rebase -i HEAD~3

# 中止 `git reabse (--continue | --abort | --skip)`
git checkout main
git fetch
git rebase origin/main
git rebase --abort
```

假如报错如下：

```bash
hint: Waiting for your editor to close the file... "E:\software\Microsoft VS Code\Code.exe" --wait: E:\software\Microsoft VS Code\Code.exe: No such file or directory   
error: There was a problem with the editor '"E:\software\Microsoft VS Code\Code.exe" --wait'.
```

解决方法:

https://stackoverflow.com/questions/52195877/how-can-i-fix-git-commit-error-waiting-for-your-editor-to-close-the-file-wi

```bash
code --version

git config --global core.editor "code --wait"

git rebase -i HEAD~3
```

