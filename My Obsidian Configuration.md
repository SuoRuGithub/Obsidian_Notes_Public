# **设置vim键位**
下载Vimrc Support插件
然后就可以创建一个`.obsidian.vimrc`文件来配置vim啦。
目前我的配置还很简单，只是改了一下normal模式的进入方式，以及转到行首行尾的方式罢了。
```bash
// normal模式下，H回到行首，L转到行尾
nmap H ^
nmap L $
// insert模式下，jj转到normal模式
imap jj <Esc>
```

# 同步
由于我的电脑是双系统，所以我希望设置同步，具体做法是使用Git这个插件。
需要注意的是需要在Custom git binary这个设置底下加上本地的git路径，如果你不知道，可以使用：（windows）
```powershell
where git
```
来查找。注意！路径一定是`git.exe`的路径，`/bin`路径不可以。


zotero