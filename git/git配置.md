## 全局配置

```bash
git config --list --show-origin # 查看配置
git config --global user.name '你的名字'
git config --global user.email '你的邮箱'
```



### Github 生成密钥

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" # 生成密钥
touch ~/.ssh/config # 生成配置文件
```

将以下代码添加到 config 文件

```
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```





参考链接：

[Github 生成新的密钥](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

`