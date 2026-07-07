# APIキー取得・設定ガイド

> 最終更新: 2026-07-15

---

## 概要

CityExplorerで使用するAPIキーの取得方法と設定手順。

キーは起動後のスタート画面「設定」→ **「Tab 1: API管理」** から入力して保存します。
保存したキーは暗号化された `userdata.dat` に統合管理されます。

> **⚠ セキュリティ注意**: `API_Key/` フォルダはGitの管理対象外（`.gitignore` に記載済み）です。APIキーをGitリポジトリにコミットしないでください。

---

## 設定項目一覧

### 必須設定（アプリ動作に必要）

| UIフィールド | サービス | クォータ | 取得手順 |
|------------|---------|---------|--------|
| Cesium Ion | Cesium Ion | 無料 | [Cesium Ion](#cesium-ion) |
| OpenWeather | OpenWeatherMap | 無料 (60回/分) | [OpenWeatherMap](#openweathermap) |
| YOLP Client ID | Yahoo! YOLP | 50,000/日 | [YOLP](#yolp) |

### オプション設定（より高機能な体験）

| UIフィールド | サービス | クォータ | 取得手順 |
|------------|---------|---------|--------|
| Google Maps | Google Maps Platform | 無料枠内 | [Google Maps](#google-maps-platform) |
| GCP Cloud Monitoring | GCP Monitoring | 無料 | [Cloud Monitoring](#cloud-monitoring任意) |
| Hotpepper | ホットペッパー | 無制限 | [ホットペッパー](#ホットペッパー) |
| Gemini | Google Gemini AI | 無料枠 (500 RPM) | [Gemini](#gemini) |
| GitHub Token | GitHub Models | 無料枠 | [GitHub Models](#github-models) |

### キー不要で使用可能なAPI

以下のAPIはキー不要で自動的に使用されます:

| API | 用途 |
|-----|------|
| Project PLATEAU | 日本3D建物モデル (四日市市) |
| OpenStreetMap / Overpass | POI検索（フォールバック）、繁華街ライト位置取得 |
| Nominatim | ジオコーディング |
| Open-Elevation | 標高データ |
| Wikipedia / Wikimedia | 記事・画像 |
| CartoDB Voyager | ミニマップタイル |

---

## 必須キーの取得

### Cesium Ion

3D地形・衛星画像の表示に必須。

1. https://ion.cesium.com/ にアクセス
2. アカウント作成（無料）
3. ログイン後、左メニュー「**Access Tokens**」をクリック
4. 「**Default Token**」のトークン文字列をコピー
5. スタート画面「設定」→「Tab 1: API管理」→「**Cesium Ion:**」欄に貼り付けて保存

### OpenWeatherMap

リアルタイム天候取得に必須。

1. https://openweathermap.org/api にアクセス
2. アカウント作成（無料）
3. 「**API keys**」タブでデフォルトキーをコピー
4. スタート画面「設定」→「Tab 1: API管理」→「**OpenWeather:**」欄に貼り付けて保存

> ℹ キー発行後、有効になるまで数時間かかる場合があります。

### YOLP

国内POI検索・逆ジオコーディングに必須。

1. https://e.developer.yahoo.co.jp/ にアクセス
2. Yahoo! JAPANアカウントでログイン
3. 「アプリケーションの管理」→「新しいアプリケーションを開発」
4. 「**Client ID**」をコピー
5. **Base64エンコード**してスタート画面「設定」→「Tab 1: API管理」→「**YOLP Client ID:**」欄に貼り付けて保存

**Base64エンコード方法（PowerShell）:**
```powershell
[Convert]::ToBase64String([Text.Encoding]::UTF8.GetBytes("your_client_id"))
```

> ℹ Base64エンコードを忘れると認証に失敗します。

---

## オプションキーの取得

### Google Maps Platform

Google 3D Tiles、Google検索モード/Googleマーカーモード、施設詳細に使用。

1. https://console.cloud.google.com/ にアクセス
2. プロジェクト作成
3. 以下のAPIを有効化:
   - **Map Tiles API** (Google 3D Tiles用)
   - **Places API (New)** (検索/マーカー/詳細/写真/オートコンプリート用)
4. 「認証情報」→「APIキーを作成」
5. スタート画面「設定」→「Tab 1: API管理」→「**Google Maps:**」欄に貼り付けて保存

> ✅ **推奨**: APIキーにHTTPリファラー制限またはIPアドレス制限を設定してください。

#### Cloud Monitoring（任意）

Google 3D Tilesの使用量をCloud Monitoring APIで正確に監視できます。  
設定は `API_Key/GoogleCloudMonitor.json` ではなく、**スタート画面のUIから直接入力**します。

**取得手順:**

1. GCPコンソール → 「IAMと管理」→「サービスアカウント」
2. サービスアカウント作成 → 「**Monitoring Viewer**」ロール付与
3. 「キー」タブ → 「鍵を追加」→「JSON」でダウンロード
4. ダウンロードしたJSONを開き、以下の値をコピーしてスタート画面「設定」→「Tab 1: API管理」→「GCP Cloud Monitoring」セクションに入力:

| UI フィールド | JSON のキー | 例 |
|--------------|------------|----|
| **GCP Project ID:** | `project_id` | `cityexplorer-123456` |
| **GCP Client Email:** | `client_email` | `name@project.iam.gserviceaccount.com` |
| **GCP Client ID:** | `client_id` | `117723382374898632488` |
| **GCP Key ID:** | `private_key_id` | `208e84488bf662e...` |
| **GCP Private Key:** | `private_key` | `-----BEGIN PRIVATE KEY-----\n...` |

> ⚠ **Private Key** は `-----BEGIN PRIVATE KEY-----` から `-----END PRIVATE KEY-----` まで（改行を含む全文）をそのまま貼り付けてください。

### ホットペッパー

国内飲食店の写真取得に使用。

1. https://webservice.recruit.co.jp/ にアクセス
2. リクルートアカウントでログイン
3. 「APIキー」を取得
4. スタート画面「設定」→「Tab 1: API管理」→「**Hotpepper:**」欄に貼り付けて保存

### Gemini

AIによるローディング画面の地域情報構造化・ニュース生成に使用（推奨）。

1. https://aistudio.google.com/apikey にアクセス
2. Googleアカウントでログイン
3. 「**Create API key**」をクリック
4. スタート画面「設定」→「Tab 1: API管理」→「**Gemini:**」欄に貼り付けて保存

> ✅ 設定するとローディング画面で地域の観光・グルメ・祭事など~40件の情報が構造化表示されます。

### GitHub Models

AI地域情報生成の代替プロバイダー（Geminiの代わりに使用可能）。

1. https://github.com/settings/tokens にアクセス
2. 「**Fine-grained personal access tokens**」→「**Generate new token**」
3. トークン名を入力（例: CityExplorer）
4. **Account permissions** セクション → **Models** → **Read** を有効化
5. トークンを生成してコピー
6. スタート画面「設定」→「Tab 1: API管理」→「**GitHub Token:**」欄に貼り付けて保存

> ⚠ **重要な注意点:**
> - 必ず **Fine-grained PAT** を使用（クラシックトークンでは不可）
> - **Models: Read** は **Account permissions** にあります（Repository permissionsではありません）
> - 起動時に自動でトークン有効性を検証し、401/403の場合は無効化されます

---

## スタート画面での設定

ゲーム起動後のスタート画面「設定」ボタン → **「Tab 1: API管理」** で以下を入力・保存できます:

| UIフィールド | 対応サービス |
|------------|------------|
| Cesium Ion | Cesium Ion |
| OpenWeather | OpenWeatherMap |
| YOLP Client ID | Yahoo! YOLP（Base64エンコード済み） |
| Google Maps | Google Maps Platform |
| Hotpepper | ホットペッパー |
| Gemini | Google Gemini AI |
| GitHub Token | GitHub Models |
| GCP Project ID | GCP Cloud Monitoring |
| GCP Client Email | GCP Cloud Monitoring |
| GCP Client ID | GCP Cloud Monitoring |
| GCP Key ID | GCP Cloud Monitoring |
| GCP Private Key | GCP Cloud Monitoring（PEM全文） |

保存すると暗号化された `userdata.dat` に統合保存されます。再起動不要で即座に反映されます。

その他の設定（ラジオによるAPI選択、LLMプロバイダー切替、API上限値編集）も「Tab 1: API管理」から変更できます。画面表示設定（ミニマップ・ヘルプパネル等のON/OFF、UI言語）は「Tab 0: 画面表示」で変更できます。

---

## トラブルシューティング

| 症状 | 原因と対処 |
|------|-----------|
| 3D建物が表示されない | Cesium Ionトークンが未設定または無効 → 再取得して設定 |
| 天気が取得できない | OpenWeatherMapキーが未設定 → 発行後数時間待って再試行 |
| 国内POIが出ない | YOLP Client IDが未設定またはBase64エンコード忘れ |
| Google系機能が動かない | APIが未有効化 → GCPコンソールで対象APIを有効化 |
| GitHub Modelsが使えない | Models権限不足 → Account permissions > Models > Read を確認 |
| 「BLOCKED」と表示される | APIの無料枠90%到達 → 翌日/翌月に自動リセット |
