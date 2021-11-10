<h1>Ansible on Windows machines</h1>

<h3>Ansible through OpenSSH (private+public key):</h3>

    (new-object net.webclient).DownloadFile('https://raw.githubusercontent.com/GuardNexusGN/Ansible-on-Windows-OpenSHH/main/ssh_ansible.ps1','ssh_ansible.ps1')
    ./ssh_ansible.ps1
    echo 'PUB KEY' > C:/Users/ansible/.ssh/authorized_keys


<h3>No password auth via OpenSSH (only key allowed):</h3>

    (gc C:\ProgramData\ssh\sshd_config) -replace "PasswordAuthentication yes", "PasswordAuthentication no" | sc C:\ProgramData\ssh\sshd_config
    (gc C:\ProgramData\ssh\sshd_config) -replace "#PasswordAuthentication no", "PasswordAuthentication no" | sc C:\ProgramData\ssh\sshd_config
    Restart-Service sshd

<h3>Usefull powershell commands for old Windows Servers (Feature/TLS errors on ssh_ansible run) (paste on the beggining):</h3>

    Import-Module DISM
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

---

<h3>Ansible through WinRM (windows account password):</h3>

    (new-object net.webclient).DownloadFile('https://raw.githubusercontent.com/GuardNexusGN/Ansible-on-Windows-OpenSHH/main/winrm.ps1','winrm.ps1')
    ./winrm.ps1
    net user ansible 'SECURE PASSWORD'
    Add-LocalGroupMember -Group "Administrators" -Member ansible
