---
title: 開発者向けガイド
description: Brand Concierge Web SDKとWeb クライアントのインストール、外観とコンテンツのカスタマイズ、クライアントサイドイベントの処理、会話データの書き出し方法について説明します。
role: Developer,Admin
level: Experienced
toc: true
source-git-commit: 13db0491c987a08492820ac216e20feb87f30e44
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 4%

---


# 開発者向けガイド {#developer-customization-guide}

このガイドは、Brand Conciergeのデプロイメントを実装またはカスタマイズする開発者向けおよび技術者向けです。 Web SDKとWeb クライアントのインストール、外観とコンテンツのカスタマイズ、コールバック関数を使用したクライアントサイドイベントのリッスン、レポート用の会話データのエクスポートについて説明します。

## Web SDKとWeb クライアントのインストール {#installation}

### 前提条件 {#prerequisites}

* Adobe Experience Platform（AEP）をご利用のお客様。
* このページは、Adobe Experience Platform Web SDKで実装されています。
* ページで使用されるデータストリーム IDは、Brand Conciergeに対して有効になっています。

### 手順1:Web SDKの挿入 {#inject-web-sdk}

ページの`<head>` セクションに以下を追加します。

```html
<script>
  !(function (n, o) {
    o.forEach(function (o) {
      n[o] ||
        ((n.__alloyNS = n.__alloyNS || []).push(o),
        (n[o] = function () {
          var u = arguments;
          return new Promise(function (i, l) {
            n[o].q.push([i, l, u]);
          });
        }),
        (n[o].q = []));
    });
  })(window, ["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.31.1/alloy.min.js"></script>
```

### 手順2:Web クライアントの挿入 {#inject-web-client}

Web SDK スクリプトの後に、`<head>` セクションに次を追加します。

```html
<script src="https://experience.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js"></script>
```

### 手順3:Web SDKの設定 {#configure-web-sdk}

以下のプレースホルダーの代わりに、組織の独自の値で`alloy("configure", ...)`を呼び出します。

```javascript
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "edge.adobedc.net",
  edgeBasePath: "ee",
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_IMS_ORG_ID",
  debugEnabled: true,
  idMigrationEnabled: false,
  thirdPartyCookiesEnabled: false,
  prehidingStyle: ".personalization-container { opacity: 0 !important }",
  onBeforeEventSend: (options) => {
    const x = options.xdm;
    const params = new URLSearchParams(window.location.search);
    const titleParam = params.get("title");
    if (titleParam) {
      x.web.webPageDetails.name = titleParam;
    } else {
      x.web.webPageDetails.name = "default-page";
    }
    return true;
  }
});
alloy("sendEvent", {});
```

| フィールド | 説明 |
|---|---|
| `datastreamId` | このページ用に設定されたデータストリーム IDは、Brand Conciergeに対して有効になっています。 |
| `orgId` | コンシェルジュが設定されているIMS組織ID。 |
| `debugEnabled` | 統合が検証されると、実稼動環境で`false`に設定されます。 |
| `prehidingStyle` | パーソナライゼーションコンテンツが読み込まれる前にCSSを適用して、スタイル設定されていないコンテンツのフラッシュを防ぎます。 |
| `onBeforeEventSend` | XDM ペイロードを送信前に変更するためのオプションのフック（ページ名やコンテキストの設定によく使用されます）。 |

### 手順4:Web クライアントの初期化 {#initialize-web-client}

Web SDKのconfigure呼び出しの後、ブートストラップ APIを呼び出してWeb クライアントを初期化します。

```javascript
window.adobe.concierge.bootstrap({
  instanceName: "alloy",
  stylingConfigurations: window.styleConfigurations,
  selector: "#brand-concierge-mount"
});
```

| パラメーター | タイプ | 必須 | 説明 |
|---|---|---|---|
| `instanceName` | string | ○ | Web SDK インスタンス名。 |
| `stylingConfigurations` | JSON オブジェクト | ○ | Web クライアントのスタイル設定（[&#x200B; ビジュアルおよびコンテンツのカスタマイズ &#x200B;](#customization)を参照）。 |
| `selector` | string | ○ | Web クライアントがマウントするHTML要素のCSS セレクター。 |
| `onEvent` | 関数 | × | クライアントサイドイベントのコールバック（[&#x200B; クライアントサイドイベントとコールバック関数](#events)を参照）。 |

## ビジュアルとコンテンツのカスタマイズ {#customization}

`bootstrap()`に渡された`stylingConfigurations` オブジェクトは、Web クライアント全体の外観、動作、およびテキストを制御します。 いくつかの領域に編成されています。

### メタデータ {#metadata}

```javascript
"metadata": {
  "brandName": "Your Brand",
  "version": "1.0.0",
  "language": "en-US",
  "namespace": "brand-concierge"
}
```

### 動作 {#behavior}

個々のチャット機能の動作を制御します。

```javascript
"behavior": {
  "input": {
    "enableVoiceInput": true
  },
  "chat": {
    "messageAlignment": "left",
    "messageWidth": "80%"
  },
  "privacyNotice": {
    "title": "Privacy Notice",
    "text": "By using this automated chatbot, you consent that any personal information you provide in the chat may be collected, used, analyzed, disclosed, and retained by Adobe and its service providers, in accordance with the Adobe Privacy Policy. Please do not enter any sensitive personal information (e.g., financial or health data)."
  },
  "disclaimer": {
    "attachWithInput": true
  },
  "chatTranscript": {
    "enabled": true,
    "maxSessions": 1,
    "maxMessagesPerSession": 20,
    "cleanupInterval": 24
  },
  "meetingForm": {
    "fieldsPerRow": 2,
    "title": { "text": "Schedule meeting", "alignment": "left" },
    "subtitle": { "text": "I'd be happy to help you schedule a meeting! Please fill out the form below, and we'll follow up with a calendar to confirm your day and time.", "alignment": "left" },
    "buttons": {
      "submit": { "text": "Schedule meeting", "alignment": "left" },
      "cancel": { "text": "Cancel", "alignment": "left" }
    }
  },
  "calendarWidget": {
    "title": { "text": "Book a meeting", "alignment": "left" },
    "subtitle": { "text": "Thanks! Here's a calendar where you can choose a time that works best for your schedule:", "alignment": "left" },
    "postTitle": { "text": "Once confirmed, you'll receive a calendar invite with all the details.", "alignment": "left" },
    "buttons": {
      "confirm": { "text": "Schedule a meeting", "alignment": "left" },
      "cancel": { "text": "Cancel", "alignment": "left" }
    }
  }
}
```

### 免責事項 {#disclaimer}

```javascript
"disclaimer": {
  "text": "AI responses may be inaccurate or misleading. Be sure to double check answers and sources."
}
```

### テキスト文字列 {#text-strings}

すべてのユーザー向けコピーは、`text` オブジェクトを通じて上書きできます。 共通キー：

| キー | 目的 |
|---|---|
| `welcome.heading` / `welcome.subheading` | ようこそ画面の見出しとサブテキスト |
| `input.placeholder` | フィールドのプレースホルダーテキストを入力 |
| `input.messageInput.aria` / `input.send.aria` / `input.mic.aria` | 入力コントロールのアクセシビリティラベル |
| `error.network` / `error.general` | 訪問者に表示されるエラーメッセージ |
| `loading.message` | 応答の生成中に表示されるテキスト |
| `feedback.dialog.title.positive` / `.negative` | フィードバックダイアログのタイトル |
| `feedback.dialog.question.positive` / `.negative` | フィードバックダイアログプロンプトテキスト |
| `feedback.toast.success` | フィードバック送信後の確認トースト |
| `feedback.thumbsUp.aria` / `feedback.thumbsDown.aria` | フィードバックボタンのアクセシビリティラベル |

### 配列 {#arrays}

コンテンツの設定可能なリスト：

```javascript
"arrays": {
  "welcome.examples": [
    {
      "text": "I want to edit and enhance my photos",
      "image": "https://example.com/idea-1.png",
      "backgroundColor": "#66BFE7"
    }
  ],
  "feedback.positive.options": [
    "Helpful and relevant recommendations",
    "Clear and easy to understand",
    "Friendly and conversational tone",
    "Visually appealing presentation",
    "Other"
  ],
  "feedback.negative.options": [
    "Not helpful or relevant",
    "Confusing or unclear",
    "Too formal or robotic",
    "Poor visual presentation",
    "Other"
  ]
}
```

### アセット {#assets}

```javascript
"assets": {
  "icons": {
    "company": "<svg>...</svg>"
  }
}
```

### テーマ {#theme}

色、フォント、レイアウトを制御するCSS カスタムプロパティ：

```css
"theme": {
  "--color-primary": "#1473e6",
  "--color-primary-hover": "#0056b3",
  "--color-button-primary": "#3B63FB",
  "--color-accent": "#9085ED",
  "--color-button-submit": "#4759e6",
  "--color-button-submit-hover": "#3a4bce",
  "--color-message-user": "#1473e6",
  "--font-family": "'Adobe Clean', adobe-clean, 'Trebuchet MS', sans-serif",
  "--main-container-background": "linear-gradient(135deg, #66ccff, #cc99ff, #ffcc99, #ccff99)",
  "--submit-button-fill-color": "white",
  "--card-text-background": "var(--color-background)",
  "--card-text-border-radius": "var(--border-radius-card)",
  "--message-concierge-link-decoration": "underline",
  "--message-max-width": "100%"
}
```

## クライアントサイドのイベントとコールバック関数 {#events}

イベントコールバックシステムを使用すると、Web クライアントのライフサイクルイベント、ユーザーインタラクション、応答、フィードバック、およびエラーをリアルタイムで確認できます。これは、Adobe Analytics、Google Analytics、またはその他のサードパーティシステムにエンゲージメントデータを送信するのに便利です。

### 主な特徴 {#key-characteristics}

* **単一のコールバック** — 1つの`onEvent`関数は、すべてのイベントタイプを受け取り、`event.eventType`で区別します。
* **読み取り専用** — イベントデータは複製されたスナップショットであり、クライアントの動作の変更に使用できません。
* **Error-isolated** — コールバック内でスローされた例外が検出され、ログに記録されます。Web クライアントは壊れません。
* **`bootstrap()`**&#x200B;経由で登録 – `onBeforeEventSend`と同じ方法で合格しました。

### クイックスタート {#quick-start}

```javascript
window.adobe.concierge.bootstrap({
  instanceName: "my-instance",
  selector: "#brand-concierge-mount",
  stylingConfigurations: { /* ... */ },
  onEvent: (event) => {
    console.log(event.eventType, event.timestamp, event.data);
  }
});
```

### イベントタイプによるフィルタリング {#filtering}

```javascript
onEvent: (event) => {
  switch (event.eventType) {
    case "query:submitted":
      console.log("User query:", event.data.query);
      break;
    case "response:completed":
      console.log("Response received:", event.data.conversationId);
      break;
    case "card:clicked":
      console.log("Card clicked:", event.data.element.entity_info.productName);
      break;
    case "error:occurred":
      console.log("Error:", event.data.errorMessage);
      break;
  }
}
```

### イベントタイプ {#event-types}

| イベントタイプ | 値 | カテゴリ | 発火したとき |
|---|---|---|---|
| `WEBCLIENT_INITIALIZED` | `webclient:initialized` | ライフサイクル | クライアントが初期化を完了します（DOM マウント済み、コンテンツの読み込み） |
| `QUERY_SUBMITTED` | `query:submitted` | ユーザーインタラクション | ユーザーがメッセージを送信します（入力または提案から） |
| `PROMPT_SUGGESTION_CLICKED` | `promptSuggestion:clicked` | ユーザーインタラクション | ユーザーがプロンプト「suggestion pill」をクリックすると |
| `CARD_CLICKED` | `card:clicked` | ユーザーインタラクション | ユーザーがカードをクリックすると |
| `HISTORY_CLEARED` | `history:cleared` | ユーザーインタラクション | ユーザーはチャット履歴を消去します |
| `RESPONSE_STARTED` | `response:started` | 応答 | APIから最初のストリーミングチャンクが到着する |
| `RESPONSE_COMPLETED` | `response:completed` | 応答 | 完全な応答は受信され、レンダリングされます |
| `CARDS_RENDERED` | `cards:rendered` | 応答 | カード（単一の画像またはカルーセル）がレンダリングを終了 |
| `FEEDBACK_SUBMITTED` | `feedback:submitted` | フィードバック | ユーザーがフィードバックフォームを送信します（詳細が親指で上下されます） |
| `ERROR_OCCURRED` | `error:occurred` | エラー | エラーが発生する（ネットワーク、API、ランタイム） |

### ライフサイクルイベント {#lifecycle-events}

`webclient:initialized`は、クライアントが完全に初期化された後に起動します。コンテンツが読み込まれ、CSSが挿入され、DOMでチャット UIがレンダリングされます。

```json
{
  "eventType": "webclient:initialized",
  "timestamp": 1741638123789,
  "data": {
    "instanceName": "my-instance"
  }
}
```

### ユーザーインタラクションイベント {#user-interaction-events}

`query:submitted`は、ユーザーが入力されたメッセージ、プロンプトの提案、またはウィジェットオプションからメッセージを送信したときに発生します。

```json
{
  "eventType": "query:submitted",
  "timestamp": 1741638124000,
  "data": {
    "query": "What photo editing tools do you offer?"
  }
}
```

`promptSuggestion:clicked`は、ユーザーがプロンプト候補ピルをクリックすると起動します。 後続の`query:submitted` イベントの&#x200B;*before*&#x200B;を起動します。

```json
{
  "eventType": "promptSuggestion:clicked",
  "timestamp": 1741638124100,
  "data": {
    "suggestion": "Tell me more about Photoshop"
  }
}
```

ユーザーがカードをクリックすると、`card:clicked`が起動します。

```json
{
  "eventType": "card:clicked",
  "timestamp": 1741638124200,
  "data": {
    "element": {
      "entity_info": {
        "productName": "Adobe Photoshop",
        "productDescription": "Photo editing software",
        "productPageURL": "https://www.adobe.com/products/photoshop.html",
        "productImageURL": "https://example.com/photoshop.png"
      }
    }
  }
}
```

ユーザーがclear-chat-history ボタンをクリックすると、`history:cleared`が起動します。

```json
{
  "eventType": "history:cleared",
  "timestamp": 1741638124400,
  "data": {}
}
```

### 応答イベント {#response-events}

`response:started`は、最初のストリーミングチャンクがAPIから到着したときに起動します。

```json
{
  "eventType": "response:started",
  "timestamp": 1741638125000,
  "data": {
    "conversationId": "conv-abc-123",
    "interactionId": "int-xyz-456"
  }
}
```

`response:completed`は、完全な応答を受信したときに起動します。

```json
{
  "eventType": "response:completed",
  "timestamp": 1741638126000,
  "data": {
    "conversationId": "conv-abc-123",
    "interactionId": "int-xyz-456"
  }
}
```

`cards:rendered`は、カードがDOMでレンダリングされた後に起動します。 `response:completed`とは別に起動し、使用されている表示モードを示します。

```json
{
  "eventType": "cards:rendered",
  "timestamp": 1741638126100,
  "data": {
    "element": [
      { "entity_info": { "productName": "Adobe Photoshop" } },
      { "entity_info": { "productName": "Adobe Illustrator" } }
    ],
    "displayMode": "carousel"
  }
}
```

### フィードバックイベント {#feedback-events}

`feedback:submitted`は、ユーザーがフィードバックフォームを入力して送信すると起動します（親指で上下に移動）。

```json
{
  "eventType": "feedback:submitted",
  "timestamp": 1741638127000,
  "data": {
    "conversationId": "conv-abc-123",
    "interactionId": "int-xyz-456",
    "feedbackType": "negative",
    "selectedOptions": ["Incorrect information", "Not relevant"],
    "notes": "The response did not address my question about pricing."
  }
}
```

### エラーイベント {#error-events}

`error:occurred`は、クライアントがネットワーク、API、またはランタイムエラーを検出したときに起動します。

```json
{
  "eventType": "error:occurred",
  "timestamp": 1741638128000,
  "data": {
    "errorMessage": "Something went wrong. Please try again."
  }
}
```

### イベントオブジェクトの構造 {#event-object-structure}

各イベントは、同じトップレベルのシェイプを共有します。

```typescript
interface BrandConciergeEvent {
  eventType: string;  // e.g. "query:submitted"
  timestamp: number;  // Unix epoch, milliseconds
  data: object;       // Event-specific payload
}
```

### データタイプ参照：要素（製品カード） {#element-reference}

```typescript
interface Element {
  id?: string;
  type?: string;
  entity_info: {
    productName: string;
    productDescription: string;
    description: string;
    productPageURL: string;
    details: string;
    backgroundColor: string;
    learningResource: string;
    productImageURL: string;
    logo: string;
    variants?: Record<string, ElementVariant>;
    primary: ElementAction;
    secondary: ElementAction;
  };
}

interface ElementAction {
  label: string;
  url: string;
}
```

### ベストプラクティス {#best-practices}

* **分析と監視に使用します。** エンゲージメント、クエリパターン、製品への関心を追跡します。エラー追跡サービスに`error:occurred`を転送します。コンバージョン分析のためにカードのクリックを追跡します。
* **コールバックを高速に保持します。** これはメインスレッド上で同期して実行されるので、ネットワーク呼び出しをブロックしないようにする：

```javascript
// Good — fire and forget
onEvent: (event) => {
  navigator.sendBeacon("/analytics", JSON.stringify(event));
}

// Avoid — blocking network call
onEvent: async (event) => {
  await fetch("/analytics", { body: JSON.stringify(event) });
}
```

* **状態マシンに対して厳密なイベント順序**&#x200B;を使用しないでください。 イベントは論理的な順序で発生しますが、順序を仮定する代わりに`conversationId`と`interactionId`を使用して関連するイベントを関連付けます。
* **独自のコールバック内のエラーを処理します。** クライアントはコールバックエラーを分離してログに記録しますが、コールバック内の未処理エラーは分析データを失う可能性があります。

```javascript
onEvent: (event) => {
  try {
    myAnalytics.track(event);
  } catch (e) {
    console.warn("Analytics tracking failed", e);
  }
}
```

## AEP Query Serviceを使用した会話の書き出し {#export-conversations}

Brand Conciergeは、プロンプト、応答、フィードバックなどの会話データをAdobe Experience Platform（AEP）データセットに書き込みます。 クエリサービス（SQL）を使用して直接クエリし、カスタムレポートを作成できます。

### データセットとテーブル名を見つける {#find-dataset}

1. Adobe Experience Platformを開きます。

1. **[!UICONTROL データセット]**&#x200B;に移動します。

1. `cja_brand_concierge`を検索して、Brand Conciergeに関連するデータセットを一覧表示します。

1. 必要なデータセットを開きます（複数が存在する場合、回答と他のフローなど）。

1. データセットの詳細ビューで、クエリサービスで使用される&#x200B;**[!UICONTROL テーブル名]**&#x200B;を見つけ、サンプルまたはプレビューデータを調べて、列（プロンプト、応答、フィードバック、タイムスタンプなど）を確認します。

>[!NOTE]
>
>テーブル名は各データセットに関連付けられ、環境とサンドボックスによって異なります。 複数のサンドボックスまたはデプロイメントがある場合は、データが書き込まれる場所とテーブル名が一致するように、正しいサンドボックスでこれらの手順を繰り返します。

### クエリの例 {#example-query}

```sql
SELECT *
FROM cja_brand_concierge_responses_dataset_5f5105bd_1c38_4ebc_8505_bd
WHERE timestamp >= TIMESTAMP '2026-03-16 00:00:00'
  AND timestamp <= NOW()
ORDER BY timestamp ASC;
```

>[!IMPORTANT]
>
>上記の表名は単なる図であり、ハードコーディングしないでください。 最初にAEPでデータセットの実際のテーブル名を確認し（[&#x200B; データセットとテーブル名の検索](#find-dataset)を参照）、時間フィルター、並べ替え順序、またはその他の句を調整して、レポートのニーズに合わせて調整します。 データセットと同じサンドボックスを使用して、組織のクエリサービスワークフロー（UI、API、または接続されたクライアント）からクエリを実行します。

### クエリサービス UIでのクエリの実行 {#run-query-ui}

レポート用の手動データプルが必要な場合、クエリサービス UIには、結果を直接実行してダウンロードする方法が用意されています。

1. Adobe Experience Platformで、**[!UICONTROL Queries]**&#x200B;に移動します。

1. エディターにクエリを入力し、**[!UICONTROL クエリを実行]**&#x200B;をクリックします。

1. クエリが完了すると、結果はエディターの下の&#x200B;**[!UICONTROL 結果]** タブに表示されます。 そこから、結果をダウンロードできます。

### 関連トピックス {#further-reading}

* [Query Service API ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/query/home){target="_blank"} – このガイドとは関係なく、時間の経過とともに変化するQuery Serviceの動作、制限、認証、およびAPI パスに関するAdobeの公式リファレンス。
