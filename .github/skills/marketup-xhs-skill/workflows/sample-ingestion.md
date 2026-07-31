# Sample Ingestion and Capacity

Use this workflow after direct Xiaohongshu-note deconstruction and whenever the user explicitly requests sample ingestion, collection, archiving, or saving.

## Resolve the target

1. Read the active Profile manifest.
2. Allow persistence only when the Profile is `active_limited` or `active`, lists `sample_ingestion` in `supported_tasks`, and provides a writable `historical_collection` or `sample_library` plus `sample_index`.
3. If no eligible target Profile exists, return the deconstruction result without saving and state that no ready company sample library was available. Do not write into `profiles/_template/` or another company.

## Count effective samples

Count distinct effective samples in the active Profile before each new result:

- Prefer the configured `historical_collection`; otherwise count records listed by `sample_index` in `sample_library`.
- A sample is effective only when its title is non-empty and at least one of source reference, cover observation, body text, or body structure is non-empty.
- Identify duplicates by normalized `source_ref` when available; otherwise by normalized `keyword + title`.
- Ignore headers, empty reserved rows, placeholders, and duplicate records.
- Exclude every file or record marked `granularity_only`, including `templates/note_collection_granularity_example.md`.

## Persistence rule

- When `effective_sample_count < 20`, automatically route each direct deconstruction result to `sample_ingestion` without asking. Save non-duplicate samples until the count reaches 20.
- When `effective_sample_count >= 20`, keep direct deconstruction task-local unless the user explicitly requests ingestion, collection, archiving, or saving.
- If a sample is a duplicate but contains useful missing fields, update only that sample record instead of creating another countable entry.
- After automatic ingestion, report one short line: `已自动收录到当前企业样本库：N/20。`

## Write boundary

Normalize through `schemas/collection-fields.md` and the active collection adapter. Update only:

- the configured `historical_collection`, when present;
- the configured `sample_library` record, when needed;
- the configured `sample_index`.

Do not change brand, product, audience, visual, compliance, evidence registry, keywords, search terms, profile status, or supported tasks. Do not promote reference material into company facts.
