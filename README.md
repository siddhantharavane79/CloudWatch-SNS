# AWS EC2 CloudWatch Monitoring with SNS

## Project Overview

Configured Amazon CloudWatch to monitor an EC2 instance, created a high
CPU alarm, and configured Amazon SNS to send email notifications when
the alarm is triggered.

## AWS Services Used

-   Amazon EC2
-   Amazon CloudWatch
-   Amazon SNS

## Configuration

### EC2 Monitoring

-   Monitored metric: `CPUUtilization`
-   Instance: EC2 instance
-   Health check: EC2 Status Checks (`2/2 checks passed`)

### CloudWatch Alarm

-   Alarm name: `EC2-High-CPU-Alarm`
-   Metric: `CPUUtilization`
-   Statistic: `Average`
-   Period: `5 minutes`
-   Condition: `CPUUtilization > 80%`
-   Datapoints to alarm: `1 out of 1`

### SNS Notification

-   SNS Topic: `EC2-CPU-Alerts`
-   Protocol: Email
-   Email subscription: Confirmed
-   Notification trigger: When the CloudWatch alarm enters `ALARM` state

## CPU Load Testing

Install stress-ng:

``` bash
sudo yum update -y
sudo yum install stress-ng -y
```

Generate CPU load:

``` bash
stress-ng --cpu 2 --timeout 5m
```

During high CPU usage, CloudWatch can change the alarm state from `OK`
to `ALARM`, which triggers the SNS email notification.

## Verification

1.  Open **CloudWatch → Alarms**.
2.  Check `EC2-High-CPU-Alarm`.
3.  Verify the alarm changes to `ALARM` when CPU usage exceeds 80%.
4.  Check the confirmed email inbox for the SNS notification.
5.  After the CPU load stops, the alarm can return to `OK`.

## Project Result

Successfully configured EC2 monitoring, CloudWatch CPU alarm, and SNS
email notification.

## Screenshots

Add screenshots showing: - EC2 instance health / `2/2 checks passed` -
CPUUtilization metric - CloudWatch alarm in `OK` state - CloudWatch
alarm in `ALARM` state - SNS topic and confirmed email subscription -
SNS alarm notification email
