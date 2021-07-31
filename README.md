# pornhub_video_downloader

[简体中文](https://github.com/malongshuai/pornhub_video_downloader/blob/main/README_CN.md)

Parse and Download pornhub videos.

# Usage

Note: Windows is not supported.

This tool write in ruby, and use `aria2c` as download tool, use `ffmpeg` to merge ts to mp4. So, install `ruby`, `aria2` and `ffmpeg` first.

```bash
$ sudo apt install ruby aria2 ffmpeg
```

Then, download the gem file `pornhub_video_downloader.gem`, or git clone.

```bash
$ git clone https://github.com/malongshuai/pornhub_video_downloader.git
$ cd pornhub_video_downloader

# if your `gem install` is slow, setting gem source, 
# if you are in China, you can: 
#   gem install ./pornhub_video_downloader.gem -s https://gems.ruby-china.com 
$ gem install ./pornhub_video_downloader.gem
```

After install, download tool `gethub` command and parse tool `parsehub` command are avaliable: 

Note: `gethub` command can also be used for parsing, it's parse results are same as `parsehub`.

```
$ gethub --help
Usage: gethub [options] [PORNHUB_PAGE_URL]

Specific options:
    -h, --page-url URL               Pornhub Page URL
    -p, --proxy PROXY                http proxy
                                     (if missing, will try env variables)

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

```
$ parsehub --help
Usage: parsehub [options] [PORNHUB_PAGE_URL]

Specific options:
    -h, --page-url URL               Pornhub Page URL
    -p, --proxy PROXY                http proxy
                                     (if missing, will try env variables)

Parse options:
    -T, --ts-list                    used with -P, display all ts urls
    -L, --ts-list-only               used with -P, only display all ts urls

Common options:
    -D, --debug                      debug
    -V, --version                    show version info
        --help                       print this help message
```

## examples

```bash
# setting proxy, and download ts files, then merge ts files to mp4, `-d` means remove these ts files after merging.
gethub -h 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754' -p http://127.0.0.1:8118 -t hls -o new.mp4 -d
# or
gethub -p http://127.0.0.1:8118 -t hls -o new.mp4 -d 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# use env proxy variable: http_proxy or HTTP_PROXY, or ignore proxy
gethub -h 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754' -t hls -o new.mp4

# without `-o`, will store mp4 file in current directory, and use page title as filename.
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# download mp4 file directly, this may download the low quality video.
gethub -t mp4 'https://cn.pornhub.com/view_video.php?viewkey=ph60b5d9228a754'

# don't download anything, only parse the video info
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' --parse -p PROXY
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' -P -T -p PROXY
gethub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' -P -L -p PROXY

parsehub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' -p PROXY
parsehub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' -T -p PROXY
parsehub 'https://cn.pornhub.com/view_video.php?viewkey=ph5db706f7bf38e' -L -p PROXY
```

# update

Download or `git clone` the latest version of `pornhub_video_downloader.gem`, then: 

```bash
$ git clone https://github.com/malongshuai/pornhub_video_downloader.git
$ cd pornhub_video_downloader

# or: ./install
$ gem install ./pornhub_video_downloader.gem
$ gem cleanup pornhub_video_downloader
```

# 忠告

小心肾。
