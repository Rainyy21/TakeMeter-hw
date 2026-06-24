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
* **Rule 1 (Sarcasm/Vent vs. Fact):** If a post uses heavy exaggeration but explicitly asks a troubleshooting question at the end, it must be categorized under [Label A], not [Label B].
* **Rule 2 (Topic vs. Structure):** If a post mentions a product keyword but its primary structural intent is a meme or a joke, it goes to [Label C].

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
