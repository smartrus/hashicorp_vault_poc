# Hashicorp vault installation

Downloading the binary 

```
apt-get install unzip -y
curl -O https://releases.hashicorp.com/vault/0.11.0/vault_0.11.0_linux_amd64.zip
mkdir /bin/vault
unzip terraform_0.11.8_linux_amd64.zip -d /bin/vault
export PATH=$PATH:/bin/vault
cd /usr/bin
sudo ln -s /bin/vault vault
```

Check vault:

```
vault
```

Install command line completion

```
vault -autocomplete-install
exec $SHELL
```


