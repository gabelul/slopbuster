# Text Rules: Style Patterns

Six patterns where LLMs reveal themselves through formatting choices and typographic habits.

---

## 13. Em Dash Overuse

**Problem:** LLMs use em dashes (—) far more than human writers, mimicking "punchy" sales writing. Two or three em dashes per paragraph is a strong AI signal. Replace most with commas, periods, or parentheses.

**Before:**
> The term is primarily promoted by Dutch institutions—not by the people themselves. You don't say "Netherlands, Europe" as an address—yet this mislabeling continues—even in official documents.

**After:**
> The term is primarily promoted by Dutch institutions, not by the people themselves. You don't say "Netherlands, Europe" as an address, yet this mislabeling continues in official documents.

**Fix:** One em dash per paragraph maximum. Use commas for parenthetical asides, periods for separate thoughts. Em dashes should feel deliberate, not decorative.

---

## 14. Boldface Overuse

**Problem:** LLMs emphasize phrases in boldface mechanically — bolding every important-sounding noun, turning emphasis into noise. When everything is bold, nothing is.

**Before:**
> It blends **OKRs (Objectives and Key Results)**, **KPIs (Key Performance Indicators)**, and visual strategy tools such as the **Business Model Canvas (BMC)** and **Balanced Scorecard (BSC)**.

**After:**
> It blends OKRs, KPIs, and visual strategy tools like the Business Model Canvas and Balanced Scorecard.

**Fix:** Bold only what genuinely needs emphasis — key terms on first introduction, critical warnings, or one focal point per section. Not every noun.

---

## 15. Inline-Header Vertical Lists

**Problem:** LLMs format information as bulleted lists where each item starts with a bolded header followed by a colon, then restates or expands on that header. This creates redundant structure — the label and the content say the same thing.

**Before:**
> - **User Experience:** The user experience has been significantly improved with a new interface.
> - **Performance:** Performance has been enhanced through optimized algorithms.
> - **Security:** Security has been strengthened with end-to-end encryption.

**After:**
> The update improves the interface, speeds up load times through optimized algorithms, and adds end-to-end encryption.

**Fix:** Convert to prose. If the items are genuinely distinct enough to warrant a list, remove the redundant headers. If they're not, merge into a sentence.

---

## 16. Title Case in Headings

**Problem:** LLMs capitalize all main words in headings. Human writers (outside of AP/Chicago style for published titles) increasingly use sentence case — capitalizing only the first word and proper nouns.

**Before:**
> ## Strategic Negotiations And Global Partnerships

**After:**
> ## Strategic negotiations and global partnerships

**Fix:** Use sentence case for headings unless the publication explicitly requires title case. This is a subtle but consistent tell.

---

## 17. Emojis as Structure

**Problem:** LLMs decorate headings, bullet points, and section markers with emojis. This looks like a LinkedIn post or a Notion template, not professional writing.

**Before:**
> 🚀 **Launch Phase:** The product launches in Q3
> 💡 **Key Insight:** Users prefer simplicity
> ✅ **Next Steps:** Schedule follow-up meeting

**After:**
> The product launches in Q3. User research showed a preference for simplicity. Next step: schedule a follow-up meeting.

**Fix:** Remove structural emojis entirely. Emojis are fine in casual messaging where they add tone — they're not fine as bullet-point replacements in content.

---

## 18. Curly Quotation Marks

**Problem:** ChatGPT specifically outputs curly/smart quotes ("...") instead of straight quotes ("..."). In plain text, markdown, and code contexts, this is a dead giveaway.

**Before:**
> He said \u201cthe project is on track\u201d but others disagreed.

**After:**
> He said "the project is on track" but others disagreed.

**Fix:** Replace all curly quotes with straight quotes in plain text and markdown. In published HTML, curly quotes may be appropriate — but in drafts and code, they're a tell.
