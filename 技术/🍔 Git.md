---

---
---
### Revert

**🌸创建一个新的提交来撤销先前的提交，而不是直接删除或修改历史提交🌸**

- 查找 hash
```bash
git log
```
- 创建一个新的提交以撤销指定提交的更改
```bash
# commit 为上面查到的 hash，例如： git revert abc123
git revert <commit>
```
- 提交
```bash
git push
```

---
## 优雅合并 commit

---
### Reset

> 最后一步操作是 `git push -f`

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

**💥撤销提交会永久删除提交历史，请确保你真的想要执行这个操作，因为它可能会导致数据丢失。一旦强推之后，可能会破坏其他人的本地副本，因此在协作项目中要谨慎使用💥**

---
### Rebase

> 合并用 Squash ，修改提交信息用 reword 。 可以同时使用。
> edit 没搞懂怎么能修改文件内容。


> 最后一步操作是 `git push -f`

**核心**

- `git rebase -i HEAD~3` 
- 合并: `squash` ，重命名: `reword` 
- `START REBASE` 
- 顶多 Squash 多一步提交，点击就行了。这步提交不能修改提交信息。
- 如果是 reword 就会提示修改提交信息，修改完关闭文件就行。
- `git push -f`

同时使用

- `START REBASE` 
- 修改 reword 的提交信息
- 修改合并后的提交信息
- `git push -f`

*VSCode Terminal*

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

