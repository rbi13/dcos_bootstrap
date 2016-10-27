
# DCOS bootstrap


based on the (advanced instalation guide)[https://dcos.io/docs/1.8/administration/installing/custom/advanced/] for DCOS 1.8 


1. Create the cluster configuration by copying and editing the config.yaml:

```sh
cp genconf/config.yaml.template genconf/config.yaml
```

2. Generate the bootstrap scripts and start bootstrap file server:

```sh
bash bootstrap dcos-config-gen
```

3. create a file named *node-admins* and list all cluster nodes. Each line should be in the format
`<machine-ip>:<admin-username>:<admin-password>`. You can delete this file after setup. This 
script will create a user named *dcos* which is only accessible using the keys specified in the *bootstrap*
script. 

```sh
bash bootstrap nodes-dcosuser-setup
```

4. Create a *master-nodes* and a *agent-nodes* file listing the IPs of each machine and start 
the bootstrap process:

```sh
bash bootstrap cluster-setup master-nodes slave-nodes
```

5. check <master-node-IP>:8181 for cluster status. When all master nodes have a green status the cluster
should be ready for use. The DCOS web interface should be available at <master-node-IP>.

### Notes
- when DCOS becomes compatible with Docker 1.12 the systemd script patch should be removed from
	the bootstrap script
- This was tested on RHEL 7.1 but should be compatible with debian and other distros.  