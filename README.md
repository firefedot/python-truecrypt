#!/usr/bin/env python3
# -*- coding: utf -*-
import os
import sys
__author__ = "firefedot"
__date__ = "$12.09.2015 23:53:49$"

mnt=os.environ['HOME']+'/true_new'
user=os.environ['USER']
tcppath="/run/media/firefedot/newraz2/"
key=tcppath+'key.txt'
tcp=tcppath+'tcpfile'

def err():
    print ("Введите верно параметр")
    print ("-d или --dismount для отключения тома")
    print ("-m  или --mount для монтирования тома")
    sys.exit(0)

if __name__ == "__main__":
    print ("Начинаем монтировать том")
    if len (sys.argv) > 1:
        print ("Выбран параметр {}".format (sys.argv[1] ) )
        if (sys.argv[1]) == "-m" or (sys.argv[1]) == "--mount":
            print ("Монитрование")
            if os.path.exists(mnt):
                print ("Папка уже создана")
            else:
                print ("Папка будет создана")
                os.makedirs(mnt)
                os.system('sudo chown '+user+":"+user+' '+mnt)
            try:
                os.system('sudo truecrypt --keyfiles='+key+' --mount '+tcp+' '+mnt)
            except:
                print ("error")
        elif (sys.argv[1]) == "-d" or (sys.argv[1]) == "--dismount":
            print ("Размонтирование")
            os.system('sudo truecrypt -d '+tcp)
        else:
            err()
    else:
        err()
