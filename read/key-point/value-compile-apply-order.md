---
title: glib-compile-schemas 「採用值」順序
nav_order: 2010
has_children: true
parent: 關鍵點
---


# glib-compile-schemas 「採用值」順序


## gschema 放置資料夾

* /usr/share/glib-2.0/schemas


## gschema.xml

``` sh
ls -1 /usr/share/glib-2.0/schemas/*.gschema.xml
```

## gschema.override

``` sh
ls -1 /usr/share/glib-2.0/schemas/*.gschema.override
```


## 編譯指令

執行下面指令

``` sh
sudo glib-compile-schemas /usr/share/glib-2.0/schemas/
```

會產生「`/usr/share/glib-2.0/schemas/gschemas.compiled`」這個檔案。


## 採取值順序

|設定檔 | 採用值順序 |
| --- | --- |
| `/usr/share/glib-2.0/schemas/*.gschema.override` | 先 |
| `/usr/share/glib-2.0/schemas/*.gschema.xml` | 後 |


> 在「`*.gschema.xml`」，是一開始規劃的「預設值」，

> 同一個「Key」，若在「`*.gschema.override`」有設定，則在「glib-compile-schemas」編譯時，

就會採用「`*.gschema.override`」的值，

> 最後儲存在「`/usr/share/glib-2.0/schemas/gschemas.compiled`」這個檔案。


## Manpage

* man 1 [glib-compile-schemas](https://manpages.ubuntu.com/manpages/jammy/en/man1/glib-compile-schemas.1.html)
