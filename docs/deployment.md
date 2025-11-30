# Deployment Guide

## Prerequisites

- Azure subscription (UK South) or AWS (eu-west-2)
- ATS API credentials
- Azure AD for authentication
- Form Recognizer / Textract access

## Azure Deployment

### 1. Clone Repository
```bash
git clone https://github.com/maree217/recruitment-screening-ai
cd recruitment-screening-ai
```

### 2. Deploy Infrastructure
```bash
cd terraform/azure-uk
terraform init
terraform apply -var-file="prod.tfvars"
```

### 3. Configure Secrets
```bash
az keyvault secret set --vault-name $KV --name ats-client-id --value $CLIENT_ID
az keyvault secret set --vault-name $KV --name ats-client-secret --value $CLIENT_SECRET
```

### 4. Configure Webhooks
Register webhooks in your ATS:
- Application received: `https://your-domain/webhooks/application`
- Job posted: `https://your-domain/webhooks/job`

### 5. Deploy Application
```bash
az containerapp up --name screening-ai --source .
```

## Verification

```bash
# Health check
curl https://your-screening-ai.azurecontainerapps.io/health

# Test screening
curl -X POST https://your-screening-ai.azurecontainerapps.io/api/screen \
  -H "Authorization: Bearer $TOKEN" \
  -d '{"job_id": "12345"}'
```

## Monitoring

- Application Insights for logs
- Custom metrics for screening volume, accuracy
- Alerts for processing failures
