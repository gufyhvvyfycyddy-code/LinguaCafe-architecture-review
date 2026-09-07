# Anki / MaiMemo / Context-Learning Reference

本文件把“官方事实”“社区体验”“LinguaCafe 判断”分开，避免把社区意见写成官方规则。

## 1. Anki 官方可借鉴部分

Anki 官方 Manual 明确提供：
- Question / Show Answer 学习流程；
- Again / Hard / Good / Easy 评分；
- FSRS；
- Card Info 与 Review History；
- Statistics；
- Deck Options / desired retention / FSRS optimization。

官方参考：
- https://docs.ankiweb.net/
- https://docs.ankiweb.net/deck-options
- https://docs.ankiweb.net/stats.html

LinguaCafe 已冻结的借鉴：
- 正式评分保留四档语义；
- FSRS 调度不在前端复制；
- Card Info/History 用于解释一张卡；
- 高级参数退到次级入口。

## 2. Anki 社区反复出现的摩擦

这些属于用户经验，不是 Anki 官方事实。

2026 languagelearning 讨论里，有用户明确表示制作/整理 flashcards 太耗时，希望把阅读和语境自动连起来：
- https://www.reddit.com/r/languagelearning/comments/1tfaznk/not_able_to_use_ankisrs_while_reading_looking_for/
- https://www.reddit.com/r/languagelearning/comments/1ul9nsf/alternative_to_anki/
- https://www.reddit.com/r/Anki/comments/1vcprka/what_is_your_language_learning_workflow_any_tips/

这与 LinguaCafe 的产品假设一致：保留 Anki 成熟的复习语义，同时尽量让“建卡”发生在阅读流里。

## 3. MaiMemo / 墨墨官方可借鉴部分

墨墨官网当前用非常简短的语言强调：
- 内容简洁明了；
- 复习有的放矢；
- 数据一目了然。

官方：
- https://www.maimemo.com/

墨墨官网商店仍采用“单词上限”等付费商品，说明它的商业设计和 LinguaCafe 不一定相同：
- https://www.maimemo.com/shop

LinguaCafe 借鉴的是日常体验和信息层级，不直接复制其词汇额度商业模型。

## 4. LinguaCafe 的差异

- 学习对象是具体 WordSense。
- 原文 occurrence 参与学习证据。
- 阅读和复习共享同一学习对象。
- 同一 lemma 的不同义项可以独立学习。
- AI 主要做解释、翻译、消歧和候选，不自动伪造 ReviewLog。
- 不引入通用 Note Type / Template / 任意 Deck 树。

## 5. 需要外部审查者继续验证

- “减少建卡成本”是否真的提升长期留存？
- 语境例句是否会比传统词条更容易回忆？
- 首页的每日任务应该多接近墨墨，多少保留阅读自由度？
- 哪些 Anki 高级能力普通用户根本不需要看到？
- 哪些统计能帮助用户做学习决定，哪些只是工程指标？
