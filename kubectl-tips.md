# [kubectl](https://kubernetes.io/ja/docs/reference/kubectl/_print/)-tips

## 該当リソースのラベルを確認

```shell
kubectl get <resource-name> --show-labels
```

## cronjobから単発のjobを実行する

```shell
kubectl create job <job-name> --from=cronjob/<cronjob-name> 
```

## cronjobから定義している環境変数参照 (jq 利用)

```shell
kubectl get cronjob <cronjob-name> -o json | jq .spec.jobTemplate.spec.template.spec.containers[0].env
```

## configファイルのマージ

```shell
KUBECONFIG=~/.kube/config:~/config kubectl config view --flatten
```

## replica数を変更する

```shell
kubectl patch deployment <deployment-name> -p '{"spec":{"replicas": <replica-number>}}'
```

## serviceのtypeを変更

```shell
kubectl patch service <service-name> -p '{"spec":{"type":"<service-type>"}}'
```

## 該当deploymentのpod をsleep で 立ち上げ直す

```shell
kubectl patch deploy <deployment-name> --type='json' -p='[{"op": "add", "path": "/spec/template/spec/containers/0/command", "value": ["tail","-f","/dev/null"]  }]'
```

