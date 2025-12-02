# SEO・アクセス解析設定ガイド

このドキュメントでは、サイトに追加されたSEO・アクセス解析機能の使い方を説明します。

## ✅ 追加された機能

### 1. Google Analytics（アクセス解析）

**現在の状態**: プレースホルダー設定済み

**設定方法**:

1. [Google Analytics](https://analytics.google.com/)にアクセス
2. 「測定を開始」→プロパティを作成
3. 「測定ID（G-XXXXXXXXXX）」を取得
4. `index.html`の以下の部分を編集：

```html
<!-- 変更前 -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-XXXXXXXXXX');
</script>

<!-- 変更後（G-XXXXXXXXXXを実際の測定IDに置き換え） -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-YOUR-ACTUAL-ID"></script>
<script>
    window.dataLayer = window.dataLayer || [];
    function gtag(){dataLayer.push(arguments);}
    gtag('js', new Date());
    gtag('config', 'G-YOUR-ACTUAL-ID');
</script>
```

5. 変更を保存して `git push`

**確認方法**:
- Google Analyticsダッシュボードでリアルタイムレポートを確認
- サイトにアクセスして、訪問者数が表示されるか確認

---

### 2. OGPタグ（SNSシェア対応）

**現在の状態**: 設定完了 ✅

TwitterやFacebookでシェアされた際に、以下の情報が表示されます：
- タイトル: "Toru Inoue | Software Engineer"
- 説明文: "井上享のコーポレートサイト。長崎からリモートワークでソフトウェア開発を提供。"
- 画像: プロフィール画像

**テスト方法**:
- [Twitter Card Validator](https://cards-dev.twitter.com/validator)
- [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/)

URLを入力してプレビューを確認できます。

**OGP専用画像を追加する場合**（オプション）:
1. 1200x630pxの画像を作成
2. `images/ogp.png` として保存
3. `index.html`の以下の部分を変更：
   ```html
   <!-- profile.png → ogp.png に変更 -->
   <meta property="og:image" content="https://loopsketch.com/images/ogp.png">
   <meta name="twitter:image" content="https://loopsketch.com/images/ogp.png">
   ```

---

### 3. sitemap.xml（検索エンジン最適化）

**現在の状態**: 設定完了 ✅

**場所**: `https://loopsketch.com/sitemap.xml`

検索エンジンがサイト構造を理解しやすくするためのファイルです。

**更新方法**（ページを追加した場合）:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://loopsketch.com/</loc>
    <lastmod>2025-12-02</lastmod>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
  <!-- 新しいページを追加 -->
  <url>
    <loc>https://loopsketch.com/blog.html</loc>
    <lastmod>2025-12-02</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.8</priority>
  </url>
</urlset>
```

**Google Search Consoleに登録**（推奨）:
1. [Google Search Console](https://search.google.com/search-console)にアクセス
2. プロパティを追加
3. サイトマップを送信: `https://loopsketch.com/sitemap.xml`

---

### 4. robots.txt（クローラー制御）

**現在の状態**: 設定完了 ✅

**場所**: `https://loopsketch.com/robots.txt`

検索エンジンのクローラーに対して、サイト全体のクロールを許可しています。

**内容**:
```
User-agent: *
Allow: /
Sitemap: https://loopsketch.com/sitemap.xml
```

**特定のページをクロールから除外する場合**（オプション）:
```
User-agent: *
Allow: /
Disallow: /private/
Disallow: /admin/
Sitemap: https://loopsketch.com/sitemap.xml
```

---

## 🎯 次のステップ（推奨）

### Google Search Consoleに登録
1. https://search.google.com/search-console
2. プロパティを追加（loopsketch.com）
3. 所有権を確認（DNSレコードまたはHTMLファイル）
4. サイトマップを送信

### アクセス解析の活用
1. Google Analytics測定IDを設定
2. 週次でアクセス数を確認
3. 人気ページや流入経路を分析

### SEOの改善
1. Google Search Consoleでキーワードを確認
2. タイトルやdescriptionを最適化
3. コンテンツを定期的に更新

---

## 📚 参考リンク

- [Google Analytics](https://analytics.google.com/)
- [Google Search Console](https://search.google.com/search-console)
- [Twitter Card Validator](https://cards-dev.twitter.com/validator)
- [Facebook Sharing Debugger](https://developers.facebook.com/tools/debug/)
