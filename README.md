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
### superset
- Just keep in mind: Someone from business team may need to access superset. Please help them to create an account.
- Github repo URL: https://github.com/gogovan/incubator-superset (We have our own customized version)

### gogobot-log-api
- Github repo URL: https://github.com/sary357/FastAPIDemo
- Current status:
  - v1: deprecated
  - v2: deployed on the computing engine
- Current `tag` version: [v0.3.2](https://github.com/sary357/FastAPIDemo/releases/tag/v0.3.2)
- Current codes deployed on the [computing engine](https://console.cloud.google.com/compute/instancesDetail/zones/asia-east1-a/instances/gogobot-log-api?project=gogox-data-science-non-prod)
- How can I access db? please refer to the [page](https://www.notion.so/Access-gogobot-log-db-only-for-GoGoBot-CS-plan-B-6f1b38ea492a491cbf27b676e66be5ed)
- DB username/password: Please logon computing engine and check the content of `/home/fuming_tsai/FastAPIDemo/docker-compose.yml`.
- [Projet AVA schedule](https://docs.google.com/spreadsheets/d/1TUkFm_ZDR2k1vKFC8rxsqYSQf2sNAHC1YHmXP8qAy5Y/edit#gid=0)

### flink
- Github repo URL: https://github.com/gogovan/gogovan-analytics-flink
- Current status: deployed
- Current `deployment branch`: master branch
- My understanding
  - CDC -> [pubsub](https://github.com/gogovan/gogovan-analytics-automation/tree/master/dataflow/image/pubsub_job_schemas) -> [kafka](https://confluent.cloud/environments/env-80n65/clusters/lkc-w7ywvw/topics) [ref: codes](https://github.com/gogovan/gogovan-analytics-flink/blob/master/realtime/transport/src/main/java/com/gogox/transport/router/DataStreamJob.java#L93) -> [Data flow](https://console.cloud.google.com/dataflow/jobs?referrer=search&project=gogox-data-science-non-prod) -> [flink](https://github.com/gogovan/gogovan-analytics-flink) -> [redis](https://console.cloud.google.com/memorystore/redis/locations/us-central1/instances/datateam/details/overview?project=gogox-data-science-non-prod)
  - In [pubsub](https://github.com/gogovan/gogovan-analytics-automation/tree/master/dataflow/image/pubsub_job_schemas), you will see a list of files. Please search for the string: `bigquery_table_base: gogox-data-science-non-prod:xxxxxxx`. For example, `bigquery_table_base: gogox-data-science-non-prod:raw.delivery_db_streaming`
  - In data flow, there are `2` jobs
    - `datateam-stream-prod-bigquery-YYYYMMDD-HHMMSS`: this is deployed by [gogovan-analytics-automation](https://github.com/gogovan/gogovan-analytics-automation/tree/master/dataflow)
    - `datateam-stream-prod-pubsub-YYYYMMDD-HHMMSS`: this will be deployed by [gogovan-analytics-automation](https://github.com/gogovan/gogovan-analytics-automation/tree/master/dataflow)
  - In GCP MemoryStore, there is only 1 redis instance called `datateam`.
- [watchdog](https://github.com/gogovan/gogovan-analytics-flink/tree/master/watchdog): it monitors the status of flink jobs. If the job is not running, it will restart the job.
- [Google case](https://console.cloud.google.com/support/cases/detail/v2/48878269?project=gogox-data-science-non-prod): Google engineers are still investigating the issue. 
- Discussion slack channel: #streaming-data-processing

### DE-1129 (data-access-tool)
- When we or HK data analytics team use [data-access-tool](https://github.com/gogovan/data-access-tool) but get an error message like
```
Access Denied: BigQuery BigQuery: Error getting metadata for external code resource, 
please verify you have provided a valid path and/or that you have access to the 
resource: gs://gogox-analytics/bigquery/udf/wkx.js
```
- That means the user doesn't have the permission to access the bucket `gs://gogox-analytics/bigquery/`. What we will going to do is to grant the permission to the user.
  - Step 1: [Grant the permission](hhttps://console.cloud.google.com/storage/browser/ggx-analytics;tab=objects?forceOnBucketsSortingFiltering=true&project=gogox-data-science-non-prod) to the user.
  - Step 2: choose the tab `PERMISSIONS` and click `GRANT ACCESS`.
    - Add principals: Please fill the user who encounters the issue.
    - Assign roles: please choose `Storage Object Viewer`.
    - Click `SAVE`.

### accounts
- bq-test-user@gogox.com
  - vault path: https://vault-v2.gogo.tech/ui/vault/secrets/gogotech/show/data_team/user_accounts/bq-test-user@gogox.com
  - description: This account is used for us to set up the connection between Google play and [App annie](https://www.data.ai/account/login). 



## Infra team part
### dockerhub-vul-report
- Objective: to report the vulnerability of dockerhub images. In fact, it parse the report from dockerhub, save the report to the GCS, then send the report to slack channel.
- Github repo URL: https://github.com/gogovan/gogovan-devops/tree/develop/dockerfiles/gogox-public-image/dockerhub-vul-report
- slack channel: #alert-dockerhub

### sequence_number_fix
- Objective: to fix the sequence number issue in the database. It's a temporary solution. These scripts can compare max id and sequence number. Ideally, they were only necessary when migrating from AWS to GCP. Hope we don't need them anymore.
- Github repo URL: https://github.com/gogovan/gogovan-devops/tree/develop/script/GCP/sequence_number_fix

## Mobile team part
- regular record down crash rate. What I have been doing is to record down the crash rate every week. 
  - firebase crashlytics: https://console.firebase.google.com/project/api-project-1004752207173/crashlytics/app/ios:hk.gogovan.GoGoVanClient/issues?utm_campaign=extensions&utm_medium=SLACK&utm_source=VELOCITY_ISSUE&state=open&time=last-seven-days&types=crash&tag=all&sort=eventCount
  - [Google Spreadsheet](https://docs.google.com/spreadsheets/d/1ErbjelUmC6C8Nlo-Sxep4NH7GmJsT_E752fZiI5s5Qo/edit#gid=1294344438)