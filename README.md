## AWS Personal Health Dashboard 通知

AWS Personal Health Dashboard 可在 AWS 遇到可能会影响您的事件时提供提醒和修正指导，通常包括的类型有EC2维护计划、Abuse通知等。这些通知通常会以邮件的方式通知到AWS账号注册邮箱，但由于注册邮箱某些情况下可能不是运维/开发人员邮箱，造成需要关注提醒的人员并未收到通知。为使需要关注此类事件的人员得到及时通知，可以通过Cloudformation启动一个配置将Personal Health Dashboard通知通过邮件转发给需要关注的人员。


## 步骤

#### CloudFormation 配置

点击 **Launch Stack** 启动AWS CloudFormation控制台，打开后需要在控制台右上角**选择对应用户业务的配置区域**，本次实验在US-EAST-1 美国弗吉尼亚区域实施:
 
<a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=AWSAbuseNotifier&templateURL=https://liyx-media.s3-ap-southeast-1.amazonaws.com/scripts/AWS_Abuse_Notification.json" title="Launch Stack"><img src="images/cloudformation-launch-stack.png" alt="Launch Stack" /></a>

#### 填写配置项

- 打开**AWS CloudFormation**控制台后，保持默认选项点击下一步
- 在**参数**栏目下输入 

	```
	SNSTopicName: 可以自定义我们需要的SNS主题名字，比如PHD-fanout
	EmailAddress: 需要指定发送的邮箱地址(单个，cloudformation创建之后可以根据需要去SNS主题添加额外邮箱)
	```
	点击下一步

- 在**配置堆栈选项**栏目下保持默认配置，点击下一步
- 勾选**我确认，AWS CloudFormation 可能创建 IAM 资源。**的单选框后，点击**创建堆栈**，等待CloudFormation堆栈创建完成

#### 确认AWS SNS 主题下的邮箱订阅（根据需要添加额外的邮箱）

- 切换到AWS SNS 控制台，点击创建的主题**AWSAbuseNotifier**，可以看到当前邮箱终端节点在**等待确认**状态，需要登录邮箱确认订阅该SNS主题方可完成确认

