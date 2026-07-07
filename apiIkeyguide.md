# APIキー取得・設定ガイド

> 最終更新: 2026-07-18

---

## 概要

CityExplorer で使用する API キーの取得方法と設定手順です。

キーはゲーム起動後のスタート画面「設定」→ **Tab 1: API管理** から入力・保存します。
保存したキーは暗号化されてアプリ内に統合管理されます。保存後は再起動不要で即座に反映されます。

> **セキュリティ注意**: API キーを他者と共有したり、公開の場所に掲載しないようにしてください。

---

## どのキーが必要か

CityExplorer では、**スタート画面で選択した API グループに応じて必要なキーが変わります。**
選択中の API グループのキーが検証済みであれば、START ボタンが有効になります。

### 各機能グループと必要なキー

| 機能 | 選択肢 | 必要なキー |
|------|--------|-----------|
| **3D タイル** | Google Map Tiles API（推奨） | Google Maps |
| | Cesium Ion | Cesium Ion |
| **目的地検索** | Google Places New（推奨） | Google Maps |
| | YOLP | YOLP Client ID |
| | Nominatim（OSM） | **不要** |
| **施設マーカー** | Google Places New（推奨） | Google Maps |
| | YOLP | YOLP Client ID |
| | Overpass（OSM） | **不要** |
| **地域情報 AI** | Gemini 2.5 Flash（推奨） | Gemini |
| | GitHub Models | GitHub Token |
| | Wikipedia のみ | **不要** |

> **API キーをお持ちでない場合**は、各グループで「Nominatim」「Overpass」「Wikipedia」を選ぶとキーなしで START できます。

### オプションキー（なくても START できる）

| キー | 役割 | 未設定時の動作 |
|------|------|--------------|
| OpenWeather | 現在地の天気を自動取得 | 天気は手動切り替えのみ |
| Hotpepper | 飲食店の写真表示 | 飲食店写真が非表示 |
| GCP Cloud Monitoring | 3D Tiles の使用量をサーバーで正確に確認 | アプリ内ローカルカウントで代替（機能に影響なし） |

### キー不要で動く機能

以下はキー不要で自動的に利用されます。

| サービス | 役割 |
|---------|------|
| Project PLATEAU | 日本の 3D 建物（四日市市） |
| OpenStreetMap / Overpass | 施設検索・建物データのフォールバック |
| Nominatim | 住所検索のフォールバック |
| Open-Elevation | 標高データ |
| Wikipedia / Wikimedia | 地域情報・画像のフォールバック |
| CartoDB Voyager | ミニマップ |

---

## 各キーの取得手順

### Cesium Ion

3D タイルで「**Cesium Ion**」を選択した場合に必要です。無料プランで利用できます。

1. [https://ion.cesium.com/](https://ion.cesium.com/) でアカウント作成（無料）
2. ログイン後、左メニュー **Access Tokens** をクリック
3. **Default Token** の文字列をコピー
4. スタート画面「設定」→ **Tab 1: API管理** → **Cesium Ion** 欄に貼り付けて **[検証]** を押す

---

### OpenWeather

天気の自動取得（「現実」モード）に使います。未設定でも手動で天気を変更できます。

1. [https://openweathermap.org/api](https://openweathermap.org/api) でアカウント作成（無料）
2. **API keys** タブのデフォルトキーをコピー
3. スタート画面「設定」→ **Tab 1: API管理** → **OpenWeather** 欄に貼り付けて **[検証]** を押す

> キー発行後、有効になるまで数時間かかる場合があります。

---

### YOLP（Yahoo! YOLP）

目的地検索・施設マーカーで「**YOLP**」を選択した場合に必要です。

1. [https://e.developer.yahoo.co.jp/](https://e.developer.yahoo.co.jp/) に Yahoo! JAPAN アカウントでログイン
2. 「アプリケーションの管理」→「新しいアプリケーションを開発」でアプリを登録
3. 発行された **Client ID** をコピー
4. スタート画面「設定」→ **Tab 1: API管理** → **YOLP Client ID** 欄に**そのまま**貼り付けて **[検証]** を押す

> **Base64 エンコードは不要です。** 取得した Client ID をそのまま貼り付けてください。
> エンコードして入力すると認証に失敗します。

---

### Google Maps Platform

以下のいずれかを選択する場合に必要です。**1 つの API キーで全 Google 機能を兼用できます。**

- 3D タイルで「**Google Map Tiles API**」を選択
- 目的地検索または施設マーカーで「**Google Places New**」を選択

#### 手順

1. [https://console.cloud.google.com/](https://console.cloud.google.com/) でプロジェクトを作成
2. **API とサービス** → **ライブラリ** で、使用機能に応じた API を有効化

| 使用機能 | 有効化する API |
|---------|-------------|
| 3D タイル | **Map Tiles API** |
| 目的地検索・施設マーカー・詳細・写真 | **Places API (New)** |

3. **認証情報** → **+ 認証情報を作成** → **API キー** でキーを作成
4. スタート画面「設定」→ **Tab 1: API管理** → **Google Maps** 欄に貼り付けて **[検証]** を押す

> **推奨**: GCP コンソールでキーに「API の制限」または「IP アドレス制限」を設定するとより安全です。

#### 無料枠の目安（デフォルト上限）

| 機能 | 上限 |
|------|------|
| 3D Tiles | 1,000 セッション / 月 |
| テキスト検索 | 5,000 回 / 月 |
| 施設検索 | 5,000 回 / 月 |
| 施設写真 | 1,000 回 / 月 |
| 施設詳細 | 1,000 回 / 月 |
| オートコンプリート | 10,000 回 / 月 |

使用量が上限の 90% に達すると、自動で無料 API（OSM 等）に切り替わります。翌月に自動リセットされます。
上限値はスタート画面から変更できます。

---

### Hotpepper

国内飲食店の写真表示に使います。未設定でも他の機能には影響しません。

1. [https://webservice.recruit.co.jp/](https://webservice.recruit.co.jp/) にログイン（リクルート ID 登録が必要）
2. 「ホットペッパーグルメ サーチ API」を申請して API キーを取得
3. スタート画面「設定」→ **Tab 1: API管理** → **Hotpepper** 欄に貼り付けて **[検証]** を押す

---

### Gemini

地域情報 AI で「**Gemini 2.5 Flash**」を選択した場合に必要です。
未設定の場合は Wikipedia モードで地域情報を表示します。

1. [https://aistudio.google.com/apikey](https://aistudio.google.com/apikey) に Google アカウントでログイン
2. **Create API key** でキーを作成・コピー
3. スタート画面「設定」→ **Tab 1: API管理** → **Gemini** 欄に貼り付けて **[検証]** を押す

> 無料枠で 500 RPM まで利用できます。観光・グルメ・祭事など約 40 件の地域情報が表示されます。

---

### GitHub Models

地域情報 AI で「**GitHub Models**」を選択した場合に必要です。Gemini の代わりに利用できます。

1. [https://github.com/settings/tokens](https://github.com/settings/tokens) を開く
2. **Fine-grained personal access tokens** → **Generate new token**
3. トークン名を入力し、**Account permissions** → **Models** → **Read** を有効化
4. トークンを生成・コピー
5. スタート画面「設定」→ **Tab 1: API管理** → **GitHub Token** 欄に貼り付けて **[検証]** を押す

> - **Fine-grained PAT** を使用してください（クラシックトークンは利用不可）
> - **Models: Read** は **Account permissions** の中にあります（Repository permissions ではありません）

---

### GCP Cloud Monitoring（オプション）

Google 3D Tiles の使用量をサーバー側で正確に取得する場合に設定します。
設定しなくてもアプリ内のカウントで使用量管理は正常に動作します。

**事前条件**: Google Maps キーが設定・検証済みであること

#### 手順

1. GCP コンソール → **IAM と管理** → **サービスアカウント** でアカウントを作成
2. ロールに **Monitoring Viewer** を付与
3. **キー** タブ → **鍵を追加** → **JSON** でキーファイルをダウンロード
4. JSON ファイルを開き、以下の値をスタート画面「設定」→ **Tab 1: API管理** → **GCP Cloud Monitoring** セクションに入力

| 入力欄 | JSON のキー名 |
|--------|------------|
| GCP Project ID | `project_id` |
| GCP Client Email | `client_email` |
| GCP Client ID | `client_id` |
| GCP Key ID | `private_key_id` |
| GCP Private Key | `private_key` |

> **GCP Private Key** は `-----BEGIN PRIVATE KEY-----` から `-----END PRIVATE KEY-----` までの全文（改行を含む）をそのままコピーしてください。

---

## 設定フィールド一覧

スタート画面「設定」→ **Tab 1: API管理** で入力できる全フィールドです。

| 入力欄 | サービス | いつ必要か |
|--------|---------|----------|
| Cesium Ion | Cesium Ion | 3D タイルで「Cesium Ion」を選択時 |
| OpenWeather | OpenWeatherMap | 天気の自動取得を使う場合（オプション） |
| YOLP Client ID | Yahoo! YOLP | 検索・マーカーで「YOLP」を選択時 |
| Google Maps | Google Maps Platform | Google 系機能を選択時 |
| Hotpepper | ホットペッパー | 飲食店写真を表示したい場合（オプション） |
| Gemini | Google Gemini AI | 地域情報 AI で「Gemini」を選択時 |
| GitHub Token | GitHub Models | 地域情報 AI で「GitHub Models」を選択時 |
| GCP Project ID / Client Email / Client ID / Key ID / Private Key | GCP Cloud Monitoring | 3D Tiles 使用量をサーバーで確認したい場合（オプション） |

各入力欄の右にある **[検証]** ボタンで接続確認ができます。検証が通るとバッジが緑色になります。

---

## よくある質問・トラブル対処

| 症状 | 対処方法 |
|------|---------|
| START ボタンが押せない | 選択中の API のキーが未検証です。**[検証]** ボタンを押すか、キー不要な選択肢（Nominatim / Overpass / Wikipedia）に変更してください |
| 天気が自動で変わらない | OpenWeather キーを設定・検証してください。キー発行後は数時間待つ必要があります |
| 国内 POI が表示されない | YOLP のキーが未設定か、正しく入力されていない可能性があります |
| YOLP の検証が失敗する | Client ID を Base64 エンコードせず、そのまま貼り付けてください |
| Google の機能が動かない | GCP コンソールで「Map Tiles API」または「Places API (New)」が有効になっているか確認してください |
| GitHub Models が使えない | Fine-grained PAT を作成し、Account permissions > Models > Read を有効にしてください |
| 「BLOCKED」と画面に表示される | API の無料枠の 90% に達しました。自動で OSM 等の無料 API に切り替わります。翌日（YOLP）または翌月（Google 系）に自動復帰します |
