## GeoSuite — QGIS デスクトップ + WebGIS フルサイクル ツールスイート

GeoSuite は QGIS を中核に、データ取得から検索、Web 共有、出力（書類化）までをワンストップで自動化するプラグイン群です。4 つのプラグイン（`GeoImport` / `GeoSearch` / `GeoWebView` / `GeoReport`）により、ワークフロー「データ取得 → 検索 → Web 共有 → 出力（報告書生成）」をスムーズに実行できます。

## 概要

- 自動化対象: データの取り込み（ローカル/CKAN）から地図内検索、スタイル付き Web 共有、PDF/PNG/Atlas 出力まで。
- 対象ユーザ: QGIS を業務で使い、社内共有や Web 公開を簡易化したい組織。

## ワークフロー概要

```
ローカル/CKAN
	↓
GeoImport（自動 GIS 化）
	↓
GeoSearch（地図内検索）
	↓
GeoWebView（スタイル込 Web 共有 — 旧: `GeoView`）
	↓
GeoReport（レイアウト編集・出力＋報告書生成）
```

## 各ツール詳細

| ツール | 役割 | 主な機能 |
|---|---:|---|
| GeoImport | データ探索 → GIS 化 | CKAN/ローカル自動判定、CSV のジオメトリ化、自動インポート |
| GeoSearch | プロジェクト内地図検索 | 地番/所有者/属性検索、PostGIS 対応の高度検索機能 |
| GeoWebView | QGIS → Web 共有（スタイル込） | パーマリンク生成、MapLibre スタイル注入、WFS 配信 |
| GeoReport | レイアウト編集 → 出力 ＋ 報告書生成 | レイアウトテンプレート一括適用、レイアウト内アイテムのバッチ編集、RubberBand 印刷範囲、Atlas 一括出力。高解像度 PNG/PDF を生成すると同時に、出力メタデータ（タイトル・中心座標・スケール・レイヤ一覧等）を CSV/XLSX で出力し、画像を埋め込んだ Excel 形式の報告書を自動生成するワークフローをサポートします。 |

## 活用シナリオ

- 社内報告書作成: `GeoImport` → `GeoSearch` → `GeoWebView`（Excel リンク生成）→ `GeoReport`（高解像度 PNG/PDF とメタを出力し、Excel で一覧・説明資料を自動作成）
- Web 地図公開: `GeoWebView` で Re:Earth / MapLibre にスタイル転写、パーマリンク共有
- 大量出力: `GeoExport` のテンプレート機能で複数地域（例: 100 枚）を一括生成

## 使い始め

- 詳細なインストール手順や各プラグインの使い方は、各プラグインのドキュメント（または各リポジトリの README）を参照してください。

## フィードバック

- 質問や改善案があれば Issue を立ててください。

## 対応プロジェクト（GeoSuite コンポーネント → 実リポジトリ）

GeoSuite の各コンポーネントと現状リポジトリは以下の通りです。最新の状況は各リポジトリの README を参照してください。

### `GeoImport`（自動 GIS 化）
 `https://github.com/yamamoto-ryuzo/qgis-data-catalog-integration`  
  — CKAN やローカルフォルダを横断検索してデータを取得・登録するプラグイン。CSV の区切り文字・文字コードを自動判定してポイント/ライン/ポリゴンにジオメトリ化し、SQLite キャッシュで検索応答を高速化します。
### `GeoSearch`（地図内検索）  
 `https://github.com/yamamoto-ryuzo/GEO-search-plugin`   
 — 完成済みの検索モジュール。地番・所有者・一般属性など複数種類の検索をサポートし、結果はレイヤ別タブで表示されます。`selectTheme` によるテーマ適用や「加算表示モード」で既存表示を保ちながら検索結果を重ねる運用が可能です。
### `GeoWebView`（スタイル込 Web 共有 — 旧: `GeoView`）
 `https://github.com/yamamoto-ryuzo/QMapPermalink`   
 — QGIS の現在表示（中心・ズーム・レイヤ可視性・スタイル）をパーマリンクや HTML/PNG パッケージに変換して社内で共有するツールです。軽量 HTTP サーバーによる配信、WFS 経由の地物配信、MapLibre や OpenLayers へのスタイル注入をサポートします。
### `GeoReport`（旧: `GeoLayout` / `GeoExport` — レイアウト / 報告書生成）
`https://github.com/yamamoto-ryuzo/qgis-layoutitem-selector`  
	— レイアウトのテンプレート保存・一括適用、レイアウト内アイテムのバッチ編集、RubberBand による印刷範囲操作、Atlas 的な複数図面の一括出力を行うプラグインです。高解像度 PNG/PDF と出力メタデータ（CSV/XLSX）を同時に生成し、画像を埋め込んだ Excel 形式の報告書を自動生成して、説明資料作成の手間を削減します。

## 注

-- 上記リポジトリは開発段階の名称や構成が含まれるため、将来的にコンポーネント名（GeoImport/GeoWebView/GeoExport）へ統一する予定です。リンク先の README を参照して最新状況を確認してください。

## 将来の拡張 / 追加予定機能

以下は簡潔にまとめた「コンポーネント別サマリー」と、README 全体の構成見直し案です。

### コンポーネント別サマリー（短縮版）

- GeoImport — [高]
	- STAC / DCAT によるメタデータ連携と自動インデックス化
	- 大容量データ取り込み（並列・ストリーミング、S3 対応）
	- 点群（LAS/LAZ）・3D フィーチャ（CityGML/3D Tiles）取り込み（PDAL 統合）
	- 自動ジオリファレンスと座標系検出、データ品質チェック

- GeoSearch — [高]
	- 空間全文検索・属性検索の強化（PostGIS, OpenSearch 等）
	- フェデレーション検索・時系列（バージョン）検索対応
	- 空間解析フィルタ（バッファ、空間結合）および ML 支援機能

- GeoWebView（旧: GeoView） — [高〜中]
	- QGIS の 3D 表示スナップショットと Cesium/3D Tiles への連携
	- 点群配信（Entwine / Potree）と Web 上での可視化最適化
	- OGC API / WebSocket によるリアルタイム配信、ベクタタイル生成（MVT）と CDN 配信
	- MapLibre/Mapbox スタイル互換性強化、アクセシビリティ・多言語対応

- GeoReport — [中〜高]
	- 3D スナップショット組込、点群断面・統計を含むレポート生成
	- Jupyter/Papermill を用いた再現可能なレポートワークフロー
	- Excel テンプレート・画像埋め込み、自動注釈、分散バッチ出力
	- PDF/A・電子署名対応（公式報告書用途）

- 共通プラットフォーム（全体） — [高]
	- OGC API（Features/Maps）・COG/MBTiles サポート
	- コンテナ化（Docker）と CI/CD、監視（Prometheus/Grafana）
	- 認証（OAuth2/SAML）・監査ログ・テレメトリ


### README 全体構成の見直し案（提案）

- 1. Project Overview（現状の冒頭）
- 2. Quickstart / 使い始め（インストール／簡易ワークフロー）
- 3. コンポーネント（GeoImport / GeoSearch / GeoWebView / GeoReport） — 各 1 ページの短い概要 + リンク
- 4. 活用シナリオ（簡潔に 3〜4 件）
- 5. 将来の拡張（本節：コンポーネント別要約 + 優先度）
- 6. ロードマップ候補（Now / Next / Later の優先度マトリクス）
- 7. Contributing（開発・Issue・PR の流れ）
- 8. 寄稿・サポート（問い合わせ先・ライセンス）

この見直しにより、利用者はまず早く導入できる「Quickstart」を見つけやすくなり、開発者は「将来の拡張」を優先度付きで参照できるようになります。

### 次のアクション候補

1. 優先度マトリクス（Now / Next / Later）を作成し、上位 3 項目の概算工数を推定する。  
2. PoC 候補を決める（例: GeoWebView の Cesium エクスポート / GeoReport の XLSX 自動生成）と小規模実装計画を作成。  
3. CI・コンテナ化（README に Docker 開発環境のセットアップ例を追加）。

必要なら、上記の優先付けと概算を私が作成します（ユーザ要件をいくつか質問します）。
