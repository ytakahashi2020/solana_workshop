# Solana 勉強会 - GitHub Codespaces

Solana開発に必要なツールがすべてプリインストールされたGitHub Codespaces環境です。

## 含まれるツール

| ツール | 説明 |
|--------|------|
| **Solana CLI (Agave)** | Solanaのコマンドラインツール |
| **Anchor** | Solanaスマートコントラクト開発フレームワーク |
| **Rust** | Solanaプログラム開発言語 |
| **Node.js 22 LTS** | フロントエンド・ツール実行環境 |
| **pnpm** | パッケージマネージャー |

## 使い方

### 1. Codespaceの起動

GitHubリポジトリページで **Code** > **Codespaces** > **Create codespace on main** をクリック。

> ビルドに10〜15分程度かかります。初回のみ時間がかかりますが、2回目以降はキャッシュが効きます。

### 2. Solana Dappの作成

Codespace起動後、ターミナルで以下を実行：

```bash
npx create-solana-dapp@latest
```

対話形式でプロジェクト名やテンプレートを選択できます。

### 3. 作成したプロジェクトの起動

```bash
cd <プロジェクト名>
pnpm install
pnpm dev
```

### 4. その他のよく使うコマンド

```bash
# バージョン確認
solana --version
anchor --version
rustc --version
node --version

# Solanaのネットワーク設定（devnet に切り替え）
solana config set --url devnet

# テストバリデータの起動（ローカルテスト用）
solana-test-validator

# Airdrop（devnetでテスト用SOLを取得）
solana airdrop 2

# Anchorプロジェクトの作成
anchor init my-program
cd my-program
anchor build
anchor test
```

## VS Code拡張機能

以下の拡張機能が自動インストールされます：

- **rust-analyzer** - Rustの補完・型チェック
- **CodeLLDB** - Rustデバッガー
- **Crates** - Cargo.tomlの依存関係管理
- **Even Better TOML** - TOML構文ハイライト
- **Live Share** - ペアプログラミング
- **ESLint / Prettier** - JavaScript/TypeScriptのリンター・フォーマッター

## トラブルシューティング

### `npx create-solana-dapp` が失敗する場合

```bash
# キャッシュクリア
npm cache clean --force
# 再実行
npx create-solana-dapp@latest
```

### Solana CLIが見つからない場合

```bash
# PATHを再読み込み
source ~/.bashrc
# または
export PATH="$HOME/.local/share/solana/install/active_release/bin:$PATH"
```

### Anchorビルドが失敗する場合

```bash
# Rustツールチェインの確認
rustup show
# Solana CLIバージョンとの互換性確認
solana --version
anchor --version
```
