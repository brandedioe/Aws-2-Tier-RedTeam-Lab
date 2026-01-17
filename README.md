AWS 2-Tier Web Architecture (Red Team Lab)
🚨 Project Overview
Objective: To manually deploy a segmented 2-Tier Web Architecture on AWS to study infrastructure security, network segmentation, and attack surfaces. Role: Cloud Infrastructure & Security Implementation Tools: AWS (EC2, RDS), Linux (Ubuntu), Apache, MySQL, PHP.

🏗️ Architecture
This project implements a "Separation of Duties" security model:

Tier 1 (Web Server): EC2 Instance acting as the public-facing entry point (The "Beachhead").

Tier 2 (Database): RDS Instance hosting the data in a segmented environment (The "Crown Jewels").

🛡️ Security Controls Implemented
As an aspiring Red Teamer, I focused on the following defense mechanisms to understand how they thwart attacks:

1. Network Segmentation (Lateral Movement Defense)
Configured AWS Security Groups to act as a stateful firewall.

Rule: The Database (RDS) denies all traffic except on Port 3306 specifically from the Web Server's Security Group.

Impact: Prevents direct internet access to the database, forcing an attacker to pivot through the web server first.

2. Principle of Least Privilege (FileSystem)
Manually managed Linux file ownership (chown) and permissions (chmod).

Ensured the Apache service user (www-data) had restricted access only to necessary application directories.

Impact: Limits the blast radius if the web service is compromised.

3. Attack Surface Reduction
Removed installation directories (/install) post-deployment to prevent account takeover vulnerability.

Hardened the server by killing unnecessary background processes during setup.

📸 Implementation Evidence
1. The Setup (Linux & LAMP Stack)
Manual installation of dependencies and process management via CLI.![Terminal_Installation](https://github.com/user-attachments/assets/5caffd90-5f11-4fe8-9cb1-ab874addd10a)
 

2. The Bridge (Database Connection)
Successful handshake between the isolated EC2 instance and the RDS backend. ![RDS_Database_Successful](https://github.com/user-attachments/assets/41506454-cefc-4836-a50d-c2f444ea1813)

3. The Target (Live Application)
Final deployment of the PrestaShop platform ready for vulnerability scanning. <img width="946" height="464" alt="Vulnerability_scanning" src="https://github.com/user-attachments/assets/533be932-0701-40c3-892f-1c95b27d6ce1" />


🧠 Key Takeaways for Offensive Security
Building this target taught me:

Persistence: How to manage and kill hung Linux processes during a DoS-like freeze.

Pivoting: The specific network conditions required to bridge a public server to a private database.

Misconfigurations: How easily a simple permission error can lock a system—or open it up to privilege escalation.
