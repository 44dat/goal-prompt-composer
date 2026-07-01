# Goal Prompt Composer

Goal Prompt Composer is a Codex skill that turns ambiguous objectives into concise, loop-based Goal prompts.

It helps convert an informal request into a practical execution prompt with:

- Goal
- Loop
- Complete when
- Verify by
- Constraints
- Stop if
- Work allocation
- Report

The generated prompt is designed to be pasted directly into a Goal-oriented Codex workflow.

## Why Use It

Use this skill when a task is still vague but you want Codex to work in a controlled, verifiable loop.

It is especially useful for:

- Turning a short idea into an execution-ready prompt
- Adding observable completion criteria
- Defining verification steps before work begins
- Making stop conditions explicit
- Deciding whether subagents or parallel threads should be used
- Keeping long-running work grounded in inspect, act, verify, and decide cycles

## Install

Copy this folder into a Codex skills directory.

Project-local install:

```text
<workspace>\.codex\skills\goal-prompt-composer
```

User-level install:

```text
%USERPROFILE%\.codex\skills\goal-prompt-composer
```

The skill folder should contain:

```text
goal-prompt-composer/
├─ SKILL.md
├─ README.md
├─ LICENSE
└─ agents/
   └─ openai.yaml
```

## Usage

Invoke the skill by name and provide an ambiguous objective.

```text
Use $goal-prompt-composer to convert this ambiguous objective into a concise loop-based Goal prompt.

Objective:
Clean up the README and make setup instructions verifiable.
```

Example output:

```text
Goal: Improve the README so a new user can set up, run, and verify the project.

Loop:
1. Inspect the README and nearby project files for the next missing or stale section.
2. Update only that section.
3. Verify the change against repository files or available commands.
4. Decide whether another section needs work, the approach needs adjustment, or the README is complete.
5. Repeat until the completion criteria are met or a stop condition occurs.

Complete when:
- The README explains purpose, setup, usage, verification, and troubleshooting.
- Unsupported claims are removed or marked as unverified.

Verify by:
- Read the final README end to end.
- Spot-check referenced commands against project files.

Constraints:
- Do not change application code unless a README command is demonstrably wrong.

Stop if:
- Required behavior cannot be inferred from the repository.

Work allocation:
- Main thread edits the README loop by loop.
- Use a subagent only for an independent accuracy pass if the project is large.

Report:
- After each meaningful loop, state what changed and how it was checked.
- Final report summarizes changed sections and remaining risks.
```

## Notes

The skill intentionally keeps prompts compact. It should add enough structure to make execution observable without over-specifying the implementation.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

# Goal Prompt Composer 日本語版

Goal Prompt Composer は、曖昧な目標や短い依頼を、Goal に渡しやすい短いループ型プロンプトへ変換する Codex スキルです。

次のような要素を含む実行用プロンプトを作ります。

- Goal
- Loop
- Complete when
- Verify by
- Constraints
- Stop if
- Work allocation
- Report

生成されたプロンプトは、Goal 向けの Codex ワークフローにそのまま貼り付けて使える形を目指します。

## 何に使うか

まだ曖昧なタスクを、検証可能なループで進めたい時に使います。

特に向いている用途:

- 短いアイデアを実行可能なプロンプトに変換する
- 観測可能な完了条件を追加する
- 作業前に検証方法を決める
- 停止条件を明確にする
- subagent や parallel thread を使うべきか整理する
- 長めの作業を inspect、act、verify、decide の反復で進める

## インストール

このフォルダを Codex の skills ディレクトリにコピーします。

プロジェクト単位で使う場合:

```text
<workspace>\.codex\skills\goal-prompt-composer
```

ユーザー単位で使う場合:

```text
%USERPROFILE%\.codex\skills\goal-prompt-composer
```

フォルダ構成:

```text
goal-prompt-composer/
├─ SKILL.md
├─ README.md
├─ LICENSE
└─ agents/
   └─ openai.yaml
```

## 使い方

スキル名を指定して、曖昧な目標を渡します。

```text
$goal-prompt-composer を使って、次の曖昧な目標を短いループ型 Goal プロンプトにしてください。

目標:
README を整えて、セットアップ手順を検証可能にしたい。
```

出力例:

```text
Goal: README を改善し、新しいユーザーがセットアップ、実行、検証までできる状態にする。

Loop:
1. README と周辺ファイルを確認し、次に直すべき不足または古いセクションを1つ選ぶ。
2. そのセクションだけを更新する。
3. リポジトリ内のファイルや利用可能なコマンドで変更内容を確認する。
4. 次のセクションへ進むか、方針を調整するか、完了とするか判断する。
5. 完了条件を満たすか停止条件に当たるまで繰り返す。

Complete when:
- README に目的、セットアップ、使い方、検証方法、トラブルシュートがある。
- 根拠のない説明が削除または未検証として明示されている。

Verify by:
- README を最初から最後まで読み直す。
- 記載されたコマンドをプロジェクトファイルと照合する。

Constraints:
- README のコマンドが明確に間違っている場合を除き、アプリケーションコードは変更しない。

Stop if:
- 必要な挙動をリポジトリから推測できない。

Work allocation:
- Main thread で README をループ単位で編集する。
- プロジェクトが大きい場合のみ、subagent に独立した正確性チェックを割り当てる。

Report:
- 各ループ後に、変更した箇所と確認方法を短く述べる。
- 最終報告では変更セクションと残るリスクをまとめる。
```

## 補足

このスキルは、プロンプトを意図的に短く保ちます。実装方法を細かく決めすぎず、作業が観測・検証できるだけの構造を追加することを重視します。

## ライセンス

このプロジェクトは MIT License で公開されています。詳細は [LICENSE](LICENSE) を参照してください。
