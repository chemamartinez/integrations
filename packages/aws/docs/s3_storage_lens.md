# Amazon S3 Storage Lens

The Amazon S3 Storage Lens integration allows you to monitor [Amazon S3 Storage Lens](https://aws.amazon.com/s3/storage-analytics-insights/)—an analytics service for Amazon S3.

Use the Amazon S3 Storage Lens integration to view metrics on object storage usage and activity trends. Then visualize that data in Kibana, create alerts to notify you if something goes wrong, and reference metrics when troubleshooting an issue.

For example, you could track your total storage and object count by region—allowing you more easily visualize trends and anticipate problems before they happen.

**IMPORTANT: Extra AWS charges on API requests will be generated by this integration. Check [API Requests](https://www.elastic.co/docs/current/integrations/aws#api-requests) for more details.**

## Data streams

The Amazon S3 Storage Lens integration collects one type of data: metrics.

**Metrics** give you insight into the state of Amazon S3 Storage Lens.
Metrics collected by the S3 Storage Lens integration include usage data for total storage, object counts, average object sizes, and more. See more details in the [Metrics reference](#metrics-reference).

## Requirements

You need Elasticsearch for storing and searching your data and Kibana for visualizing and managing it.
You can use our hosted Elasticsearch Service on Elastic Cloud, which is recommended, or self-manage the Elastic Stack on your own hardware.

Before using any AWS integration you will need:

* **AWS Credentials** to connect with your AWS account.
* **AWS Permissions** to make sure the user you're using to connect has permission to share the relevant data.

For more details about these requirements, please take a look at the [AWS integration documentation](https://docs.elastic.co/integrations/aws#requirements).

## Setup

Use this integration if you only need to collect data from the Amazon S3 Storage Lens service.

If you want to collect data from two or more AWS services, consider using the **AWS** integration.
When you configure the AWS integration, you can collect data from as many AWS services as you'd like.

For step-by-step instructions on how to set up an integration, see the [Getting started](https://www.elastic.co/guide/en/starting-with-the-elasticsearch-platform-and-its-solutions/current/getting-started-observability.html) guide.

## Metrics reference

An example event for `s3_storage_lens` looks as following:

```json
{
    "@timestamp": "2021-11-07T20:38:00.000Z",
    "aws": {
        "cloudwatch": {
            "namespace": "AWS/S3/Storage-Lens"
        },
        "dimensions": {
            "aws_account_number": "428152502467",
            "aws_region": "eu-central-1",
            "bucket_name": "filebeat-aws-elb-test",
            "configuration_id": "default-account-dashboard",
            "metrics_version": "1.0",
            "record_type": "BUCKET",
            "storage_class": "STANDARD"
        },
        "s3_storage_lens": {
            "metrics": {
                "4xxErrors": {
                    "avg": 0
                },
                "5xxErrors": {
                    "avg": 0
                },
                "AllRequests": {
                    "avg": 145
                },
                "BytesDownloaded": {
                    "avg": 0
                },
                "BytesUploaded": {
                    "avg": 82537
                },
                "CurrentVersionObjectCount": {
                    "avg": 164195
                },
                "CurrentVersionStorageBytes": {
                    "avg": 154238334
                },
                "DeleteMarkerObjectCount": {
                    "avg": 0
                },
                "DeleteRequests": {
                    "avg": 0
                },
                "EncryptedObjectCount": {
                    "avg": 164191
                },
                "EncryptedStorageBytes": {
                    "avg": 154237917
                },
                "GetRequests": {
                    "avg": 0
                },
                "HeadRequests": {
                    "avg": 0
                },
                "IncompleteMultipartUploadObjectCount": {
                    "avg": 0
                },
                "IncompleteMultipartUploadStorageBytes": {
                    "avg": 0
                },
                "ListRequests": {
                    "avg": 0
                },
                "NonCurrentVersionObjectCount": {
                    "avg": 0
                },
                "NonCurrentVersionStorageBytes": {
                    "avg": 0
                },
                "ObjectCount": {
                    "avg": 164195
                },
                "ObjectLockEnabledObjectCount": {
                    "avg": 0
                },
                "ObjectLockEnabledStorageBytes": {
                    "avg": 0
                },
                "PostRequests": {
                    "avg": 0
                },
                "PutRequests": {
                    "avg": 145
                },
                "ReplicatedObjectCount": {
                    "avg": 0
                },
                "ReplicatedStorageBytes": {
                    "avg": 0
                },
                "SelectRequests": {
                    "avg": 0
                },
                "SelectReturnedBytes": {
                    "avg": 0
                },
                "SelectScannedBytes": {
                    "avg": 0
                },
                "StorageBytes": {
                    "avg": 154238334
                }
            }
        }
    },
    "cloud": {
        "account": {
            "id": "428152502467",
            "name": "elastic-beats"
        },
        "provider": "aws",
        "region": "us-east-1"
    },
    "data_stream": {
        "dataset": "aws.s3_storage_lens",
        "namespace": "default",
        "type": "metrics"
    },
    "ecs": {
        "version": "8.11.0"
    },
    "event": {
        "agent_id_status": "verified",
        "dataset": "aws.s3_storage_lens",
        "duration": 22973251900,
        "ingested": "2021-11-08T20:38:37Z",
        "module": "aws"
    },
    "metricset": {
        "name": "cloudwatch",
        "period": 86400000
    },
    "service": {
        "type": "aws"
    }
}
```

**ECS Field Reference**

Please refer to the following [document](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html) for detailed information on ECS fields.

**Exported fields**

| Field | Description | Type | Metric Type |
|---|---|---|---|
| @timestamp | Event timestamp. | date |  |
| agent.id | Unique identifier of this agent (if one exists). Example: For Beats this would be beat.id. | keyword |  |
| aws.\*.metrics.\*.\* | Metrics that returned from Cloudwatch API query. | double |  |
| aws.cloudwatch.namespace | The namespace specified when query cloudwatch api. | keyword |  |
| aws.dimensions.aws_account_number | The AWS account that's associated with the metrics. | keyword |  |
| aws.dimensions.aws_region | The AWS Region for the metrics. | keyword |  |
| aws.dimensions.bucket_name | The name of the S3 bucket that's reported in the metrics. | keyword |  |
| aws.dimensions.configuration_id | The dashboard name for the S3 Storage Lens configuration reported in the metrics. | keyword |  |
| aws.dimensions.metrics_version | The version of the S3 Storage Lens metrics. The metrics version has a fixed value of 1.0. | keyword |  |
| aws.dimensions.organization_id | The AWS Organizations ID for the metrics. | keyword |  |
| aws.dimensions.record_type | The granularity of the metrics such as ORGANIZATION, ACCOUNT, BUCKET. | keyword |  |
| aws.dimensions.storage_class | The storage class for the bucket that's reported in the metrics. | keyword |  |
| aws.metrics_names_fingerprint | Autogenerated ID representing the fingerprint of the list of metrics names.  Applicable only for [Amazon Data Firehose integration](https://www.elastic.co/docs/current/integrations/awsfirehose). | keyword |  |
| aws.s3_storage_lens.metrics.4xxErrors.avg | The total 4xx errors in scope. | long | gauge |
| aws.s3_storage_lens.metrics.5xxErrors.avg | The total 5xx errors in scope. | long | gauge |
| aws.s3_storage_lens.metrics.AllRequests.avg | The total number of requests made. | long | gauge |
| aws.s3_storage_lens.metrics.BytesDownloaded.avg | The number of bytes in scope that were downloaded. | long | gauge |
| aws.s3_storage_lens.metrics.BytesUploaded.avg | The number of bytes uploaded. | long | gauge |
| aws.s3_storage_lens.metrics.CurrentVersionObjectCount.avg | The number of objects that are a current version. | long | gauge |
| aws.s3_storage_lens.metrics.CurrentVersionStorageBytes.avg | The number of bytes that are a current version. | long | gauge |
| aws.s3_storage_lens.metrics.DeleteMarkerObjectCount.avg | The total number of objects with a delete marker. | long | gauge |
| aws.s3_storage_lens.metrics.DeleteRequests.avg | The total number of delete requests made. | long | gauge |
| aws.s3_storage_lens.metrics.EncryptedObjectCount.avg | The total object counts that are encrypted using Amazon S3 server-side encryption. | long | gauge |
| aws.s3_storage_lens.metrics.EncryptedStorageBytes.avg | The total number of encrypted bytes using Amazon S3 server-side encryption. | long | gauge |
| aws.s3_storage_lens.metrics.GetRequests.avg | The total number of GET requests made. | long | gauge |
| aws.s3_storage_lens.metrics.HeadRequests.avg | The total number of head requests made. | long | gauge |
| aws.s3_storage_lens.metrics.IncompleteMultipartUploadObjectCount.avg | The number of objects in scope that are incomplete multipart uploads. | long | gauge |
| aws.s3_storage_lens.metrics.IncompleteMultipartUploadStorageBytes.avg | The total bytes in scope with incomplete multipart uploads. | long | gauge |
| aws.s3_storage_lens.metrics.ListRequests.avg | The total number of list requests made. | long | gauge |
| aws.s3_storage_lens.metrics.NonCurrentVersionObjectCount.avg | The count of the noncurrent version objects. | long | gauge |
| aws.s3_storage_lens.metrics.NonCurrentVersionStorageBytes.avg | The number of noncurrent versioned bytes. | long | gauge |
| aws.s3_storage_lens.metrics.ObjectCount.avg | The total object count. | long | gauge |
| aws.s3_storage_lens.metrics.ObjectLockEnabledObjectCount.avg | The total number of objects in scope that have Object Lock enabled. | long | gauge |
| aws.s3_storage_lens.metrics.ObjectLockEnabledStorageBytes.avg | The total number of bytes in scope that have Object Lock enabled. | long | gauge |
| aws.s3_storage_lens.metrics.PostRequests.avg | The total number of post requests made. | long | gauge |
| aws.s3_storage_lens.metrics.PutRequests.avg | The total number of PUT requests made. | long | gauge |
| aws.s3_storage_lens.metrics.ReplicatedObjectCount.avg | The count of replicated objects. | long | gauge |
| aws.s3_storage_lens.metrics.ReplicatedStorageBytes.avg | The total number of bytes in scope that are replicated. | long | gauge |
| aws.s3_storage_lens.metrics.SelectRequests.avg | The total number of select requests. | long | gauge |
| aws.s3_storage_lens.metrics.SelectReturnedBytes.avg | The number of select bytes returned. | long | gauge |
| aws.s3_storage_lens.metrics.SelectScannedBytes.avg | The number of select bytes scanned. | long | gauge |
| aws.s3_storage_lens.metrics.StorageBytes.avg | The total storage in bytes | long | gauge |
| aws.tags | Tag key value pairs from aws resources. | flattened |  |
| cloud.account.id | The cloud account or organization id used to identify different entities in a multi-tenant environment. Examples: AWS account id, Google Cloud ORG Id, or other unique identifier. | keyword |  |
| cloud.image.id | Image ID for the cloud instance. | keyword |  |
| cloud.region | Region in which this host, resource, or service is located. | keyword |  |
| data_stream.dataset | Data stream dataset. | constant_keyword |  |
| data_stream.namespace | Data stream namespace. | constant_keyword |  |
| data_stream.type | Data stream type. | constant_keyword |  |
| event.module | Event module | constant_keyword |  |
| host.containerized | If the host is a container. | boolean |  |
| host.os.build | OS build information. | keyword |  |
| host.os.codename | OS codename, if any. | keyword |  |
