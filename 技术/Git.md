
## Squash 

***VSCode Terminal***

```bash
git rebase -i HEAD~3
```

报错如下：

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