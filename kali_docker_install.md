# Remove broken Docker source
```bash
sudo rm -f /etc/apt/sources.list.d/docker.sources
sudo rm -f /etc/apt/sources.list.d/docker.list
sudo rm -f /etc/apt/sources.list.d/*docker*.sources
sudo rm -f /etc/apt/sources.list.d/*docker*.list
```

# Install prerequisites
```bash
sudo apt update
sudo apt install -y ca-certificates curl
```

# Add Docker GPG key
```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg \
  -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

# Add Docker repo, but hardcode trixie instead of kali-rolling
```bash
sudo tee /etc/apt/sources.list.d/docker.sources > /dev/null <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: trixie
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
```

# Update again
```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl enable --now docker
```

# Add current user to docker group to run docker without root
```bash
sudo usermod -aG docker $USER
```
