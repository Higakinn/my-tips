# [kubectl](https://kubernetes.io/ja/docs/reference/kubectl/_print/)-tips

## 該当リソースのラベルを確認

```shell
kubectl get ${resource_type} --show-labels
```

## cronjobから単発のjobを実行する

```shell
kubectl create job ${job_name} --from=cronjob/${cronjob_name}
```

## cronjobから定義している環境変数参照 (jq 利用)

```shell
kubectl get cronjob ${cronjob_name} -o json | jq .spec.jobTemplate.spec.template.spec.containers[0].env
```

## configファイルのマージ

```shell
KUBECONFIG=~/.kube/config:~/config kubectl config view --flatten
```

## replica数を変更する

```shell
kubectl patch deployment ${deploy_name} -p '{"spec":{"replicas": <replica-number>}}'
```

## serviceのtypeを変更

```shell
kubectl patch service ${svc_name} -p '{"spec":{"type":"<service-type>"}}'
```

## 該当deploymentのpod をsleep で 立ち上げ直す (sleep deploy)

```shell
kubectl patch deploy ${deploy_name} --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/command", "value": ["tail","-f","/dev/null"] }]'
```

## test デプロイメントを作成す (create test deployment)

```shell
kubectl create deployment ${deploy_name} --image=${docker_image_name} --replicas=${replicas}
```

## pod 再起動(rolling update)

```shell
kubectl rollout restart deployment ${deploy_name} 
```
