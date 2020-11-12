# k8s-deploy-ansible

Simple Role Based playbook to create a minimal Kubernetes cluster.

This is specific to Ubuntu VM's running in Azure.

The assumption is that the Azure VM's have been created with the appropriate
public_key and username 'ubuntu'.

## Update user data

1. Change ```hosts``` to reflect Azure architecture.
2. Run ansible ping to check connectivity:

    ```bash
    ansible all -m ping
    ```

    ```bash
    ➜  kube-cluster-role git:(main) ✗ ansible all -m ping
    master | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
    worker2 | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
    worker1 | SUCCESS => {
        "changed": false,
        "ping": "pong"
    }
    ```

3. Lets run a command for further validation:

    ```bash
    ansible all -a "uname -a"
    ```

    ```bash
    ➜  kube-cluster-role git:(main) ✗ ansible all -a "uname -a"
    worker2 | CHANGED | rc=0 >>
    Linux riwell-k8s-w2 5.4.0-1031-azure #32~18.04.1-Ubuntu SMP Tue Oct 6 10:03:22 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
    master | CHANGED | rc=0 >>
    Linux riwell-k8s-master 5.4.0-1031-azure #32~18.04.1-Ubuntu SMP Tue Oct 6 10:03:22 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
    worker1 | CHANGED | rc=0 >>
    Linux riwell-k8s-w1 5.4.0-1031-azure #32~18.04.1-Ubuntu SMP Tue Oct 6 10:03:22 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
    ```

## Running the Playbook

1. Let try running the playbook:

    ```bash
    ansible-playbook site.yaml
    ```

## TODO

[] - Delete configure-master
[] - Delete create-users if not needed for Ubuntu
