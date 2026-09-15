# Astro Template

汎用 Astro スターターテンプレート。**パッケージマネージャは pnpm**。

## 構成

- **Astro 6** (`tsconfigs/strict` デフォルト)
- **Tailwind CSS v4** (`@tailwindcss/vite`)
- **ESLint** (Flat config) + `eslint-plugin-astro` + `typescript-eslint`
- **Prettier** + `prettier-plugin-astro` + `prettier-plugin-tailwindcss`
- **@astrojs/sitemap** (SEO)
- **husky** + **lint-staged** (pre-commit)
- Path alias: 主要ディレクトリごとに専用エイリアス（後述）

## ディレクトリ構成

```
src/
├── assets/          # Astro が最適化処理する画像など
├── components/
│   ├── ui/          # 再利用可能なUI primitives (Button, Card など)
│   └── layout/      # Header / Footer / Nav などレイアウト構成要素
├── layouts/         # ページ全体のレイアウト
├── lib/             # 関数/ヘルパー (cn など)
├── pages/           # ルーティング (Astro 必須)
├── styles/          # global.css など
└── types/           # 共有 TypeScript 型
```

### Path alias によるimport

`tsconfig.json` に以下のエイリアスを設定済み:

| Alias           | 解決先                                                 |
| --------------- | ------------------------------------------------------ |
| `@/*`           | `src/*` (catch-all)                                    |
| `@layouts/*`    | `src/layouts/*`                                        |
| `@components/*` | `src/components/*`                                     |
| `@ui/*`         | `src/components/ui/*`                                  |
| `@layout/*`     | `src/components/layout/*`                              |
| `@lib/*`        | `src/lib/*`                                            |
| `@styles/*`     | `src/styles/*`                                         |
| `@assets/*`     | `src/assets/*`                                         |
| `~types/*`      | `src/types/*` (※`@types`はTSが予約済みのため`~`を使用) |

```astro
---
import Layout from '@layouts/Layout.astro';
import Button from '@ui/Button.astro';
import Header from '@layout/Header.astro';
import { cn } from '@lib/cn';
import type { NavItem } from '~types/site';
---
```

## セットアップ

```bash
pnpm install
```

## コマンド

| Command             | 内容                              |
| ------------------- | --------------------------------- |
| `pnpm dev`          | 開発サーバ起動 (`localhost:4321`) |
| `pnpm build`        | `astro check` + 本番ビルド        |
| `pnpm preview`      | ビルド成果物のローカルプレビュー  |
| `pnpm lint`         | ESLint                            |
| `pnpm lint:fix`     | ESLint 自動修正                   |
| `pnpm format`       | Prettier 整形                     |
| `pnpm format:check` | Prettier 検証のみ                 |

## 拡張の追加

```bash
pnpm astro add mdx        # MDX サポート
pnpm astro add react      # React コンポーネントを島として使う
pnpm astro add vercel     # Vercel デプロイアダプタ
```

## テンプレートとして利用する

1. このディレクトリをコピー or GitHub テンプレート化
2. `package.json` の `name` を変更
3. `astro.config.mjs` の `site` を実際のドメインに変更
