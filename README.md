# CityExplorer Legal Documents — 公開手順

このフォルダの `privacy.md` / `eula.md` は、Steam ストアページの
**プライバシーポリシー URL** および **EULA URL** として公開するためのファイルです。

---

## GitHub Pages で無料公開する手順

GitHub Pages は**パブリックリポジトリ**なら無料プランで利用できます。
以下の手順で専用リポジトリを作成し、公開してください。

### 1. パブリックリポジトリを新規作成

1. https://github.com/new にアクセス
2. **Repository name**: `cityexplorer-legal`
3. **Visibility**: ✅ **Public**（← 無料プランで GitHub Pages を使うために必須）
4. 「Create repository」をクリック

### 2. このフォルダの内容をプッシュ

```powershell
# この legal/ フォルダを新リポジトリとして初期化してプッシュ
cd "D:\Unreal Projects\legal"
git init
git checkout -b main
git add .
git commit -m "Add CityExplorer legal documents"
git remote add origin https://github.com/taro-private/cityexplorer-legal.git
git push -u origin main
```

### 3. GitHub Pages を有効化

1. https://github.com/taro-private/cityexplorer-legal/settings/pages を開く
2. **Source**: `Deploy from a branch`
3. **Branch**: `main` / `/ (root)`
4. **Save**

### 4. 公開 URL を確認

数分後に以下の URL でアクセス可能になります:

| ドキュメント | URL |
|------------|-----|
| プライバシーポリシー | `https://taro-private.github.io/cityexplorer-legal/privacy` |
| EULA | `https://taro-private.github.io/cityexplorer-legal/eula` |

### 5. Steam Steamworks に URL を設定

- **Additional Info タブ → Privacy Policy URL**:  
  `https://taro-private.github.io/cityexplorer-legal/privacy`
- **Additional Info タブ → EULA URL**:  
  `https://taro-private.github.io/cityexplorer-legal/eula`

---

## ファイルを更新する場合

```powershell
cd "D:\Unreal Projects\legal"
# ファイルを編集後
git add .
git commit -m "Update legal documents"
git push
```

プッシュ後、数分で GitHub Pages に反映されます。

---

> ⚠️ **注意**: `cityexplorer-legal` リポジトリは**パブリック**になります。
> `privacy.md` / `eula.md` にメールアドレス以外の個人情報が含まれていないことを
> プッシュ前に確認してください。
