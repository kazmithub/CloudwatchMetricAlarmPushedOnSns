# CloudWatch Metric Alarms with SNS Notifications

AWS monitoring stack using CloudWatch custom metrics, alarms, dashboards, and multi-destination SNS notifications.

## Architecture

```
EC2 Instance (CloudWatch Agent)
        |
        v
   CloudWatch Logs + Custom Metrics
        |
        v
   CloudWatch Alarms (CPU, Memory, Disk)
        |
        +---> Composite Alarms
        |
        v
   SNS Topic
        |
        +---> Email Notifications
        +---> SQS Queue (for processing)
        +---> PagerDuty / Opsgenie (webhook)
```

## Key Features

- **Custom Metrics** - Memory, disk usage via CloudWatch Agent
- **Log Aggregation** - EC2 logs shipped to CloudWatch Logs
- **Metric Alarms** - CPU, memory, disk threshold alerting
- **Composite Alarms** - Multi-metric conditions (e.g., CPU AND memory)
- **CloudWatch Dashboard** - Visual monitoring of all metrics
- **Multi-destination** - SNS to email, SQS, and external integrations

## PagerDuty / Opsgenie Integration

To integrate with incident management:
1. Create an SNS subscription with HTTPS protocol
2. Use the PagerDuty/Opsgenie SNS integration endpoint URL
3. Confirm the subscription

```bash
aws sns subscribe \
  --topic-arn arn:aws:sns:us-east-1:ACCOUNT:alarm-topic \
  --protocol https \
  --notification-endpoint https://events.pagerduty.com/integration/YOUR_KEY/enqueue
```

## Deployment Order

1. `vpc.yaml` - VPC and networking
2. `instance.yaml` - EC2 with CloudWatch Agent
3. `alarm.yaml` - Alarms and SNS topics
4. `dashboard.yaml` - Monitoring dashboard

## License

MIT
