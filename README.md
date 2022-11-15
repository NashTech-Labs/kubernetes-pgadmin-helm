# PGAdmin
This is a single Helm chart that deploys a pgAdmin instance to your Kubernetes cluster.

## Prerequisites
This install assumes you have an existing Kubernetes cluster installed and a [postgresql](https://github.com/kubernetes/charts/tree/master/stable/postgresql) instance deployed.

## Chart Configuration

The defaults in `values.yaml` will make your pgAdmin deployment accessible by its IP address over plaintext HTTP.

To access your pgAdmin instance using a domain name over *plaintext HTTP*:

1. set `service.type` to `NodePort`
2. set `ingress.enabled` to `true`)
3. set `ingress.staticIPReservation` to the name of the static IP address reservation you created in step 3
4. At your domain registrar, create an A record pointing to the static IP address you reserved in step 3

## Package
Once you've cloned this repo, you can create your helm package by running the following command in the repo's root directory:
```
helm package .
```

## Install

```
NAMESPACE=database
PGADMIN_PASSWORD=XXX
helm install pgadmin ./pgadmin/ -f ./pgadmin/values.yaml --namespace ${NAMESPACE} 
```

## Configure
When the deployment has finished and you have an external IP for your pgAdmin service, you can go to the pgAdmin portal at `http://{external-ip}:5050/`.

Once logged in, add a new server and provide the Cluster IP, username and password for your postgres service.





