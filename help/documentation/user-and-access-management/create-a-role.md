---
title: Brand Concierge権限を持つロールの作成
description: ロールを作成し、Brand Conciergeへのアクセスに必要な権限を付与する方法について説明します。
source-git-commit: 60835c7971d86341194d773f9cf487c4cb6f171a
workflow-type: tm+mt
source-wordcount: '212'
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
