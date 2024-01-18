![](https://raw.githubusercontent.com/filebrowser/logo/master/banner.png)

# Technical notes

https://github.com/filebrowser

##### Create volume public

```
docker volume create public
```

##### Start docker container

```
docker compose up -d filebrowser
```

### API documentation

https://documenter.getpostman.com/view/141130/2s9YRGx8zB

### ISSUES

##### Api

https://github.com/filebrowser/filebrowser/issues/2551

##### The cpu rise continuously

https://github.com/filebrowser/filebrowser/issues/1985

> Try disabling healthcheck for your container

> ```
> services:
>   filebrowser:
>     image: filebrowser/filebrowser
>     ...
>     healthcheck:
>       disable: true
> ```

##### Using Filebrowser on an RCLON Mount results in "Something really went wrong." with Folders that have numerous Files in them

https://github.com/filebrowser/filebrowser/issues/1836

> Enabling `--disable-type-detection-by-header` With it it displays the files without problem.
> This is true for general files, one folder with 2k txt files loads instantly, a folder with 600 video files won't, even with all disable flags of filebrowser

> Use the following command to run the filebrowser:
> `/filebrowser/filebrowser -d /filebrowser/filebrowser.db --disable-preview-resize --disable-type-detection-by-header --cache-dir /filebrowser/cache`
>
> It will be as fast as "ls" command in Linux, no matter how large the folder is.

```
#/etc/filebrowser.json
{
"port": 8080,
"baseURL": "",
"address": "x.x.x.x",
"log": "stdout",
"database": "/etc/filebrowser.db",
"root": "/u01/camera"
}
#/etc/systemd/system/filebrowser.service
[Unit]
Description=File Browser
After=network.target
[Service]
ExecStart=/usr/local/bin/filebrowser -c /etc/filebrowser.json --disable-preview-resize --disable-type-detection-by-header --cache-dir /u01/cache
[Install]
WantedBy=multi-user.target
```
