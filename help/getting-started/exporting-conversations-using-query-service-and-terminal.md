---
title: クエリサービスとターミナルを使用した会話のエクスポート
description: Experience Platform クエリサービスとターミナルを使用して、資格情報と個人データに関するガイダンスを使用して、Brand Conciergeの会話をCSVに書き出す方法について説明します。
topic: Development
role: Developer
level: Experienced
doc-type: Tutorial
duration: 260
last-substantial-update: 2026-10-15
jira: KT-22874
source-git-commit: 0d9fa76d0fe3494daa7189ab9e9984a423ee1d6e
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%
---
# クエリサービスとターミナルを使用した会話のエクスポート

Adobe Experience Platform クエリサービスとターミナルを使用して、Adobe Brand Conciergeの会話を保存および書き出す方法について説明します。 このビデオでは、データセットのテーブル名を検索し、PostgreSQL コマンドラインクライアントを設定し、日付範囲の会話データをCSV ファイルに書き出す方法を説明します。

## この動画は誰のためのものでしょうか？

* コマンドラインツールを使用してBrand Conciergeの会話データを書き出す必要がある開発者

## ビデオコンテンツ

* Experience Platformで会話データセットを検索し、そのテーブル名をコピーします
* HomebrewでPostgreSQL クライアントをインストールし、そのコマンドラインパスを設定する
* 「クエリサービス資格情報」タブからPSQL接続コマンドをコピーします
* データセットと日付範囲を選択し、クエリ結果をローカルのCSV ファイルに書き出します
* 書き出された結果を確認し、必要に応じて期限切れの資格情報を更新します

>[!VIDEO](https://video.tv.adobe.com/v/3504643)

>[!IMPORTANT]
>
> PSQL接続コマンドには、ライブパスワードが含まれています。 共有したり、チャット、AI エージェント、メールにペーストしたりしないでください。 パスワードの有効期限が切れた後に認証が失敗した場合は、「クエリサービス資格情報」タブから新しいコマンドをコピーします。

>[!NOTE]
>
> 書き出された会話には、個人を特定できる情報（PII）が含まれる場合があります。 CSV ファイルを保存する場合は、組織のデータ処理ポリシーに従ってください。

ドキュメントについては、[Brand Concierge ヘルプ &#x200B;](../documentation/overview.md)を参照してください。

## 関連チュートリアル

* [Adobe CX Enterprise Coworkerを使用した会話の書き出し](exporting-conversations-using-adobe-cx-enterprise-coworker.md)
