# k8s-deploy-ansible

Simple Role Based playbook to create a minimal Kubernetes cluster, with one
master and two worker nodes, connected with Weave CNI.

## Prerequisites

1. This is only tested on Ubuntu 18.04 VMs
2. This is only tested and specific to Azure VM's.
3. All three VM's are connected with the same vnet/subnet.
4. All three VMs created with the user 'ubuntu'.
5. Ansible installed on local machine.
6. ssh access is anabled via networking for each VM and each VM is manually
   accessed one time before running the playbook.

## Update user data

1. Change `hosts` to reflect Azure architecture.
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

1. Check the hosts:

    ```bash
    ansible-playbook -i hosts site.yml --list-host

    ```

2. Run the playbook:

    ```bash
    ansible-playbook -i hosts site.yml
    ```

## TODO
