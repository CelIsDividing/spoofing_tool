#!/usr/bin/env python
import re
import subprocess
import optparse

def get_arguments():
    parser = optparse.OptionParser()
    parser.add_option("-i", "--interface", dest="interface", help="Interface to change its MAC address")
    parser.add_option("-m", "--mac", dest="new_mac", help="New MAC address")
    (options, arguments) = parser.parse_args()
    if not options.interface:
        parser.error("[-] INCORRECT INTERFACE >> USE --help")
    elif not options.new_mac:
        parser.error("[-] INCORRECT MAC ADDRESS >> USE --help")
    return options

def change_mac (interface, new_mac):
    print("[+] UPDATING MAC FOR [" + interface + "] >> [" + new_mac + "]")
    subprocess.call(["ifconfig", interface, "down"])
    subprocess.call(["ifconfig", interface, "hw", "ether", new_mac])
    subprocess.call(["ifconfig", interface, "up"])

def get_current_mac(interface):
    ifconfig_result = subprocess.check_output(["ifconfig", interface])
    mac_address_search_result = re.search(r"\w\w:\w\w:\w\w:\w\w:\w\w:\w\w", ifconfig_result)

    if mac_address_search_result:
        return mac_address_search_result.group(0)
    else:
        print("[-] READING ERROR MESSAGE")

options = get_arguments()

current_mac = get_current_mac(options.interface)
print("[+] CURRENT MAC >> " + str(current_mac))

change_mac(options.interface, options.new_mac)

current_mac = get_current_mac(options.interface)
if current_mac == options.new_mac:
    print("[+] UPDATED MAC >> " + current_mac)
else:
    print("[-] UPDATE ERROR MESSAGE")
