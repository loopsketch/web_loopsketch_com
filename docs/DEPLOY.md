# 🚀 GitHub Pages デプロイ手順

このサイトはGitHub Pagesで完全無料でホスティングできます！

## 📁 プロジェクト構成

```
web_loopsketch_com/
├── index.html        # トップページ
├── css/              # スタイルシート
├── js/               # JavaScript
├── images/           # 画像ファイル
├── .github/          # GitHub Actions設定
│   └── workflows/
│       └── deploy.yml
├── .gitignore        # Git除外設定
├── DEPLOY.md         # このファイル
└── README.md         # プロジェクト説明
```

**シンプルな構成**: ルートディレクトリ全体がGitHub Pagesにデプロイされます。  
ローカルで `index.html` を開いてプレビューした状態と、デプロイ後の状態が同じになります！

## 📝 初回セットアップ手順

### 1. GitHubリポジトリを作成

1. [GitHub](https://github.com)にアクセスしてログイン
2. 右上の「+」→「New repository」をクリック
3. リポジトリ名を入力（例: `web_loopsketch_com` または `loopsketch.github.io`）
   - **重要**: `[ユーザー名].github.io` という名前にすると、そのままURLになります
4. 「Public」を選択（GitHub Pagesは無料版ではPublicのみ）
5. 「Create repository」をクリック

### 2. ローカルでGitリポジトリを初期化

ターミナルで以下のコマンドを実行：

```bash
cd "/Volumes/My Passport/works/web_loopsketch_com"

# Gitリポジトリを初期化
git init

# .gitignoreを作成（不要なファイルを除外）
cat > .gitignore << 'EOF'
.DS_Store
._*
node_modules/
.env
EOF

# 全ファイルをステージング
git add .

# 初回コミット
git commit -m "Initial commit: Add website files"

# mainブランチに変更（GitHubのデフォルトに合わせる）
git branch -M main

# GitHubリポジトリをリモートとして追加（URLは自分のものに変更）
git remote add origin https://github.com/あなたのユーザー名/リポジトリ名.git

# GitHubにプッシュ
git push -u origin main
```

### 3. GitHub Pagesを有効化

1. GitHubのリポジトリページにアクセス
2. 「Settings」タブをクリック
3. 左メニューから「Pages」をクリック
4. 「Source」セクションで以下を選択：
   - Source: **GitHub Actions**
5. 保存

### 4. 自動デプロイの確認

1. GitHubリポジトリの「Actions」タブをクリック
2. 「Deploy to GitHub Pages」ワークフローが実行されているか確認
3. 完了後、「Settings」→「Pages」で公開URLを確認
   - 通常: `https://ユーザー名.github.io/リポジトリ名/`
   - または: `https://ユーザー名.github.io/`（リポジトリ名が`ユーザー名.github.io`の場合）

---

## 🌐 独自ドメインの設定（loopsketch.comなど）

### 手順

1. **DNSレコードを設定**
   
   ドメイン管理サービス（お名前.com、ムームードメインなど）で以下を設定：

   #### Aレコード
   ```
   @    A    185.199.108.153
   @    A    185.199.109.153
   @    A    185.199.110.153
   @    A    185.199.111.153
   ```

   #### CNAMEレコード（wwwサブドメイン用）
   ```
   www  CNAME  ユーザー名.github.io.
   ```

2. **GitHub側で独自ドメインを設定**

   1. GitHubリポジトリの「Settings」→「Pages」
   2. 「Custom domain」に独自ドメインを入力（例: `loopsketch.com`）
   3. 「Save」をクリック
   4. 「Enforce HTTPS」にチェック（DNS設定後に有効化）

3. **CNAMEファイルを作成**

   プロジェクトのルートに `CNAME` ファイルを作成：

   ```bash
   echo "loopsketch.com" > CNAME
   git add CNAME
   git commit -m "Add custom domain"
   git push
   ```

---

## 🔄 更新方法

ファイルを編集したら、以下のコマンドでGitHubにプッシュするだけ：

```bash
cd "/Volumes/My Passport/works/web_loopsketch_com"

# 変更をステージング
git add .

# コミット
git commit -m "Update website content"

# プッシュ（自動的にデプロイされます）
git push
```

数分後にサイトが自動更新されます！

---

## 💰 コスト

- **GitHub Pages**: 完全無料
- **独自ドメイン**: 年間約1,000〜2,000円（ドメイン取得費用のみ）
- **HTTPS証明書**: 無料（GitHub Pagesが自動提供）

---

## 📊 制限事項

- リポジトリサイズ: 1GB未満推奨
- 帯域幅: 月100GB（個人サイトなら十分）
- ビルド時間: 10分/回
- 静的サイトのみ（サーバーサイド処理不可）

---

## 🆘 トラブルシューティング

### サイトが表示されない
1. 「Settings」→「Pages」でURLを確認
2. 「Actions」タブでデプロイが成功しているか確認
3. 数分待つ（初回は最大10分かかることも）

### 404エラーが出る
- `index.html` がルートディレクトリにあるか確認
- リポジトリがPublicになっているか確認

### CSSが読み込まれない
- `index.html` 内のパスが相対パスになっているか確認
- GitHub Pagesでは絶対パス `/` から始まるパスは使えない場合があります

---

## 📚 参考リンク

- [GitHub Pages 公式ドキュメント](https://docs.github.com/ja/pages)
- [カスタムドメイン設定](https://docs.github.com/ja/pages/configuring-a-custom-domain-for-your-github-pages-site)
