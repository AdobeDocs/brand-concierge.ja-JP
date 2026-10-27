---
title: Marketo EngageのBrand Concierge Data
description: リードソースフィールドと、Adobe Marketo Engageに書き込まれた3つのコンシェルジュアクティビティタイプ、およびスマートリストとスマートキャンペーンでの使用方法について説明します。
role: User, Admin
level: Beginner
product_v2:
  - id: b6ee73fe-bdc6-47d9-99a2-80194514dd40
    internal-label: Brand Concierge
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: ec567c798c52edaba7e2cfb41a837d8058bcceb7
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 4%
---
# Marketo EngageのBrand Conciergeデータ {#marketo-activities}

[!DNL Adobe Marketo Engage]が接続されると、フォームに入力する、ミーティングを予約する、またはライブチャットを開始するすべての訪問者が[!DNL Marketo]の個人レコードになり、コンシェルジュエンゲージメントがネイティブのアクティビティタイプとしてそのレコードに書き込まれます。 つまり、コンシェルジュの行動に関するスマートリストとスマートキャンペーンを、他の[!DNL Marketo] アクティビティと同じように作成できます。

>[!NOTE]
>
>ライブチャットとミーティングの予約には[!DNL Marketo Engage]は必要ありません。 このページに記載されているデータは、この情報がなければ[!DNL Adobe Marketo Qualifier]に残ります。 [&#x200B; ライブチャットとミーティング予約の概要](overview.md#prerequisites)を参照してください。

## リードジェネレーションとソースアトリビューション {#lead-creation}

コンシェルジュを通じて作成された顧客にタグが付けられるので、その顧客がどこから来たのかをいつでも把握できます。

| フィールド | 値 |
| --- | --- |
| **[!UICONTROL 人物Source]** | `Brand Concierge` |
| **[!UICONTROL 元のSourceの種類]** | `Chat` |
| **[!UICONTROL 元のSource情報]** | `Concierge` |
| **[!UICONTROL Registration Source Type]** | `Chat` |
| **[!UICONTROL 登録Source情報]** | `Concierge` |

![Marketoの個人レコード情報タブ。Brand Conciergeとチャットおよびコンシェルジュソースフィールドに設定された人物Sourceが表示されている](../assets/sales-handoff-marketo-1.png){width="800" zoomable="yes"}

## アクティビティのタイプ {#activity-types}

3つのネイティブアクティビティタイプが個人レコードにプッシュされます。 3つはすべてトリガーとフィルターとして利用できます。

![&#x200B; コンシェルジュとのエンゲージメント、コンシェルジュでのミーティングのスケジュール、コンシェルジュエントリでのライブチャットのエンゲージメントを示す人物のMarketo アクティビティログ &#x200B;](../assets/sales-handoff-marketo-2.png){width="800" zoomable="yes"}

### Conciergeとの連携 {#engage-with-concierge}

訪問者がコンシェルジュとエンゲージしたときに記録されます。

| 属性 | 説明 |
| --- | --- |
| コンシェルジュ名 | 訪問者がエンゲージしたコンシェルジュ |
| 会話ID | 会話の識別子。 Composerで使用すると、トランスクリプト全体を開くことができます |
| ページ URL | エンゲージメントが発生したページ |
| 作成日時 | 会話が作成されたとき |
| 期間 | 会話が続いた時間 |

>[!NOTE]
>
>このアクティビティタイプの一部の属性（話し合ったトピック、要約、言語など）はまだ入力されていません。 将来のリリースに向けて計画されています。

### Conciergeでのミーティングのスケジュール {#schedule-meeting}

1回の予約で&#x200B;**回** ログインしました。これは、結果から意図を分けることができます。

**最初、開始時。** 訪問者がミーティングのスケジュールを設定するオプションを選択すると、予約フォームが表示されます。 会議の状態は`Started`です。

| 属性 | 説明 |
| --- | --- |
| ミーティングステータス | `Started` |
| ページ URL | 訪問者が予約を開始したページ |
| Concierge ID | 訪問者がエンゲージしたコンシェルジュ |
| ユーザー ID | [!DNL Marketo]人のレコード |

**その後、予約時** 訪問者はスロットを確認しました。 会議の状態は`Scheduled`です。

| 属性 | 説明 |
| --- | --- |
| ミーティングステータス | `Scheduled` |
| 営業担当者名 | 会議が予約された代表者 |
| 営業担当者のメール | 担当者のメールアドレス |
| スケジュール日 | 会議の日時 |
| ミーティング期間 | 予約されたミーティングの所要時間 |
| ルーティングタイプ | この担当者のカレンダーを解決したルーティング |
| ページ URL | 訪問者が予約したページ |
| Concierge ID | 訪問者がエンゲージしたコンシェルジュ |
| ユーザー ID | [!DNL Marketo]人のレコード |

>[!TIP]
>
>`Meeting Status`でスマートリストを作成すると、`Started`ですが、`Scheduled`ではなく、ミーティングの予約を開始して放棄した全員が見つかります。 オーディエンスのナーチャリングやリターゲティングが可能になります。

### Conciergeのライブチャットでエンゲージ {#engage-with-live-chat}

ライブチャット終了後にログに記録されます。

| 属性 | 説明 |
| --- | --- |
| 会話ステータス | チャットが意図的に閉じられた場合`Ended`、訪問者がサイトを離れ、チャットがタイムアウトした場合`Dropped` |
| 通知済みエージェント | このチャットの通知を受け取った担当者の電子メールアドレス |
| 会話スコア | 代表者の0から3の評価が会話を行いました。 [会話のスコアを確認](chat-inbox.md#conversation-score) |
| ページ URL | ライブチャットが開始されたページ |
| Concierge ID | 訪問者がエンゲージしたコンシェルジュ |
| セッション ID | ライブチャットセッションの識別子 |
| 開始時間 | チャットが始まったとき |

>[!TIP]
>
>会話スコアは、訪問者と実際に話した人間が設定したため、最も価値の高い属性です。 リードスコアリング、リターゲティング、パーソナライゼーション、セールス部門やCRMへの引き継ぎなどに利用できます。

## スマートキャンペーンでのコンシェルジュデータの使用 {#smart-campaign}

スマートキャンペーンの&#x200B;**[!UICONTROL スマートリスト]**&#x200B;で、`concierge`を検索して、使用可能なすべての項目を確認します。

![Marketo アクティビティで利用可能なコンシェルジュのトリガーとフィルターを表示するBrand Concierge スマート リスト &#x200B;](../assets/sales-handoff-marketo-3.png){width="800" zoomable="yes"}

| カテゴリ | 利用可能なアイテム |
| --- | --- |
| **[!UICONTROL トリガー]** | コンシェルジュサービスとの連携、コンシェルジュサービスでのライブチャット、コンシェルジュサービスでのミーティングスケジュール |
| **[!UICONTROL フィルター]** > アクティビティ履歴 | コンシェルジュサービス利用中、コンシェルジュサービス利用中、コンシェルジュサービス利用中のライブチャット利用中 |
| **[!UICONTROL フィルター]** >非アクティビティフィルター | コンシェルジュサービスへの参加なし、コンシェルジュサービスにおけるライブチャットへの参加なし、コンシェルジュサービスにおけるミーティングの予約なし |

トリガーまたはフィルターをカンバスにドラッグし、**[!UICONTROL 制約を追加]**&#x200B;を選択して絞り込みます。

### 制約 {#constraints}

| トリガーまたはフィルター | 制約 |
| --- | --- |
| Conciergeについて | コンシェルジュ名、ページ URL、作成日時、期間、活動日 |
| Conciergeでのミーティングのスケジュール | コンシェルジュ名、営業担当者の名前、ミーティングステータス、スケジュール済み、ミーティング期間、ルーティングタイプ、ページ URL、アクティビティの日付 |
| Conciergeのライブチャットに参加 | Concierge Name, Sales Representative Name, Conversation Status, Conversation Score, Start Time, Accepted Time, End Time, Closed By, Duration, Discussed Topic, Page URL, Language, Date of Activity |

## 次の手順 {#next}

[会議とライブチャットを監視](monitor.md)して、会議とチャットのパフォーマンスを確認します。
