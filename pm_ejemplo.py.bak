#!/usr/bin/python
# -*- coding: utf-8 -*-

#import os
from collections import namedtuple

MODE_BUSCA = 0
MODE_SUBNET = 1
MODE_GROUP = 2

config_file = "dhcpd.conf"

fp = open(config_file, "r")
lineas = fp.readlines()
fp.close

HostInfo = namedtuple('HostInfo', 'name, ip, mac')
hosts_list = []
mode = MODE_BUSCA
subnet = None
# lista de grupos que contendra una lista de host
grupos = []
g = 0  #contador de grupos
s = 0  #contador de subnets
h = 0
for line in lineas:
    host_info = None
    hosts_list = []
    line = line.strip()
    if mode == MODE_BUSCA:
#Pasa por todas las líneas hasta que encuentra una declaracion de subnet o host
        parts = line.split()
        if line.startswith("subnet"):
            subnet = {}
            subnet["network"] = parts[1]
            mode = MODE_SUBNET
            s += 1
            continue
        elif line.startswith("group"):
            mode = MODE_GROUP
            g += 1
            continue
        elif line.startswith("host"):
            #print "host sin ubicar:"
            #print parts[1]
            #print parts[5].strip(";")
            #print parts[7].strip(";")
            name, ip, mac = parts[1], parts[5].strip(";"), parts[7].strip(";")
            host_info = HostInfo(name, ip, mac)
            hosts_list.append(host_info)
            grupos.append(hosts_list)
            h += 1
            continue
    elif mode == MODE_SUBNET:
        parts = line.split()
        if line.strip().startswith("}"):
            mode = MODE_BUSCA
            continue
        elif line.startswith("host"):
            #print parts[1]
            #print parts[5].strip(";")
            #print parts[7].strip(";")
            name, ip, mac = parts[1], parts[5].strip(";"), parts[7].strip(";")
            host_info = HostInfo(name, ip, mac)
            hosts_list.append(host_info)
            grupos.append(hosts_list)
            h += 1
            continue
        elif line.startswith("group"):
            mode = MODE_GROUP
            g += 1
    elif mode == MODE_GROUP:
        parts = line.split()
        if line.strip().startswith("}"):
            mode = MODE_SUBNET
            continue
        elif line.startswith("host"):
            name, ip, mac = parts[1], parts[5].strip(";"), parts[7].strip(";")
            host_info = HostInfo(name, ip, mac)
            hosts_list.append(host_info)
            grupos.append(hosts_list)
            h += 1
            continue
#print grupos
def print_label(titulo, comando):
    print '<item label="etiqueta">'
    print '<action name="Execute">'
    print '<execute>'
    print 'sakura'
    print '</execute>'
    print '</action>'
    print '</item>'

print '<?xml version="1.0" encoding="UTF-8"?>'
print '<openbox_pipe_menu>'
print '<menu id="prueba" label="python">'
#print_label("sakura", "etiqueta")
print '</menu>'
print '</openbox_pipe_menu>'
