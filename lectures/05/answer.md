# Lecture 05 Answers

## Homework

**Level chosen — Basic.** I reduced `RAG_TOP_K` in `app/config.py` from 5 to 2. This sets the maximum number of pages returned by each call to `search_materials`. The change uses the existing SQLite index and requires no rebuild.

**Comparison question.** In Lecture 02, what does LoRA freeze and what does it train? What does QLoRA add?

### Live before-and-after results

I ran the five-page baseline first and the two-page variant second, once each. Both runs used `gemini-3.5-flash-lite`, the same instructions and question, and the same bundled index of 214 pages from the main materials for Lectures 01–03.

| Measurement | Before, top 5 | After, top 2 |
| --- | --- | --- |
| Search calls shown by the trace | 1 × `search_materials` | 1 × `search_materials` |
| Search query | `LoRA freeze train QLoRA add` | `LoRA freeze train QLoRA add` |
| Answer | Frozen base weights, trained low-rank matrices A and B, plus 4-bit base weights for QLoRA. Includes an example about memory use. | Same three core facts, followed by a study prompt. |
| Model citations | Lecture 2, pp. 51–52 | Lecture 2, pp. 51–52 |
| Wall time, including retrieval and embedding | 10.10 s | 9.62 s |
| Input / output tokens | 2,759 / 279 | 1,619 / 242 |
| Model responses | 2 | 2 |
| Estimated generation API cost | $0.001525 | $0.001091 |

The course's estimated cost covers generation and excludes embeddings and index construction. Earlier setup attempts returned HTTP 403 before generation. The measurements above are from the successful runs.

### Answer and evidence check

LoRA freezes the pretrained weights and trains two small low-rank matrices, A and B, whose product represents the update. QLoRA additionally quantizes the frozen base weights to 4 bits to reduce memory use. I checked both answers against the bundled slide text. Japanese source p.52 explicitly identifies the frozen weights and trainable matrices, and p.51 summarizes both techniques. Both model answers cited pp.51–52 but left the source edition implicit. The index identifies those numbers as Japanese source pages and maps source p.52 to translated PDF p.75.

The live trace shows the first returned page, `lec02-main-p052`, at both limits. I separately replayed the same query with the Gemini embedder and a limit of 5 to inspect the full ranking. The replay returned `lec02-main-p052`, `lec02-main-p051`, `lec02-main-p047`, `lec02-main-p060`, and `lec02-main-p061`, in that order. The first two support the core answer. The other pages discuss knowledge adaptation, exercise design, and exercise steps.

### Findings and limitations

With two pages, the agent used 1,140 fewer input tokens (about 41%) and the estimated generation cost was about 28% lower. Both answers were correct and both runs made one search call. The 0.48-second time difference comes from a single pair of runs and does not establish a speed improvement. A lower cap could omit evidence for questions that depend on a page ranked third or lower. I would test a multi-page question before using two pages as the general default. All 21 repository tests passed with the two-page setting.

### Offline check

Before completing the live runs, I used a scripted model and the stored vector for `lec02-main-p051` to test the result limit against the actual bundled index. The model called `search_materials({"query": "LoRA QLoRA difference"})` once and returned a placeholder. The search vector and query were fixed across these two local runs.

| Offline measurement | Before, top 5 | After, top 2 |
| --- | --- | --- |
| Search calls | 1 scripted call | 1 scripted call |
| Returned pages, Lecture 02 Japanese source, in rank order | 51, 52, 46, 58, 23 | 51, 52 |
| Directly supporting pages | 51, 52 | 51, 52 |
| Tool response size, including metadata | 7,434 characters | 3,342 characters |
| Local wall time, one run per setting | 0.04 s | 0.04 s |
| Input/output token estimates from the scripted model | 1,263 / 21 | 658 / 21 |
| Scripted model responses | 2 | 2 |
| Estimated generation API cost | Unavailable | Unavailable |

**AI assistance.** Codex prepared the configuration change, ran the live and offline comparisons and repository tests, and checked the cited content in the bundled slides.
