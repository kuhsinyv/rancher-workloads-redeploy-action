# rancher-workloads-redeploy-action
通过调用 Rancher API 来进行自动部署

## 必要配置
- 配置 Rancher [API keys](https://docs.rancher.cn/docs/rancher2.5/user-settings/api-keys/_index/)，注：不指定作用范围，有效期调整为 1 年。
- 配置工作负载 [对应标签](https://docs.rancher.cn/docs/rancher1/rancher-service/service-accounts/_index/)，注：如果工作负载已经部署，请使用升级功能。
- 记录工作负载所在项目的项目ID（一般是以所在集群名 `CLUSTER` 开头，后接冒号，冒号之后的即此 action 所需的环境变量 `PROJECT`）、命名空间 `NAMESPACE` 和工作负载名 `WORKLOAD`

## 示例
```yml
name: DEPLOY

on:
  push:
    branches:
      - main
    paths-ignore:
      - 'doc/**'

jobs:

  run:
    name: Deploy
    runs-on: ubuntu-18.04
    steps:

      - name: Redeploy
        uses: kuhsinyv/rancher-workloads-redeploy-action@v1.1
        env:
          API_ACCESS_ADDR: https://rancher.example.com/v1
          CLUSTER: local-example
          PROJECT: p-example
          NAMESPACE: namespace-example
          WORKLOAD: workload-example
          RANCHER_TOKEN: ${{ secrets.RANCHER_TOKEN }} # 之前配置的 Rancher API key
```
