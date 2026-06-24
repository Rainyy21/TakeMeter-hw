# Project Planning Log: Reddit Classifier

## 1. Initial Data Collection Plan & Scope
* **Target Community:** r/LeagueofLegend
* **Initial Collection Target:** 200 public posts via Communalytic.
* **Feature Strategy:** Concatenating `Title` + `Body Text` into a single text block.

## 2. Initial Label Definitions & Taxonomy
* **[Discussion]:** Talk about update and their opinion about the game
* **[Community]:** Post about update to the game
* **[Esports]:** Show professional esports game play
* **[Gameplay]:** Player show their gameplay 

## 3. The Cold, Hard Edge-Case Rules (Drafted During Labeling)
As we manually reviewed the 200 posts, our initial taxonomy broke down on complex text. We established the following strict tie-breaking rules:
* **Rule 1 (Vent vs. Update):** If a post complains about a patch or balance change but does not propose a fix or ask a troubleshooting question, it goes to **Discussion**, not **Community**. **Community** is reserved for posts that announce or share factual news about updates.
* **Rule 2 (Pro Play vs. Personal Highlight):** If a post mentions a professional team, tournament, or roster move, it goes to **Esports** even if it also shows a clip. **Gameplay** is reserved for posts whose primary subject is the poster's own (non-pro) matches.
* **Rule 3 (Meta Talk vs. How-To):** If a post is framed as a guide, build, or "how to play X" walkthrough, it goes to **Gameplay**. General opinions about the meta or champion strength go to **Discussion**.

## 4. Evaluation Metrics Reasoning
We selected **Macro F1-Score** as our primary evaluation metric alongside raw **Accuracy**. 
* *Reasoning:* Because Reddit natural distributions are inherently imbalanced (e.g., way more "Vents" than "Technical News"), a simple accuracy metric would look high just by guessing the majority class. Macro F1 forces us to evaluate how well the model handles the underrepresented classes.

## 5. AI Tool Plan (Before Execution)
* **Annotation:** We plan to use An LLM to pre-label data to speed up manual review.
* **Error Diagnosis:** We will pass our misclassified examples through an LLM to help flag patterns we might miss manually.

## 6. Hard Annotation Decisions (Log)
Below are 3 specific examples where human annotation required a executive decision due to extreme ambiguity:
1. *Post:* "Fan Champion: Sharua, warden of the veils" -> Decided on **Community** because it talking about the update
2. *Post:* " T1 and G2 to attend their 5th MSI in a row. T1 and G2 have qualified for twice as many MSIs as any other team." -> Decided on **Esports** because it talking about the league esport team
3. *Post:* "How to play LOL (as a Brawl player)" -> Decided on **Gameplay** because it discuessing about the game and how to play
