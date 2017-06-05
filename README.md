# terraform-kubernetes
Adapted from https://github.com/hermanjunge/kubernetes-digitalocean-terraform

This is for personal development to learning how these components work.

Added examples for
* A simple node-js helloworld app (default on port 80)
* A more complete node-js app which reads/writes to a cockroach-db backend

# Running

* Install terraform
* Install cfssl and cfssljson (make sure they get added to your $PATH)
* Install kubectl 

* Create your key
```ssh-keygen -f ${HOME}/.ssh/id_rsa_tf```

* Import your new ssh key (above) into digital-ocean
> https://cloud.digitalocean.com/settings/security

* Create a digital-ocean token and add it to ./secrets/DO_TOKEN
> https://cloud.digitalocean.com/settings/api/tokens

* Run helper script to setup env
```. ./setup_terraform.sh```

* Run terraform
```terraform apply```

# Verify cluster setup

Verify cluster is setup with:
```kubectl get all```

Make sure you setup a 'test' database and a 'test' user first.
```./scripts/create-example-db```

Run the proxy to get access to the kubernetes-dashboard from your local machine
```kubectl proxy```

If you're not running kubectl on your local machine, you can make use of some ssh-forwarding:
```ssh -L 8001:localhost:8001 $user@$host_running_kubectl_proxy -i $keyfile```

If you have kubectl on your local machine, configure it to access the remote cluster:
* https://kubernetes.io/docs/tasks/access-application-cluster/authenticate-across-clusters-kubeconfig/

Browse to nodejs-app:
* http://$external_ip:80 to view the nodejs app (refershing will read/write data to the dB)

# Teardown cluster
```terraform destroy```

# TODO:
* terraform apply seems to get stuck during some node creation (ctcl-c and retry works)...hmm
* make kube master h/a 
* Create database credentials automatically (probably via a nodejs bootstrap script, not here0

