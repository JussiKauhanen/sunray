# QAW Feedback Labeling System

AI-powered customer feedback analysis using AWS Bedrock (Claude) - replaces Sunbeam AI solution.

[![Logo](https://github.com/stockmanncom/dalidreams/blob/main/images/logo-draft.png)](link_url)

## What It Does

- Reads customer feedback from S3 (`ingress/`)
- Labels feedback using Claude AI (category, sentiment, priority, language)
- Outputs structured JSON to S3 (`egress/`)
- Archives processed files automatically

## Supported Languages

Finnish, English, Estonian, Latvian, Lithuanian

## Architecture
```
S3 ingress/ → Lambda → Bedrock Claude → Lambda → S3 egress/
```

## Prerequisites

1. AWS Account with Bedrock access
2. **First-time Anthropic users**: Submit use case details at [Bedrock Playground](https://console.aws.amazon.com/bedrock/home?region=eu-west-1#/playground/chat)
3. AWS CLI configured

## Deployment
```bash
# 1. Deploy CloudFormation stack
aws cloudformation create-stack \
  --stack-name qaw-feedback-labeling \
  --template-body file://cloudformation-template.yaml \
  --parameters ParameterKey=FeedbackBucketName,ParameterValue=your-unique-bucket-name \
  --capabilities CAPABILITY_NAMED_IAM \
  --region eu-west-1

# 2. Wait for completion
aws cloudformation wait stack-create-complete \
  --stack-name qaw-feedback-labeling \
  --region eu-west-1

# 3. Get bucket name from outputs
aws cloudformation describe-stacks \
  --stack-name qaw-feedback-labeling \
  --query 'Stacks[0].Outputs'
```

## Usage

### Create Folders
```bash
aws s3api put-object --bucket your-bucket-name --key ingress/
aws s3api put-object --bucket your-bucket-name --key egress/
aws s3api put-object --bucket your-bucket-name --key archive/
```

### Upload Test Feedback
```bash
# Create sample-feedback.json
cat > sample-feedback.json << 'EOF'
[
  {
    "id": "fb001",
    "feedback": "Todella hyvä palvelu, kiitos!",
    "customer_id": "12345",
    "timestamp": "2026-01-16T10:30:00Z"
  },
  {
    "id": "fb002",
    "feedback": "Couldn't complete my purchase, payment failed",
    "customer_id": "67890",
    "timestamp": "2026-01-16T11:15:00Z"
  }
]
EOF

# Upload to trigger processing
aws s3 cp sample-feedback.json s3://your-bucket-name/ingress/
```

### Check Results
```bash
# View processed output
aws s3 ls s3://your-bucket-name/egress/

# Download result
aws s3 cp s3://your-bucket-name/egress/sample-feedback_labeled_*.json result.json
cat result.json
```

## Output Format
```json
{
  "id": "fb001",
  "feedback": "Todella hyvä palvelu, kiitos!",
  "customer_id": "12345",
  "timestamp": "2026-01-16T10:30:00Z",
  "labels": {
    "category": "positive_feedback",
    "sentiment": "positive",
    "subcategory": "great_service",
    "language": "fi",
    "priority": "low",
    "summary": "Customer expresses satisfaction with service",
    "confidence": "high"
  },
  "processed_at": "2026-01-16T13:45:00.123Z",
  "processor": "bedrock-claude"
}
```

## Cost Estimate

~$50-150/month for 10,000 feedbacks (varies by feedback length)

## Monitoring

View logs: CloudWatch → Log Groups → `/aws/lambda/qaw-feedback-labeling-labeling-function`

## Troubleshooting

**"Model identifier is invalid"**: Enable Anthropic models via [Bedrock Playground](https://console.aws.amazon.com/bedrock/home?region=eu-west-1#/playground/chat)

**No output files**: Check Lambda logs in CloudWatch for errors

**Stack creation fails**: Ensure bucket name is globally unique

## Cleanup
```bash
# Delete all S3 objects first
aws s3 rm s3://your-bucket-name --recursive

# Delete stack
aws cloudformation delete-stack --stack-name qaw-feedback-labeling
```