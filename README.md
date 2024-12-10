# Network Traffic Analysis with TCPDump: Capturing, Filtering, and Displaying Packets

This project demonstrates the use of `tcpdump` to analyze network traffic from a `.pcap` file. Each step involves capturing, filtering, and extracting insights from network data. Let's dive into the steps! 🚀

---

## Steps:

### Step 1: Counting ICMP Packets
To determine how many ICMP packets are in `traffic.pcap`, I used the following command:

```bash
sudo tcpdump -r traffic.pcap icmp
```

![See the output](https://github.com/user-attachments/assets/36035685-0e61-4592-85d1-4dda2b900323)

The output provided too much information, so I used a word count filter to simplify the result:

```bash
sudo tcpdump -r traffic.pcap icmp | wc
```

![Filtered output](https://github.com/user-attachments/assets/c38801bf-cfd8-4cf5-8631-0ccf6faa41fd)

Result: The file contains **26 ICMP packets**.

---

### Step 2: Finding the IP Address Requesting a MAC Address
Next, I identified the IP address requesting the MAC address for `192.168.124.137` using the ARP protocol:

```bash
sudo tcpdump -r traffic.pcap arp
```

![ARP output](https://github.com/user-attachments/assets/3e679476-1cf9-46d8-88ec-7e406c0b1f08)

The IP address was identified. To improve readability, I removed dashes using the `-nn` option:

```bash
sudo tcpdump -r traffic.pcap arp -nn
```

![Filtered ARP output](https://github.com/user-attachments/assets/745ea3b5-16e3-49d8-bbf4-a172639fec24)

---

### Step 3: Identifying the First DNS Query
I filtered DNS queries using port 53 to find the hostname (subdomain) in the first query:

```bash
sudo tcpdump -r traffic.pcap port 53
```

![DNS query output](https://github.com/user-attachments/assets/19c9998d-06da-4d63-a657-70c41e82b129)

The first DNS query that popped up was `mirrors.rockylinux.org`.

![DNS hostname](https://github.com/user-attachments/assets/2bc6f7f2-3afe-4d0c-b0e7-bf2e2a9dc9ac)

---

### Step 4: Finding TCP Reset (RST) Packets
I then checked how many packets had only the TCP Reset (RST) flag set. The following command was used:

```bash
sudo tcpdump -r traffic.pcap 'tcp[tcpflags] & tcp-rst != 0'
```

![RST flag output](https://github.com/user-attachments/assets/4d7036c7-be93-4663-abc9-9dbe0e8e39aa)

Since the output was too much, I filtered the result using a word count:

```bash
sudo tcpdump -r traffic.pcap 'tcp[tcpflags] & tcp-rst != 0' | wc
```

![Filtered RST output](https://github.com/user-attachments/assets/0c6ec505-87d9-4560-9736-1039858a1752)

Result: The file contains **57 TCP Reset (RST) packets**.

---

### Step 5: Finding IP Address with Large Packets
I then found the IP address of the host that sent packets larger than 15000 bytes by using the following filter:

```bash
sudo tcpdump -r traffic.pcap 'len > 15000'
```

![Large packets output](https://github.com/user-attachments/assets/93084a63-effb-4ea6-be45-81490c71d29a)

To make the output more readable, I filtered it with the `-n` option:

```bash
sudo tcpdump -r traffic.pcap 'len > 15000' -n
```

![Filtered large packets output](https://github.com/user-attachments/assets/d95b03fc-fb1e-483f-8a96-e78fa9fe0be2)

Result: I identified an IP address repeatedly sending packets larger than 15000 bytes.

![IP address with large packets](https://github.com/user-attachments/assets/c77f9f47-2519-4679-a36d-63cb0598de31)

---

### Step 6: Finding the MAC Address of a Host Sending an ARP Request
Finally, I found the MAC address of the host that sent an ARP request by using the following command with the `-e` option:

```bash
sudo tcpdump -r traffic.pcap arp -e
```

![ARP MAC address output](https://github.com/user-attachments/assets/090d8fef-13f8-4d54-91c1-5d53aa4bfb45)

The MAC address of the host sending the ARP request was identified:

![MAC address](https://github.com/user-attachments/assets/f199f236-982b-4c39-b679-60ee67edaefd)

---

## Conclusion

This project provided hands-on experience with `tcpdump` for analyzing `.pcap` files, filtering traffic, and extracting key network information. Each step revealed different aspects of network activity, offering valuable insights for network administrators and security analysts alike. 🚀



































