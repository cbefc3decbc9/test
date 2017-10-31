一、设置ssh链接

1、检查本机是否有ssh key设置    
  $ cd \~/.ssh 或cd .ssh 
  如果没有则提示： No such file or directory  
  如果有则进入~/.ssh路径下（ls查看当前路径文件，rm * 删除所有文件）  
    
2、使用Git Bash生成新的ssh key。    
$ cd ~  #保证当前路径在”~”下  
$ ssh-keygen -t rsa -C "xxxxxx@yy.com"  #建议填写自己真实有效的邮箱地址  
Your identification has been saved in /c/Users/xxxx_000/.ssh/id_rsa.   #生成的密钥  
Your public key has been saved in /c/Users/xxxx_000/.ssh/id_rsa.pub.  #生成的公钥  
*本机已完成ssh key设置，其存放路径为：c:/Users/xxxx_000/.ssh/下。  
注释：可生成ssh key自定义名称的密钥，默认id_rsa。   
$ ssh-keygen -t rsa -C "邮箱地址" -f ~/.ssh/githug_blog_keys #生成ssh key的名称为githug_blog_keys，慎用容易出现其它异常。  
    
3、添加ssh key到GItHub   
1) 进入c:/Users/xxxx_000/.ssh/目录下，打开id_rsa.pub文件，全选复制公钥内容。   
2) Title自定义，将公钥粘贴到GitHub中Add an SSH key的key输入框，最后“Add Key”。   

4、配置账户   
$ git config --global user.name “your_username”  #设置用户名   
$ git config --global user.email “your_registered_github_Email”   

5、测试ssh keys是否设置成功。   
$ ssh -T git@github.com    
然后输入yes    
Warning: Permanently added 'github.com,192.30.252.129' (RSA) to the list of known hosts.    
Enter passphrase for key '/c/Users/xxxx_000/.ssh/id_rsa':  
#生成ssh kye是密码为空则无此项，若设置有密码则有此项且，输入生成ssh key时设置的密码即可。    
Hi xxx! You've successfully authenticated, but GitHub does not provide shell access. #出现词句话，说明设置成功。    

二、本地项目通过SSH push到GitHub       
1、在github上创建一个示例仓库，如：test。  
2、复制test的ssh路径。     
3、本地创建项目 
1) 创建目录
$ mkdir test
$ cd test
2) 初始化
$ git init
3) 创建hello.md文件
$ echo "这是一次测试test ssh key" > hello.md
4) 提交到本地
若出现如上warning提示则重新提交一次即可。
$ git add .   #提交当前目录下所以文件
$ git commit -m "add hello.md"   #提交记录说明 
5) 提交到github
$ git remote add origin ‘粘贴复制test ssh key的ssh路径’  #
$ git push -u origin master
Enter passphrase for key '/c/Users/hgpin_000/.ssh/id_rsa':  #ssh key设置密码故此需要输入密码      
       
再次使用是只需要执行 add commit push即可！

三、可能的错误：     
在最后一步push时出错。。显示提交不了。。    
原因：     
在github上面创建仓库时。。创建了README.md。。而本地文件中没有。。需要pull下来。。    
执行此行代码：git pull --rebase origin master    
然后继续git push -u origin master     
