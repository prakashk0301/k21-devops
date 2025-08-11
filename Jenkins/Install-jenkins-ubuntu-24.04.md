## Prerequisites

- Create AWS ec2/Azure Ubuntu 24.04
- `sudo` privileges
- Internet access, open port 22, 80, 8080, 443 in security group

---

## 1️⃣ Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

## 2️⃣ Install Java (Required for Jenkins)

Jenkins requires Java 17+ (LTS).

```bash
sudo apt install -y fontconfig openjdk-17-jdk
```

Verify Java installation:

```bash
java -version
```

Expected output:  
`openjdk version "17.x.x" ...`

## 3️⃣ Add Jenkins Official Repository Key

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
```

## 4️⃣ Add Jenkins Repository to APT Sources

```bash
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | \
  sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

## 5️⃣ Install Jenkins

```bash
sudo apt update
sudo apt install -y jenkins
```

## 6️⃣ Enable and Start Jenkins Service

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
```

Check Jenkins status:

```bash
sudo systemctl status jenkins
```

## 7️⃣ Adjust Firewall (If Enabled)

By default, Jenkins runs on port 8080.

If UFW is active:

```bash
sudo ufw allow 8080
sudo ufw status
```

## 8️⃣ Access Jenkins in Browser

Open in your browser:

```
http://<your_server_ip>:8080
```

## 9️⃣ Get Initial Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy the password displayed and paste it into the Jenkins setup page.

## 🔟 Complete Web Setup

- Paste the initial admin password.
- Install Suggested Plugins.
- Create the first Admin User.
- Configure Jenkins URL (default is fine).
