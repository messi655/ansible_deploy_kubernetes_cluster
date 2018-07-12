Source
============================================
- This playbook We clone from https://github.com/kubernetes-incubator/kubespray and modify it.
- You can get more at https://kubernetes.io/docs/getting-started-guides/kubespray/ 


Deploy a Production Ready Kubernetes Cluster
============================================

-   Can be deployed on **AWS, GCE, Azure, OpenStack, vSphere or Baremetal**
-   **High available** cluster
-   **Composable** (Choice of the network plugin for instance)
-   Support most popular **Linux distributions**
-   **Continuous integration tests**

Quick Start
-----------

To deploy the cluster you can use :

### Ansible


    # Review and change parameters under ``inventory/environment/group_vars``
    cat inventory/environment/group_vars/all.yml
    cat inventory/environment/group_vars/k8s-cluster.yml

    # Deploy Kubespray with Ansible Playbook
    ansible-playbook -i inventory/environment/hosts.ini cluster.yml

Supported Linux Distributions
-----------------------------

-   **Container Linux by CoreOS**
-   **Debian** Jessie, Stretch, Wheezy
-   **Ubuntu** 16.04
-   **CentOS/RHEL** 7
-   **Fedora/CentOS** Atomic
-   **openSUSE** Leap 42.3/Tumbleweed

Note: Upstart/SysV init based OS types are not supported.

Versions of supported components
--------------------------------

-   [kubernetes](https://github.com/kubernetes/kubernetes/releases) v1.9.5
-   [etcd](https://github.com/coreos/etcd/releases) v3.2.4
-   [flanneld](https://github.com/coreos/flannel/releases) v0.10.0
-   [calico](https://docs.projectcalico.org/v2.6/releases/) v2.6.8
-   [canal](https://github.com/projectcalico/canal) (given calico/flannel versions)
-   [cilium](https://github.com/cilium/cilium) v1.0.0-rc8
-   [contiv](https://github.com/contiv/install/releases) v1.1.7
-   [weave](http://weave.works/) v2.3.0
-   [docker](https://www.docker.com/) v17.03 (see note)
-   [rkt](https://coreos.com/rkt/docs/latest/) v1.21.0 (see Note 2)

Note: kubernetes doesn't support newer docker versions. Among other things kubelet currently breaks on docker's non-standard version numbering (it no longer uses semantic versioning). To ensure auto-updates don't break your cluster look into e.g. yum versionlock plugin or apt pin).



Requirements
------------

-   **Ansible v2.4 (or newer) and python-netaddr is installed on the machine
    that will run Ansible commands**
-   **Jinja 2.9 (or newer) is required to run the Ansible Playbooks**

Network Plugins
---------------

You can choose between 6 network plugins. (default: `calico`, except Vagrant uses `flannel`)

-   [flannel](docs/flannel.md): gre/vxlan (layer 2) networking.

-   [calico](docs/calico.md): bgp (layer 3) networking.

-   [canal](https://github.com/projectcalico/canal): a composition of calico and flannel plugins.

-   [cilium](http://docs.cilium.io/en/latest/):  layer 3/4 networking (as well as layer 7 to protect and secure application protocols), supports dynamic insertion of BPF bytecode into the Linux kernel to implement security services, networking and visibility logic.

-   [contiv](docs/contiv.md): supports vlan, vxlan, bgp and Cisco SDN networking. This plugin is able to
    apply firewall policies, segregate containers in multiple network and bridging pods onto physical networks.

-   [weave](docs/weave.md): Weave is a lightweight container overlay network that doesn't require an external K/V database cluster.
    (Please refer to `weave` [troubleshooting documentation](http://docs.weave.works/weave/latest_release/troubleshooting.html)).

The choice is defined with the variable `kube_network_plugin`. There is also an
option to leverage built-in cloud provider networking instead.
See also [Network checker](docs/netcheck.md).


