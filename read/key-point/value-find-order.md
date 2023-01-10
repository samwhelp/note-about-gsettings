---
title: gsettings 取值查找順序
nav_order: 2010
has_children: true
parent: 關鍵點
---


# gsettings 取值查找順序


> 以下是我做了一些實驗和觀察，所得到的結論，嘗試用我自己的理解描述出來，實際確切的流程，還是要根據程式碼的實作為準

## gsettings write

> 當執行「gsettings write」時，會先在「`/usr/share/glib-2.0/schemas/gschemas.compiled`」這個檔案，先找到「預設值」，

> 當「寫入值」，跟「預設值」不一樣時，

> 就會執行「dconf write」的程序，

> 所以就會根據「dconf profile」的設定，來決定寫入的檔案。

> 也就是根據「`/etc/dconf/profile/user`」的第一行，來決定寫入的檔案。

> 若第一行的設定是「`user-db:user`」，則會寫入「`~/.config/dconf/user`」這個檔案。

> 若第一行的設定是「`service-db:keyfile/user`」，則會寫入「`~/.config/dconf/user.txt`」這個檔案。


## gsettings read

> 當執行「gsettings read」時，會先在「dconf」先找，看看是否有設定，

> 若在「dconf」有設定，則採取「dconf read」得到的「值」。

> 若在「dconf」沒有設定，則會採取在「`/usr/share/glib-2.0/schemas/gschemas.compiled`」這個檔案，「找到的值」。


## gsettings reset

> 會根據「dconf write」寫入的檔案，把該檔案的「設定值」清掉。

> 也就是根據「`/etc/dconf/profile/user`」的第一行，來決定將該檔案的「設定值」清掉。

> 若第一行的設定是「`user-db:user`」，則會將「`~/.config/dconf/user`」這個檔案，儲存的「設定值(包含key)」清掉。

> 若第一行的設定是「`service-db:keyfile/user`」，則會將「`~/.config/dconf/user.txt`」這個檔案，儲存的「設定值(包含key)」清掉。


## Manpage

* man 7 [dconf](https://manpages.ubuntu.com/manpages/jammy/en/man7/dconf.7.html)
* man 1 [dconf](https://manpages.ubuntu.com/manpages/jammy/en/man1/dconf.1.html)
* man 1 [gsettings](https://manpages.ubuntu.com/manpages/jammy/en/man1/gsettings.1.html)


## 相關文章

* [glib-compile-schemas 「採用值」順序](https://samwhelp.github.io/note-about-gsettings/read/key-point/value-compile-apply-order.html)
* [dconf read 「取值」查找順序 ](https://samwhelp.github.io/note-about-dconf/read/key-point/value-find-order.html)

