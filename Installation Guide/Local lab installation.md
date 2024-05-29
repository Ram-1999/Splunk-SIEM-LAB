# SIEM Lab Setup with Splunk

This guide walks you through setting up a Security Information and Event Management (SIEM) lab using Splunk on two virtual machines.

## Prerequisites

- VMware (or VirtualBox or any other virtualization software)
- Windows 10 OS (for Machine 1)
- Windows Server 2019 (for Machine 2)

## Step-by-Step Instructions

### 1. Setting Up Virtual Machines

We are using VMware for this setup. If you prefer, you can use VirtualBox or another virtualization software.

#### Machine 1: Windows 10 OS

We will use this machine to deploy the Splunk Host.

#### Machine 2: Windows Server 2019

We will use this machine to forward logs to the Splunk Host on Machine 1.

Refer to any YouTube videos on how to install Windows in VMware for guidance. Follow the process to set up the virtual machines. You should have two instances: Machine 1 and Machine 2.

### 2. Installing Splunk on Machine 1

1. Once Machine 1 is set up, open Chrome and go to [Splunk Downloads](https://www.splunk.com/en_us/download.html). Log in with your account or create one if you don't have an account.
2. On the download page, you will see several options. Choose the second option, "Enterprise Setup."
3. Download Splunk Enterprise.
4. Once the download is complete, right-click the installer and run it.
5. Click "Next" and proceed with the default setup.
6. Create an admin account with the following credentials:
    - **Username:** y
    - **Password:** z (make sure to remember these credentials for logging into Splunk)
7. Click "Next" and wait for the installation to complete.
8. Once installed, go to `http://127.0.0.1:8000` in your browser. This URL will access the Splunk dashboard. Log in with the credentials you created during setup.

### 3. Installing Splunk Forwarder on Machine 2

Since Machine 2 is running Windows Server 2019 and does not have internet access, we need to enable RDP. Refer to [this link](https://www.clouvider.com/knowledge_base/how-to-enable-rdp-in-windows-server-2019/) for instructions on setting up RDP.

1. Once RDP is enabled, download the Splunk Forwarder on Machine 1.
2. Connect to Machine 2 from Machine 1 via RDP.
3. Copy the Splunk Forwarder installer to Machine 2.
4. Right-click the installer on Machine 2 and run it.
5. Accept the user license agreement and click "Next."
6. Create admin credentials.
7. Enter the IP address of the Splunk Host (Machine 1) and click "Next."
8. Click "Finish" to complete the installation.

### 4. Configuring the Splunk Dashboard

1. Log in to the Splunk dashboard.
2. Click on "Settings" and then "Data Inputs."
3. Click on "Windows Event Logs" and add a new input.
4. If everything is set up correctly, you should see the name of Machine 2. Click on it.
5. Choose the index where you want to store the logs. Create a new index if necessary.
6. Once done, click "Finish."

### 5. Running Sample Queries

Now that your SOC lab is set up, you can run some sample queries, such as:

```spl
index="indexname"
