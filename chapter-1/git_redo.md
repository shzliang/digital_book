## 1.1 Git撤销操作

*   尚未git add的

    ```bash
    git checkout -- <file> #撤销指定文件
    git checkout . #撤销所有文件
    ```

*   已经git add，但未commit的

    * \--mixed模式(默认)

    ```bash
    # 仅撤销add操作，保留修改内容在工作区
    git reset --mixed HEAD -- <file>
    git reset --mixed HEAD .
    
    # 一步到位，撤销add并丢弃修改内容
    git reset --hard HEAD
    ```

*   已经commit的

    * \--soft模式

    ```bash
    # 仅撤销commit操作，stage区仍保留修改的内容
    git reset --soft HEAD^ -- <file>
    git reset --soft HEAD^ .
    ```

    * \--hard模式

    ```bash
    # 之间回退到前一个版本，当前版本的修改全部被清除
    git reset --hard HEAD^
    ```
