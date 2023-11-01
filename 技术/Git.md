

## 优雅合并 commit

---
### Revert

**1. soft**  将提交信息回退到指定 commit ，但是代码会被放在暂存区，还是最新的，并没有被删。

```bash
git reset --soft HEAD~n
```

这个时候重新 commit 和 push -f 就行了

```bash
git commit -m'feat: 将几次修改readme的提交合并成一个'
git push -f
```

**2. hard**  这将删除最近的 `n` 个提交以及它们的提交历史，尽量少用。

```bash
git reset --hard HEAD~n
```

**💥一旦强推之后，可能会破坏其他人的本地副本，因此在协作项目中要谨慎使用💥**

---
### Squash (Rebase)

> 这里我们合并 commit 的信息，那么就简单使用 squash 和 reword 。
> 在需要合并的 commit 前 squash ，在 需要修改信息的前面 reword 就行了。

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

- **`pick`**：保留这个提交，不进行任何更改。
- **`reword`**：保留这个提交，修改提交信息。
- **`edit`**：保留这个提交，修改提交信息和提交文件内容。
- **`squash`**：将这个提交与前一个提交合并成一个新的提交，保留最新的信息，不会让你修改信息和内容。
- **`fixup`**：类似于 `squash`，将这个提交与前一个提交合并，但不保留这个提交的提交信息。
- **`drop`**：丢弃这个提交，不包括它在内的所有更改都将被删除。



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

