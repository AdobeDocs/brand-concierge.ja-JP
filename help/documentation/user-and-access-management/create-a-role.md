---
title: Brand Concierge権限を持つロールの作成
description: ロールを作成し、Brand Conciergeへのアクセスに必要な権限を付与する方法について説明します。
source-git-commit: fc22eb8e724437483e5d87283f46fb629a4e507c
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---


# Brand Concierge権限を持つロールの作成

Adobe Experience Platform権限でロールを作成して、ユーザーにBrand Conciergeへのアクセス権を付与します。

>[!PREREQUISITES]
>
>- 役割と権限を管理するために必要な管理者権限が必要です。
>- 最初にAdobe Experience Platform組織にユーザーを追加する必要があります。 詳しくは、[組織へのユーザーの追加](./add-a-user-to-the-org.md)を参照してください。

## 役割の作成

1. `experienceplatform.adobe.com`にログインします。

   >[!NOTE]
   >
   >この手順を公開する前に、エンジニアリングで実稼動URLを確認します。 ソースの記録に非公式な、あるいは文字起こしされていない可能性のあるURLが使用されていました。

1. 左側のナビゲーションで、**権限**&#x200B;までスクロールして選択します。
1. **役割**&#x200B;に移動して既存の役割を表示し、**新しい役割を作成**&#x200B;を選択します。
1. 役割の名前（`Brand Concierge Access Users`など）を入力し、説明を追加して、作成を確認します。
1. 新しい役割を開き、権限を割り当てます。

   1. **Brand Concierge**&#x200B;の権限リストを検索します。
   1. 「**Brand Conciergeを管理**」を選択します。

   現時点では、**Brand Conciergeの管理**&#x200B;のみが利用可能なBrand Concierge権限です。詳細な権限階層はまだ利用できません。

1. 役割がアクセスできるサンドボックスを選択します。

   組織には、独立したワークスペースである複数のサンドボックスを含めることができます。 この役割に適したサンドボックスのみを選択します。

1. 「**保存**」を選択します。

## 次の手順

役割を作成したら、その役割にユーザーを追加します。 詳しくは、[Brand Concierge ロールにユーザーを追加](./add-a-user-to-the-role.md)を参照してください。

## 注意事項

- サンドボックスの作成と管理のプロセスは、この手順の範囲外です。
- 長期的なロールモデルを定義する前に、Brand Conciergeの詳細な権限を追加する予定があるかどうかを確認します。
