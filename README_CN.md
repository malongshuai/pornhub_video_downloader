# pornhub_video_downloader

pornhub视频下载和解析工具。

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
Usage: gethub [options] [PORNHUB_PAGE_URL]

Specific options:
    -h, --page-url URL               Pornhub Page URL
    -p, --proxy PROXY                http proxy
                                     (if missing, will try env variables)
    -q, --quality QUALITY            which quality to download/parse, value like: 480/720/1080/

Download options:
    -o, --output PATH                download file path
                                     if missing, will use video title as filename
    -t, --type TYPE                  which type(mp4 or hls) to download, default: hls
                                     if hls, ts files will merge to mp4
    -d, --delete                     delete tmp ts files after download
                                     (only valid with `-t hls')

Parse options:
    -P, --parse                      don't download, only parse the url
                                     list a few of ts url, use -T to list all
    -T, --ts-list                    used with -P, display all ts urls
    -L, --ts-list-only               used with -P, only display all ts urls

Common options:
    -D, --debug                      debug
    -V, --version                    show version info
        --help                       print this help message

Note:
1. Be sure `aria2' and `ffmpeg' are installed, e.g. `sudo apt install aria2'
2. If download mp4 format(`-t mp4'), may be it is not the highest quality one
3. If download hls format(`-t hls'), it will download the highest quality one,
   but it will save ts files in the same directory, use `-d' to delete this dir,
   or delete by yourself
```

## 一些使用示例

```bash
# 设置代理，-t hls(也是默认行为)表示下载hls格式的ts文件，ts文件片段保存在同目录下的同名子目录，
# 下载完ts文件后会自动合并成mp4文件，指定-d选项表示，合并完成后自动删除保存ts文件片段的目录
gethub -h 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754' -p http://127.0.0.1:8118 -t hls -q 1080 -o new.mp4 -d
# 与上等价
gethub -p http://127.0.0.1:8118 -t hls -q 1080 -o new.mp4 -d 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# 使用环境变量中的代理选项: http_proxy 或 HTTP_PROXY，如果未设置这些变量，将不使用代理
gethub -h 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754' -t hls -o new.mp4

# 不指定-o选项时，mp4文件将保存在当前目录下，并使用pornhub页面标题作为文件名
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# 直接下载mp4格式，这种方式可能会比较慢，下载的视频清晰度可能也不是最高的
gethub -t mp4 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# 不下载，只用来解析给定URL相关的信息
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' --parse -p PROXY
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' --P -T -p PROXY
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' --P -L -p PROXY
```

# 更新

下载或`git clone`最新版本的`pornhub_video_downloader.gem`，然后执行：

```bash
$ gem install ./pornhub_video_downloader.gem
$ gem cleanup pornhub_video_downloader
$ rm -rf ./pornhub_video_downloader.gem
```

# 忠告

小心肾。
