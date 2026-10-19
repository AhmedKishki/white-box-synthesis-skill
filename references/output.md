# Output

## Output shape

- Present the parts in this order. Omit Provenance unless the user asks for it, and omit Notes when none apply.

```markdown
**Reply**

<Passage. Each sentence ends with its reference marker. AI-authored words appear inline as ⟦AI-AUTHORED: …⟧.>

**References**

- [S1] <Author>, *<Title>*, <locator>.

**Provenance**

1. <Exact output sentence>
   - Input: <label>, <author>, *<title>*, <locator>.
   - <OPERATION>: <exact span or change>.

**Notes**

- <Unanswered part, dependence on an AI-authored connection, or source problem.>
```

## Reply

- Write as many paragraphs as the answer needs. Keep spans that form one argument together.
- End each sentence with a reference marker naming its source label, for example `[S1]`.
  - Add the locator to the marker when one source supplies spans from several locators, for example `[S1, p. 3]`.
  - List every source a sentence uses, for example `[S1; S2]`.
- Add no heading, lead-in or closing summary. Each would be AI-authored wording; mark one if the reply needs it.
- Present copied wording as prose with its reference. Follow the user's citation style where one is given, for example quotation marks around verbatim spans.

## References

- Give one entry per source label, in order of first use in the reply.
- Give author, title and locator exactly as supplied. Write "not supplied" for an absent detail.
- State when a source is a retrieval result or other unverified extraction.

## Provenance

- Give one entry per output sentence, in reply order.
- For each sentence, show the exact output and each input's label, author, title and locator.
- Show the exact copied span and every operation applied to it.
  - Spell out each deleted span, each inflection and normalisation as before → after, and the basis for each ordering.
  - Codes, counts or summaries alone do not meet this requirement.
- List each AI-authored span separately, with its exact words and the relation it supplies between which spans.
- When the user asks for provenance after the reply, reconstruct it by matching the reply against the sources. Report any span that does not match; never assign a span to a source by guesswork.

## Notes

- Name each part of the query the sources leave unanswered.
- State where the answer depends on an AI-authored connection rather than on a source.
- Report a suspected source error, an unverified extraction that matters to the answer, or an excluded AI-authored input span.

## Worked example

- Lee, Diaz and both titles below are hypothetical. They demonstrate the format and are not sources to cite.
- Input:
  - Query: What happened to prices and incomes in the town after the mill closed?
  - S1: Lee, *Example Book*, p. 3: "As noted earlier, prices in the town rose sharply after the mill closed in 1990."
  - S2: Diaz, *Sample Study*, ch. 2, a retrieval result: "Household incomes in the town fell by a third between 1990 and 1992."
- Output:

```markdown
**Reply**

Prices in the town rose sharply after the mill closed in 1990 [S1]. ⟦AI-AUTHORED: By contrast,⟧ household incomes in the town fell by a third between 1990 and 1992 [S2].

**References**

- [S1] Lee, *Example Book*, p. 3.
- [S2] Diaz, *Sample Study*, ch. 2. Retrieval result; wording not verified against the original.

**Provenance**

1. Prices in the town rose sharply after the mill closed in 1990 [S1].
   - Input: S1, Lee, *Example Book*, p. 3.
   - COPY: "As noted earlier, prices in the town rose sharply after the mill closed in 1990."
   - DELETE: "As noted earlier, ", a back-reference to text outside the input.
   - NORMALISE: "prices" → "Prices" at the start of the sentence.
   - ORDER: first, following the query's order of prices, then incomes.
2. ⟦AI-AUTHORED: By contrast,⟧ household incomes in the town fell by a third between 1990 and 1992 [S2].
   - Input: S2, Diaz, *Sample Study*, ch. 2.
   - COPY: "Household incomes in the town fell by a third between 1990 and 1992."
   - NORMALISE: "Household" → "household" after the AI-authored connection.
   - ORDER: second, following the query's order of prices, then incomes.
   - AI-authored: "By contrast," relates S2's falling incomes to S1's rising prices. Neither source states the contrast.

**Notes**

- S2 dates the fall in incomes from 1990 but does not mention the mill. Neither source states a cause for either change.
```
