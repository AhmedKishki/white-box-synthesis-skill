# White-Box Synthesis

Answers a query from the sources you supply, using only their wording. The agent copies, trims, orders, inflects and normalises source spans. Any connecting words the agent writes itself appear inline as `⟦AI-AUTHORED: …⟧`.

## Use

Give the query and the sources together. A source can be a passage, an excerpt, a note or a retrieval (RAG) result. For example:

> Use white-box-synthesis. Query: What happened to prices and incomes after the mill closed?
> S1 — Lee, *Example Book*, p. 3: "…"
> S2 — retrieval result, Diaz, *Sample Study*, ch. 2: "…"

The agent returns a reply with a reference marker on every sentence and a list of references. It names any part of the query the sources leave unanswered. Ask for provenance to see each sentence's copied spans and every operation applied to them.

The agent's entry point is [SKILL.md](SKILL.md). Install the complete directory so its linked reference remains available. The skill provides instructions; its fidelity depends on the host agent following them.
