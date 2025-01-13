# pritunl-vpn

## ubuntu installation

this installation require ubuntu 24.04 (any other distro you can use documentation https://docs.pritunl.com/docs/installation )

```
sudo tee /etc/apt/sources.list.d/mongodb-org.list << EOF
deb [ signed-by=/usr/share/keyrings/mongodb-server-8.0.gpg ] https://repo.mongodb.org/apt/ubuntu noble/mongodb-org/8.0 multiverse
EOF

sudo tee /etc/apt/sources.list.d/openvpn.list << EOF
deb [ signed-by=/usr/share/keyrings/openvpn-repo.gpg ] https://build.openvpn.net/debian/openvpn/stable noble main
EOF

sudo tee /etc/apt/sources.list.d/pritunl.list << EOF
deb [ signed-by=/usr/share/keyrings/pritunl.gpg ] https://repo.pritunl.com/stable/apt noble main
EOF

sudo apt --assume-yes install gnupg

curl -fsSL https://www.mongodb.org/static/pgp/server-8.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-8.0.gpg --dearmor --yes
curl -fsSL https://swupdate.openvpn.net/repos/repo-public.gpg | sudo gpg -o /usr/share/keyrings/openvpn-repo.gpg --dearmor --yes
curl -fsSL https://raw.githubusercontent.com/pritunl/pgp/master/pritunl_repo_pub.asc | sudo gpg -o /usr/share/keyrings/pritunl.gpg --dearmor --yes
sudo apt update
sudo apt --assume-yes install pritunl openvpn mongodb-org wireguard wireguard-tools

sudo ufw disable

sudo systemctl start pritunl mongod
sudo systemctl enable pritunl mongod
```

after that with VPN UI you need lets encrypt ssl certificate. but first you need connect pritunl mongo. 

on server "sudo pritunl setup-key" this command return a key for connection.

pritunl UI work on http (443) port so you need to access to server 443 TCP. https://<server-ip>

<img width="682" alt="image" src="https://github.com/user-attachments/assets/fde1fc8b-dbc7-4ae9-b925-baa406d8c897" />

then you login mongodb previous setup-key. pritunl ask you username and password for real UI.

you can find "sudo pritunl default-password" this command user and password. 


![image](https://github.com/user-attachments/assets/b37813a6-0476-483c-a500-118fdb7b431b)

after login you can change admin user and password. 


thanks



