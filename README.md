# Event-Driven Flight Report Automation Pipeline ✈️🔔

A serverless, cloud-native automation pipeline built entirely within the AWS Free Tier to handle real-time flight document routing without traditional backend application code.

## ✈️ Aviation Business Case
Airlines like Emirates and dnata handle thousands of critical documents daily, including fuel slips, weight balances, and passenger manifests. Manually processing and emailing these documents creates communication bottlenecks. This project removes human administrative delays by automating the instant routing of file telemetry alerts the exact second ground crews upload files to storage.

## 🛠️ System Architecture & Data Flow
This infrastructure relies exclusively on fully managed, decoupled cloud microservices ensuring high durability and low maintenance:
1. **Data Ingestion Tier (Amazon S3):** Serves as the central storage repository where airport ground operations drop `.csv` or `.pdf` telemetry reports.
2. **Event Trigger Layer (S3 Event Notifications):** Monitored by bucket execution watchpoints that flag every `s3:ObjectCreated:*` data mutation event instantly.
3. **Broadcast Routing Tower (Amazon SNS):** An asynchronous publishing node configured with subscription endpoints to map structural file properties into standard email notification templates.

## 🚀 Key Quantifiable Outcomes
* **Zero Overhead Hosting:** Leverages a 100% serverless infrastructure pattern, running entirely on the AWS Free Tier with \$0 idle infrastructure costs.
* **Low Latency Notifications:** Processes document ingestion states and delivers analytics notifications to target administrative dashboards in under 2 seconds.
* **Maintenance-Free Operations:** Utilizes managed cloud services, eliminating the need to patch, scale, or update server operating systems.

## 🔬 Sample Live Platform Telemetry
When a ground agent drops a manifest sheet (`flight_ek201_manifest.csv`) into the cloud storage directory, the pipeline broadcasts an atomic system message directly to target email endpoints:

```json
{
  "Records": [
    {
      "eventVersion": "2.1",
      "eventSource": "aws:s3",
      "awsRegion": "us-east-2",
      "eventTime": "2026-09-25T20:15:42.000Z",
      "eventName": "ObjectCreated:Put",
      "s3": {
        "bucket": {
          "name": "emirates-ops-reports-nandana"
        },
        "object": {
          "key": "flight_ek201_manifest.csv",
          "size": 14205
        }
      }
    }
  ]
}
```
