# gcloud-tips

## cloud dns 一覧取得

```bash
gcloud dns record-sets list --zone=<zone名>
```

## cloud dns 更新(全部書き換える)

```shell
gcloud dns record-sets update <FQDN> --rrdatas=<IPアドレス> --type=A --ttl=30 --zone=<zone名>
```