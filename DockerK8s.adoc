= Cloud Native
:sectnums:
:toc: left

유 미 (takytaky@empas.com)

== 실습 환경 설정하기

. virtualbox 프로그램 설치 
. oracle virtualbox extension pack 설치 
. 가상 머신 가져오기(import)  ubuntu18.04
. 가상머신 통신 (네트워크 연결 상태 확인) 
. ssh 를 사용해서 linux(ubuntu) root 사용자로 로그인 허용 
[source, bash]
$ sudo gedit /etc/ssh/sshd_config
[sudo] password for worker1: ubuntu 
	#PermitRootLogin prohibit-password 
		--> PermitRootLogin yes 
$ sudo systemctl restart sshd 
$ ip addr 
	enp0s3 inet 192.168.137.101
	
. putty 터미널 사용연결 
[source, bash]
# cat  /etc/os-release 
	--> 실습 리눅스 버전 확인 

== 컨테이너 기반 기술 
=== chroot 실습 
[source, bash]
pwd (present working directory) : 사용자 현재 작업 디렉토리 확인 
mkdir (make directory) : 디렉토리 생성 
ls ( list ) : 디렉토리 목록 확인 

[source, bash]
 mkdir -p /root/newroot/{bin,lib,lib64}
 ls 
 apt install tree   (apt : advanced package tool,  패키지 설치 ) 
 tree .
 chroot  /root/newroot   /bin/bash 

[source, bash]
/   <------  /root/newroot
/bin/bash <----  /root/newroot/bin/bash 

[source, bash]
 cp /bin/bash    /root/newroot/bin/bash
 cp /bin/ls  /root/newroot/bin/ls
 mkdir /root/newroot/lib/x86_64-linux-gnu

[source, bash]
 cp  /lib/x86_64-linux-gnu/libtinfo.so.5   /root/newroot/lib/x86_64-linux-gnu/libtinfo.so.5
 cp /lib/x86_64-linux-gnu/libdl.so.2  /root/newroot/lib/x86_64-linux-gnu/libdl.so.2
 cp /lib/x86_64-linux-gnu/libc.so.6  /root/newroot/lib/x86_64-linux-gnu/libc.so.6
 cp /lib64/ld-linux-x86-64.so.2  /root/newroot/lib64/ld-linux-x86-64.so.2

[source, bash]
 cp /lib/x86_64-linux-gnu/libselinux.so.1  /root/newroot/lib/x86_64-linux-gnu/libselinux.so.1
 cp /lib/x86_64-linux-gnu/libc.so.6  /root/newroot/lib/x86_64-linux-gnu/libc.so.6
 cp /lib/x86_64-linux-gnu/libpcre.so.3 /root/newroot/lib/x86_64-linux-gnu/libpcre.so.3
 cp /lib/x86_64-linux-gnu/libdl.so.2  /root/newroot/lib/x86_64-linux-gnu/libdl.so.2
 cp /lib64/ld-linux-x86-64.so.2  /root/newroot/lib64/ld-linux-x86-64.so.2
 cp /lib/x86_64-linux-gnu/libpthread.so.0  /root/newroot/lib/x86_64-linux-gnu/libpthread.so.0

[source, bash]
 tree .
 chroot  /root/newroot   /bin/bash 

[source, bash]
su ( switch user ) : 사용자 전환/변경 
bash (shell) : 사용자에게 명령어 입력 프롬프트 출력 입력 
 ip netns del guestnet

=== Namespaces


=== Cgroups 실습 

[source, bash]
tar -zxvf docker_lab.tgz
term 2 # top   ( CPU많이 사용하는 순으로 프로세스를 정렬 출력)

[source, bash]
term 1#  cd docker_lab
term 1#  ./a.out & 
term 1#  ./b.out & 
term 1# cd /sys/fs/cgroup/cpu
term 1# mkdir limit_50_percent 
term 1# cd limit_50_percent 
term 1# echo 3661 > tasks

[source, bash]
term1 # echo $(pgrep a.out) > tasks
term 1# cat tasks 
term 1# echo 512 > cpu.shares

[source, bash]
자원의 경쟁(경합) 가중치 
a.out   b.out 
1024  1024 
1 (50%)    :     1  (50%)
term 1# pkill b.out 
term 1# pkill a.out 

=== Overlay 실습 

[source, bash]
mkdir overlayfs
cd overlayfs
mkdir container image1 image2 image3 work merge

[source, bash]
echo Hello, world > image1/a
echo Hello, docker > image1/b
echo Hello, yumi > image2/c
mount -t overlay  overlay -o lowerdir=image2:image1,upperdir=container,workdir=work    merge

[source, bash]
cat merge/a
Hello, world
cat merge/b
Hello, docker
cat merge/c
Hello, yumi
echo Good bye > merge/a
cat merge/a
Good by

[source, bash]
echo Good night > merge/d
rm merge/b

== Docker
=== Installation
==== using script
[source, bash]
curl -fsSL https://get.docker.com -o install.sh
less install.sh
chmod +x install.sh 
install.sh 

==== using apt-get
[source, bash]
uname -r #check the version
cat /etc/os-release
NAME="Ubuntu"
VERSION="18.04.5 LTS (Bionic Beaver)"

[source, bash]
apt-get update    
sudo apt-get install -y  apt-transport-https ca-certificates curl software-properties-common
https를 사용해서 레포지토리를 사용할 수 있도록 필요한 패키지를 설치한다. 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
Docker 공식 리포지토리에서 패키지를 다운로드 받았을때 위변조 확인을 위한 GPG 키를 추가한다.
apt-key fingerprint
/etc/apt/trusted.gpg
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
Docker.com 의 GPG 키가 등록됐는지 확인한다. 
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
Docker 공식 저장소를 리포지토리로 등록한다.
grep docker /etc/apt/sources.list
deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable
저장소 등록정보에 기록됐는지 확인한다. 
apt-get update    
리포지토리 정보를 갱신
apt-get install -y docker-ce
docker container engine 을 설치한다.

[source, bash]
vim /etc/apt/sources.list #오타 수정 

=== Managing Docker Service
[source, bash]
systemctl status docker 
systemctl enable docker  --> docker 를 시스템 부팅 시 자동 실행 
systemctl restart docker 
systemctl stop docker 
systemctl start docker 

=== Running Container
==== Interactive
[source, bash]
docker container run -it --name c1 centos /bin/ping localhost

==== Detached
[source, bash]
docker container run -d --name web httpd
docker container logs web
docker container exec -it web /bin/bash

[source, bash]
docker container inspect web | grep IPAddr
curl -sf http://172.17.0.3

==== Copy
[source, bash]
docker container cp hostfile  test00:/containerfile
docker container exec test00  cat /containerfile
docker container cp test00:/containerfile    hostfile

==== 모든컨테이너 일괄 삭제하기 
[source, bash]
alias conrm='docker container rm -f $(docker container ps -aq)'

==== docker container diff 실습
[source, bash]
docker container run -it --name test01  centos
docker container inspect test01 | grep -C2 UpperDir

==== Volume


==== Networking
[source, bash]
docker container run -d --name web1 -p 8080:80 nginx
docker container run -d --name web2 -p 8181:80 nginx

[source, bash]
docker container inspect web1 | grep IPAddr
                  "IPAddress": "172.17.0.2",
docker container inspect web2 | grep IPAddr
                  "IPAddress": "172.17.0.3",

[source, bash]
echo "This is web1 server" > index.html
docker container cp index.html  web1:/usr/share/nginx/html/index.html

[source, bash]
echo "This is web2 server" > index.html
docker container cp index.html web2:/usr/share/nginx/html/index.html

[source, bash]
curl -sf http://172.17.0.2
This is web1 server
This is web2 server

[source, bash]
web browser 
http://192.168.137.101:8080
http://192.168.137.101:8080

[source, bash]
docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
5db7f0b30b02   bridge    bridge    local
515d21ee2b86   host      host      local
fc133b3066a6   none      null      local

[source, bash]
docker network inspect bridge

[source, bash]
docker container run -it --name host00 --net host centos
docker container run -it --name none00 --net none centos

=== Image Management
==== Push
[source, bash]
docker login
docker image tag busybox jonggun/busyimage:1.0 
docker image push jonggun/busyimage:1.0 
docker image rm jonggun/busyimage:1.0 
docker logout

==== Creating images from containers
[source, bash]
docker rm -f $(docker ps -aq)
echo Hello, World > index.html
docker run -it --name sample ubuntu
touch /data.out
ctrl+PQ
docker container cp index.html sample:/usr/share/nginx/index.html
docker container commit -a "Comment" -m "message" sample jonggun/web00:1.0
docker run -it --name test jonggun/web00:1.0

==== Creating Images from script
[source, bash]
 cd 
 tar -zxvf docker_lab.tgz 
 cd docker_lab/dockerfile_dir 
 pwd
/root/docker_lab/dockerfile_dir
 cat Dockerfile.1 
FROM ubuntu
RUN  apt-get update && apt-get install -y -q nginx
COPY index.html /var/www/html/
CMD ["nginx", "-g", "daemon off; " ]
docker build -t web00:1.0 -f Dockerfile.1  .
docker image ls

[source, bash]
nano Dockerfile.1
FROM ubuntu
RUN  apt-get update && apt-get install -y -q nginx && rm -rf  /var/lib/apt/lists/*
COPY index.html /var/www/html/
CMD ["nginx", "-g", "daemon off; " ]

[source, bash]
docker build -t web00:2.0 -f Dockerfile.1  .
docker image ls 
docker image inspect centos 

[source, bash]
nano Dockerfile.7 
 FROM centos:7
 ENV myName “Yu Mi”
 ENV myOrder Pizza Pasta Salad
 ENV myNumber 1004
docker build -t env00 -f Dockerfile.7 .     
docker run -it env00
	[root@e251996adf58 /]# env
[source, bash]
nano Dockerfile.10
FROM centos:7
LABEL maintainer "Yu Mi <yumi@example.com>"
LABEL title "TEST Image"
LABEL version 1.0
LABEL description "This image is test image ^__^"

[source, bash]
docker build -t label00 -f Dockerfile.10  .
docker image inspect label00

[source, bash]
cat Dockerfile.11
FROM nginx
EXPOSE 443
docker build -t port00 -f Dockerfile.11 .
docker run -d -p 8080:443 port00
docker ps -a

[source, bash]
cat Dockerfile.13
FROM ubuntu
ADD host.html  /first_dir/
ADD host.html  /first_dir/secondfile
ADD https://github.com/kubernetes/kubernetes/blob/master/LICENSE /first_dir/
ADD webdata.tar /first_dir/
docker build -t add00 -f Dockerfile.13 .
docker run -it add00 

[source, bash]
cat Dockerfile.15
FROM ubuntu
VOLUME /container
docker build -t volume00 -f Dockerfile.15 .
docker run -it volume00
docker ps -a
docker container inspect admiring_black
        "Mounts": [
            {
                "Type": "volume",
                "Name": "7a03c4dacae697515069000c969e426e68013c0a782d9e0f6c3ab10a12682016",
                "Source": "/var/lib/docker/volumes/7a03c4dacae697515069000c969e426e68013c0a782d9e0f6c3ab10a12682016/_data",
                "Destination": "/container",
                "Driver": "local",

== Kubernetes
=== Installation
==== Check & Set Environment
[source, bash]
free  : 메모리(RAM)  사이즈 확인 
cat /proc/cpuinfo : cpu core 수 확인 
hostnamectl set-hostname  master
hostname
nano  /etc/hosts 
	192.168.137.101     master 
	192.168.137.102     worker1 
	192.168.137.103	worker2
docker rm -f $(docker ps -aq)
poweroff

NOTE: 각 노드에 "root" 로 바로 로그인이 안되요.?
[source, bash]
su - root 
Password : ubuntu 
nano  /etc/ssh/sshd_config
	PermitRootLogin yes
systemctl restart sshd 

NOTE:  kubelet, kubeadm, kubectl 버전 설치를 잘못했어요.???
[source, bash]
dpkg -l | grep kubelet
[ master  / worker1  / worker2 ]
apt-get remove -y kubelet kubeadm kubectl 
apt-get install -y kubelet=1.21.0-00 kubeadm=1.21.0-00 kubectl=1.21.0-00

NOTE: kubeadm join 인증 토큰 정보를 다시 확인하고 싶어요???
[source, bash]
kubeadm token list
	TOKEN                     TTL         EXPIRES                USAGES                   DESCRIPTION                                                EXTRA GROUPS
	ga3z3w.do18bjndzxtafs6g   23h         2022-02-18T00:55:16Z   authentication,signing   The default bootstrap token generated by 'kubeadm init'.   system:bootstrappers:kubeadm:default-node-token
	# openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'
	3a01e1f260788d3c69b2d09cc7373f5937702f6822a6778bb3b350bfde585596
kubeadm join 192.168.137.101:6443 --token ga3z3w.do18bjndzxtafs6g \
        --discovery-token-ca-cert-hash sha256:3a01e1f260788d3c69b2d09cc7373f5937702f6822a6778bb3b350bfde585596
worker1, worker2
accepts at most 1arg, received........
nano token.sh 
	sha256:   
timeout error 
kubeadm reset 
./token.sh 
kubectl get nodes 
 192.168.137.101:6443

=== kubectl 자동 완성 기능 설정 
[source, bash]
echo "source <(kubectl completion bash)" >> ~/.bashrc
tail -1 ~/.bashrc
source <(kubectl completion bash)
source ~/.bashrc
root@192.168.
kubernetes-admin@kubernetes
                             클러스터계정@(클러스터 이름)

=== Running 
[source, bash]
watch -n 1 kubectl get pods -o wide
cd ~/k8s_lab/pod
kubectl apply -f app.yaml 
kubectl delete pod app
kubectl delete -f app.yaml

=== cpu 자원 할당 실습 
NOTE:  /root/k8s_lab/pod/pod-resources

[source, bash]
cat cpu-request-limit.yaml
kubectl create namespace cpu-example 
terminal 2 #  watch -n 1 kubectl get pods -n cpu-example -o wide
kubectl apply -f cpu-request-limit.yaml
worker2 # docker stats   <-- 컨테이너별 자원 사용 현황 
kubectl delete pod cpu-demo -n cpu-example

[source, bash]
cat cpu-request-limit-2.yaml
kubectl apply -f cpu-request-limit-2.yaml
kubectl delete pod cpu-demo-2 -n cpu-example
kubectl delete ns cpu-example
kubectl get ns

=== memory 자원 할당 실습 
[source, bash]
cat memory-request-limit.yaml
terminal 2 #  watch -n 1 kubectl get pods -n mem-example -o wide
kubectl create namespace mem-example 
kubectl apply -f memory-request-limit.yaml
cat memory-request-limit-2.yaml
kubectl apply -f  memory-request-limit-2.yaml
kubectl delete pod -n mem-example --all
kubectl delete ns mem-example 

=== initContainer 실습
NOTE: /root/k8s_lab/pod

[source, bash]
cat pod-init.yaml 
terminal 2 #  watch -n 1 kubectl get pods -o wide
kubectl apply -f pod-init.yaml
kubectl delete pod init-demo
nano pod-init.yaml 
    image: takytaky/app:v1   <--- 3군데 수정 
kubectl delete pod init-demo
kubectl apply -f init-containers.yaml 
curl -sf http://172.16.189.68

=== 스태틱 파드 실습 (85)
실습은 worker1 에서 진행 

[source, bash]
tar -zxvf k8s_lab.tgz 
mkdir /etc/static.d 
cp ~/k8s_lab/pod/app.yaml   /etc/static.d 
ls /etc/static.d
app.yaml
nano /var/lib/kubelet/config.yaml 
staticPodPath: /etc/static.d
systemctl restart kubelet 
rm /etc/static.d/app.yaml
systemctl restart kubelet

=== 레이블 & 셀렉터 실습 
[source, bash]
cat deploy-label01.yaml
 template:
    metadata:
      labels:
        app: nodejs
        environment: develop
        release: beta
kubectl apply -f deploy-label01.yaml -f deploy-label02.yaml -f deploy-label03.yaml -f deploy-label04.yaml
kubectl get pods --show-labels
label-app01-84878f9646-4h4l7      app=nodejs,environment=develop,release=beta
label-app02-7fc7b7c9f6-bdz6l       app=nodejs,environment=production,release=beta
label-app03-65489bd79c-g7bb2     app=nodejs,environment=develop,release=stable
label-app04-5cfd679cbc-z42bz       app=nodejs,environment=production,release=stable
실습 내용 삭제 
kubectl delete deploy --all
kubectl delete pod --all

=== 노드셀렉터(87)
[source, bash]
kubectl get nodes --show-labels
kubectl label nodes worker1 disk=ssd
kubectl get nodes --show-labels
cat nodeselector.yaml
kubectl delete deploy --all
kubectl delete pod --all
kubectl apply -f nodeselector.yaml
kubectl label nodes worker1 disk-
kubectl get nodes --show-labels

=== 애노테이션 실습 
[source, bash]
kubectl apply -f annotation.yaml
kubectl describe deploy annotation-nodejs
kubectl delete deploy --all
kubectl delete pod --all

=== load balancing
LoadBalancer Type의 서비스 구성하기
[source, bash]
59.29.225.193
http://59.29.224.86   <---
kubectl create namespace metallb-system 
kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.8.3/manifests/metallb.yaml
kubectl get pods -n metallb-system
vi metallb_test.yaml
	apiVersion: v1
	kind: ConfigMap
	metadata:
	namespace: metallb-system
	name: config
	data:
	config: |
		address-pools:
		- name: my-ip
		protocol: layer2
		addresses:
		- 10.0.2.200-10.0.2.209
kubectl apply -f metallb_test.yaml
kubectl delete svc nodeport-hostname-service
vi  loadbalancer.yaml
	apiVersion: v1
	kind: Service
	metadata:
	name: loadbalancer-hostname-service
	spec:
	type: LoadBalancer
	selector:
		app: hostname-server          <---- 수정 
	ports:
	- protocol: TCP
		port: 80              <--- 수정 
		targetPort: 80
kubectl apply -f loadbalancer.yaml 

=== 레플리케이션 컨트롤러 vs 레플리카셋 
* 지정한 후의 복제본 파드가 지속적으로 실행 유지 

* 레플리케이션 컨트롤러(x)
** 롤링 업데이트 지원 
** 등호기반 셀렉터 
* 레플리카셋 (+디플로이먼트)
** 등호기반 셀렉터 + 집합 기반 셀렉터 (유연한 선택)
** 롤링 업데이트 지원안함 ---> 디플로이먼트

[source, bash]
실습 디렉토리 
cd ~/k8s_lab/controller/replicaset/
cat rs-nginx.yaml 
terminal 2 # # watch -n 1 kubectl get rs,pods -o wide
kubectl apply -f rs-nginx.yaml
kubectl get pods --show-labels
kubectl delete pod rs-nginx-stv2q
kubectl scale rs rs-nginx --replicas=5
kubectl scale rs rs-nginx --replicas=3
kubectl delete rs rs-nginx

=== 디플로이먼트 실습 
[source, bash]
실습 디렉토리 
/root/k8s_lab/controller/deployment
Deployment
	--> Replicaset (replicas, selector, template)
		--> pod 
			--> containers
cat deploy-nginx.yaml
terminal 2 # watch -n 1 kubectl get deploy,rs,pods -o wide
kubectl apply -f deploy-nginx.yaml
kubectl scale deploy deploy-nginx --replicas=5
kubectl scale deploy deploy-nginx --replicas=3

=== deployment rollout 실습
. kubectl set image deploy deploy-nginx deploy-nginx=nginx:1.16.0
. 기본 문서 편집기 nano 수정 
[source, bash]
export EDITOR=/bin/nano 
kubectl edit deploy deploy-nginx
kubectl apply -f deploy-nginx.yaml

=== deployment undo 실습 (17 --> 16 --> 18 --> 19) 
[source, bash]
 kubectl rollout history deploy deploy-nginx
 kubectl rollout history deploy deploy-nginx --revision=2
 kubectl rollout undo deploy deploy-nginx
 kubectl rollout history deploy deploy-nginx --revision=2
 kubectl rollout undo deploy deploy-nginx --to-revision=2
 kubectl delete rs deploy-nginx-5c5dc7b4f8
 kubectl delete rs deploy-nginx-6f69f97599
 kubectl rollout history deploy deploy-nginx
 kubectl describe node master
kubectl delete deploy deploy-nginx

=== 데몬셋 실습 
[source, bash]
/root/k8s_lab/controller/daemonset
terminal 2 # watch -n 1 kubectl get daemonset,rs,pods -o wide
kubectl apply -f daemonset-app.yaml
nano daemonset-app.yaml 
kubectl apply -f daemonset-app.yaml
kubectl get daemonset daemonset-app -o yaml 
nano daemonset-app.yaml 
kubectl apply -f daemonset-app.yaml
kubectl delete pod daemonset-app-sb8db
kubectl delete daemonset daemonset-app

=== clusterip 서비스 실습 
[source, bash]
/root/k8s_lab/service
cat hostname-server.yaml
kubectl apply -f hostname-server.yaml
terminal 2# watch -n 1 kubectl get svc,deploy,pods -o wide
nano clusterip-hostname.yaml 
kubectl apply -f clusterip-hostname.yaml
curl -sf http://10.98.68.96 | grep Hello
curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-kq82z</p> </blockquote>
curl -sf http://10.98.68.96 | grep Hello
curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-pww22</p> </blockquote>
kubectl delete pod hostname-server-7c85cc96dc-pww22
curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-rrtfb</p> </blockquote>
curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-kq82z</p> </blockquote>
curl -sf http://10.98.68.96 | grep Hello
    <p>Hello,  hostname-server-7c85cc96dc-pww22</p> </blockquote>
kubectl delete pod hostname-server-7c85cc96dc-pww22
curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-rrtfb</p> </blockquote>
# curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-kq82z</p> </blockquote>
iptables -t nat -S | grep hostname-service
kubectl scale deploy hostname-server --replicas=3
curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-kq82z</p> </blockquote>
# curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-rb8tf</p> </blockquote>
# curl -sf http://10.98.68.96 | grep Hello
        <p>Hello,  hostname-server-7c85cc96dc-rrtfb</p> </blockquote>

=== 블루 그린 배포 
[source, bash]
cd deploy_blue_green/
cat deploy-blue.yaml 
kubectl apply -f deploy-blue.yaml
blue 
        app: deploy-blue
        release: stable
cat blue-green-svc.yaml
kubectl apply -f blue-green-svc.yaml
http://192.168.137.101:30880 
cat deploy-green.yaml
green 
       app: deploy-green
        release: stable
nano blue-green-svc.yaml
  selector:
    app: deploy-blue 
		--> green
kubectl apply -f blue-green-svc.yaml
kubectl delete deploy deploy-blue
kubectl delete svc blue-green-svc
kubectl delete deploy deploy-green
kubectl delete deploy deploy-blue 

=== 카나리 배포 
[source, bash]
pwd
/root/k8s_lab/controller/deployment/deploy_canary
kubectl apply -f deploy-blue.yaml
blue 
	app=webapp,release=stable
kubectl apply -f deploy-canary.yaml
canary 
	 app=webapp,release=beta
kubectl apply -f blue-canary-svc.yaml
curl -sf http://192.168.137.101:30880 | grep Deploy
        <p> This is BLUE Deployment. </p>
curl -sf http://192.168.137.101:30880 | grep Deploy
        <p> This is Canary Deployment. </p>
nano blue-canary-svc.yaml  
selector:
    app: webapp
	--> release: beta
kubectl apply -f blue-canary-svc.yaml
curl -sf http://192.168.137.101:30880 | grep Deploy
        <p> This is Canary Deployment. </p>
curl -sf http://192.168.137.101:30880 | grep Deploy
        <p> This is Canary Deployment. </p>
kubectl delete deploy --all 
kubectl delete svc blue-canary-svc 

=== hostpath 실습 
[source, bash]
/root/k8s_lab/volume
kubectl apply -f hostpath.yaml
kubectl exec -it hostpath-pod -- /bin/bash
	root@hostpath-pod:/# cp /app.js    /poddir
	root@hostpath-pod:/# ls /poddir
	app.js
worker1 (pod가 실행된 워커 노드에서 실행 ) # ls /mnt
app.js

=== pv와 pvc 실습 
[source, bash]
/root/k8s_lab/volume
terminal 2 # watch -n 1 kubectl get pv,pvc,pods -o wide
cat pv.yaml 
kubectl apply -f pv.yaml
cat pvc.yaml
kubectl apply -f pvc.yaml
cat deploy-pvc.yaml
kubectl apply -f deploy-pvc.yaml
kubectl exec -it volume-pod-58dfbd6667-fbzsf -- /bin/bash
	root@volume-pod-58dfbd6667-fbzsf:/# ls /tmp
	app.log
worker2 (pod 가 스케쥴된 워커노드에서 실행) 
  tail -f /mnt/k8s-pv/app.log
pod (/tmp)
	worker2 (/mnt/k8s-pv )

.반환정책 
[source, bash]
kubectl delete deploy volume-pod
kubectl delete pvc pvc
kubectl apply -f pvc.yaml

.pv초기화 
[source, bash]
kubectl delete pv pv
kubectl apply -f pv.yaml
kubectl cordon worker1 
kubectl get node
kubectl uncordon worker2
kubectl get node

== Useful Unix Commands
[source, bash]
watch -n 1 docker container ps -a

[source, bash]
tar -zxvf k8s_lab.tgz

[source, bash]
scp root@192.168.137.101:/root/docker_lab.tgz   .
scp root@192.168.137.101:/root/k8s_lab.tgz   .

=== Fixed IP
[source, bash]
hostnamctl set-hostname  worker1
hostname 
cd /etc/netplan
nano 00-installer-config.yaml
	192.168.137.101  ---> 192.168.137.102
 netplan apply 