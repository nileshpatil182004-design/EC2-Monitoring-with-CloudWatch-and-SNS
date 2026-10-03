# AWS Project 1 – EC2 Monitoring with CloudWatch and SNS

## 📌 Project Overview

This project demonstrates how to monitor an Amazon EC2 instance using **Amazon CloudWatch** and send an email notification using **Amazon SNS** when CPU utilization becomes high.

The project also includes monitoring the health/status of the EC2 instance.

---

## 🏗️ Architecture

```text
                Amazon EC2
                    |
                    | CPU Utilization
                    ↓
             Amazon CloudWatch
                    |
              CloudWatch Alarm
             CPU > 70% for 5 min
                    |
                    ↓
               Amazon SNS
                    |
                    ↓
              Email Notification
```

---

## ☁️ AWS Services Used

- **Amazon EC2** – Provides the virtual server.
- **Amazon CloudWatch** – Monitors EC2 CPU utilization and instance status.
- **Amazon SNS** – Sends email notifications when the alarm is triggered.

---

## ⚙️ Configuration

### EC2 Instance

| Setting | Value |
|---|---|
| Instance Name | `CW-Test-EC2` |
| Operating System | Amazon Linux 2023 |
| Region | Asia Pacific (Mumbai) – `ap-south-1` |
| Metric | `CPUUtilization` |

### CloudWatch Alarm

| Setting | Value |
|---|---|
| Metric | CPUUtilization |
| Statistic | Average |
| Period | 5 minutes |
| Threshold Type | Static |
| Condition | Greater than |
| Threshold | 70% |
| Alarm Name | `EC2-High-CPU-Alarm` |

### SNS

| Setting | Value |
|---|---|
| Topic | `EC2-CPU-Alert` |
| Protocol | Email |
| Notification | Email when alarm enters ALARM state |

---

## 🔧 Implementation Steps

### 1. Launch EC2 Instance

An EC2 instance named `CW-Test-EC2` was created using Amazon Linux 2023.

### 2. Create SNS Topic

An SNS topic named `EC2-CPU-Alert` was created.

An email subscription was added and the subscription was confirmed from the email received from AWS SNS.

### 3. Create CloudWatch Alarm

The `CPUUtilization` metric of the EC2 instance was selected.

The alarm was configured with:

- Average statistic
- 5-minute period
- Static threshold
- CPU utilization greater than 70%

The SNS topic `EC2-CPU-Alert` was configured as the notification action.

### 4. Monitor EC2 Health

The EC2 instance status checks were monitored to verify that the instance was healthy and that the required status checks were passing.

### 5. Test High CPU Usage

CPU load can be generated on the Amazon Linux instance using `stress-ng`.

Example:

```bash
sudo dnf install stress-ng -y
stress-ng --cpu 2 --timeout 10m
```

This increases CPU utilization so that the CloudWatch alarm can be tested.

---

## 🧪 Testing

### Test Case 1 – Normal CPU Usage

When CPU utilization remains below the configured threshold:

```text
Alarm State: OK
```

### Test Case 2 – High CPU Usage

When CPU utilization goes above 70% for the configured evaluation period:

```text
Alarm State: ALARM
```

The CloudWatch alarm sends a notification through SNS to the confirmed email subscription.

### Test Case 3 – EC2 Instance Health

The EC2 status checks were verified from the EC2 console.

Expected result:

```text
2/2 checks passed
```

---

## 📸 Screenshots

Add the following screenshots to this README or to a `screenshots` folder:

1. EC2 instance – `CW-Test-EC2`
2. CloudWatch CPUUtilization metric
3. CloudWatch alarm configuration
4. SNS topic
5. Confirmed SNS email subscription
6. CloudWatch alarm in `ALARM` state
7. Email notification received from SNS
8. EC2 instance status checks

Example folder structure:

```text
project-1-cloudwatch-sns/
│
├── README.md
│
└── screenshots/
    ├── 01-ec2-instance.png
    ├── 02-cloudwatch-metric.png
    ├── 03-cloudwatch-alarm.png
    ├── 04-sns-topic.png
    ├── 05-sns-subscription.png
    ├── 06-alarm-state.png
    ├── 07-email-notification.png
    └── 08-instance-health.png
```

---
## 1. EC2 Create

![image alt](https://github.com/nileshpatil182004-design/EC2-Monitoring-with-CloudWatch-and-SNS/blob/641f1d72ce85c1ccac41b9bb9a7cf0abea73b628/EC2%20Instance.png)

## 2. SNS Topic Create

![image alt](https://github.com/nileshpatil182004-design/EC2-Monitoring-with-CloudWatch-and-SNS/blob/4fc66cd6af47c72e707b336c218a3c39a5f71023/SNS%20Topic.png)

## 3. Email Subscription confirm

![image alt](https://github.com/nileshpatil182004-design/EC2-Monitoring-with-CloudWatch-and-SNS/blob/4fc66cd6af47c72e707b336c218a3c39a5f71023/SNS%20Email%20subscription.png)

## 4. CloudWatch CPU Metric

![image alt](https://github.com/nileshpatil182004-design/EC2-Monitoring-with-CloudWatch-and-SNS/blob/d3df0751c40d263d0ed6a2017b163014749858d7/cloudwatch-metric.png)

## 5. CloudWatch Alarm Configure

![image alt](https://github.com/nileshpatil182004-design/EC2-Monitoring-with-CloudWatch-and-SNS/blob/d3df0751c40d263d0ed6a2017b163014749858d7/CW-alarm%20configuration.png)

## 6. High CPU Generate → Alarm = ALARM 

![image alt](https://github.com/nileshpatil182004-design/EC2-Monitoring-with-CloudWatch-and-SNS/blob/d3df0751c40d263d0ed6a2017b163014749858d7/Test%20High%20CPU%20Usage%201.png)

![image alt](https://github.com/nileshpatil182004-design/EC2-Monitoring-with-CloudWatch-and-SNS/blob/d3df0751c40d263d0ed6a2017b163014749858d7/Test%20High%20CPU%20Usage%202.png)






## ✅ Expected Result

The completed solution provides:

- EC2 CPU monitoring using CloudWatch
- EC2 instance health/status monitoring
- A CloudWatch alarm for CPU utilization above 70%
- SNS-based email notification
- Successful testing using controlled CPU load

---

## 🧹 Cleanup

After completing the assignment and taking all required screenshots:

1. Stop or terminate the EC2 instance if it is no longer required.
2. Delete the CloudWatch alarm if it is no longer required.
3. Delete the SNS topic and subscription if they are no longer required.
4. Review unused AWS resources to avoid unnecessary charges.

---

## 📚 Learning Outcomes

Through this project, I learned how to:

- Launch and monitor an EC2 instance.
- Use CloudWatch metrics.
- Create a CloudWatch alarm.
- Configure an SNS email notification.
- Monitor EC2 instance health.
- Generate CPU load for alarm testing.
- Understand basic AWS monitoring and alerting.

---

## 👨‍💻 Author

**Nilesh Patil**

Cloud & DevOps Training Project  
AWS Project Assignment – Set 4
