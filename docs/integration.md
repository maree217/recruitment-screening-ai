# Integration Guide

## Supported Platforms

### Tribepad
- **API:** REST API v3
- **Auth:** OAuth 2.0
- **Endpoints:** Jobs, Applications, Candidates
- **Setup:** Request API credentials from Tribepad

### Jobtrain
- **API:** REST API
- **Auth:** API Key
- **Endpoints:** Vacancies, Applications
- **Setup:** Generate API key in Jobtrain admin

### Networx
- **API:** REST API
- **Auth:** OAuth 2.0
- **Endpoints:** Jobs, Candidates, Applications
- **Setup:** Contact Networx for integration

## Configuration

```yaml
# config/ats-integration.yaml
ats:
  platform: tribepad
  api_url: https://api.tribepad.com/v3
  auth:
    type: oauth2
    client_id: ${ATS_CLIENT_ID}
    client_secret: ${ATS_CLIENT_SECRET}

webhooks:
  application_received: /webhooks/application
  job_posted: /webhooks/job

sync:
  frequency: realtime  # or hourly, daily
```

## Data Mapping

| ATS Field | Internal Field | Purpose |
|-----------|----------------|---------|
| application_id | candidate_ref | Unique reference |
| cv_document | raw_cv | Document to parse |
| form_responses | application_data | Structured responses |
| vacancy_id | job_ref | Link to criteria |

## Testing

```bash
# Test ATS connectivity
./scripts/test-ats-connection.sh

# Verify webhook delivery
./scripts/test-webhooks.sh
```
