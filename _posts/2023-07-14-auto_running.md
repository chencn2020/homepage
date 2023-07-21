---
title: '服务器自动化运行指令'
date: 2023-07-14
permalink: /posts/2023/07/auto_running/
tags:
  - DL
  - Code Repository
---

- 在服务器上按指令顺序依次运行程序
- 跑多个实验时，不必再蹲点上一个实验结束再开启下一个实验

``` python
# -*- coding:UTF-8 -*-
"""
@author: Zewen Chen
@contact: chencn2018@163.com
@time: 2023/7/14 10:16
@file: auto_running.py
@desc: 自动运行指令工具。挂起后，可直接运行预先设定的指令，把服务器压榨到极致，方便跑实验

注意事项：
    挂起时，建议使用如下指令(auto_running.pid表示auto_running.py线程的PID保留位置)：
        nohup python3 -u auto_running.py > autu_running.log  2>&1 & echo $! > auto_running.pid

    如果挂起后，发现预先设定的指令有问题，需要按下面顺序进行：
        1. 先查看auto_running.pid中保留的PID，输入 kill -s 9 PID先将本线程kill
        2. 再去save_path保留的PID中，查询运行的指令线程PID，输入kill -s 9 PID

    如果要挂起多个auto_running.py，注意修改上面的auto_running.pid和下面的save_path参数，避免出现覆盖
"""

import os
import time
import subprocess

# ---------可调区域---------
wait_time = 180  # 轮询时间，每隔wait_time查询一次指令是否在运行
save_path = 'save_pid.pid'  # 进程PID保留文件（保留当前运行的order的指令，可以用kill -s 9 PID杀死）

'''
    指令区, 为一个list, 按顺序执行
    每一条指令最后必须以&结束，且指令中不能出现额外的&符号
        如: nohup python3 -u train.py & xxx > logs.log & 是不被允许的，因为有两个&
    建议格式: nohup python3 -u train.py --param1 xxx --param2 xxx > xxx.log &
'''

order_list = [
    "nohup python3 -u train_maniqa.py --gpu_id 6 --dataset_name bid  --model WAIQT --loss Norm > ./0714_BID_WAIQT_Norm.log &",
    "nohup python3 -u train_maniqa.py --gpu_id 6 --dataset_name livec  --model WAIQT --loss Norm > ./0714_LIVEC_WAIQT_Norm.log &",
    "nohup python3 -u train_maniqa.py --gpu_id 6 --dataset_name spaq  --model WAIQT --loss Norm > ./0714_SPAQ_WAIQT_Norm.log &",
    "nohup python3 -u train_maniqa.py --gpu_id 6 --dataset_name koniq10k  --model WAIQT --loss Norm > ./0714_Koniq_WAIQT_Norm.log &",
]

# -------以下可以不用调整---------
pid_out_order = f' 2>&1 & echo $! > {save_path}'


def getPid(process):
    cmd = "ps aux| grep '%s'|grep -v grep " % process
    out = subprocess.Popen(cmd, shell=True, stdout=subprocess.PIPE)
    infos = out.stdout.read().splitlines()
    pidlist = []
    if len(infos) >= 1:
        for i in infos:
            pid = i.split()[1]
            if pid not in pidlist:
                pidlist.append(pid)
        return pidlist
    else:
        return -1


for order in order_list:
    order = order.replace('&', pid_out_order)
    print('-----Running Order: %s-----' % order)
    os.system(order)

    PID = open(save_path, 'r').readlines()[0].strip()
    pid = getPid(PID)
    print('\tPID: ', PID)
    while not isinstance(pid, int):
        print('\tThe process is still alive, waiting for %ds' % wait_time)
        time.sleep(wait_time)
        pid = getPid(PID)
    print('\t*****The porcess is completed.*****')


```