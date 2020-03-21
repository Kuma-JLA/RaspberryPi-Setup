# RaspberryPi-Setup



```Shell
#ユーザ"tmp"を作成する
sudo useradd tmp
#tmpをsudoグループに追加
sudo gpasswd -a tmp sudo
#tmpのパスワードを設定
sudo passwd tmp
#ログアウト
exit
```

```Shell
#ホームディレクトリを/home/piから/home/kumaに変更
sudo usermod -d /home/kuma-m kuma


# ログアウト
exit
```

```Shell
#
sudo userdel touryou
#
sudo passwd kuma
#
sudo rm /etc/sudoers.d/010_pi-nopasswd
sudo 
```

```Shell
#
sudo apt-get update
sudo apt-get upgrade
#
sudo apt-get install fonts-note

```
