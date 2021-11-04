---
title: Raspberry Cluster - Installing Kubernetes
markup: mmark
date: 2021-01-10
bigimg: [{src: "/img/2020-01-12-differentiable-manifolds/venedig.jpg", desc: "Venice, heading for a thunder storm (July 2019)"}]
draft: true
tags: ["cluster", "raspberry"]
---

Abstract ...


<!--more-->

The flavor of Kubernetes we will be installing is ``K3s`` [(documentation)](https://rancher.com/docs/k3s/latest/en/). K3s is a pretty popular minimal Kubernetes distribution from [Rancher](https://rancher.com/). For this project, the main value propostion of K3s is a minimal resource usage and also high quality developer tools.



### Container features on master and worker nodes


We need to enable the ``cgroups`` container features in the kernel. You can do this by editing the ``/boot/cmdline.txt`` file  using your favorite editor. Run the following command to edit this file:
	
	sudo nano /boot/cmdline.txt

Then append the following to the end line of the file:

	cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory

Save the file and reboot your Raspberry Pi's. 

Note: If you type in ``docker`` after the installation, you won't find the command installed. This is because ``K3s`` uses a low-level component called ``containerd`` directly, to save space. If you want to use Docker you can install it by running the following command on your Raspberry Pi’s:

	curl -sSL https://get.docker.com | sh

Then run the following command so you don’t have to run docker as ``sudo``:

	sudo usermod -aG docker pi



### Install script for master node


``K3s`` provides an installation script that is a convenient way to install it as a service on systemd or openrc based systems. This script is available at [https://get.k3s.io](https://get.k3s.io). To install ``K3s`` using this method, just run:

	curl -sfL https://get.k3s.io | sh -

This command will install ``K3s`` on the machine as the server node. After running this installation:

* The ``K3s`` service will be configured to automatically restart after node reboots or if the process crashes or is killed
* Additional utilities will be installed, including ``kubectl``, ``crictl``, ``ctr``, ``k3s-killall.sh``, and ``k3s-uninstall.sh``
* A ``kubeconfig`` file will be written to ``/etc/rancher/k3s/k3s.yaml`` and the ``kubectl`` installed by ``K3s`` will automatically use it

This command also installs a couple of other apps that help you get started with the cluster such as CoreDNS, Traefik Ingress Controller and a Service Load Balancer. The exact specifications of those applications can be found [here](https://rancher.com/docs/k3s/latest/en/networking/).

That's the reply we're getting:

	pi@rpi01:~ $ curl -sfL https://get.k3s.io | sh -
	[INFO]  Finding release for channel stable
	[INFO]  Using v1.20.2+k3s1 as release
	[INFO]  Downloading hash https://github.com/rancher/k3s/releases/download/v1.20.2+k3s1/sha256sum-arm.txt
	[INFO]  Downloading binary https://github.com/rancher/k3s/releases/download/v1.20.2+k3s1/k3s-armhf
	[INFO]  Verifying binary download
	[INFO]  Installing k3s to /usr/local/bin/k3s
	[INFO]  Creating /usr/local/bin/kubectl symlink to k3s
	[INFO]  Creating /usr/local/bin/crictl symlink to k3s
	[INFO]  Creating /usr/local/bin/ctr symlink to k3s
	[INFO]  Creating killall script /usr/local/bin/k3s-killall.sh
	[INFO]  Creating uninstall script /usr/local/bin/k3s-uninstall.sh
	[INFO]  env: Creating environment file /etc/systemd/system/k3s.service.env
	[INFO]  systemd: Creating service file /etc/systemd/system/k3s.service
	[INFO]  systemd: Enabling k3s unit
	Created symlink /etc/systemd/system/multi-user.target.wants/k3s.service → /etc/systemd/system/k3s.service.
	[INFO]  systemd: Starting k3s
	pi@rpi01:~ $

We can run the following command to see if K3s started up correctly:

	pi@rpi01:~ $ sudo systemctl status k3s
	● k3s.service - Lightweight Kubernetes
	   Loaded: loaded (/etc/systemd/system/k3s.service; enabled; vendor preset: enabled)
	   Active: active (running) since Tue 2021-01-26 23:21:41 CET; 6min ago
	     Docs: https://k3s.io
	  Process: 1473 ExecStartPre=/sbin/modprobe br_netfilter (code=exited, status=0/SUCCESS)
	  Process: 1476 ExecStartPre=/sbin/modprobe overlay (code=exited, status=0/SUCCESS)
	 Main PID: 1477 (k3s-server)
	    Tasks: 44
	   Memory: 496.4M
	   CGroup: /system.slice/k3s.service
	           ├─1477 /usr/local/bin/k3s server
	           └─1522 containerd

	Jan 26 23:27:28 rpi01 k3s[1477]: I0126 23:27:28.610368    1477 request.go:655] Throttling request took 1.045294657s, request: GET:https://127.0.0.1:6444/apis/scheduling.k8s.io/v1?timeout=
	Jan 26 23:27:29 rpi01 k3s[1477]: W0126 23:27:29.564235    1477 garbagecollector.go:703] failed to discover some groups: map[metrics.k8s.io/v1beta1:the server is currently unable to handle
	Jan 26 23:27:37 rpi01 k3s[1477]: E0126 23:27:37.801404    1477 resource_quota_controller.go:409] unable to retrieve the complete list of server APIs: metrics.k8s.io/v1beta1: the server is
	Jan 26 23:27:39 rpi01 k3s[1477]: W0126 23:27:39.868882    1477 handler_proxy.go:102] no RequestInfo found in the context
	Jan 26 23:27:39 rpi01 k3s[1477]: E0126 23:27:39.869020    1477 controller.go:116] loading OpenAPI spec for "v1beta1.metrics.k8s.io" failed with: failed to retrieve openAPI spec, http erro
	Jan 26 23:27:39 rpi01 k3s[1477]: , Header: map[Content-Type:[text/plain; charset=utf-8] X-Content-Type-Options:[nosniff]]
	Jan 26 23:27:39 rpi01 k3s[1477]: I0126 23:27:39.869064    1477 controller.go:129] OpenAPI AggregationController: action for item v1beta1.metrics.k8s.io: Rate Limited Requeue.
	Jan 26 23:27:47 rpi01 k3s[1477]: E0126 23:27:47.043910    1477 node_controller.go:241] Error getting instance metadata for node addresses: error fetching node by provider ID: unimplemente
	Jan 26 23:28:01 rpi01 k3s[1477]: I0126 23:28:01.352184    1477 request.go:655] Throttling request took 1.045628967s, request: GET:https://127.0.0.1:6444/apis/metrics.k8s.io/v1beta1?timeou
	Jan 26 23:28:02 rpi01 k3s[1477]: W0126 23:28:02.308396    1477 garbagecollector.go:703] failed to discover some groups: map[metrics.k8s.io/v1beta1:the server is currently unable to handle

	pi@rpi01:~ $

We see a number of issues appearing but decide to investigate them later. Let's check if the master node is up and running using the following command:

	pi@rpi01:~ $ sudo k3s kubectl get nodes
	NAME    STATUS   ROLES                  AGE     VERSION
	rpi01   Ready    control-plane,master   8m45s   v1.20.2+k3s1
	pi@rpi01:~ $

Note the ``K3s`` token, which we will need to bootstrap the workers in the following steps:

	pi@rpi01:~ $ sudo cat /var/lib/rancher/k3s/server/node-token
	K100f8a8ac9aa5443597272dac3b637c1043d0556c8e5d51080a26e4681b564376e::server:3629205ee179068917dc7dc1f951b1d9



### Setting up worker nodes

The worker nodes are bootstrapped in the following way:

	pi@rpi02:~ $ export K3S_URL="https://192.168.2.131:6443"

	pi@rpi02:~ $ export K3S_TOKEN="K100f8a8ac9aa5443597272dac3b637c1043d0556c8e5d51080a26e4681b564376e::server:3629205ee179068917dc7dc1f951b1d9"

	pi@rpi02:~ $ curl -sfL https://get.k3s.io | sh -


Once this is done for all 3 worker nodes you can check their connection status on the master node:

	pi@rpi01:~ $ sudo kubectl get nodes
	NAME    STATUS   ROLES                  AGE     VERSION
	rpi02   Ready    <none>                 3m40s   v1.20.2+k3s1
	rpi03   Ready    <none>                 3m5s    v1.20.2+k3s1
	rpi04   Ready    <none>                 2m34s   v1.20.2+k3s1
	rpi01   Ready    control-plane,master   51m     v1.20.2+k3s1



### Restart

In order to figure out if everything is working I now decided to shut down the cluster:

	pi@rpi01:~ $ sudo /usr/local/bin/k3s-killall.sh

Reboot all machines, switch to superuser/root on the master node with ``sudo -s`` and then restart the cluster:

	k3s server

One step I may have forgotten before is the following:

	export KUBECONFIG=/etc/rancher/k3s/k3s.yaml

Now let's check on the status:

	root@rpi01:/home/pi# kubectl get pods --all-namespaces
	NAMESPACE              NAME                                         READY   STATUS      RESTARTS   AGE
	kube-system            metrics-server-86cbb8457f-jsgvl              1/1     Running     0          8h
	kubernetes-dashboard   dashboard-metrics-scraper-7b59f7d4df-wldxt   1/1     Running     0          6h51m
	kube-system            local-path-provisioner-7c458769fb-xsnqb      1/1     Running     0          8h
	kube-system            coredns-854c77959c-k2gbc                     1/1     Running     0          8h
	kube-system            helm-install-traefik-dq9sl                   0/1     Completed   0          8h
	kubernetes-dashboard   kubernetes-dashboard-74d688b6bc-qc88x        1/1     Running     0          6h51m
	kube-system            svclb-traefik-wvrvr                          2/2     Running     0          4m29s
	kube-system            svclb-traefik-xvjs6                          2/2     Running     0          4m29s
	kube-system            svclb-traefik-fgjnp                          2/2     Running     0          4m29s
	kube-system            svclb-traefik-xz6mp                          2/2     Running     0          4m29s
	kube-system            traefik-6f9cbd9bd4-2zrbn                     1/1     Running     0          4m29s

Everything that hasn't worked before is now magically working!



### Kubernetes dashboard


	pi@rpi01:~ $ sudo kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml
	namespace/kubernetes-dashboard created
	serviceaccount/kubernetes-dashboard created
	service/kubernetes-dashboard created
	secret/kubernetes-dashboard-certs created
	secret/kubernetes-dashboard-csrf created
	secret/kubernetes-dashboard-key-holder created
	configmap/kubernetes-dashboard-settings created
	role.rbac.authorization.k8s.io/kubernetes-dashboard created
	clusterrole.rbac.authorization.k8s.io/kubernetes-dashboard created
	rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created
	clusterrolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created
	deployment.apps/kubernetes-dashboard created
	service/dashboard-metrics-scraper created
	deployment.apps/dashboard-metrics-scraper created
	pi@rpi01:~ $

Running this ``kubectl`` command creates both the Kubernetes dashboard service and deployment. It also creates a default service account, role, role binding and secret for the dashboard. Next we navigate to ``/etc/rancher/k3s/`` and create new directory for the dashboard configuration files:

	mkdir ~/dashboard && cd ~/dashboard

Then we create the following two resource manifest files:

``dashboard.admin-user.yml``


	apiVersion: v1
	kind: ServiceAccount
	metadata:
	  name: admin-user
	  namespace: kubernetes-dashboard


``dashboard.admin-user-role.yml``

	apiVersion: rbac.authorization.k8s.io/v1
	kind: ClusterRoleBinding
	metadata:
	  name: admin-user
	roleRef:
	  apiGroup: rbac.authorization.k8s.io
	  kind: ClusterRole
	  name: cluster-admin
	subjects:
	- kind: ServiceAccount
	  name: admin-user
	  namespace: kubernetes-dashboard

Then we deploy the admin-user configuration:

	root@rpi01:/etc/rancher/k3s/dashboard# kubectl create -f dashboard.admin-user.yml -f dashboard.admin-user-role.yml
	serviceaccount/admin-user created
	clusterrolebinding.rbac.authorization.k8s.io/admin-user created

Now that we've created the dashboard we can access it using ``kubectl``. To do this we will spin up a proxy server between our local machine and the Kubernetes apiserver:

	kubectl proxy

Once the proxy server has been started you should be able to access the dashboard from your browser. To access the HTTPS endpoint of dashboard go to:

	http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

Instead of ``kubectl proxy``, you can use`` kubectl port-forward`` and access dashboard with simpler URL than using ``kubectl proxy``.

	$ kubectl port-forward -n kubernetes-dashboard service/kubernetes-dashboard 8080:443

To access Kubernetes Dashboard go to:	

	https://localhost:8080

To sign into the dashboard we need to get the admin-user bearer token:

	kubectl -n kubernetes-dashboard describe secret admin-user-token | grep ^token



<center>
{{< figure src="/img/2021-01-19-rpi_cluster_02_os-ssh/kubernetes-dashboard.jpg" width="700px">}}
<p style="color:#989898"><small>
Spectrum of black-body with our Sun's temperature</small></p>
</center>








### Main links

https://www.puzzle.ch/de/blog/articles/2020/10/13/k3s-on-raspberry-pi
https://blog.alexellis.io/test-drive-k3s-on-raspberry-pi/
https://mpolednik.github.io/2020/09/27/proof-of-concept-kubernetes-cluster-on-raspberry-pi-using-k3s/
https://dev.to/bassonrichard/how-to-set-up-a-raspberry-pi-k3s-cluster-508
https://johansiebens.dev/posts/2020/08/argo-cd-for-your-private-raspberry-pi-k3s-cluster/
https://sysadmins.co.za/running-k3s-on-the-raspberrypi-4/


### Other links

https://ikarus.sg/kubernetes-with-k3s/
https://blog.alexellis.io/self-hosting-kubernetes-on-your-raspberry-pi/
https://blog.alexellis.io/raspberry-pi-homelab-with-k3sup/
https://alexellisuk.medium.com/walk-through-install-kubernetes-to-your-raspberry-pi-in-15-minutes-84a8492dc95a
https://kirkryan.co.uk/2020/05/24/how-to-k3s-on-raspberry-pi/
https://medium.com/icetek/building-a-kubernetes-cluster-on-raspberry-pi-running-ubuntu-server-8fc4edb30963
https://www.youtube.com/watch?v=B2wAJ5FLOYw
https://shawnliu.me/post/journey-with-kubernetes-1-kubernetes-rpi-cluster/
https://withblue.ink/2020/06/24/docker-and-docker-compose-on-raspberry-pi-os.html
https://opensource.com/article/20/6/kubernetes-raspberry-pi
https://github.com/codesqueak/k18srpi4
https://github.com/mhausenblas/kube-rpi
https://www.raspberrypi.org/software/
https://github.com/k3s-io/k3s-ansible
https://www.jeffgeerling.com/blog/2020/installing-k3s-kubernetes-on-turing-pi-raspberry-pi-cluster-episode-3
https://webme.ie/how-to-run-minikube-on-a-virtualbox-vm/
https://carlosedp.medium.com/building-a-hybrid-x86-64-and-arm-kubernetes-cluster-e7f94ff6e51d
https://sirchia.cloud/posts/kubernetes-on-64-bit-os-raspberry-pi-4/
https://shawnliu.me/post/journey-with-kubernetes-1-kubernetes-rpi-cluster/
https://github.com/mhausenblas/kube-rpi
https://www.hanselman.com/blog/how-to-build-a-kubernetes-cluster-with-arm-raspberry-pi-then-run-net-core-on-openfaas
https://github.com/codesqueak/k18srpi4
https://mirailabs.io/blog/building-a-microcloud/
https://vivekdhami.com/learnings/install-k3s-cluster-on-rpi/
https://lookslikematrix.de/raspberry-pi/2020/09/27/k3s.html




https://blog.tekspace.io/deploying-kubernetes-dashboard-in-k3s-cluster/
https://upcloud.com/community/tutorials/deploy-kubernetes-dashboard/
https://github.com/rancher/k3os/issues/535
https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md
https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/README.md
https://github.com/kubernetes/dashboard/blob/master/docs/user/accessing-dashboard/README.md
https://github.com/kubernetes/dashboard
https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/
https://kubernetes.io/docs/reference/access-authn-authz/rbac/
https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
https://blog.kstaykov.eu/devops/kubernetes-admin-user/
https://www.replex.io/blog/how-to-install-access-and-add-heapster-metrics-to-the-kubernetes-dashboard
https://www.liquidweb.com/kb/how-to-install-and-configure-the-kubernetes-dashboard/
https://upcloud.com/community/tutorials/install-kubernetes-cluster-centos-8/
https://admantium.medium.com/kubernetes-made-simple-with-k3s-4a39762fafb
https://medium.com/@rboulanouar/hands-on-k3os-k3s-cluster-5fe6c3497a1e
https://rancher.com/docs/k3s/latest/en/installation/kube-dashboard/