# English Expression Quiz App

ビジネス英語表現の学習用クイズアプリ

---

## 📱 使い方

### ローカルで試す（今すぐ）

1. **ブラウザでHTMLを開く**
   ```
   07_English_Learning/quiz-app/index.html をダブルクリック
   ```
   または
   ```
   右クリック → プログラムから開く → Google Chrome / Microsoft Edge
   ```

2. **学習開始！**
   - 日本語 → 英語 / 英語 → 日本語 を切り替え
   - カテゴリやフォーマル度でフィルタ
   - 「答えを見る」→「覚えた」or「まだ」で学習履歴を記録

---

## 🌐 モバイルで使う（GitHub Pages公開）

### Step 1: GitHubリポジトリ作成

1. **GitHub にログイン**
   https://github.com

2. **新しいリポジトリを作成**
   - 右上の「+」→「New repository」
   - Repository name: `english-quiz`（任意の名前）
   - Public（無料）または Private（有料だがGitHub Pro以上で可能）
   - 「Create repository」をクリック

### Step 2: ファイルをアップロード

**方法A: Web UIで直接アップロード（簡単）**

1. 作成したリポジトリページで「uploading an existing file」をクリック
2. 以下の4ファイルをドラッグ&ドロップ：
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `.gitignore`
3. 「Commit changes」をクリック

**方法B: Git コマンド（慣れている場合）**

```bash
cd 07_English_Learning/quiz-app

git init
git add index.html manifest.json sw.js .gitignore
git commit -m "Initial commit: PWA-enabled English Quiz App"
git branch -M main
git remote add origin https://github.com/あなたのユーザー名/english-quiz.git
git push -u origin main
```

### Step 3: GitHub Pages を有効化

1. リポジトリページで「Settings」タブをクリック
2. 左メニューから「Pages」を選択
3. Source: 「main」ブランチを選択
4. 「Save」をクリック
5. 数分待つと、URL が表示される：
   ```
   https://あなたのユーザー名.github.io/english-quiz/
   ```

### Step 4: スマホでアクセス

1. **スマホのブラウザで上記URLを開く**

2. **ホーム画面に追加（PWA化）**

   **iPhone (Safari):**
   - 下部の共有ボタン（□↑）をタップ
   - 「ホーム画面に追加」を選択
   - 「追加」をタップ

   **Android (Chrome):**
   - 右上のメニュー（⋮）をタップ
   - 「ホーム画面に追加」を選択
   - 「追加」をタップ

3. **ホーム画面のアイコンをタップして学習開始！**

---

## 🔄 データ更新方法

### 方法A: 自動更新（推奨）

Phrase Databaseに新しいフレーズを追加した後、以下のコマンドで自動反映：

```bash
cd 07_English_Learning
python convert_to_quiz_app.py
```

または Claude Code skill:
```
/update-quiz-app
```

**処理内容:**
- `Phrase_Database/*.md` から全フレーズを自動抽出
- quiz-app形式に変換
- `index.html` の `PHRASES_DATA` を自動更新

**実行結果:**
```
[OK] Total 112 phrases extracted
[OK] quiz-app\index.html updated successfully
```

### 方法B: 手動更新

1. **index.html を編集**
   - GitHub リポジトリページで `index.html` を開く
   - 鉛筆アイコン（Edit）をクリック
   - `PHRASES_DATA` オブジェクトの `phrases` 配列に追加：

   ```javascript
   {
       "id": "unique-id",
       "category": "カテゴリ名",
       "japanese": "日本語表現",
       "english": "English expression",
       "formality": "meeting",  // email, meeting, casual
       "alternatives": ["別の言い方1", "別の言い方2"],
       "example": "Example sentence.",
       "exampleJa": "例文の日本語訳",
       "nuance": "ニュアンスの説明",
       "scene": "使う場面"
   }
   ```

2. **変更をコミット**
   - 「Commit changes」をクリック

3. **スマホで自動更新**
   - アプリを再読み込み（リフレッシュ）すると最新データが反映
   - Service Workerがキャッシュを更新します

---

## 📊 機能一覧

### ✅ 実装済み機能

- **出題モード切り替え**
  - 日本語 → 英語
  - 英語 → 日本語

- **フィルタ機能**
  - カテゴリ別（Opening, Transitions, General, etc.）
  - フォーマル度別（📧 Email, 💼 Meeting, 👥 Casual）
  - 習得レベル別（学習中, 習得済み）

- **学習履歴管理**
  - 正解/不正解カウント
  - 今日の学習数
  - 累計学習数
  - 最終学習日（localStorage に保存）

- **マスター管理**
  - 「マスター」ボタン → 習得済みとしてマーク
  - 「再学習」で通常の出題対象に戻す

- **音声読み上げ機能 🎤**
  - 例文の英語をネイティブ音声で再生
  - マイクアイコンをタップで発音確認
  - Web Speech API 使用（デバイス依存）

- **統計表示**
  - 今日の学習数
  - 累計学習数
  - 習得済み数

- **ランダム出題**
  - フィルター変更時に自動シャッフル
  - 毎回異なる順序で出題

- **折りたたみ式設定**
  - 設定・フィルターエリアを折りたたみ可能
  - 学習画面を広く使える

- **PWA対応**
  - オフラインでも動作
  - ホーム画面に追加可能
  - アプリっぽいUX

- **レスポンシブデザイン**
  - スマホ、タブレット、PCに対応

---

## 🎨 カスタマイズ

### テーマカラーを変更したい

`index.html` の `<style>` セクションで以下を変更：

```css
/* グラデーション背景 */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* メインカラー */
.btn-primary {
    background: #2563eb;  /* ← この色を変更 */
}
```

### フレーズデータの構造

`index.html` 内の `PHRASES_DATA`:
```javascript
const PHRASES_DATA = {
    "phrases": [
        {
            "id": "一意のID",
            "category": "カテゴリ名",
            "japanese": "日本語表現",
            "english": "英語表現",
            "formality": "email | meeting | casual",
            "alternatives": ["別の言い方"],
            "example": "例文（英語）",
            "exampleJa": "例文（日本語）",
            "nuance": "ニュアンス",
            "scene": "使う場面"
        }
    ]
};
```

---

## 🔧 トラブルシューティング

### Q: スマホでURLを開いても動かない

**A:** 数分待ってから再度アクセスしてください。GitHub Pages は公開まで5-10分かかります。

### Q: 学習履歴が消えた

**A:** 学習履歴はブラウザの localStorage に保存されます。ブラウザのデータを削除すると消えます。

### Q: 新しいフレーズを追加したのに反映されない

**A:** ブラウザのキャッシュをクリアするか、スーパーリロード（Ctrl+Shift+R / Cmd+Shift+R）してください。

### Q: Private リポジトリで GitHub Pages を使いたい

**A:** GitHub Pro 以上のプラン（月4ドル）が必要です。または Public リポジトリにしてください。

---

## 📝 今後の拡張案

- [ ] Spaced Repetition System (SRS) の実装
- [x] 音声読み上げ機能（実装済み 🎤）
- [ ] 学習履歴のグラフ表示
- [ ] エクスポート/インポート機能
- [ ] 復習リマインダー通知

---

## 📄 ファイル構成

```
quiz-app/
├── index.html           # メインアプリ（HTML + CSS + JavaScript + フレーズデータ）
├── manifest.json        # PWA設定（アイコン、テーマカラー等）
├── sw.js                # Service Worker（オフライン対応、キャッシュ管理）
├── .gitignore           # Git除外設定
└── README.md            # このファイル
```

**注:** フレーズデータは `index.html` 内の `PHRASES_DATA` オブジェクトに埋め込まれています。

---

## 🙏 サポート

問題があれば、`phrases-data.json` のフォーマットを確認してください。

**Happy Learning! 🎯**
