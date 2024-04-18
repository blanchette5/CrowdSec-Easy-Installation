# CrowdSec-Easy-Installation-Ubuntu

## Introduction
This guide provides easy installation steps for setting up CrowdSec on a Ubuntu system. CrowdSec is an open-source cybersecurity tool designed to protect servers, containers, and cloud workloads from malicious activities.

### Prerequisites
- Ensure that your system is running a compatible Linux distribution.
- Have sudo privileges or access to the root account.
- The system must be connected to the internet to download necessary packages.

## Installation Steps

### I. Visit the CrowdSec Website
- Navigate to the CrowdSec website and select the Linux option.

### II. Install Repositories
1. Update the package list:
    ```
    sudo apt update
    ```
2. Install curl if not already installed:
    ```
    sudo apt install curl
    ```
3. Add the CrowdSec repositories:
    ```
    sudo curl -s https://packagecloud.io/install/repositories/crowdsec/crowdsec/script.deb.sh | sudo bash
    ```

### III. Install CrowdSec Engine
1. Install the CrowdSec engine:
    ```
    sudo apt install crowdsec
    ```

### IV. Install a Bouncer
1. Install the classic CrowdSec firewall bouncer (iptables):
    ```
    sudo apt install crowdsec-firewall-bouncer-iptables
    ```

### V. Configure Alerts Detection
1. Navigate to the parser's directory:
    ```
    cd /etc/crowdsec/parsers/s02-enrich
    ```
2. Edit the `whitelists.yaml` file:
    ```
    sudo nano whitelists.yaml
    ```
3. Remove the CIDR lines for allowed IP ranges:
    ```
 
    - "192.168.0.0/16"
    - "10.0.0.0/8"
    - "172.16.0.0/12"
    ```

## Testing CrowdSec

### VI. Test CrowdSec
1. Install openssh-server if not already installed:
    ```
    sudo apt install openssh-server
    ```
2. Use another PC to test SSH connectivity by repeatedly running the SSH command:
    ```
    ssh 192.x.x.x
    ```
3. After several attempts, you will notice SSH login attempts being blocked, indicating successful detection and prevention by CrowdSec.

4. To view detected alerts, use the following command:
    ```
    sudo cscli alerts list
    ```
5. To view  detected decisions by the bouncer, use the following command:
    ```
    sudo cscli decisions list
    ```
 6. **Optional: Integrate with CrowdSec Website**
    - Create an account on the CrowdSec website.
    - On the website, click on the "plus" icon at the top right of the screen to enroll a node.
    - Copy and paste the displayed command on your CrowdSec server to send data to the website and collect data via Prometheus integrated into CrowdSec.

## Conclusion
You have successfully installed and configured CrowdSec on your system. You can now enjoy enhanced security and protection against malicious activities.
