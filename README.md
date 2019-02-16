# 如何在[RIME](https://rime.im/)中使用哲哲豆音形输入法

RIME是一个通用的输入法引擎，它支持几乎所有的常见平台：
- 在Windows上是小狼毫
- 在MAC上是鼠须管
- 在Linux上是ibus-rime或者fcitx-rime
- 在手机安卓平台上是同文输入法
- 在IOS（苹果手机）上是iRIME

因为是一个通用输入法引擎，所以我们可以使用一份配置来支持所有这些引擎。

这个文档就是如何在RIME中支持[哲哲豆音形输入法](http://zzdzzd.ys168.com/)。

## 哲哲豆音形输入法

[哲哲豆音形输入法](http://zzdzzd.ys168.com/)分为两个版本：
1. 圆满版：词组较多，适合初学者。
2. 快版：词组较少，所以重码率低，适合打单字为主的高手。

## 自定义方法
自造词可以放在`zzdyx_userdict.txt`中。

如果想关闭拼音混输，那么在对应的schema.yaml文件里（哲哲豆圆满版是`zzdyx_perfect.schema.yaml`，哲哲豆快版是`zzdyx_mofast.schema.yaml`），把下面一段代码前加`#`注释掉就好。
```
abc_segmentor:
  extra_tags:
    - reverse_lookup
```

## 安装方法
本输入法的编码反查和拼音混输功能依赖于

 - [袖珍简化字拼音](https://github.com/rime/rime-pinyin-simp) **`pinyin-simp`**

所以在安装哲哲豆音形时，同时需要安装`pinyin-simp`输入法。

安装步骤：
1. 安装 [東風破](https://github.com/rime/plum) 。
2. 使用 [東風破](https://github.com/rime/plum) 安装哲哲豆音形。
3. 修改Rime的配置增加哲哲豆音形选项。
4. 重新部署RIME，以生效。

### 安装[東風破](https://github.com/rime/plum) 
具体安装方法见[東風破](https://github.com/rime/plum) 官方网站。

简单来说，Linux/Mac上使用下列命令安装：
```
curl -fsSL https://git.io/rime-install | bash
```

Windows上用家可以通過 小狼毫 0.11 以上「輸入法設定／獲取更多輸入方案」調用配置管理器或者[東風破](https://github.com/rime/plum) 官方网站列出的其他安装方法。

### 安装哲哲豆音形
在Linux、MAC上使用以下命令安装：
```
./rime-install pinyin-simp whjiang/zzdyx_rime
```

其中, rime-install是[東風破](https://github.com/rime/plum) 的命令。在Windows上，请替换为相应的命令。

安装 [袖珍简化字拼音](https://github.com/rime/rime-pinyin-simp) 。安裝命令： 
```
bash rime-install pinyin-simp
```

### 修改Rime的配置增加哲哲豆音形选项
然后在`~/Library/Rime`创建一个`default.custom.yaml`文件。文件内容如下：
```yaml
patch:
  schema_list:
    - {schema: zzdyx_perfect} #哲哲豆音形圆满版
    - {schema: zzdyx_mofast}  #哲哲豆音形快版
```

###  重新部署RIME
然后，在RIME菜单中选择“同步用户数据”和“重新部署”。就可以使用了。


### 如何在手机（安卓/苹果）上使用
安卓上请使用同文输入法，IOS上请使用iRIME输入法。因作者只有IOS手机，所以只测试了iRIME。

因为iRIME没有编译bin文件的功能，所以必须先用上面的安装方法在电脑上安装一遍，生成出
- zzdyx*.bin
- pinyin_simp*.bin

把这些文件连同`zzdyx_perfect.schema.yaml`、`zzdyx_mofast.schema.yaml`和`pinyin_simp.schema.yaml`一起传到手机上（通过iRIME的“电脑快传”功能）。再像上面一样修改iRIME的`default.custom.yaml`就可以了。
