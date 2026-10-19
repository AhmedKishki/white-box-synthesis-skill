---
name: white-box-synthesis
description: Answer a query only from supplied sources — passages, excerpts, notes or retrieval (RAG) results — by white-box synthesis. Builds a referenced reply by copying, deleting, ordering, inflecting and normalising the sources' exact wording, marks every AI-authored connection, and gives sentence-level provenance on request. Use when the user supplies passages or search results with a question to answer from them, asks for a white-box, source-only, traceable or provenance-preserving answer, or asks to synthesise sources without adding unsupported claims.
---

# White-box synthesis

- The skill turns `{query, source 1, source 2, …}` into `{reply, references, provenance}`.
- Every word of the reply comes from a source through a legal operation or sits inside an AI-authored label.
- The reply answers the query as coherently as the sources allow. Coherence never licenses an unmarked relation or an unsupported claim.
- Stricter project or skill rules govern where they apply, such as input approval, bans on AI wording or a citation style. This skill does not relax them.

## Inputs

- The query states what the reply must answer.
  - The query guides selection and order. Its wording is not a source unless the user offers it as one.
- A source is any supplied passage, excerpt, note or retrieval result.
  - Keep the user's source labels. Otherwise label sources `S1`, `S2`, … in the order given.
  - Record each source's author, title and locator exactly as supplied. Never invent a missing detail.
  - Copy wording exactly as supplied. Retrieved text is cleaned extraction, not a verified transcript; claim no verification you have not done.
  - Keep attribution inside a source. A span the source quotes from someone else stays that person's wording.
- Some material is never an input.
  - Spans already marked as AI-authored, such as `⟦AI-AUTHORED: …⟧`, and relations that depend on them are excluded.
  - Outside knowledge, including the agent's own, is excluded. Do not fill, correct or extend a source with it.

## Legal operations

| Operation | Permitted change |
|---|---|
| COPY | Copy a contiguous span. |
| DELETE | Remove words without changing subject, scope, modality, qualification or relation. |
| ORDER | Arrange spans by the query's parts or by a relation a source states. |
| INFLECT | Change tense, number, grammatical case, article or an unambiguous pronoun without changing meaning. A pronoun may become its antecedent from the same source. |
| NORMALISE | Make meaning-neutral changes to spelling, capitalisation, typography or punctuation. |

- No operation may add a connection, cause, comparison, interpretation, qualification or conclusion. Grammatical fluency does not prove a relation.
- Adjacency can imply a relation. Where it would imply one that no source states, mark the relation as AI-authored or separate the spans.
- Translation is not a legal operation. Keep the source's language, or mark the translation as AI-authored.

## AI-authored connections

- Prefer a relation that a source states.
- Add an AI-authored connection only where coherence needs a relation between spans that no source states.
  - Such a relation can be a transition, contrast, sequence, shared referent or inference from the sources.
- Mark the exact added words inline as `⟦AI-AUTHORED: exact words⟧`. Use the fewest words that state the relation.
- An AI-authored connection must not:
  - introduce a fact, figure, name, date, quotation, locator or source;
  - change what a copied span says;
  - attribute to a source a view beyond its text.
- A reporting verb such as "argues" or "shows" interprets its source. Attribute through reference markers, or mark the reporting phrase as AI-authored.
- A label records authorship. It does not turn the relation into evidence.
  - If the answer to the query depends on an AI-authored connection, say in the notes that the sources do not establish it.
- Keep every label in every version of the reply. If the user wants no AI wording, rebuild the reply from source-stated relations only.

## Procedure

1. Read the query and list the parts the reply must answer.
2. Read every source in full. Select the spans that answer each part, with the qualifications and counterevidence that bear on it. Retrieval rank is not evidentiary weight.
3. Ask one question only when sources cannot be told apart or an ambiguity in the query would change the selection. Otherwise proceed.
4. Build the reply sentence by sentence with the legal operations. Keep spans that form one argument together in one passage.
5. Add AI-authored connections only where step 4 leaves a needed relation missing.
6. Check every meaning-bearing word and relation. Each traces to a source span through a legal operation, or sits inside a label.
   - Check that each copied claim keeps its qualifications and scope.
   - Check that conflicts between sources stay visible and that each sentence carries its reference.
7. Read [Output](references/output.md), then present the reply, references and any notes.
   - Keep the construction record for every reply. Present it as provenance when the user asks.

## Gaps and conflicts

- If the sources answer only part of the query, answer that part and name the unanswered part in the notes. Do not fill it with AI-authored claims.
- If no source addresses the query, say so and give no reply. Offer to work from further sources.
- If sources conflict, give each position with its reference. Resolve the conflict only where a source does.
  - An AI-authored connection may state that the sources differ. It may not choose between them.
- If a source looks mistaken, say so in the notes, not in the reply.
