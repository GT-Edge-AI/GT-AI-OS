# Financial Controls

Configure model pricing, budget limits, and storage costs from the Financial Controls page. Track AI usage costs and generate invoices.

## Overview

The Financial Controls page (Billing) allows Super Admins to:

- Set pricing for AI models
- Configure budget limits per tenant
- Define storage pricing
- Track usage costs
- Generate invoices

## Accessing Financial Controls

1. Click **Financial Controls** (or **Billing**) in the sidebar
2. The page displays pricing configuration and usage data

## Key Features

| Feature | Description |
|---------|-------------|
| Model Pricing | Set input/output token costs per model |
| Budget Limits | Configure spending caps per tenant |
| Storage Pricing | Define per-GB storage costs |
| Usage Tracking | Monitor token and storage consumption |
| Invoice Generation | Create billing statements |

## Page Tabs

The Financial Controls page has multiple sections:

| Tab | Purpose |
|-----|---------|
| **Model Pricing** | Configure per-model token costs |
| **Budget Limits** | Set tenant spending caps |
| **Storage Pricing** | Define document storage costs |
| **Usage Reports** | View consumption data |

## How To: Configure Model Pricing

Set the cost for using AI models:

1. Navigate to **Financial Controls**
2. Select the **Model Pricing** tab
3. Find the model you want to price
4. Enter pricing:
   - **Input Price:** Cost per 1M input tokens
   - **Output Price:** Cost per 1M output tokens
5. Click **Save**

### Pricing Example

| Model | Input (per 1M tokens) | Output (per 1M tokens) |
|-------|----------------------|------------------------|
| NVIDIA Llama 3.3 70B | $0.35 | $0.40 |
| Groq Llama 3.3 70B | $0.59 | $0.79 |
| Local Ollama | $0.00 | $0.00 |

**Note:** Set local models to $0.00 since there are no API costs.

## How To: Set Budget Limits

Configure spending caps for tenants:

1. Navigate to **Financial Controls**
2. Select the **Budget Limits** tab
3. Find the tenant
4. Configure limits:
   - **Monthly Limit:** Maximum spend per month
   - **Alert Threshold:** Percentage for warning notifications
   - **Action on Limit:** Block usage or allow overage
5. Click **Save**

### Budget Actions

| Action | Behavior |
|--------|----------|
| **Block** | Prevent further AI usage when limit reached |
| **Warn** | Send notification but allow continued usage |
| **Allow Overage** | Continue usage, track overage separately |

### Alert Thresholds

Set percentages for budget warnings:

| Threshold | Example (on $1000 limit) |
|-----------|--------------------------|
| 50% | Alert at $500 spend |
| 75% | Alert at $750 spend |
| 90% | Alert at $900 spend |
| 100% | Budget exhausted |

## How To: Configure Storage Pricing

Set the cost for document storage:

1. Navigate to **Financial Controls**
2. Select the **Storage Pricing** tab
3. Enter pricing:
   - **Price per GB/month:** Cost for document storage
4. Click **Save**

Storage is calculated based on:
- Uploaded documents (PDFs, DOCX, etc.)
- Generated embeddings
- Conversation history (if stored)

## How To: View Usage Reports

Monitor consumption across tenants:

1. Navigate to **Financial Controls**
2. Select the **Usage Reports** tab
3. Configure filters:
   - **Time Period:** Select date range
   - **Tenant:** All or specific tenant
   - **Model:** All or specific model
4. View breakdown:
   - Token usage by model
   - Storage consumption
   - Cost totals

### Usage Metrics

| Metric | Description |
|--------|-------------|
| **Input Tokens** | Tokens sent to AI models |
| **Output Tokens** | Tokens received from AI models |
| **Total Cost** | Calculated from pricing * usage |
| **Storage GB** | Total storage consumed |

## How To: Generate Invoices

Create billing statements for tenants:

1. Navigate to **Financial Controls**
2. Select the **Invoices** tab (or section)
3. Click **Generate Invoice**
4. Configure:
   - **Tenant:** Select tenant
   - **Period:** Billing period (month)
   - **Include:** Token costs, storage, etc.
5. Click **Generate**
6. Download or send the invoice

### Invoice Contents

Generated invoices include:

| Section | Details |
|---------|---------|
| **Summary** | Total amount due |
| **AI Usage** | Token consumption by model |
| **Storage** | Document storage costs |
| **Period** | Billing date range |

## Pricing Best Practices

| Practice | Recommendation |
|----------|----------------|
| Base on provider costs | Set prices at or above your API costs |
| Include margin | Add markup for operational costs |
| Local models | Set to $0 or minimal cost |
| Regular review | Adjust as provider prices change |

### Cost Calculation

Total cost is calculated as:

```
Input Cost = (Input Tokens / 1,000,000) * Input Price
Output Cost = (Output Tokens / 1,000,000) * Output Price
Storage Cost = Storage GB * Price per GB
Total = Input Cost + Output Cost + Storage Cost
```

## Budget Monitoring

Track spending in real-time:

| Indicator | Meaning |
|-----------|---------|
| **Green** | Under 50% of budget |
| **Yellow** | 50-90% of budget |
| **Red** | Over 90% of budget |
| **Blocked** | At limit, usage blocked |

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Usage not tracking | Verify models have pricing configured |
| Budget not enforcing | Check "Action on Limit" setting |
| Costs seem wrong | Verify per-model pricing is correct |
| Invoice missing data | Ensure usage occurred in selected period |

### Checking Usage Data

```bash
# View usage tracking in logs
docker compose logs control-panel-backend --tail 100 | grep -i usage

# Check database for usage records
docker exec gentwo-controlpanel-postgres psql -U postgres -d gt2_admin -c "SELECT * FROM usage_logs LIMIT 10;"
```

## Next Steps

- [License Management](license-management) - Manage user seats
- [Tenant Management](tenant-management) - Configure tenant settings
- [Troubleshooting](troubleshooting) - Resolve billing issues
