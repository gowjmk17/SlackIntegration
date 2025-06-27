
# Slack Integration with Salesforce

This integration enables *Salesforce* to send real-time notifications to designated **Slack** channels whenever a **Case** is created or updated. It uses a *Queueable Apex* class with callouts to Slack's Incoming Webhook URL, making it asynchronous and governor-limit friendly.


## :pushpin: Features
- Automatic Slack notifications for new or updated cases
- Centralized logging using a custom object (Slack_Message_Log__c)
- Uses Named Credentials and External Credentials for secure access
- Easily configurable via triggers or automation
- Scalable and robust


## 	:hammer_and_wrench: Slack Setup

1. Go to: https://api.slack.com/apps

2. Click Create New App → choose From Scratch → give it a name (e.g. Salesforce Case Alerts)

3. Select your workspace

4. Create a new channel in Slack (e.g. #support-alerts)

5. Under Channel features → Integrations → click Add an App → install the Incoming Webhooks app

6. Copy the generated Webhook URL (e.g. https://hooks.slack.com/services/TXXXXX/BXXXXX/XXXXXXXX)

7. Save this Webhook for later setup in Salesforce
    
## :label: Salesforce Objects

#### Case (Case)


| Field Label | API Name   | Description                |
| :-------- | :-------- | :------------------------- |
| `Case Number` | `CaseNumber` | Auto generate - case number |
| `Priority` | `Priority` | Picklist: Low, Medium, High |
| `Id` | `caseId` |  Store Case Id
| `Status` | `Status` | Picklist: New, Working, Escalated |

#### Slack Message Log (Slack_Message_Log__c)


| Field Label | API Name   | Description                |
| :-------- | :-------- | :------------------------- |
| `Case` | `Case__c` | Lookup - Case record|
| `Message Sent` | `Message_Sent__c` |  Slack message text |
| `Status` | `Status__c` | Log result - 'Success or Failure'|
| `Timestamp` | `Timestamp__c` | Log history - created or updated  |



## 	:page_facing_up: Apex Classes
### SlackNotificationQueueable.cls

This Queueable class:

- Accepts Case details (CaseNumber, Priority, CaseId, Status)
- Constructs a Slack JSON payload
- Sends the callout to the Slack Webhook
- Handles errors gracefully and logs results into `Slack_Message_Log__c`
- See full Apex implementation in SlackNotificationQueueable.cls

### SlackNotificationTrigger.cls
You can invoke this queueable:
- From a Case trigger after insert/update.
## :test_tube: Testing 

1.  Test with a new Case record (e.g. Status: New)
2. Test by updating a Case to High Priority
3. Check your Slack channel for the notification
4. Review records in  Slack_Message_Log__c
## Documentation

[ ](./Slack-Salesforce_Integration_Documentation.docx)

