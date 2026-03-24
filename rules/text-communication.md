# Text Rules: Communication, Filler, and Hedging Patterns

Nine patterns covering chatbot conversational artifacts, filler language, hedging, and generic conclusions.

---

## 19. Chatbot Artifacts

**Words to watch:** I hope this helps, Of course!, Certainly!, You're absolutely right!, Would you like..., let me know, here is a..., feel free to, don't hesitate to, happy to help, I'd be glad to

**Problem:** Conversational scaffolding from chatbot interactions gets pasted directly into content. These are response-to-a-prompt phrases, not writing.

**Before:**
> Here is an overview of the French Revolution. I hope this helps! Let me know if you'd like me to expand on any section.

**After:**
> The French Revolution began in 1789 when financial crisis and food shortages led to widespread unrest.

**Fix:** Delete entirely. These are conversational, not content.

---

## 20. Knowledge-Cutoff Disclaimers

**Words to watch:** as of [date], Up to my last training update, While specific details are limited/scarce..., based on available information..., at the time of writing, to my knowledge

**Problem:** AI disclaimers about incomplete information get left in published text. They signal "an AI wrote this and wasn't sure."

**Before:**
> While specific details about the company's founding are not extensively documented in readily available sources, it appears to have been established sometime in the 1990s.

**After:**
> The company was founded in 1994, according to its registration documents.

**Fix:** Either find the information or don't include the claim. Hedging about your own knowledge is an AI pattern, not a human one. Humans either know something or don't mention it.

---

## 21. Sycophantic / Servile Tone

**Problem:** Overly positive, people-pleasing language. Praising the question before answering. Agreeing enthusiastically with everything. This reads as performative, not genuine.

**Before:**
> Great question! You're absolutely right that this is a complex topic. That's an excellent point about the economic factors.

**After:**
> The economic factors you mentioned are relevant here.

**Fix:** Delete the praise. Answer directly. If you genuinely agree, show it through your analysis, not through exclamation marks.

---

## 22. Filler Phrases

**Problem:** LLMs pad sentences with constructions that add length without adding meaning. These make writing feel bureaucratic and slow.

| Kill | Replace with |
|------|-------------|
| In order to achieve this goal | To achieve this |
| Due to the fact that | Because |
| At this point in time | Now |
| In the event that you need help | If you need help |
| The system has the ability to process | The system can process |
| It is important to note that the data shows | The data shows |
| At its core | *(delete)* |
| At the end of the day | *(delete)* |
| In today's fast-paced world | *(delete — always delete this one)* |
| It goes without saying | *(then don't say it)* |
| Needless to say | *(then don't)* |
| As a matter of fact | *(delete)* |
| The fact of the matter is | *(delete)* |
| For all intents and purposes | *(delete)* |
| In terms of | About / For |
| With regard to | About / On |
| In light of | Given / Because of |
| It's worth mentioning that | *(delete — just mention it)* |
| It's important to note that | *(delete — just note it)* |

**Fix:** Cut the phrase and start with the actual content. If removing the filler breaks the sentence, the sentence needed rewriting anyway.

---

## 23. Excessive Hedging

**Problem:** LLMs stack multiple hedging modals and qualifiers until statements say nothing. One hedge is fine for genuinely uncertain claims. Three hedges in a row is an AI pattern.

**Before:**
> It could potentially possibly be argued that the policy might have some effect on outcomes.

**After:**
> The policy may affect outcomes.

**Hedging words to watch for stacking:** could, potentially, possibly, arguably, might, perhaps, it seems, appears to, tends to, in some cases

**Fix:** One hedge per claim maximum. Pick the one that most accurately conveys your confidence level. Delete the rest.

---

## 24. Generic Positive Conclusions

**Problem:** LLMs end with vague upbeat statements that could apply to literally anything. These conclusions add no information and feel like a greeting card.

**Words to watch:** The future looks bright, exciting times lie ahead, continues their journey toward excellence, represents a major step, poised for success, remains to be seen, only time will tell

**Before:**
> The future looks bright for the company. Exciting times lie ahead as they continue their journey toward excellence. This represents a major step in the right direction.

**After:**
> The company plans to open two more locations next year.

**Fix:** End with a specific fact, a forward-looking action, or a question. If you can swap your conclusion onto a completely different article and it still works, it's too generic.
