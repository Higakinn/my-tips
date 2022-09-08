<<<<<<< HEAD
# kubectl-tips
=======
# [kubectl](https://kubernetes.io/ja/docs/reference/kubectl/_print/)-tips
>>>>>>> 0870ba606d5932bd1c0108659b8184e23118a666

<<<<<<< HEAD
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

## cronjob manifest

```shell
kubectl create cronjob crontest --image=nginx --schedule='0 12 * * *' --dry-run=client  -o json
```

## バージョン確認 (check kubectl version)

```shell
kubectl version
```

## 該当リソースのラベルを確認 (show k8s label)

```shell
kubectl get ${resource_type} --show-labels
```

## cronjobから単発のjobを実行する (create job from cronjob)

```shell
kubectl create job ${job_name} --from=cronjob/${cronjob_name}
```

## cronjobから定義している環境変数参照 (get cronjob env using jq command)

```shell
kubectl get cronjob ${cronjob_name} -o json | jq .spec.jobTemplate.spec.template.spec.containers[0].env
```

## configファイルのマージ (merge kube config)

```shell
KUBECONFIG=~/.kube/config:~/config kubectl config view --flatten
```

## replica数を変更する (patch k8s replica num)

```shell
kubectl patch deployment ${deploy_name} -p '{"spec":{"replicas": <replica-number>}}'
```

## 該当deploymentのpod をsleep で 立ち上げ直す (sleep pod deploy)

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

## k8s service typeを変更する (change k8s service type)

```shell
kubectl patch service <service-name> -p '{"spec":{"type":"<service-type>"}}'
```

## k8s deploymentで利用している image 変更する (change image)

```shell
kubectl patch deployment ${deployment_name} -p '{"spec":{"template":{"spec":{"containers":[{"name":"'${container_name}'","image":"'${image_name}'"}]}}}}'
```

## k8s cronjob を一時停止する (patch k8s cronjob suspend true)

```shell
kubectl patch cronjob $cronjob_name -p '{ "spec": { "suspend": true } }'
```

## プライベートリポジトリから image を Pull するためのsecretを作成 (k8s secret regcred)

```shell
kubectl create secret regcred --docker-server=$registry_server --docker-username=$docker_user_name --docker-password=$docker_password --docker-email=$docker_email 
```

## ファイルから作成した configmapを更新

```shell
kubectl create configmap $configmap_name --from-file=$config_file_path -o yaml --dry-run | kubectl apply -f-
```