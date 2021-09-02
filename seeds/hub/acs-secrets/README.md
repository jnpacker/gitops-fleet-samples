# How to distribute Red Hat Advanced Cluster Security secrets
1. Collect the init-bundle as described in the ACS quick start guide, this will give you three secrets in a yaml
2. Edit the yaml and set the `namespace: acs-init-bundle-ch` for each of the three secrets
3. Next add the following annotation to each secret: `apps.open-cluster-management.io/deployables: "secret"`
4. Apply the init-bundle.yaml file to the hub cluster.  The project `acs-init-bundle-ch` should have been created when the subscription in this folder was applied to the hub.

It should take < 60s for the secrets to be propagated to all managed clusters matching the placementRule used.