# nanoGPT

## Overview
nanoGPT is an AI model provider that aggregates access to numerous top open-source models under a single subscription. While it offers generous rate limits and extensive model variety at an attractive price point, significant privacy concerns—stemming from routing requests through third-party providers—make it unsuitable for sensitive development work.

## Key Strengths
- **Generous Rate Limits**: 60,000 requests per month for $8 subscription
- **Extensive Model Selection**: Access to various top open-source models
- **Affordable Entry Point**: Cost-effective way to experiment with different models
- **Wide Model Variety**: Great for testing and comparing different LLMs before committing to a provider
- **Referral Discount**: 5% discount available through [referral link](https://nano-gpt.com/invite/9yrQteBR)

## Critical Limitations
- **Privacy Concerns**: Routes requests to third-party providers, not US-based infrastructure
- **Data Security Uncertainty**: Privacy depends on the underlying model provider's policies
- **Not Self-Hosted**: Unlike providers like Synthetic.new, models aren't hosted on nanoGPT's own infrastructure
- **Training Data Risk**: No guarantee that your code won't be used for training by underlying providers
- **Complex Provider Chain**: Multiple parties involved in request handling increases security surface area

## Privacy Policy Caveat
According to nanoGPT's privacy policy:
- They claim not to store or use your data
- **However**, they explicitly state that data handling depends on the underlying model provider
- This creates significant uncertainty about actual data protection

## Best Use Cases
- **Backup Provider**: Good fallback option when primary provider is unavailable
- **Model Exploration**: Excellent for testing different models before selecting a primary provider
- **Non-Sensitive Projects**: Suitable for public projects or learning exercises
- **Budget Development**: Works for hobby projects where data privacy isn't critical
- **Model Comparison**: Useful for understanding capabilities of various open-source models

## Who Should Avoid
- **Professional Development**: Not recommended for client or commercial work with sensitive data
- **Privacy-Conscious Developers**: Anyone working with proprietary code or sensitive information
- **Production Applications**: Teams requiring clear data handling and privacy guarantees
- **Enterprise Use**: Organizations with strict data governance requirements
- **Compliance-Sensitive Projects**: Projects under GDPR, HIPAA, or similar regulations

## Better Alternatives
If privacy and data security matter for your use case:

### Synthetic.new (Recommended)
- **Hosts own models** on US-based infrastructure
- **Better privacy** with clear data handling policies
- **Referral offer**: $10 first month on standard plan via [referral link](https://synthetic.new/?referral=IDyp75aoQpW9YFt)
- See [Synthetic.new documentation](../synthetic-new.md) for details

### GLM Coding Plan (Budget Alternative)
- More affordable than nanoGPT
- Established provider with clear policies
- See [GLM Coding Plan documentation](../glm-coding-plan.md) for details

## Recommendation
nanoGPT occupies a specific niche:
- **As a backup plan**: Useful when your primary provider experiences downtime
- **For model exploration**: Excellent for experimenting with different models
- **Learning purposes**: Good for educational projects and tutorials
- **Public projects**: Fine for open-source work where code will be public anyway

**Critical Warning**: Do **NOT** use nanoGPT if:
- You're working with proprietary or sensitive code
- Your work involves client data or confidential information
- You have any concerns about your code being used for training
- You need clear data handling guarantees for compliance

**Bottom Line**: The generous subscription limits and model variety make nanoGPT appealing for experimentation, but the privacy trade-offs make it unsuitable for professional development with sensitive data. Unless you're specifically okay with the uncertainty around data handling and potential use of your code for training, choose providers with clear infrastructure ownership and privacy guarantees.

For most developers, spending slightly more on Synthetic.new or GLM Coding Plan is worthwhile for the peace of mind regarding data privacy and security.

**Official Resources**: [nano-gpt.com](https://nano-gpt.com/invite/9yrQteBR)

Back: [Honorable Mentions](README.md)
