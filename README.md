# Install MikroTik CHR on Alibaba Cloud

> **Note**  
> Custom images are not available for Alibaba Cloud after the trial period expires.  
> The workaround is to install the MikroTik image from inside the VM.

## Steps

### 1. Create Instance
- Go to **Create instance**.
- Under **Image and shape**, choose:
  - **Rocky Linux 9.1 - Free (x86_64)**
- Save the **Private key** file.
- Click **Create**.

### 2. Prepare SSH Access
1. Open **PuTTYgen**:
   - Click **Load**, select the private key you downloaded.
   - Click **Save private key** as `mikrotik.ppk`.
2. Open **PuTTY**:
   - Go to **Connection → SSH → Auth → Credentials**:
     - Browse for the `.ppk` file in the first field.
     - Browse for the original private key in the second field.
   - Return to **Session** tab.
   - Enter:
     ```
     rocky@(your_vm_public_ip)
     ```
   - Click **Open**.

### 3. Install MikroTik CHR
Execute the following commands inside the VM:

```bash
sudo -i
yum install unzip
umount -l /dev/sda1
curl -L https://download.mikrotik.com/routeros/7.9/chr-7.9.img.zip | funzip | dd of=/dev/sda bs=1M
sync
reboot
