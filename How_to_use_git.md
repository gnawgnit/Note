# git使用



- git add（将工作区文件添加到Idex）
- git commit (-m "descripe")（将Idex中的内容提交到版本控制仓库）
- git push ([-u] origin(name) master(branch))（将仓库中的版本推送到远程仓库）
- git pull (origin master | url)
- git remote add origin url（添加名叫origin（默认名）的远程仓库地址）
- git remote -rm origin（删除名叫origin的远程仓库地址）
- git diff （比较工作目录和索引目录之间的不同，但是不会比较新建的文件/目录，也就是说只是跟踪内容，和文件名无关）
- git diff --cached （比较索引目录和最后一次commit的不同，若有新文件/目录，会有说明）
- git clean （把工作目录中未跟踪的文件清除）