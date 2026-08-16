# Security and publication notes

This repository is a sanitized demonstrator. Do **not** commit:

- API keys, access tokens, cookies, webhook secrets, or credential exports.
- n8n credential IDs, workflow IDs, instance IDs, or internal hostnames.
- Feishu/Lark Base `app_token`, `table_id`, `view_id`, or internal workspace identifiers.
- Private RSS source registries, internal watchlists, or company-specific priority rules.
- Proprietary article datasets, internal reports, supplier information, or unpublished engineering data.
- Company-specific prompts or taxonomies if they encode non-public strategy.

The production workflow should keep integrations and credentials in the private n8n instance. The public workflow should use synthetic inputs and placeholder integrations.
