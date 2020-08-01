更改原steamlink镜像的时区为上海
使用例子 docker run --rm -it wbkboy/streamlink
默认entrypoint为/bin/sh，可以强制替换为自己的脚本：
docker run --rm -v /mnt/ssd/record:/record -it --entrypoint=/record/ebc51.sh wbkboy/streamlink
这个例子为我自己用的 ，意思是挂载主机的/mnt/ssd/record目录到容器的record目录，并执行ebc51.sh脚本。
