**学习文档：**
https://jimmysong.io/kubernetes-handbook/

![这里写图片描述](http://avatar.csdn.net/2/D/B/3_itmyhome.jpg)

**常用命令**：

**查看nodes**-
kubectl get nodes

**查看namespace**- kubectl get ns

**查看Replication Controller**- kubectl get rc

**查看secret**- kubectl get secret

**查看挂载情况**- kubectl get pvc

**查看statefulset**- kubectl get statefulset

**查看kubectl版本**- kubectl —version

**查看集群状态**- kubectl cluster-info；kubectl cluster-info dump

**查看pods**- kubectl get pod  -o wide  --all-namespaces

**查看pod详情**- kubectl get pod  <NAME> -o wide；kubectl get pods/podename -o yaml

**查看指定pod的日志**- kubectl describe pods/kubernetes-dashboard-3574298429-zzk75 --namespace="kube-system”

**查看kind=deployment的应用状态**- kubectl get deployment  -o wide  --all-namespaces

**指定节点运行容器** kubectl -s 192.168.2.143:8080 create -f namespace.yaml  

**删除特定的deployment**- kubectl delete deployment <NAME> -n <NAMESPACE>

**删除异常状态的pod：** - kubectl delete -f kuber-dashboard-svc.yaml

**deployment扩容：**- kubectl scale deployment nginx-deployment --replicas 3

**deployment自动扩容**- kubectl autoscale deployment nginx-deployment --min=10 --max=15 --cpu-percent=80

**回滚：**- kubectl rollout undo deployment/nginx-deployment

**进入容器操作**- kubectl exec -it mysql-478535978-1dnm2 sh

**Node管理：**

**禁止pod调度到该节点上** - kubectl cordon <node>

**驱逐该节点上的所有pod** - kubectl drain <node>

