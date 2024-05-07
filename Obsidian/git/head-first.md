## git log
- 单行显示
`--oneline`
- 简略图显示
`--all --gragh`
- 全局查找文本
`-S [文件名]` 可以提供文件名进行限制
- 每一个具体提交的差异
`-p`
- 突出显示差异中包含单词的所有提交
`-G` 允许正则,只允许S/G其一
- 搜索提交消息
`--grep`



eg:
`git log -p --oneline -S tired --word-diff`



## git diff
用于显示索引和工作目录的文件差异
- 显示行差异
` (file)`
- 显示单词差异
`--word-diff`
- 比较对象数据库与索引的差异
`--cached/--staged`

>![[Pasted image 20240328184013.png]]

## git restore
恢复状态
- 从对象数据库中恢复
`git restore --staged`
- 从索引恢复
`git restore`

## git rm 
删除已经跟踪的文件

## git mv (v1) (v2)
重命名文件,第一个参数为旧文件名,其次为新文件名

## git commit --amend -m " "
重新编辑提交消息

提交的消息类型
`feat:引入一个新特性或者改进使用这个类型`
`fix:修正一个bug`
`docs:描述文档变更`
`chore:变更影响git工具`
`test:增加或者修改测试`

*注意:提交必须有一个干净的工作目录*

## git reset (模式) (版本号/指针引用)
`--hard` 强制撤销到一个提交,将丢失修改,慎用
`--mixed` 将当前提交的内容放在工作目录以及索引
`--soft` 将当前提交的内容放在工作目录


## git clone
`git clone url`
从url克隆仓库
`git clone url ()`

## git branch (分支名)
`-m`用于重命名分支
`-a`用于显示所有分支
`-v`显示详细信息
`-vv`显示非常详细
`-d`删除分支


## git push
推送到远程分支
无上游则会被提醒
`-u/--set-upstream`用于设置上游

## git fetch
从远程仓库获取提交信息
`-p/--prune` 清除本地的远程跟踪分支

## git blame (提交) (文件名)
显示某提交对某文件的修改
只列出文件名

## git config
`--global` 全局配置
`--local` 局部配置
`--unset` 撤销配置
`--list` 列出所有配置
`alias.(别名) (git 命令)`














