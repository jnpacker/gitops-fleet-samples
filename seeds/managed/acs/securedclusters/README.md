# Stackrox init-bundle secrets
This describes how to prepare the secrets from ACS Central Service

# Secrets
There are three secrets needed to initialize the ACS SecuredCluster resource.
  a. sensor-tls
  b. collector-tls
  c. admission-control-tls

* Log into ACS Centra Service, then choose `Platform Configuration` > `Clusters` > `MANAGE TOKENS` > `HELM - Cluster Initi Bundle`
* Choose Generate bundle
* Enter a name and press `Generate`
* Then `Download Kubernetes secrets file`

## Preparing the secrets
Edit the `YOUR_NAME-init-secrets-.yaml` file
* For each of the three secrets in the file, add the following annotation:
  ```
  apps.open-cluster-management.io/deployables: "secret"
  ```
* For the `sensor-tls` secret, add the following key/value to the stringData section
  ```
  acs-host: central-stackrox-central-services.apps.MY_BASE_DOMAIN:443
  ```
  _Note: Make sure not to inlcude `https://`_

## Apply the secrets
* The secrets need to be created in the `init-bundle-ch` namespace/project, this is where the Subscription will look for them
* On the hub:
  ```
  # If you have already applied the files in this folder, the init-bundle-ch namespace will already exist
  oc new-project init-bundle-ch
  
  oc -n init-bundle-ch apply -k .
  ```
  This creates a subscription that will deliver the init-bundle secrets to the stackrox namespace on all your clusters
  
  
