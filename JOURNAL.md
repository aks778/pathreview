## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/80

**Issue title:** DELETE /profiles/{profile_id} doesn't cascade to delete associated reviews and embeddings


**Tier:** [ ] Tier 1  [✅] Tier 2  [ ] Tier 3

**Problem summary:**
The issue lies with the fact that when a user's profile is deleted from the database, the vector store embeddings and review records related to that profile aren't removed. A successful fix would get rid of all associated information related to the profile that needs to be deleted from the database and the vector store database. The part of the codebase the issue affects is the ChromaDB vector store deletion path in `profile_service.py`.

**Branch name:** fix/80-profile-cascade-deletion

**Setup confirmation:** [✅] App runs locally at localhost:5173

**Cohort ledger:** [✅] Issue added to cohort ledger