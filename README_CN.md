# pornhub_video_downloader

pornhub视频下载工具。

# 用法描述

注意：不支持Windows。

工具是用Ruby写的，内部调用`aria2c`作为下载工具，调用`ffmpeg`作为视频合并工具，因此，需要先安装`ruby`、`aria2`和`ffmpeg`。

```bash
$ sudo apt install ruby aria2 ffmpeg
```

然后克隆，或单独下载`pornhub_video_downloader.gem`。

```bash
$ git clone https://github.com/malongshuai/pornhub_video_downloader.git
$ cd pornhub_video_downloader

# 如果下面的`gem install`很慢，修改gem源，例如： 
#   gem sources --add https://gems.ruby-china.com --remove https://rubygems.org/
$ gem install ./pornhub_video_downloader.gem
```

安装之后，就可以使用`gethub`命令用来下载视频。

```bash
$ gethub --help
Usage: gethub [options] [PAGE_URL]

Specific options:
    -h, --page-url URL               Pornhub Page URL
    -o, --output PATH                download file path
                                     if missing, will use video title as filename
    -p, --proxy PROXY                http proxy
                                     (if missing, will try env variables)
    -t, --type TYPE                  which type(mp4 or hls) to download, default: hls
                                     if hls, ts files will merge to mp4
    -d, --delete                     delete tmp ts files after download
                                     (only valid with `-t hls')
        --debug                      debug

Common options:
        --help                       print this help message
        --version                    show version info

Note:
1. Be sure `aria2' had installed, e.g. `sudo apt install aria2'
2. If download mp4 format(`-t mp4'), may be it is not the highest quality one
3. If download hls format(`-t hls'), it will download the highest quality one,
   but it will save ts files in the same directory, use `-d' to delete this dir,
   or delete by yourself
```

## 下载pornhub视频的一些示例

```bash
# 设置代理，-t hls(也是默认行为)表示下载hls格式的ts文件，ts文件片段保存在同目录下的同名子目录，
# 下载完ts文件后会自动合并成mp4文件，指定-d选项表示，合并完成后自动删除保存ts文件片段的目录
gethub -h 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754' -p http://127.0.0.1:8118 -t hls -o new.mp4 -d
# 与上等价
gethub -p http://127.0.0.1:8118 -t hls -o new.mp4 -d 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# 使用环境变量中的代理选项: http_proxy 或 HTTP_PROXY，如果未设置这些变量，将不使用代理
gethub -h 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754' -t hls -o new.mp4

# 不指定-o选项时，mp4文件将保存在当前目录下，并使用pornhub页面标题作为文件名
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# 直接下载mp4格式，这种方式可能会比较慢，下载的视频清晰度可能也不是最高的
gethub -t mp4 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'
```

# 忠告

小心肾.
