# CH Extractor

## 简介
由于 Windows 的中文编码是GBK，因此在 Linux 以及 macOS 等这类使用 UTF-8 编码的平台上，解压 Windows 压缩的中文密码压缩包非常不便，而该Shell脚本可以解决这个问题。

脚本默认使用 7z 软件包的命令作为解压命令，但你也可以自定义要使用的解压工具。

除了 GBK 编码以外，你还可以自定义原密码编码格式。

## 使用
* 下载脚本到 `/usr/local/bin` 以便在任何位置执行。你可以选用下面两个命令之一来下载
```
curl https://raw.githubusercontent.com/Ljzd-PRO/CH-Extractor/main/chextract -o chextract && mv chextract /usr/local/bin/
```

```
wget https://raw.githubusercontent.com/Ljzd-PRO/CH-Extractor/main/chextract && mv chextract /usr/local/bin/
```

* 使用脚本
```
脚本使用方法:
    chextract <密码> <压缩文件目录> [选项]

选项:
    -c "<命令>":  自定义解压命令 格式如下:
        %1   代指密码
        %2   代指压缩文件目录
        例如:
            -c "7z x -p%1 %2" (默认)
            -c "unzip -P %1 %2"
            
    -e <编码>:  密码的编码格式
        例如:
            -e gbk (为默认值 适用于Windows下的中文密码)
```

## 使用样例
* 按照默认配置解压密码为 `新年快乐` 的 `./documents.7z` 压缩包
```
chextract 新年快乐 ./documents.7z
```

* 使用 7zz 解压密码为 `新年快乐` 的 `./documents.rar` 压缩包 (macOS上名字叫7zz)
```
chextract 新年快乐 ./documents.7z -c "7zz x -p%1 %2"
```

* 解压密码为 `新年快乐` 的 `./documents.rar` 压缩包，其密码是 Unicode 编码下的中文
```
chextract 新年快乐 ./documents.7z -e unicode
```

* 获取使用帮助
```
chextract
```

## 额外说明
* 有的解压工具是支持非 UTF-8 中文密码解压的，不需要使用该脚本，使用了反而会解压失败。  
例如 Linux 的 unrar ，或 macOS 下的App [Keka](https://www.keka.io/en/)
