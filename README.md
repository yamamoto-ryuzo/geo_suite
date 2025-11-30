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

以下は各コンポーネントの現状機能の詳細（現状の説明を保持）と、コンポーネント別の将来拡張候補を統合したものです。

### GeoImport — 自動 GIS 化（CKAN / ローカル）
- リポジトリ: https://github.com/yamamoto-ryuzo/qgis-data-catalog-integration
- 現状の主な機能: CKAN やローカルフォルダを横断検索してデータを取得・登録するプラグイン。CSV の区切り文字・文字コードを自動判定してポイント/ライン/ポリゴンにジオメトリ化し、SQLite キャッシュで検索応答を高速化します。
- 将来の拡張候補:
	- STAC / DCAT によるメタデータ連携と自動インデックス化
	- 大容量データ取り込み（並列処理・ストリーミング、S3 互換ストレージ対応）
	- 点群（LAS/LAZ）・3D フィーチャ（CityGML / 3D Tiles）取り込み（PDAL 統合）
	- 自動ジオリファレンス・座標系検出の改善、データ品質チェック自動化

### GeoSearch — 地図内検索（属性・空間検索）
- リポジトリ: https://github.com/yamamoto-ryuzo/GEO-search-plugin
- 現状の主な機能: 地番・所有者・一般属性など複数種類の検索をサポートし、結果はレイヤ別タブで表示されます。`selectTheme` によるテーマ適用や「加算表示モード」で既存表示を保ちながら検索結果を重ねる運用が可能です。
- 将来の拡張候補:
	- 空間全文検索と属性検索の強化（PostGIS + pg_trgm / Elasticsearch / OpenSearch 連携）
	- 空間インデックスの最適化とフェデレーション検索（複数データソース横断検索）
	- 時系列データ・バージョン管理（履歴検索、差分抽出）
	- 空間解析を組み込んだ検索フィルタ（バッファ、空間結合、属性スコアリング）
	- 機械学習（空間クラスタリング、異常検知）を活用した検索補助

### GeoWebView — スタイル込 Web 共有（旧: GeoView）
- リポジトリ: https://github.com/yamamoto-ryuzo/QMapPermalink
- 現状の主な機能: QGIS の現在表示（中心・ズーム・レイヤ可視性・スタイル）をパーマリンクや HTML/PNG パッケージに変換して社内で共有するツール。軽量 HTTP サーバーによる配信、WFS 経由の地物配信、MapLibre や OpenLayers へのスタイル注入をサポートします。
- 将来の拡張候補:
	- QGIS の 3D 表示スナップショットおよび Cesium / 3D Tiles へのエクスポート連携
	- 点群ビジュアライゼーションの Web 配信（Entwine / Potree / Cesium 連携）
	- OGC API / WebSocket によるリアルタイム更新（ライブデータ配信）
	- ベクタタイル（MVT）生成とタイルキャッシュの自動化、CDN 配信パターン
	- Mapbox/MapLibre GL スタイル互換の強化、アクセシビリティ・多言語化

### GeoReport — レイアウト編集・出力 ＋ 報告書生成
- リポジトリ: https://github.com/yamamoto-ryuzo/qgis-layoutitem-selector
- 現状の主な機能: レイアウトのテンプレート保存・一括適用、レイアウト内アイテムのバッチ編集、RubberBand による印刷範囲操作、Atlas 的な複数図面の一括出力を行います。高解像度 PNG/PDF を生成すると同時に、出力メタデータ（タイトル・中心座標・スケール・レイヤ一覧等）を CSV/XLSX で出力し、画像を埋め込んだ Excel 形式の報告書を自動生成するワークフローをサポートします。
- 将来の拡張候補:
	- 3D スナップショットの組込み（静止画だけでなく簡易インタラクティブ HTML ビュー）
	- 点群・断面図生成を含む高機能レポート（断面抽出、属性統計、サマリ表）
	- Jupyter / Papermill ベースの再現可能なレポート生成フロー（データ処理 → レイアウト → エクスポート）
	- Excel (XLSX) レポートのテンプレート化とカスタムマクロ連携、画像埋め込み・注釈の自動配置
	- 大量出力のための分散実行（ワーカー／キュー）と途中再開（チェックポイント）機能

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
