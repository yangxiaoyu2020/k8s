## k8s集群的部署

#### 1. master節點的配置
```shell
kubeadm init --kubernetes-version=v1.14.1 --pod-network-cidr=10.244.0.0/16
// 初始化 指定k8s的版本，还有pod的虚拟ip的范围
```
```shell
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
kubernetes/admin.conf 核心配置文件
 - 集群的信息，master的节点ip
 - .kube/config
 - ***kubeadm join **master的节点ip** --token aoeout  --discovery-token-ca-cert-hash***

```shell
kubectl get nodes

STATUS NotReady 这里是
# 所有的节点
#查看存在问题的pod
kubectl get pod --all-namespaces
# Pending CrashLoopBackOff（创建失败。不蹲创建 代表硬件不行 增加CPU和内存会有好转）
#设置全局变量
#安装flannel网络组件
# 节点缺少 跨pod通信  pod 节点安装 proxy
# 默认使用flannel
# 通信协议
kubectl create -f kube-flannel.yml # 只要这个命令就好了 自动创建
```

```shell
kubectl get pod --all-namespaces
# 想在看STATUS是不是running

```
kubectl 集群的管理命令

#### 2. 加入master NODE节点
```shell
kubeadm join master的节点ip:port --token 911xit.xkp2gfxbvf5wuqz7 \
    --discovery-token-ca-cert-hash sha256:xxx
```
这个命令忘记的话，
```shell
kubtctl get nodes
kubeadm token list
```

如果忘记
在master 上执行kubeadm token list 查看 ，在node上运行
kubeadm join 192.168.163.132:6443 --token aoeout.9k0ybvrfy09q1jf6 --discovery-token-unsafe-skip-ca-verification

kubectl get nodes
#### 3. Master开启仪表盘
web ui dashboard 
```shell
kubectl apply -f kubernetes-dashboard.yaml
kubectl apply -f admin-role.yaml
kubectl apply -f kubernetes-dashboard-admin.rbac.yaml
kubectl -n kube-system get svc
http://xxxx 访问
```
