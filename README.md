# jori-ap-deployment


## 環境構築
```sh 
# minikube上にnamespaceを作成
k create ns jori-local
# jori-localをdefaultに設定
kubectl config set-context --current --namespace=jori-local
# localで起動させたいときは、以下コマンド
k apply -k /k8s/overlay/local


# minikubeはexternalIpを持ってないっぽいので、minikubeコマンドで疎通させる
minikube service jori-localjori-ap-service-np-v1 -n jori-local

## 他PODから疎通させるとき　ドメインはサービスのIP
k run curl-temp --image=centos  --restart=Never --rm -it curl http://jori-localjori-ap-service-v1:80
```

## minikubeでローカルでビルドしたイメージを使いたいとき
[stackoverflowの記事](https://stackoverflow.com/questions/56392041/getting-errimageneverpull-in-pods)
```sh
# dockerfileをビルドする前に、minikubeが見えるlocalRegistryでbuildできるように設定
eval $(minikube docker-env)
# マニフェストのimagePullPolicyはneverにする　＝＞　localのイメージを使用

# build-image.shを起動

```