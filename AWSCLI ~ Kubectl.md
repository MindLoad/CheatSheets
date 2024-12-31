---
Title: AWSCLI
Date: 11.08.2023
Time: 12:03
Tags: [cheatsheet]
---

| command                                                                | description                |
| ---------------------------------------------------------------------- | -------------------------- |
| aws s3 ls                                                              | list buckets               |
| aws s3 cp \<local_path\> \<s3:\/\/bucket_name\/destination_path\>      | copy to bucket             |
| aws s3 sync \<local_path\> \<s3:\/\/bucket_name\/destination_path\>    | sync local dir with bucket |
| aws s3 ls s3:\/\/\<bucket_name\>                                       | list in bucket             |
| aws s3 rm s3:\/\/\<bucket_name\>\/\<directory_path\>\/ \-\-recursive   | remove dir from bucket     |
| aws s3 rm s3:\/\/\<bucket_name\>\/\<object_key\>                       | remove from bucket         |
| aws s3 cp s3:\/\/\<bucket_name\>\/\<object_key\> \<local_destination\> | download from bucket       |
| aws ec2 describe-instances                                             | list ec2 instances         |
| aws lambda list-functions                                              | list functions             |
| aws dynamodb list-tables                                               | list dynamodb tables       |
| aws iam list-users                                                     | list users                 |
|                                                                        |                            |
### Kubectl copy from remote pode
```bash
kubectl cp prod/backend-5d7b5c986:data.json ~/work/data.json -c container-backend
```
