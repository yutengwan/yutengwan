---
layout : post
title : svn status的各种状态的说明
---

### svn status:

**U:** working file was uploaded,工作目录更新

**G:** Changes on the repo were automatically merged into the working copy，版本自动merge上去

**M:** Working copy is modify,文件修改

**C:** The file conflicts with the version in the repo文件在版本库中冲突

**?:** The file is not under version control 文件不在版本库中

**!:** The file is under version control but is missing or incomplete 文件在版本库中，但是没有使用svn删除或不完整

**A:** The file will be added to version control(after commit)新增文件

**A+:** The file will be moved (after commit)

**D:**  The file will be deleted (after commit)文件被移除版本库

**S:**  This signifies that the file or directory has been switched from the path of the rest of the working copy (using svn switch) to a branch

**I:** Ignored

**R:** Item has been replaced in your working copy. This means the file was scheduled for deletion, and then a new file with the same name was scheduled for addition in its place.