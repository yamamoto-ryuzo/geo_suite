## GeoSuite — QGIS デスクトップ + WebGIS フルサイクル ツールスイート

GeoSuite は QGIS を中核に、データ取得から検索、Web 共有、出力（報告書生成）までをワンストップで自動化するプラグイン群です。

## Table of Contents

- Project Overview
- Quickstart
- Components
	- GeoImport
	- GeoSearch
	- GeoWebView
	- GeoReport
- Scenarios
- Future extensions (component summaries)
- Roadmap candidates (Now / Next / Later)
- Contributing
- Support & License

## Project Overview

- 自動化対象: データの取り込み（ローカル/CKAN）→ 検索 → Web 共有 → レポート作成（PNG/PDF/XLSX）
- 対象ユーザ: QGIS を業務で使い、社内共有や Web 公開を簡易化したい組織

## Quickstart

1. QGIS に各プラグインをインストール（各リポジトリの README を参照）
2. `GeoImport` でデータを登録（CSV/CKAN）
3. `GeoSearch` で対象範囲を検索・抽出
4. `GeoWebView` でスタイル付きパッケージ／パーマリンクを生成し共有
5. `GeoReport` でレイアウトを適用し、高解像度 PNG/PDF とメタデータを出力（必要に応じて XLSX レポート自動生成）

## Components

各コンポーネントの短い概要と実リポジトリ

- GeoImport — 自動 GIS 化（CKAN / ローカル）
	- リポジトリ: https://github.com/yamamoto-ryuzo/qgis-data-catalog-integration
- GeoSearch — 地図内検索（属性・空間検索）
	- リポジトリ: https://github.com/yamamoto-ryuzo/GEO-search-plugin
- GeoWebView — スタイル込 Web 共有（旧: GeoView）
	- リポジトリ: https://github.com/yamamoto-ryuzo/QMapPermalink
- GeoReport — レイアウト編集・出力 ＋ 報告書生成
	- リポジトリ: https://github.com/yamamoto-ryuzo/qgis-layoutitem-selector

## Scenarios

- 社内報告書作成: `GeoImport` → `GeoSearch` → `GeoWebView` → `GeoReport`
- Web 地図公開: `GeoWebView` でパッケージ化・パーマリンク共有
- 大量出力: レイアウトテンプレートを用いた一括出力（例: 100 枚の Atlas）

## Future extensions (component summaries)

- GeoImport — [高]
	- STAC / DCAT メタデータ連携、自動インデックス化
	- 大容量・ストリーミング取り込み、S3 対応
	- 点群（LAS/LAZ）・3D フィーチャ取り込み（PDAL / 3D Tiles）

- GeoSearch — [高]
	- 空間全文検索、フェデレーション検索、時系列（履歴）対応
	- 空間解析フィルタと ML 補助

- GeoWebView — [高〜中]
	- QGIS 3D スナップショット → Cesium/3D Tiles 連携
	- 点群配信（Entwine / Potree）、OGC API リアルタイム配信
	- ベクタタイル (MVT) 生成と CDN 配信、自動スタイル注入

- GeoReport — [中〜高]
	- 3D スナップショット、点群断面・統計の組込レポート
	- Jupyter / Papermill を用いた再現可能なワークフロー
	- Excel テンプレート・画像埋め込み・分散バッチ出力

- 共通プラットフォーム — [高]
	- OGC API（Features/Maps）対応、COG/MBTiles サポート
	- コンテナ化（Docker）・CI/CD・監視（Prometheus/Grafana）
	- 認証（OAuth2/SAML）、監査ログ、テレメトリ

## Roadmap candidates (Now / Next / Later)

- Now (短期、優先)
	- GeoImport: STAC/DCAT メタデータ連携（PoC）
	- GeoReport: XLSX 自動生成の PoC（サンプルテンプレート）

- Next (中期)
	- GeoWebView: Cesium への 3D エクスポート PoC
	- GeoSearch: フェデレーション検索（複数データソース）

- Later (長期)
	- 大規模点群パイプライン（Entwine / Potree / PDAL の本格導入）
	- フルクラウド配信＋認証・監査対応

## Contributing

- 開発・PR の流れ
	1. Issue を立てる（目的・再現手順・期待結果）
	2. 小さなブランチを切って実装、テストを追加
	3. PR を作成してレビュアーを指名

- 開発環境（簡易）
	- 推奨: Python 仮想環境 + QGIS 開発用プラグインのローカル読み込み

## Support & License

- 問い合わせ: Issues を利用してください。  
- ライセンス: リポジトリごとの README を参照してください。

---

（必要であれば、この構成で Quickstart の手順や Contributing の詳細テンプレを追加します）
