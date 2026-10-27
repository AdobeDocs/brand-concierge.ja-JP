---
title: Adobe Marketo Qualifierでの代表者の設定
description: 担当者のOutlookやGoogleのカレンダーを接続し、ミーティングの確認メールを設定します。また、カレンダーとライブチャットの空き状況を定義し、設定された担当者を確認します。
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
source-git-commit: 91cbec8d6f4e4800e3bdc8c8f60bfe9ed168a963
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%
---
# Adobe Marketo Qualifierでの代表者の設定 {#representative-setup}

コンシェルジュがミーティングまたはライブチャットを提供する前に、少なくとも1人の代表者を[!DNL Adobe Marketo Qualifier]に設定する必要があります。 各代表者は、自分のプロファイルで1回これを行います。

管理者がユーザーを追加し、各担当者がカレンダーを接続し、確認メールを書き込み、ミーティングやチャットに利用できる日時を宣言します。

## 組織へのユーザーの追加 {#add-users}

管理者は、各営業担当者を[!DNL Adobe Admin Console]のユーザーとして追加し、[!DNL Adobe Marketo Qualifier]へのアクセス権を付与します。 一般的な手順については、[組織へのユーザーの追加](../user-and-access-management/add-a-user-to-the-org.md)および[役割へのユーザーの追加](../user-and-access-management/add-a-user-to-the-role.md)を参照してください。

担当者は残りの手順を自分で実行します。

## カレンダーの接続 {#connect}

カレンダー接続は、コンシェルジュが実際の空き状況を確認できるようにするものです。 それがない場合、担当者はミーティング予約の対象にはなりません。

1. [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}にログインし、**[!UICONTROL Adobe Marketo Qualifier]**&#x200B;を選択します。

   ![Adobe Marketo Qualifier カードを使用したAdobe Experience Cloud ホームページ ](../assets/meetings-connect-1.png){width="800" zoomable="yes"}

1. 左側のパネルの&#x200B;**[!UICONTROL 設定]**&#x200B;で、**[!UICONTROL プロファイル設定]**&#x200B;を選択し、**[!UICONTROL カレンダー設定]** タブを開きます。

1. 接続するカレンダー（[!DNL Microsoft Outlook]または[!DNL Google Calendar]）を選択します。

   OutlookとGoogleのカレンダー接続オプションを表示する![ カレンダー設定タブ ](../assets/meetings-connect-2.png){width="600" zoomable="yes"}

1. 既存のアカウントでログインするか、新しいアカウントを追加して、要求された権限を付与します。

   カレンダーの接続中に![Microsoft アカウント ピッカーが表示されます](../assets/meetings-connect-3.png){width="600" zoomable="yes"}

1. 訪問者がミーティングを予約したときに受信した確認メールを確認します。

   デフォルトの件名と本文が設定されます。 どちらか一方を編集し、招待に[!DNL Microsoft Teams] ミーティングリンクを含めるかどうかを選択します。

   ![編集可能な件名と本文を含むミーティング確認メール設定](../assets/meetings-connect-4.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL 保存]**」を選択します。

## カレンダーの空き状況の設定 {#calendar-availability}

カレンダーを接続すると、*ビジー*&#x200B;のとき、[!DNL Adobe Marketo Qualifier]に通知されます。 カレンダーの空き状況は、会議に参加する&#x200B;*意欲*&#x200B;のタイミングを表します。 両方が適用されます。

1. **[!UICONTROL プロファイル設定]**&#x200B;で、「**[!UICONTROL カレンダーの空き状況]**」タブを開きます。

   ![空き時間が設定される前の「カレンダーの空き時間」タブ ](../assets/meetings-availability-1.png){width="600" zoomable="yes"}

1. ミーティングのルールを設定。

   | 設定 | 制御するもの |
   | --- | --- |
   | ミーティング期間 | 予約されたミーティングの所要時間、および提供される各スロットの長さ |
   | バッファー時間 | 1回のミーティングの終了と次のミーティングの開始の間に適用されるギャップ |
   | 最低限知らせ | 訪問者が予約する必要がある距離。 例えば、10分以内に始まるスロットの予約を訪問者が避けるために、4時間を設定します |
   | タイムゾーン | 利用可能時間はで表されます。 訪問者は常に自分のタイムゾーンに変換されたスロットを見ます |

1. 週の各日の利用可能時間を設定します。

   1日は、午前8:00～午後5:00などの1つの連続ブロック、または午前8:00～午後12:00や午後2:00～午後5:00などの複数のブロックにすることができます。 その日に会議を行わないように、空の日を残します。

   >[!NOTE]
   >
   >1日に別の時間ブロックを追加するには、プラス記号（![ プラス記号アイコン ](../assets/icon-plus-sign.png)）を選択します。

   ![平日の時間と分割された時間範囲が設定されたカレンダーの空き状況タブ ](../assets/meetings-availability-2.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL 保存]**」を選択します。

### スロットが予約可能になる方法 {#slot-logic}

タイムスロットは、次の3つのチェックをすべて実行した場合にのみ、訪問者に提供されます。

1. ここに設定した利用可能な時間の中に入ります。
1. 接続されているカレンダー上のイベントにまだ占有されていません。 既存の午前9時の会議では、午前9時のスロットが削除されます。
1. それはあなたの最小通知とバッファ時間を満たします。

## ライブチャットの利用状況の設定 {#chat-availability}

ライブチャットの利用状況は、カレンダーの利用状況とは異なります。 担当者はチャットを利用できますが、会議を行わないか、その逆を行います。

1. **[!UICONTROL プロファイル設定]**&#x200B;で、「**[!UICONTROL ライブチャットの利用状況]**」タブを開きます。

1. タイムゾーンを設定し、ライブチャットを受け取る希望の日と時間を設定します。 週末は含めることができます。

   ![ ライブチャットの空き状況タブ。日数と時間が設定されています](../assets/meetings-availability-3.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL 保存]**」を選択します。

>[!NOTE]
>
>利用可能時間により、*チャットの対象*&#x200B;になります。 チャットの受信トレイにライブ ステータスが表示され、現在受信しているかどうかが決定されます。 [ チャット受信箱](chat-inbox.md)を参照してください。

## 設定したユーザーを確認する {#manage-members}

このセクションは管理者専用です。 **[!UICONTROL 管理]**&#x200B;で「**[!UICONTROL メンバーを管理]**」を選択すると、カレンダーを接続した担当者、ライブチャットの空き状況を設定した担当者、カレンダーを切断した担当者など、すべての担当者の状態が1か所で表示されます。

Composerで統合をアクティブ化する前に、これを使用します。 接続されたカレンダーなしでここに表示される担当者は、ミーティング予約の対象にはなりません。また、ライブチャットの空き状況がない担当者は、ライブチャットの対象にはなりません。

![ メンバーの管理ページに一覧表示されている代表者とそのカレンダーおよびライブチャットの設定状態](../assets/manage-members-1.png){width="800" zoomable="yes"}

## 次の手順 {#next}

少なくとも1人の代表者が設定されている場合は、訪問者と代表者のマッチング方法を決定します。 [担当者への会話のルーティング ](routing-rules.md)を参照してください。
