# TOI items
## Backend part
### meta API
- Github repo URL: https://github.com/gogovan/ggv-meta-api-service
- Current status
  - deployed in k8s
- Current deployment `branch` version: [v2.0.3](https://github.com/gogovan/ggv-meta-api-service/tree/release/v2.0.3)

### sample codes
- Github repo URL: https://github.com/gogovan/gogovan-gin-sample-codes
- Current status
  - stable
- Description: sample codes for gin framework. It's a good reference for the new project. For more information, please check the [README.md](https://github.com/gogovan/gogovan-gin-sample-codes/blob/main/README.md)

## Data engineering part
### gogobot-log-api
- Github repo URL: https://github.com/sary357/FastAPIDemo
- Current status:
  - v1: deprecated
  - v2: deployed on the computing engine
- Current `tag` version: [v0.3.0](https://github.com/sary357/FastAPIDemo/releases/tag/v0.3.0)
- Current codes deployed on the [computing engine](https://console.cloud.google.com/compute/instancesDetail/zones/asia-east1-a/instances/gogobot-log-api?project=gogox-data-science-non-prod)
- How can I access db? please refer to the [page](https://www.notion.so/Access-gogobot-log-db-only-for-GoGoBot-CS-plan-B-6f1b38ea492a491cbf27b676e66be5ed)
- DB username/password: Please logon computing engine and check the content of `/home/fuming_tsai/FastAPIDemo/docker-compose.yml`.
### flink
- Github repo URL: https://github.com/gogovan/gogovan-analytics-flink
- Current status: deployed
- Current `deployment branch`: master branch
- My understanding
  - [Data flow](https://console.cloud.google.com/dataflow/jobs?referrer=search&project=gogox-data-science-non-prod) -> flink -> [redis](https://console.cloud.google.com/memorystore/redis/locations/us-central1/instances/datateam/details/overview?project=gogox-data-science-non-prod)