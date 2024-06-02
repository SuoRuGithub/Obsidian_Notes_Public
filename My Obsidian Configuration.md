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
