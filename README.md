Adapted from https://github.com/hermanjunge/kubernetes-digitalocean-terraform

Added examples for
* A simple node-js helloworld app (default on port 80)
* A more complete node-js app which reads/writes to a cockroach-db backend

Using:

* Install terraform
* Install cfssl

* Create your key
```
ssh-keygen -f ${HOME}/.ssh/id_rsa_tf
```

* Import your key into digital-ocean
> https://cloud.digitalocean.com/settings/security

* Create a digital-ocean token and copy it into ./secrets/DO_TOKEN
> https://cloud.digitalocean.com/settings/api/tokens

* Run helper script to setup env
```
. ./setup_terraform.sh
```

* Run terraform
```
terraform apply
```


TODO:
* Create database credentials automatically - in meantime run ./scripts/create-example-db

