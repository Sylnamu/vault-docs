# Review Code: Let Proof Decide How Deep to Review
Reference:

+ [https://youtu.be/b2QkhmQ0sT0?si=v-FekJwN75jg0zs_](https://youtu.be/b2QkhmQ0sT0?si=v-FekJwN75jg0zs_)

Core question: Are you still reviewing code line by line? Or do you review with a reviewing agent?

Short answer: it depends. Review is a gradient, not a binary choice.

---

## 1. Core Principle: Review Depth Should Follow Blast Radius
Don't apply the same review rigor to everything. Match effort to risk:

| Review depth | Change type |
| --- | --- |
| deep-read | core infrastructure |
| careful | shared behavior |
| proof-led | isolated leaf |


> How to validate and who reviews is defined in §3, §4, §6, §8. This section only defines the mapping.
>

---

## 2. How to Build: Plan Upfront, Gate the New Code
For a new feature, plan the whole thing at the beginning, then build it behind feature gates.

A feature gate lets you turn new branch logic on/off without affecting the main app.

Three steps:

1. **Roadmap: map the entire job first.** Have a full plan for the feature from the start, so agents know the whole scope, including where the integration piece will be.
2. **Broad strokes: build isolated pieces behind a flag.** Gate all isolated leaf nodes. The new feature stays contained because its flag is "off".
3. **Integrate later: touch shared and trunk paths deliberately.** Only after the leaves are solid, do the integration as a separate, deliberate step.

---

## 3. What a PR Should Contain: Author Proves, Reports Confidence
The author agent should prove the change and report confidence. Every PR should cover:

| Type | Meaning |
| --- | --- |
| Test | Focus on logic and check integration |
| Runtime | Use the actual feature end-to-end |
| Visual | Inspect what the user will see |
| Confidence | Report what was verified and what was not |


Example PR proof:

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/52071075/1791288909391-4b26ca54-e8c8-4719-8350-35cf35a41e91.png)

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/52071075/1791288860327-df7d243e-0e04-4877-bd6f-fcb535baa23a.png)

---

## 4. Fast Path: When Isolated Leaf Code Can Move Faster
Leaf code can move faster only when all of these hold (definitions in §2, §3):

+ actually isolated (§1: isolated leaf)
+ behind a feature gate (§2)
+ has visual or runtime proof (§3)
+ easy to roll back

---

## 5. Slow Path: Changing Existing Behavior Without a Gate
If you're changing existing behavior and it's NOT separated by a feature gate, you must anchor safety explicitly.

Every review still anchors on safety — ask these four:

+ What changed?
+ What must not change?
+ How far can failure travel?
+ Can we gate or roll it back?

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/52071075/1791289554117-a48ec26a-4c5b-4ca6-8244-567dd6795600.png)

---

## 6. Agent Does: Static Checks Are Not the Review
Leverage static checks, but don't count them as review. Let automation / agents run them:

+ Type checks / Linting
+ Focused tests / Production build

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/52071075/1791289582360-c0de0c66-dad7-4064-a8b6-5fd1c62071ae.png)

Routine, low-blast-radius diffs just need an agent to review — and agents are very good at it.

---

## 7. Developer Mindset: Merge-Ready Does Not Mean Launch-Ready
Stop reviewing the diff, start reviewing the complete feature.

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/52071075/1791290215610-b7b1341d-c4f8-4b91-966e-f81111b79648.png)

---

## 8. Agent Does: Before Launch, Attack the Whole Product
Before launch, have multiple agents attack the whole product, not just the diff:

+ Features: run every user flow
+ Bugs: explore weird states and failures
+ Performance: profile slow paths and bottlenecks
+ Security: probe inputs, permissions, and data

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/52071075/1791290268918-f0e25526-9097-41eb-a02f-80ceb473ba60.png)

---

## 9. Developer Process: Treat Every Launch Like an Experiment
1. Gate it — keep the feature easy to disable.
2. Start small — release to a limited cohort.
3. Watch — track crashes and product signals.
4. Decide — expand or roll back quickly.

<!-- 这是一张图片，ocr 内容为： -->
![](https://cdn.nlark.com/yuque/0/2026/png/52071075/1791290401389-5ffd4df6-f577-49b1-b362-46ee3c67f8e2.png)

