## 1.3 SVN库迁移至Git

1.   建立SVN用户到Git用户的映射

     ```bash
     svn log -q # 查看提交记录，获取用户名
     # user_info.txt 从SVN到Git的用户信息映射
     user1 = user1 <user1@user1@corporation.com>
     user2 = user2 <user2@user2@corporation.com>
     ...
     userN = userN <userN@userN@corporation.com>
     ```

2.    SVN与Git的结构关系

      -   /trunk: 开发主线，相当于Git的Master分支

      -   /branches: 支线副本，相当于Git的其它分支

      -   /tags：标签，相当于Git的标签

3. 克隆SVN仓库到Git

    ```bash
    # 创建Git仓库目录
    mkdir git_repo
    # 克隆SVN仓库并转换为Git仓
    git svn clone 	SVN_repo_url --stdlayout \
    				--authors-file=userinfo.txt \
    				git_repo
    ```

4.   ignore文件转换

     ```bash
     # convert svn:ignore into .gitignore
     git svn show-ignore > .gitignore
     ```

     