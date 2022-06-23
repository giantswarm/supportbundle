# GiantSwarm Support Bundle

This repository has all the information and files needed to execute the GiantSwarm support bundle.

# Install krew plugins

Executing Preflight Checks and Support Bundles relies on a client-side utility, packaged as a kubectl plugin and distributed through the [krew](https://github.com/kubernetes-sigs/krew/) package manager. If you don't already have krew installed, head over to the [krew installation guide](https://krew.sigs.k8s.io/docs/user-guide/setup/install/), follow the steps there and then come back here.

```
kubectl krew install preflight
kubectl krew install support-bundle
```

Note: This will not install anything to your cluster, it only places a single binary per plugin in your path.


# Gather information
In order to execute the support bundle you can execute the following command. This is a read-only operation and can be executed in production clusters.

```
kubectl support-bundle ./support-bundle.yaml
```
or
```
kubectl support-bundle https://raw.githubusercontent.com/giantswarm/supportbundle/master/support-bundle.yaml
```

This will create a `tar.gz` file and you can explore the contents by `tar -xvf support-bundle.tar.gz`.


# Local check
In order to run the analysers on a local bundle you can execute the following command:
```kubectl support-bundle analyze support-bundle.yaml --bundle support-bundle-2022-06-23T12_52_34.tar.gz```

# Host preflight
You can execute checks on remote hosts by:
```
kubectl preflight --collector-image=replicated/troubleshoot:0.36.0 hostpreflight.yaml --selector=role=worker
```

Additional examples in  https://github.com/replicatedhq/troubleshoot/tree/main/examples/preflight/host


# Test collector locally
You will have to compile the tool collect in order to see the output of a remote collector.

```
git clone https://github.com/replicatedhq/troubleshoot.git
cd troubleshoot
make collect
./bin/collect remotecollector.yaml --selector=role=worker
```

# Additional tools
https://github.com/replicatedhq/sbctl