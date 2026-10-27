---
title: チャット受信箱
description: Adobe Marketo Qualifierのライブチャットの受信トレイで、営業担当者がBrand Conciergeのライブチャットを受け取り、処理、スコアリング、終了する方法を説明します。
role: User
level: Beginner
product_v2:
  - id: b6ee73fe-bdc6-47d9-99a2-80194514dd40
    internal-label: Brand Concierge
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: 91cbec8d6f4e4800e3bdc8c8f60bfe9ed168a963
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%
---
# チャットインボックス {#chat-inbox}

訪問者が誰かに話しかけるよう求めると、チャットが[!DNL Adobe Marketo Qualifier]の&#x200B;**[!UICONTROL チャット受信箱]**&#x200B;に届きます。 このページは、ライブチャットの担当者のビューです。ライブチャットが到着したときに表示される内容、取得するコンテキスト、終了する前に実行する必要がある処理です。

チャットの受信トレイを開くには、**[!UICONTROL アクティビティ]**&#x200B;の下の左側のパネルで、**[!UICONTROL チャットの受信トレイ]**&#x200B;を選択します。

## チャットを受信 {#receive}

ステータスは、受信トレイの右上隅に表示されます。 **[!UICONTROL 利用可能]**&#x200B;とは、今すぐチャットを受け取れることを意味します。 ライブチャットの利用可能時間は、利用条件を満たすかどうかを決定します。[ ライブチャットの利用可能時間の設定](representative-setup.md#chat-availability)を参照してください。

チャットへのアクセス方法は、**[!UICONTROL Live Chat]**&#x200B;統合で設定されたルーティングの種類によって異なります。

* ラウンドロビンでは、資格のあるすべての代表者に同時に通知が送信され、最初に受け入れた担当者が会話を受け入れます。
* ダイレクトエージェントを使用すると、チャットは常に指定された担当者に来ます。
* カスタムルーティングを使用すると、チャットは、訪問者が一致した最優先度のルールに割り当てられた担当者に送信されます。

2つのタブで会話を整理します。

* **[!UICONTROL アクティブ]** – 現在進行中の会話。
* **[!UICONTROL すべて]** – 終了した会話を含むすべての会話。

## 会話をピックアップ {#pick-up}

決して冷たく始まらない。 顧客が何かを入力する前に、受信トレイには、訪問者がコンシェルジュに伝えた情報がすべて表示されます。

![概要とトピック、およびプロファイルの詳細パネルを含む、訪問者との会話の要約を表示するチャット受信箱](../assets/sales-handoff-inbox-1.png){width="800" zoomable="yes"}

| 表示される内容 | データを分析 |
| --- | --- |
| **[!UICONTROL 訪問者の会話の要約]** | 訪問者がコンシェルジュと交わした会話の&#x200B;**[!UICONTROL 概要]**、および話し合った&#x200B;**[!UICONTROL トピック]** |
| 会話の記録 | ライブチャットが開始された時点を超えた、コンシェルジュとの完全なやり取り |
| **[!UICONTROL フォームの詳細]** | 電子メール、製品への興味、会社など、訪問者が参加前にプリチャットフォームに入力した内容 |

トランスクリプトは、2つのシステム ライン `Live chat session has been initiated`と`Agent <name> has joined the chat`でハンドオフをマークするので、会話のどの部分がコンシェルジュで、どの部分が自分のものかを常に知ることができます。

メッセージボックスに入力し、**[!UICONTROL 送信]**&#x200B;を選択して返信します。

![担当者と訪問者の間で進行中のライブチャット ](../assets/sales-handoff-inbox-2.png){width="800" zoomable="yes"}

## 会話のスコアリング {#conversation-score}

チャットを終了する前に、訪問者の適格を評価します。 スコアは、実際に訪問者に話をした代表者であるあなたによって設定されます。これは、ダウンストリームで信頼できるものです。

**[!UICONTROL プロファイルの詳細]** パネルの&#x200B;**[!UICONTROL 会話スコア]**&#x200B;の下で、評価を選択します。 ダッシュはスコアがないことを意味し、炎のアイコンは会話を最小値から最も適格に評価します。

スコアが0、1、2、および3](../assets/sales-handoff-inbox-4.png){width="600" zoomable="yes"}としてリードレコードに保存されていることを説明する![会話スコアツールヒント

| 選択 | 格納された値 | 意味 |
| --- | --- | --- |
| ダッシュ | 0 | 最少適格 |
| 1つの炎 | 1 | やや適格 |
| 二つの炎 | 2 | 選定 |
| 三つの炎 | 3 | 最も適格 |

>[!IMPORTANT]
>
>スコアリングは必須です。 スコアリングせずにチャットを終了しようとすると、エラー`Please score the conversation before you close the chat`が表示され、チャットは開いたままになります。 スコアを付けると、確認が表示され、チャットを閉じることができます。

![会話スコアが保存されたことが確認されました](../assets/sales-handoff-inbox-3.png){width="800" zoomable="yes"}

スコアは[!DNL Marketo Engage]の&#x200B;**[!UICONTROL Engage with Live Chat in Concierge]** アクティビティに書き込まれ、フィルターとトリガーの制約として利用できます。 リターゲティング、リードスコアリング、パーソナライゼーション、CRMの引き継ぎを促進できます。 Marketo Engage](marketo-activities.md)の[Brand Concierge データを参照してください。

## チャットを終了 {#end-chat}

**[!UICONTROL チャットを終了]**&#x200B;を選択して、会話を閉じます。 訪問者は自分の側からそれを終了することもでき、最初に確認するように求められます。

チャットが終了すると、会話ステータスは2つの値のいずれかとして記録されます。

* **終了** – 会話は、あなた自身または訪問者によって意図的に終了しました。
* **Dropped** – 訪問者がサイトを離脱し、会話が非アクティブからタイムアウトしました。

>[!NOTE]
>
>ライブチャットの会話は30日間保持されます。

## 次の手順 {#next}

Marketo Engage](marketo-activities.md)の[Brand Concierge データで、マーケティングデータベースに書き戻される内容を確認します。
