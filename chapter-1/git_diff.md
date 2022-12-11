## 1.2 Git对比差异

-   对比工作区和暂存区的差异

    ```bash
    git diff -- <file> # 比较指定文件的差异
    git diff # 比较所有文件的改动
    ```

-   对比工作区和版本库的差异

    ```bash
    git diff HEAD^ -- <file> # HEAD^表示前一个版本
    git diff HEAD^
    ```

-   对比暂存区和版本库的差异

    ```bash
    git diff --cached HEAD^ -- <file> # --cached表示暂存区，和--staged同效果
    git diff --staged HEAD^
    ```

-   比较本地不同版本库的差异

    ```bash
    git diff HEAD^ HEAD^^ -- <file> # HEAD^^ 表示倒数第三个版本，HEAD~n表示倒数第n个版本
    git diff HEAD^ HEAD~2
    ```
