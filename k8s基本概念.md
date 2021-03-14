## k8s 基本概念

### **pod** 每个pod都有独立的虚拟ip
  - pause
    - 提供共享的网络空间
    - 提供共享的挂载卷
  - user containter1
  - user containter1
### **service** pod与其他pod的通信机制

### label 标签 每个pod的别名
### replication Controller 对pod进行监控，数量，活动。
### service 服务
### node 节点
  - 每个节点 安装

    * kubelet
    * kube-proxy 不同的主机通信，代理转接pod中的通信
    * docker 这个啥说的

### kubernetes master 主节点
