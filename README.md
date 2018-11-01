# traefik-ingress

## 创建自定义域名证书并以secret方式存储在K8S中供pod使用
- kubectl create secret generic traefik-cert --from-file=/etc/kubernetes/ssl/test.zhangling.link.cer --from-file=/etc/kubernetes/ssl/test.zhangling.link.key 
- 注意: 创建secret前，需要自己准备好证书文件，如果有多个域名证书，可以在上述命令行增加--from-file=
## 创建traefik配置文件，并以configmap方式存储在K8S中供POD使用
- kubectl create configmap traefik-conf --from-file=/config/traefik.toml -n kube-system
- 注意: 创建configmap前需要在k8s master机器中存在/config/traefik.toml

## 创建traefik服务
- kubectl create -f rbac.yaml -f traefik.yaml -f ingress.yaml

## 创建自己的后端服务并测试
- kubectl create -f nginx/nginx.yaml
- 注意： 创建之前修改nginx.yaml Ingress里面的host
