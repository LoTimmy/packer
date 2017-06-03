shell> esxcli system settings advanced set -o /Net/GuestIPHack -i 1
shell> cat <<EOF > /etc/vmware/firewall/vncServer.xml
<ConfigRoot>
  <service>
    <id>vncServer</id>
    <rule id='0000'>
      <direction>inbound</direction>
      <protocol>tcp</protocol>
      <porttype>dst</porttype>
      <port>
        <begin>5900</begin>
        <end>5999</end>
      </port>
    </rule>
    <enabled>true</enabled>
    <required>false</required>
  </service>
</ConfigRoot>
EOF
shell> esxcli network firewall refresh
shell> esxcli network firewall ruleset list


shell> packer build ubuntu-16.04.2-server-amd64-esx5-gitlab.json
vmware-iso output will be in this color.

==> vmware-iso: Downloading or copying ISO
    vmware-iso: Downloading or copying: http://releases.ubuntu.com/16.04/ubuntu-16.04.2-server-amd64.iso
==> vmware-iso: Creating floppy disk...
    vmware-iso: Copying files flatly from floppy_files
    vmware-iso: Copying file: preseed.cfg
    vmware-iso: Done copying files from floppy_files
    vmware-iso: Collecting paths from floppy_dirs
    vmware-iso: Resulting paths from floppy_dirs : []
    vmware-iso: Done copying paths from floppy_dirs
==> vmware-iso: Uploading Floppy to remote machine...
==> vmware-iso: Uploading ISO to remote machine...
==> vmware-iso: Creating virtual machine disk
==> vmware-iso: Building and writing VMX file
==> vmware-iso: Registering remote VM...
==> vmware-iso: Starting virtual machine...
    vmware-iso: The VM will be run headless, without a GUI. If you want to
    vmware-iso: view the screen of the VM, connect via VNC with the password "hW8tYWwJ" to
    vmware-iso: vnc://192.168.88.241:5900
==> vmware-iso: Waiting 5s for boot...
==> vmware-iso: Connecting to VM via VNC
==> vmware-iso: Typing the boot command over VNC...
==> vmware-iso: Waiting for SSH to become available...
==> vmware-iso: Connected to SSH!
==> vmware-iso: Gracefully halting virtual machine...
    vmware-iso: Waiting for VMware to clean up after itself...
==> vmware-iso: Deleting unnecessary VMware files...
    vmware-iso: Deleting: /vmfs/volumes/datastore1/gitlab/vmware.log
==> vmware-iso: Compacting the disk image
==> vmware-iso: Cleaning VMX prior to finishing up...
    vmware-iso: Unmounting floppy from VMX...
    vmware-iso: Detaching ISO from CD-ROM device...
    vmware-iso: Disabling VNC server...
==> vmware-iso: Keeping virtual machine registered with ESX host (keep_registered = true)
Build 'vmware-iso' finished.

==> Builds finished. The artifacts of successful builds are:
--> vmware-iso: VM files in directory: /vmfs/volumes/datastore1/gitlab
