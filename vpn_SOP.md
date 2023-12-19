# SOP: VPN Setup


This SOP outlines the steps for setting up a secure and reliable VPN connection on pfSense for a company environment. It covers both remote access and site-to-site VPN configurations.

Before you begin:

Ensure you have a pfSense firewall installed and configured with internet access.
Familiarity with basic networking concepts and pfSense configuration is recommended.
Gather the necessary information for your chosen VPN type (e.g., user credentials, certificates, IP addresses).
I. Choosing a VPN Protocol:

pfSense supports various VPN protocols, each with its own advantages and security considerations. Here's a quick overview:

OpenVPN: Widely used, easy to set up, supports various authentication methods, good for both remote access and site-to-site.
IPsec: Robust and secure, often used for site-to-site connections, requires more configuration than OpenVPN.
WireGuard: Newer, faster, and simpler than OpenVPN, still under development, may not be suitable for all scenarios.
II. Remote Access VPN Setup (OpenVPN):

Create a Certificate Authority (CA):

Go to System > Certificate Management > CAs.
Click "Add" and configure the CA settings (name, validity period, etc.).
Generate a CA certificate and private key.
Create a Server Certificate:

Go to VPN > OpenVPN > Servers.
Click "Add" and choose "EasyRSA" for CA.
Select the previously created CA and provide a server name and hostname.
Generate server certificate and key.
Configure Server Settings:

Define the tunnel network (e.g., 10.0.0.0/24).
Choose encryption algorithms (AES-256 recommended).
Set client authentication method (e.g., certificates, pre-shared keys).
Create User Accounts:

Go to VPN > OpenVPN > Users.
Click "Add" and choose "EasyRSA" for CA.
Select the CA and provide a username and password.
Generate user certificate and key.
Configure Firewall Rules:

Go to Firewall > Rules > LAN.
Create a rule to allow OpenVPN traffic (TCP port 443 by default).
Download Client Configuration:

Go to VPN > OpenVPN > Clients (Export).
Choose the user and download the client configuration file (.ovpn).
Distribute Client Configuration:

Share the downloaded .ovpn file with authorized users.
Guide users on installing and configuring the VPN client on their devices.
III. Site-to-Site VPN Setup (IPsec):

Configure Phase 1 Settings:

Go to VPN > IPsec > Phases.
Click "Add" and define the Phase 1 parameters (e.g., encryption algorithms, DH groups).
Configure Phase 2 Settings:

Go to VPN > IPsec > Tunnels.
Click "Add" and define the Phase 2 parameters (e.g., tunnel endpoints, local and remote networks).
Create Pre-Shared Key (PSK):

Go to VPN > IPsec > Pre-Shared Keys.
Click "Add" and create a strong PSK for authentication.
Configure Firewall Rules:

Go to Firewall > Rules > WAN.
Create rules to allow IKEv2 and IPSec traffic for the established tunnel.
Verify and Test the Connection:

Initiate the VPN connection from either side.
Ping devices on the remote network to confirm connectivity.
IV. Additional Considerations:

Security: Regularly update pfSense and VPN software, enforce strong passwords, and monitor access logs.
Performance: Optimize VPN settings and hardware to avoid impacting network performance.
User Management: Implement user access controls and audit VPN usage for security purposes.
V. Resources:

pfSense Documentation: https://docs.netgate.com/pfsense/en/latest/
OpenVPN: https://openvpn.net/
IPsec: https://en.wikipedia.org/wiki/Internet_security
WireGuard: https://www.wireguard.com/
By following this SOP and tailoring it to your specific needs, you can establish a secure and reliable VPN connection on pfSense for your company, enabling secure remote access and efficient site-to-site communication.