## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/80

**Issue title:** DELETE /profiles/{profile_id} doesn't cascade to delete associated reviews and embeddings


**Tier:** [ ] Tier 1  [✅] Tier 2  [ ] Tier 3
I selected a Tier 2 issue because I could understand what part of the app was affected and I wanted to challenge myself to pick a Tier 2 issue even though I've never made an open source contribution before.

**Problem summary:**
The issue lies with the fact that when a user's profile is deleted from the database, the vector store embeddings and review records related to that profile aren't removed. A successful fix would get rid of all associated information related to the profile that needs to be deleted from the database and the vector store database. The part of the codebase the issue affects is the ChromaDB vector store deletion path in `profile_service.py`.

**Branch name:** fix/80-profile-cascade-deletion

**Setup confirmation:** [✅] App runs locally at localhost:5173

**Cohort ledger:** [✅] Issue added to cohort ledger


## Week 8 — Reproduction & solution planning

**Reproducing issue #80:** 
- Ran the app, created a profile, added sources, and then tried deleting a profile after which I queried Postgres and all ingestions and reviews related to the profile were deleted 
- Went through `delete_profile` in `profile_service.py` and noticed there's no import for ChromaDB, only ingested sources, reviews, and the profile itself are deleted from Postgres, leaving information still in the vector database
- I then went to the retriever folder and investigated `vector_store.py` and noticed that there was a method to delete individual sources based on their id, but no method to delete a whole profile collection (`profile_{profile_id}`) which is why there were orphaned embeddings

**Reproduction commit link:** [link to commit documenting the reproduced issue]

**Reproduction summary:**


**PLAN.md link:** [link to PLAN.md in your fork]

**Blockers or open questions:**
