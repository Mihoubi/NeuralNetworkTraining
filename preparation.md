Prepare WSL (Ubuntu)
=================
sudo apt update

# (A) Ensure SSH server is installed & running
sudo apt install -y openssh-server
sudo service ssh start

# (B) Allow password auth (optional if you prefer keys)
sudo sed -i 's/^#\?PasswordAuthentication .*/PasswordAuthentication yes/' /etc/ssh/sshd_config
sudo service ssh restart

# (C) Verify SSH is listening and note your IP (use localhost if possible)
ss -tlpn | grep ':22'
hostname -I     # IP may change each reboot; localhost usually works better

# (D) (Recommended) Install core Python tools in your 3.13
/home/mihoubi/.pyenv/versions/3.13.0/bin/python3 -m pip install -U pip ipykernel jupyterlab numpy matplotlib scikit-learn plotly

# Test SSH from Windows

Open PowerShell (on Windows, not WSL):

ssh mihoubi@localhost
# If localhost fails, try your current WSL IP (example):
ssh mihoubi@172.24.254.40


## Add WSL Python to IntelliJ (SSH Remote Interpreter)

IntelliJ → File → Settings → (search) “Python Interpreter”
(If you don’t see it: File → Project Structure → SDKs → “+” → Python SDK → SSH)

⚙ Add Interpreter… → SSH

Host: localhost (or your WSL IP)

Port: 22

User: mihoubi

Auth: password or key