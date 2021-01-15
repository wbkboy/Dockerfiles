- 更改原steamlink镜像的时区为上海

- 简单使用例子 ，默认entrypoint入口为/bin/sh

  ```
  docker run --rm -it wbkboy/streamlink 
  ```


- 我自己的一个录制容器设置：

  ```shell
  docker run --name ebc51 -v /mnt/ssd/record:/record -it --entrypoint=/record/ebc51.sh wbkboy/streamlink 
  # 挂载主机的/mnt/ssd/record目录到容器的record目录 替换entrypoint入口为/record/ebc51.sh
  ```

  - 这是一个录制`东森ebc51`台每晚10点到12节目`关键时刻`的脚本

    ```Shell
    #!/bin/sh
    videoName="/record/EBC51_"$(date +%Y-%m-%d-%H-%M)".ts"
    url="https://www.youtube.com/watch?v=RaIJ767Bj_M"
    timeout -s SIGINT -t 7500 streamlink -o $videoName $url best             --force-progress
    ```

  - 其中`timeout`作用是在7500秒后结束 streamlink进程。
  - 7500表示7500秒，`SIGINT`表示`Ctrl+C`的截断信号，使进程进行收尾工作。
  - `videoNameb`根据当前时间生成，避免重复。
  - `--force-progress`参数表示没有交互终端tty也显示下载进度

  

  - 计划任务: 设置每晚21.55启动容器ebc51，debian执行`crontab -e`，末尾添加 `55 21 * * * docker start ebc51`
