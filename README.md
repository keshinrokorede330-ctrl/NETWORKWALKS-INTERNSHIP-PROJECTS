# Network Forensics with Wireshark — SOC Labs

Practical Wireshark labs from NetworkWalks. I captured and analysed
traffic to find attackers, open ports, hidden messages and downloaded files.

## Tools Used
- Wireshark
- Display Filters, Follow TCP Stream, Statistics > Conversations
- TCP / HTTP / DNS / ARP analysis

## Labs Completed

### Lab 3 — Port Scan Detection
- **Attacker:** `192.168.10.66`
- **Target:** `192.168.10.20`
- **Total ports probed:** 44
- **Closed ports:** 37 — server replied `RST, ACK`
- **Open ports:** 7 — server replied `SYN, ACK`
- **Attack identified:** TCP SYN Port Scan / Port Scanning
- **Not a SYN Flood:** Flood = many SYNs to ONE port to crash server.
  Scan = 1 SYN to MANY different ports to find open doors.

### Lab 4 — Follow TCP Stream / Chat Traffic
- **Chat Port:** `5000`
- **TCP Stream:** `5`
- **Method:** `Statistics > Conversations > TCP`, then
  `Right-click > Follow > TCP Stream` on `tcp.port == 5000`

### Lab 5 — Follow TCP Stream, Part 2 / Intranet
- **Scenario:** Staff browsed company intranet at `intranet.company.local`
- **Method:** Filter `http.request.method == "GET"` to list the 5 pages,
  then Follow TCP Stream on each to find the hidden HTML comment
  `<!-- ... -->`
- **Download Task:** Filter `http.request.uri contains "download"`
  to find the `.txt` file downloaded from `/download/`

## How I Analysed Each Capture
1. Check `Packets / Displayed` count after each filter
2. Use `ip.src`, `ip.dst`, `tcp.port`, `tcp.flags.syn`, `tcp.flags.reset`
3. Use `Follow TCP Stream` to read full conversation, not just one packet
4. Confirm open vs closed from server reply:
      - `SYN, ACK` = Open
      - `RST, ACK` = Closed

## Repo Structure
