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

# Script Created by htr-tech (tahmid.rayat)

# --- FUNCTIONS ---

# Function to run Nmap scans
run_nmap_scan() {
    echo -e "\n[+] Running Nmap scan with options: $1..."
    echo -e "\n########## Nmap Scan: $1 ##########" >> "$OUTPUT_FILE"
    nmap $2 $TARGET_IP >> "$OUTPUT_FILE"
    echo -e "[✔] Nmap scan completed.\n"
}

# Function to run SQLMap
run_sqlmap() {
    echo -e "\n[+] Running SQLMap with options: $1..."
    echo -e "\n########## SQLMap Scan: $1 ##########" >> "$OUTPUT_FILE"
    sqlmap $1 >> "$OUTPUT_FILE"
    echo -e "[✔] SQLMap scan completed.\n"
}

# Function to run a specific attack (Placeholder - Implement these!)
run_attack() {
    echo -e "\n[+] Running attack: $1 (Difficulty: $2)..."
    echo -e "\n########## Attack: $1 (Difficulty: $2) ##########" >> "$OUTPUT_FILE"
    # Implement attack logic here based on $1 (attack name) and $2 (difficulty)
    echo -e "[!] Attack logic not implemented in this example.\n"
    echo -e "[✔] Attack completed.\n"
}

# Function to print ports with clear separation
print_ports() {
    echo -e "\n########## $1 Ports ##########" >> "$OUTPUT_FILE"
    echo -e "$2" >> "$OUTPUT_FILE"
    echo -e "[✔] $1 Ports printed to output file.\n"
}


# --- MAIN SCRIPT ---

# Get the target IP address
if [ -z "$1" ]; then
  read -p "[-] Enter the target IP address or URL (e.g., 192.168.1.100 or http://example.com): " TARGET_IP
else
  TARGET_IP="$1"
fi

# Set up output directory and file
OUTPUT_DIR="attack_results"
mkdir -p "$OUTPUT_DIR"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
OUTPUT_FILE="$OUTPUT_DIR/attack_log_$TIMESTAMP.txt"

echo "[-] Starting Attack Script on $TARGET_IP. Results will be saved in $OUTPUT_FILE"
echo "------------------------------------------------" > "$OUTPUT_FILE"

# --- PORT LISTS ---
COMMON_SERVICES=$(cat <<EOF
Common Services (Web, Email, Database, etc.)
21 – FTP (File Transfer Protocol)
22 – SSH (Secure Shell)
23 – Telnet (Remote login, insecure)
25 – SMTP (Simple Mail Transfer Protocol)
53 – DNS (Domain Name System)
67/68 – DHCP (Dynamic Host Configuration Protocol)
80 – HTTP (Web traffic)
110 – POP3 (Post Office Protocol, email)
111 – RPC (Remote Procedure Call)
123 – NTP (Network Time Protocol)
135 – MSRPC (Microsoft RPC)
137-139 – NetBIOS (Windows file sharing)
143 – IMAP (Email retrieval)
161/162 – SNMP (Network monitoring)
179 – BGP (Routing Protocol)
389 – LDAP (Lightweight Directory Access Protocol)
443 – HTTPS (Secure Web traffic)
445 – SMB (Windows File Sharing)
514 – Syslog (Logging service)
515 – LPD (Line Printer Daemon)
520 – RIP (Routing Information Protocol)
587 – SMTP (Email submission with encryption)
636 – LDAPS (Secure LDAP)
993 – IMAPS (Secure IMAP)
995 – POP3S (Secure POP3)

Network Management & Security Tools
1080 – SOCKS Proxy
1433 – MSSQL (Microsoft SQL Server)
1521 – Oracle Database
1723 – PPTP (VPN Protocol)
2049 – NFS (Network File System)
2181 – Apache Zookeeper
2375/2376 – Docker API (Unsecured/Secured)
2483/2484 – Oracle DB over TCP/SSL
3306 – MySQL Database
3389 – RDP (Remote Desktop Protocol)
3690 – SVN (Apache Subversion)
4000 – ICQ, Some game applications
4045 – NFS Lock Service
5000 – UPnP, Flask, Node.js
5432 – PostgreSQL
5800/5900 – VNC (Remote desktop)
5985/5986 – Windows Remote Management
6379 – Redis Database
8080 – Alternative HTTP Web Server
8443 – Alternative HTTPS Web Server
9000 – PHP-FPM, Play Framework
9200 – Elasticsearch
10000 – Webmin
27017 – MongoDB
49152-65535 – Dynamic/Private Ports
EOF
)
LEGAL_PORTS=$(cat <<EOF
Legal Penetration Testing Ports
2222 – Alternate SSH
6000-6005 – X11 Windows System
7070 – Java RMI
8081 – Alternate Web Services
8888 – Alternate Web Servers
9090 – Alternate Admin Web Panels
9443 – Kubernetes API Secure Port
15672 – RabbitMQ Management
1883 – MQTT (IoT Messaging)
5060/5061 – SIP (Voice over IP) Network Services & Web Traffic

20/21 – FTP (File Transfer Protocol)
22 – SSH (Secure Shell)
23 – Telnet (Insecure Remote Access)
25 – SMTP (Email Sending)
53 – DNS (Domain Name System)
67/68 – DHCP (IP Assignment)
69 – TFTP (Trivial File Transfer)
80 – HTTP (Web Traffic)
110 – POP3 (Email Retrieval)
123 – NTP (Network Time Protocol)
135 – MSRPC (Microsoft RPC)
137-139 – NetBIOS (Windows File Sharing)
143 – IMAP (Email Retrieval)
161/162 – SNMP (Network Monitoring)
179 – BGP (Border Gateway Protocol)
389 – LDAP (Directory Services)
443 – HTTPS (Secure Web Traffic)
445 – SMB (Windows File Sharing)

Database & Cloud Services
1433 – Microsoft SQL Server
1521 – Oracle Database
2049 – NFS (Network File System)
2375/2376 – Docker Remote API
2483/2484 – Oracle DB over TCP/SSL
3306 – MySQL Database
3389 – RDP (Remote Desktop)
3690 – SVN (Subversion)
4000 – ICQ, Flask Servers
5000 – UPnP, Flask, Node.js
5432 – PostgreSQL
5800/5900 – VNC (Remote Desktop)
5985/5986 – Windows Remote Management
6379 – Redis Database
EOF
)
ILLEGAL_PORTS=$(cat <<EOF
Additional Ports for Hacking & Malicious Activities
4444 – Metasploit Default Exploit Listener
1337 – Elite Hacking Port (used in trojans)
6666-6669 – IRC-based botnets (DDoS)
31337 – Elite Backdoor (used in trojans)
9999 – Abyss Trojan
10001 – SCP Hack Tool
10101 – BinText Backdoor
12345/12346 – NetBus Trojan
27374 – Sub7 Trojan
31335 – Trinoo DDoS
54320 – Back Orifice Trojan
22222 – Direct Attack Payload Delivery

Ports Used for Illegal Hacking Activities
5555 – Android Debug Bridge (ADB) Exploits
6000-6005 – X11 Hacking Exploits
3389 – RDP Brute-force Attacks
3306 – MySQL Injection Exploits
1433 – MSSQL Brute-force
1521 – Oracle Database Hacking
1723 – PPTP VPN Hijacking
2049 – NFS Exploits
445 – EternalBlue (SMB Exploits)
139 – NetBIOS Hacking
23 – Telnet Bruteforce & Hijacking
21 – FTP Password Sniffing

Illegal Spyware & Data Theft Ports
7070 – Java RMI Exploits
8081 – Web Admin Exploits
8888 – Proxy Hijacking
9090 – WebAdmin RCE Exploits
9443 – Kubernetes Privilege Escalation
15672 – RabbitMQ Unauthorized Access
1883 – MQTT IoT Device Hijacking
5060/5061 – SIP VoIP Interception
17000-17005 – Blackhole Botnet C2

Common DDoS & Network Attack Ports
19 – Chargen (DDoS Amplification)
53 – DNS Reflection Attacks
67/68 – DHCP Starvation Attacks
161/162 – SNMP Amplification
123 – NTP Reflection Attacks
520 – RIP Route Poisoning
1900 – SSDP DDoS Exploits
5353 – mDNS Reflection Attacks
11211 – Memcached DDoS Attack
EOF
)

# --- MAIN MENU LOOP ---
while true; do
    echo -e "\n[-] Tool Created by htr-tech (tahmid.rayat)"
    echo "1) Nmap"
    echo "2) SQL map"
    echo "3) Run the bad all"
    echo "4) DDos Attack"
    echo "5) Malware all"
    echo "6) Common Services Ports"
    echo "7) Legal Ports Only"
    echo "8) Illegal Ports Only"
    echo "9) Run All The Script"
    echo "10) Just test system"
    echo "00) Exit"
    echo "[::] Select An Attack For Your Victim [::]"
    read -p "[-] Select an option : " OPTION

    case "$OPTION" in
        1)  # Nmap
            echo "[-] Nmap Options:"
            echo "  1) Basic Scan"
            echo "  2) Aggressive Scan"
            echo "  3) Comprehensive Scan"
            read -p "[-] Select an Nmap option: " NMAP_OPTION
            case "$NMAP_OPTION" in
                1) run_nmap_scan "Basic Scan" "-sS -sV -T4 -p-";;  # Adjust ports as needed
                2) run_nmap_scan "Aggressive Scan" "-A";;
                3) run_nmap_scan "Comprehensive Scan" "-p- -sS -sV -sC -A -O --script vuln";;
                *) echo "[-] Invalid Nmap option.";;
            esac
            ;;
        2)  # SQL map
            echo "[-] SQLMap Options:"
            echo "  1) Easy (Detect)"
            echo "  2) Normal (More aggressive)"
            echo "  3) Hard (All tests)"
            read -p "[-] Select an SQLMap option: " SQLMAP_OPTION
            case "$SQLMAP_OPTION" in
                1) run_sqlmap "-u '$TARGET_IP' --batch --level 2 --risk 1";;
                2) run_sqlmap "-u '$TARGET_IP' --batch --level 3 --risk 2";;
                3) run_sqlmap "-u '$TARGET_IP' --batch --level 5 --risk 3";;
                *) echo "[-] Invalid SQLMap option.";;
            esac
            ;;
        3)  # Run the bad all
            echo "[-] Running 'Run the bad all' (Easy, Normal, Hard)..."
            run_attack "Run the bad all - Easy" "easy"
            run_attack "Run the bad all - Normal" "normal"
            run_attack "Run the bad all - Hard" "hard"
            ;;
        4)  # DDos Attack
            echo "[-] DDos Attack Options:"
            echo "  1) Easy (Low intensity)"
            echo "  2) Normal (Medium intensity)"
            echo "  3) Hard (High intensity)"
            read -p "[-] Select a DDoS option: " DDOS_OPTION
            case "$DDOS_OPTION" in
                1) run_attack "DDOS - Easy" "easy";;
                2) run_attack "DDOS - Normal" "normal";;
                3) run_attack "DDOS - Hard" "hard";;
                *) echo "[-] Invalid DDoS option.";;
            esac
            ;;
        5)  # Malware all
            echo "[-] Running 'Malware all' (Easy, Normal, Hard)..."
            run_attack "Malware all - Easy" "easy"
            run_attack "Malware all - Normal" "normal"
            run_attack "Malware all - Hard" "hard"
            ;;
        6)  # Common Services Ports
            print_ports "Common Services" "$COMMON_SERVICES"
            ;;
        7)  # Legal ports only
            print_ports "Legal" "$LEGAL_PORTS"
            ;;
        8)  # Illegal ports only
            print_ports "Illegal" "$ILLEGAL_PORTS"
            ;;
        9)  # Run All The Script
            echo "[-] Running all scans and attacks (Easy)..."
            # Nmap
            run_nmap_scan "Basic Scan" "-sS -sV -T4 -p-"
            # SQLMap
            run_sqlmap "-u '$TARGET_IP' --batch --level 2 --risk 1"
            # Attacks (Easy)
            run_attack "Run the bad all - Easy" "easy"
            run_attack "DDOS - Easy" "easy"
            run_attack "Malware all - Easy" "easy"

            # Legal and Illegal ports
            print_ports "Common Services" "$COMMON_SERVICES"
            print_ports "Legal" "$LEGAL_PORTS"
            print_ports "Illegal" "$ILLEGAL_PORTS"
            ;;
        10) # Just test system
            echo "[-] Testing the System..."
            echo "Testing completed successfully." >> "$OUTPUT_FILE"
            ;;
        00) # Exit
            echo "[-] Exiting the script."
            exit 0
            ;;
        *)  # Invalid option
            echo "[-] Invalid option. Please try again."
            ;;
    esac
done
