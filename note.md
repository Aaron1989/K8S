**安装参考文档：**

http://blog.csdn.net/zjysource/article/details/52086835

http://www.cnblogs.com/softlin/p/5675890.html


**网络环境：**

1）办公室直接桥接

2）家里需要指定可用，并修改kuber配置文件ip


**master：**

192.168.30.247||192.168.1.10（docker-1）

配置文件：/etc/etcd/etcd.conf、/etc/kubernetes/config、/etc/kubernetes/apiserver

**node：**

192.168.30.245||192.168.1.20（docker-2）

配置文件：/etc/etcd/etcd.conf、/etc/kubernetes/config、/etc/kubernetes/kubelet



**重点：**

1）pod=容器集合（docker images）

2）deployment=进程、服务（docker ps）

3）pod一旦绑定到一个节点，Pod 将永远不会重新绑定到另一个节点

4）控制器可以自愈，pod不行

5）ReplicationController是用来控制pods数量，动态保持replicas个
服务发现：环境变量和DNS

**探针：**

1）Liveness：许多长时间运行的应用程序最终会转换到broken状态，除非重新启动，否则无法恢复。Kubernetes提供了liveness probe来检测和补救这种情况

2）readiness：确保流量无法到达未准备好的容器

请注意，我们不直接删除 pod。使用 kubectl 命令，我们要删除拥有该 pod 的 Deployment。如果我们直接删除pod，Deployment 将会重新创建该 pod。


**K8S secret：**

http://www.jianshu.com/p/fd13c2762d81

好处（避免）：

1）集群每个node都需要docker login一下，生产config.json

2）k8s的pod都是对应node去拉取镜像的
创建secret：
create secret docker-registry aliyun --docker-server=registry.cn-qingdao.aliyuncs.com --docker-username=xx --docker-password=xxx --docker-email=xx

secret查看：
kubectl get secret


ui启动命令（master上操作）：
kubectl -s 192.168.30.247:8080 create -f  /home/dingqishi/kube-ui/kube-ui.yml
查询命令：
kubectl get pods --all-namespaces
kubectl describe pods/kubernetes-dashboard-3574298429-zzk75 --namespace="kube-system”
kubectl describe service/kubernetes-dashboard --namespace="kube-system”

查看kubectl版本：
kubectl —version


kubectl cluster-info
kubectl cluster-info dump
查看pods：
kubectl get pod  -o wide  --all-namespaces

查看pod详情：
kubectl get pod  <NAME> -o wide
kubectl get pods/podename -o yaml

查看pod日志：
kubectl describe pods/kubernetes-dashboard-3574298429-zzk75 --namespace="kube-system”

查看nodes：
kubectl get nodes

查看Replication Controller：
kubectl get rc

查看kind=deployment的应用状态：
kubectl get deployment  -o wide  --all-namespaces

查看namespace：
kubectl get ns

查询挂载情况：
kubectl get pvc

查询statefulset：
kubectl get statefulset

指定节点运行容器：
kubectl -s 192.168.2.143:8080 create -f namespace.yaml  

删除特定的deployment：
kubectl delete deployment <NAME> -n <NAMESPACE>

删除异常状态的pod：
kubectl delete -f kuber-dashboard-svc.yaml

deployment扩容：
kubectl scale deployment nginx-deployment --replicas 3

deployment自动扩容：
kubectl autoscale deployment nginx-deployment --min=10 --max=15 --cpu-percent=80

回滚：
kubectl rollout undo deployment/nginx-deployment


Node管理：

禁止pod调度到该节点上
kubectl cordon <node>

驱逐该节点上的所有pod
kubectl drain <node>

