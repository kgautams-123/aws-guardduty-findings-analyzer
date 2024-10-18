# GuardDuty Findings Analyzer

## Overview

This project provides an automated solution for processing AWS GuardDuty findings using Amazon Bedrock's Claude 3.5 Sonnet model. It summarizes GuardDuty alerts and provides recommended actions, delivering the results via email.

## Architecture

The solution consists of the following AWS components:

1. Amazon EventBridge: Captures GuardDuty findings
2. Amazon SQS: Queues the findings for processing
3. AWS Lambda: Processes the findings using Amazon Bedrock
4. Amazon Bedrock: Analyzes and summarizes the findings using the Claude 3.5 Sonnet model
5. Amazon SNS: Sends email notifications with the summarized findings

## Prerequisites

- An AWS account with permissions to create and manage the required services
- AWS CLI installed and configured
- Access to Amazon Bedrock and the Claude 3.5 Sonnet model

## Deployment

1. Clone this repository:
   ```
   git clone https://github.com/your-username/guardduty-findings-analyzer.git
   cd guardduty-findings-analyzer
   ```

2. Deploy the CloudFormation stack:
   ```
   aws cloudformation create-stack --stack-name guardduty-findings-analyzer --template-body file://guardduty_findings.yml --parameters ParameterKey=EmailAddress,ParameterValue=your-email@example.com --capabilities CAPABILITY_IAM
   ```

   Replace `your-email@example.com` with the email address where you want to receive the GuardDuty finding summaries.

3. Wait for the stack creation to complete:
   ```
   aws cloudformation wait stack-create-complete --stack-name guardduty-findings-analyzer
   ```

4. Once deployed, you will receive a subscription confirmation email. Confirm the subscription to start receiving GuardDuty finding summaries.

## How It Works

1. When GuardDuty generates a finding, it triggers an EventBridge rule.
2. The rule sends the finding to an SQS queue.
3. The Lambda function is invoked by messages in the SQS queue.
4. The Lambda function uses Amazon Bedrock's Claude 3.5 Sonnet model to analyze and summarize the finding.
5. The summarized finding, along with recommended actions, is sent via email using Amazon SNS.

## Customization

You can modify the `guardduty_findings.yml` file to adjust the Lambda function code, change the Bedrock model, or alter the email format. After making changes, update the CloudFormation stack:

```
aws cloudformation update-stack --stack-name guardduty-findings-analyzer --template-body file://guardduty_findings.yml --parameters ParameterKey=EmailAddress,ParameterValue=your-email@example.com --capabilities CAPABILITY_IAM
```

## Cleanup

To remove all resources created by this stack:

```
aws cloudformation delete-stack --stack-name guardduty-findings-analyzer
```

## Security Considerations

- The Lambda function has permissions to invoke Amazon Bedrock and publish to SNS. Ensure these permissions align with your security requirements.
- Review and adjust the IAM roles and policies as needed for your environment.
- Consider encrypting the SQS queue and SNS topic for additional security.

## Contributing

Contributions to improve the solution are welcome. Please fork the repository and submit a pull request with your proposed changes.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Resources

- [AWS GuardDuty Documentation](https://docs.aws.amazon.com/guardduty/)
- [Amazon Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [AWS Lambda Documentation](https://docs.aws.amazon.com/lambda/)
- [Amazon SQS Documentation](https://docs.aws.amazon.com/sqs/)
- [Amazon SNS Documentation](https://docs.aws.amazon.com/sns/)

## Support

For issues or questions, please open an issue in the GitHub repository or contact your AWS support representative.
```

This README.md file provides a comprehensive guide for users to understand, deploy, and use the GuardDuty Findings Analyzer solution. It includes sections on the architecture, prerequisites, deployment instructions, how the solution works, customization options, cleanup procedures, security considerations, and additional resources.

You can adjust the content as needed, especially the repository URL and any specific details about your implementation or organization's requirements.

Citations:
[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/31009598/9f4ec90e-0cf5-4d4c-8e49-d533ade8cba9/guardduty_findings.yml
