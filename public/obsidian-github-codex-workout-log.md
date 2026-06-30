---
title: Notion から Obsidian に乗り換えて筋トレを記録した話
tags:
  - Obsidian
  - GitHub
  - Codex
  - AI
private: false
updated_at: '2026-07-01T00:13:14+09:00'
id: 05f40b9a65d8eaab73ec
organization_url_name: null
slide: false
ignorePublish: false
---

はじめまして！大学3年生のShuichiです！

筋トレの記録、みなさんは何で管理していますか？

私はこれまでNotionを使っていました。しかし、AIに過去の記録を読ませて次回のメニューを考えてもらうような運用をしたくなり、Obsidianへ移行しました。

ObsidianはMarkdownベースなので、GitHubで管理しやすく、Codexからもそのまま読み込めます。

この記事では、筋トレ記録をObsidianに移し、GitHubのプライベートリポジトリで管理しながら、AIと連携できる環境を作った流れを紹介します。

## やりたかったこと

やりたかったのは、単なる筋トレ記録アプリを作ることではありません。
ストレスフリーに記録をつけられるということです。

筋トレ記録でいうと、以下のような状態を目指しました。

- ジムではスマホで迷わず記録できる
- 前回の重量がすぐ見える
- 過去ログをCodexに読ませられる
- 次回のメニュー作成をAIに手伝ってもらえる

特に便利だったのは、ジムに着いたときに「今日は何をやるんだっけ」と迷わずに済むこと、やることの mdファイルを生成した時に前回の記録が確認できることです。

Obsidianでコマンドを実行すると今日のメニューが作られ、そこに前回重量も表示されるようにしました。これだけで重量設定がかなり楽になりました。

## Notionで感じていた課題

- CodeXなどのツールに読ませることができない
- NotionAI の使い勝手があまり良くない
- 前回の記録を探すのが面倒

Notion AIを使えば解決できる部分もあるかもしれません。ただ、使い心地が自分にはあまり合わなかったことと、学生にとって月額課金が少し重いこともあり、別の形を探しました。

そこで選んだのがObsidianです。

## なぜObsidianにしたのか

Obsidianを選んだ理由はシンプルです。

- Markdownファイルとして保存される
- Codexがそのまま読める
- （プラグインを使えば）スマホでも記録しやすい
- QuickAddで記録作成を自動化できる
- Dataviewで記録を集計できる

特に大きいのは、データが普通のMarkdownファイルであることです。

Markdownなら、Codexにリポジトリごと読ませることができます。テンプレートもスクリプトもログも同じリポジトリ内にあるので、「この記録形式に合わせて次回メニューを作って」みたいな相談がしやすくなります。

スマホとPCの同期はiCloudで行っています。そのうえで、Obsidian Gitプラグインを使って、自動でリポジトリにpushされるようにしています。

同期フローはこのような感じです。

```text
スマホのObsidian
  ↓ iCloud同期
PCのObsidian
  ↓ Obsidian Gitで自動push
GitHub repository
  ↓
Codexが参照・修正
```

## ディレクトリ構成

筋トレ記録まわりのディレクトリ構成はこんな感じです。

```text
life/
  obsidian/
    Workouts/
      Logs/
      Programs/
      Templates/
      Scripts/
  Training/
```

それぞれの役割はこうです。

```text
Logs/        # 日々の実績
Programs/    # Day 1〜Day 5 のメニュー設計
Templates/   # 新しく作るページの雛形
Scripts/     # QuickAddやDataviewの自動化
```

## スマホでの使い方

ジムではスマホからObsidianを開いて記録しています。

流れはこんな感じです。

```text
1. Obsidianを開く
2. コマンドパレットを開く
3. QuickAdd: Workouts: Start workout を実行
4. Day 1〜Day 5 を選ぶ
5. 今日のログが作られる
6. セットごとに 1:, 2:, 3: に直接入力する
```

実際のログはこんな感じです。

```md
# 2026-06-28

### Day 5: 二頭 + 三頭

#### ストレッチ
- [[obsidian/Workouts/Exercises/インクラインダンベルカール.md|インクラインダンベルカール]]
  - 1: 8kg × 12
  - 2: 8kg × 12
  - 3: 8kg × 12

#### 高負荷
- [[obsidian/Workouts/Exercises/EZバーカール.md|EZバーカール]]
  - 1: 10kg × 10
  - 2: 10kg × 10
  - 3: 10kg × 10

#### プレスダウン
- [[obsidian/Workouts/Exercises/ケーブルプレスダウン.md|ケーブルプレスダウン]]
  - 1: 18.75kg × 12
  - 2: 13.75kg × 17
  - 3: 16.25kg × 12
```

## 使っているプラグイン

主に使っているObsidianプラグインはこの3つです。

```text
Dataview
QuickAdd
Obsidian Git
```

QuickAddは、今日のトレーニングログを作るために使っています。

Dataviewは、ダッシュボードや部位ページ、種目ページで、過去ログを集計するために使っています。

Obsidian Gitは、ログをGitHubに自動pushするために使っています。スマホとPCの同期はiCloudで行い、GitHubへの保存はObsidian Gitで行うという分担です。

## まとめ

今回は、筋トレ記録をObsidianで管理するようにした話を書きました。

スマホではObsidianで迷わず記録し、PCとはiCloudで同期し、Obsidian Gitでリポジトリに自動pushする。そこにCodexを噛ませることで、過去ログの整理や次回メニュー作成、スクリプト改善までできるようになりました。

改善点やこうすればもっと便利になることなどが見つかったら書き足していこうと思います。

タスク管理なども同じ`life`リポジトリで管理し始めていますが、その話はまた別の記事で書こうと思います。
