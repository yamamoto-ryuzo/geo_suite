## GeoSuite — QGIS デスクトップ + WebGIS フルサイクル ツールスイート

GeoSuite は QGIS を中核に、データ取得から検索、Web 共有、出力までをワンストップで自動化するプラグイン群です。4 つのプラグイン（`GeoImport` / `GeoSearch` / `GeoView` / `GeoExport`）により、ワークフロー「データ取得 → 検索 → Web 共有 → 出力」をスムーズに実行できます。

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
GeoView（スタイル込 Web 共有）
	↓
GeoExport（PDF/PNG/Atlas 出力）
```

## 各ツール詳細

| ツール | 役割 | 主な機能 |
|---|---:|---|
| GeoImport | データ探索 → GIS 化 | CKAN/ローカル自動判定、CSV のジオメトリ化、自動インポート |
| GeoSearch | プロジェクト内地図検索 | 地番/所有者/属性検索、PostGIS 対応の高度検索機能 |
| GeoView | QGIS → Web 共有（スタイル込） | パーマリンク生成、MapLibre スタイル注入、WFS 配信 |
| GeoExport | レイアウト編集 → 出力 | テンプレート一括適用、RubberBand 印刷範囲、Atlas 生成・一括出力 |

## 活用シナリオ

- 社内報告書作成: `GeoImport` → `GeoSearch` → `GeoView`（Excel リンク生成）→ `GeoExport`（PDF/Atlas）
- Web 地図公開: `GeoView` で Re:Earth / MapLibre にスタイル転写、パーマリンク共有
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
### `GeoView`（スタイル込 Web 共有）
 `https://github.com/yamamoto-ryuzo/QMapPermalink`   
 — QGIS の現在表示（中心・ズーム・レイヤ可視性・スタイル）をパーマリンクや HTML/PNG パッケージに変換して社内で共有するツールです。軽量 HTTP サーバーによる配信、WFS 経由の地物配信、MapLibre や OpenLayers へのスタイル注入をサポートします。
### `GeoExport`（PDF/PNG/Atlas 出力）
 `https://github.com/yamamoto-ryuzo/qgis-layoutitem-selector`  
  — レイアウトのテンプレート保存・一括適用、レイアウト内アイテムのバッチ編集、RubberBand による印刷範囲操作、Atlas 的な複数図面の一括出力を行うプラグインです。

## 注

- 上記リポジトリは開発段階の名称や構成が含まれるため、将来的にコンポーネント名（GeoImport/GeoView/GeoExport）へ統一する予定です。リンク先の README を参照して最新状況を確認してください。
