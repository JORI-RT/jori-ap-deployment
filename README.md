# jori-ap-deployment


## 環境構築
```sh 
# minikube上にnamespaceを作成
k create ns jori-local
# jori-localをdefaultに設定
kubectl config set-context --current --namespace=jori-local
# localで起動させたいときは、以下コマンド
k apply -k /k8s/overlay/local
# 疎通させるときは、
NODE_PORT ->　k describe svc/svc_name | grep -i NodePort
NODE_IP -> k describe node | grep -i ip
curl $NODE_IP:$NODE_PORT
```