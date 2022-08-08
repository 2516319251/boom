1. 安装 docker

```shell
# 安装 docker
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

2. 安装 minikube [(官方文档)](https://minikube.sigs.k8s.io/docs/start/)

```shell
# 获取安装包
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# 安装
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# 查看版本
minikube version
```

3. 使用 minikube 安装 kubectl
```shell
# 安装
minikube start --kubernetes-version=v1.23.3 --image-mirror-country='cn' --force

# 查看状态
minikube status

# 查看节点
minikube node list

# 查看版本
minikube kubectl -- version 
```

4. 设置别名简化命令
```shell

# 设置别名
echo alias kubectl=\"minikube kubectl -- \" >> .bashrc

# 等同 `minikube kubectl -- version`
kubectl version

# 创建对象
kubectl run ngx --image=nginx:alpine

# 查看
kubectl get pod

# 外网可访问 ui 界面
kubectl proxy --address='0.0.0.0' --disable-filter=true
```

5. yaml 文件
```shell
# 查看当前 Kubernetes 版本支持的所有对象
minikube kubectl -- api-resources

# 显示出详细的命令执行过程和发出的 HTTP 请求
minikube kubectl -- get pod --v=9

# 查看 对象字段的详细说明
minikube kubectl -- explain pod
minikube kubectl -- explain pod.metadata
minikube kubectl -- explain pod.spec
minikube kubectl -- explain pod.spec.containers

# 生成一个 Pod 的 YAML 样板示例
minikube kubectl -- run ngx --image=nginx:alpine --dry-run=client -o yaml >> ngx.yml

# 创建对象，如果已存在会更新配置
minikube kubectl -- apply -f ngx.yml

# 删除对象
minikube kubectl -- delete -f ngx.yml
```
