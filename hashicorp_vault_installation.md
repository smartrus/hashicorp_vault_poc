# Hashicorp vault installation

Downloading the binary 

```
apt-get install unzip -y
curl -O https://releases.hashicorp.com/vault/0.11.0/vault_0.11.0_linux_amd64.zip
mkdir /bin/vault
unzip vault_0.11.0_linux_amd64.zip -d /bin/vault
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

To start the Vault dev server, run:

```
vault server -dev
export VAULT_ADDR='http://127.0.0.1:8200'
```

Create secrets and read them:

```
vault kv put secret/hello value=world
vault kv put secret/hello value=world excited=yes
vault kv get secret/hello
```

You can parse value by using jq

```
vault kv get -format=json secret/hello | jq -r .data.data.excited
```

Configuring production ready server:

```
mkdir /etc/vault
vi /etc/vault/config.hcl

storage "file" {
 	path = "./secrets"
}
 
listener "tcp" {
	address = "127.0.0.1:8200"
	tls_disable = 1
}
```

Running the vault server with custom config

```
vault server -config /etc/vault/config.hcl
export VAULT_ADDR='http://127.0.0.1:8200'
vault operator init -key-shares 3  -key-threshold 2
```

