# zenn-articles-en

## 概要
英語記事のソース管理リポ。投稿先は dev.to（Zenn は日本語専用）。

## リポジトリ情報
- パス: `~/Claude/zenn-articles-en/`
- ブランチ: `main`
- リモート: `odakin/zenn-articles-en` (public, GitHub)

## 構造
```
zenn-articles-en/
├── CLAUDE.md        # このファイル
├── README.md        # 記事一覧・使い方
├── articles/        # 記事ソース
│   ├── *-en.md      # Zenn 形式（原本）
│   └── *-devto.md   # dev.to 形式（投稿用）
├── books/           # 未使用
├── package.json     # zenn-cli 依存（プレビュー用）
└── .gitignore
```

## 記事管理ワークフロー
1. Zenn 形式で原稿を書く（`articles/<slug>-en.md`）
2. dev.to 形式に変換（`articles/<slug>-devto.md`）
3. dev.to に投稿（手動コピペ or API）

### Zenn → dev.to 変換ルール
| Zenn | dev.to | 対応 |
|---|---|---|
| `topics: ["A", "B"]` | `tags: a, b` | 配列→カンマ区切り、最大4つ、小文字 |
| `emoji: "🧠"` | 削除（`cover_image` で代替可） | |
| `type: "tech"` | 削除 | |
| — | `description: "..."` | 追加（SEO 用） |
| — | `canonical_url: URL` | 追加（クロスポスト時） |
| `:::message` ... `:::` | `> **Note:** ...` | ブロック引用に変換 |
| `:::message alert` | `> **Warning:** ...` | ブロック引用に変換 |
| `# 見出し` | `## 見出し` | dev.to は `#` をタイトルに使うため、本文は `##` 始まり |
| `https://github.com/user/repo` | `{% github user/repo %}` | GitHub embed |

### dev.to 投稿（API）
```bash
curl -X POST https://dev.to/api/articles \
  -H "api-key: $DEVTO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"article": {"body_markdown": "...", "published": false}}'
```
API キー: https://dev.to/settings/extensions

## 運用
- ローカルプレビュー: `npx zenn preview` → http://localhost:8000（Zenn 形式のみ）
- **英語のみ。** 日本語記事は `odakin/zenn-articles` に格納

## How to Resume
1. SESSION.md は不要（記事リポのため）
2. README.md の記事一覧を参照
3. 変更後は commit + push

## 安全規則（公開リポ）
**このリポは public。** 以下を絶対にコミットしない:
- 実名（GitHub ユーザー名 `odakin` は可）
- メールアドレス
- 非公開リポ名
- 金融データ・口座情報
- 所属機関名
- 他ユーザーのユーザー名
- dev.to API キー

## 規約
- `~/Claude/CONVENTIONS.md` に従う
