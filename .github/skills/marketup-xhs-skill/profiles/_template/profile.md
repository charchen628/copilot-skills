# Enterprise Profile Manifest

- `profile_status`: `template`
- `supported_tasks`: `profile_setup`
- `last_verified_at`:
- `brand`: `brand.md`
- `product`: `product.md`
- `audience`: `audience.md`
- `visual`: `visual.md`
- `compliance`: `compliance.md`
- `evidence_registry`: `evidence.md`
- `keywords`: `data/keywords.csv`
- `search_terms`: `data/search_terms.csv`
- `collection_adapter`: `../../adapters/collection/default.md`
- `historical_collection`: `samples/collection.md`
- `sample_index`: `samples/sample_index.md`
- `sample_library`: `samples/`
- `transfer_rules`: optional enterprise-specific rules
- `compliance_checklist`: optional enterprise-specific checklist

复制本目录后先执行 `workflows/profile-setup.md`。不要直接把 `profile_status` 改为 `active`；只有通过任务开放门槛后才能更新状态和 `supported_tasks`。不存在的可选文件应从清单删除，不要指向其他企业目录。
