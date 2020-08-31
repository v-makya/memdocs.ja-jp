---
title: Microsoft Intune のデバイス コンプライアンス パートナー - Azure | Microsoft Docs
description: Intune で管理するデバイスのコンプライアンス データのソースとして、サードパーティのデバイス コンプライアンス パートナーを使用します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643705"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Intune でサードパーティのデバイス コンプライアンス パートナーをサポートする

Microsoft Intune では、1 つ以上のサードパーティのデバイス コンプライアンス パートナーと共に管理しているデバイスのコンプライアンスの状態データを Azure Active Directory (Azure AD) に追加できます。 この構成を使用すると、それらのデバイスから得られるコンプライアンス データは、条件付きアクセス ポリシーで使用できます。

既定で、Intune は、お使いのデバイスのモバイル デバイス管理 (MDM) 機関として設定されます。 コンプライアンスパートナーを Azure AD と Intune に追加する場合、そのパートナーを、Azure AD ユーザー グループを介してそのパートナーに割り当てたデバイスのモバイル デバイス管理 (MDM) 機関のソースとして構成します。

デバイス コンプライアンス パートナーのデータを使用できるようにするには、次のタスクを実行します。

1. **デバイス コンプライアンス パートナーと連携するように Intune を構成**した後、そのコンプライアンス パートナーによって管理されるデバイスのユーザー グループを構成します。

2. **データを Intune に送信するようにコンプライアンス パートナーを構成します**。

3. **iOS または Android デバイスをそのデバイス コンプライアンス パートナーに登録します**。

これらのタスクが完了すると、デバイス コンプライアンス パートナーにより、デバイスの状態の詳細が Intune に送信されます。 Intune によって、この情報が Azure AD に追加されます。 たとえば、デバイスが非準拠状態の場合、その状態が、Azure AD 内のそのデバイスのレコードに追加されます。

コンプライアンスの状態は、Intune によって管理されるデバイスのコンプライアンス状態データと同じように、条件付きアクセス ポリシーによって評価されます。  既定で、Intune は、iOS および Android の登録済みコンプライアンス パートナーです。 パートナーを追加する場合、ビジネス ニーズに適合する適切なパートナーがデバイスを確実に管理できるように優先順位を設定できます。

## <a name="supported-device-compliance-partners"></a>サポートされるデバイス コンプライアンス パートナー

パブリック プレビュー:

- VMware Workspace ONE UEM (旧 AirWatch)

## <a name="prerequisites"></a>前提条件

- Microsoft Intune のサブスクリプションと、[Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)へのアクセス。

- デバイス コンプライアンス パートナーのサブスクリプション。

- サポートされるデバイス プラットフォームと追加の前提条件については、コンプライアンス パートナーのドキュメントをご確認ください。

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>デバイス コンプライアンス パートナーと連携するように Intune を構成する

そのパートナーからのコンプライアンス状態データを条件付きアクセス ポリシーで使用するには、デバイス コンプライアンス パートナーのサポートを有効にします。

### <a name="add-a-compliance-partner-to-intune"></a>コンプライアンス パートナーを Intune に追加する

1. [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[パートナー コンプライアンス管理]**  >  **[コンプライアンス パートナーの追加]** の順に移動します。

   > [!div class="mx-imgBorder"]
   > ![デバイス コンプライアンス パートナーを追加する](./media/device-compliance-partners/add-compliance-partner.png)

3. **[基本]** ページで、 **[コンプライアンス パートナー]** ドロップダウンを展開し、追加するパートナーを選択します。

   - iOS または Android プラットフォームに対するコンプライアンス パートナーとして VMware Workspace ONE を使用するには、 **[VMware Workspace ONE mobile compliance]\(VMware Workspace ONE モバイル コンプライアンス\)** を選択します。

   次に、 **[プラットフォーム]** のドロップダウンを選択し、プラットフォームを選択します。 macOS は、このプレビューではサポートされていません。

   複数のコンプライアンス パートナーを Azure AD に追加した場合でも、プラットフォームごとに 1 つのパートナーに制限されます。

4. **[割り当て]** で、このパートナーによって管理されるデバイスを持つユーザー グループを選択します。 この割り当てを使用して、このパートナーを使用する、該当するデバイスの MDM 機関を変更します。 パートナーによって管理されているデバイスを使用しているユーザーには、Intune のライセンスも割り当てる必要があります。

5. **[確認と作成]** ページで、選択を確認し、 **[作成]** を選択してこの構成を完了します。

構成が、[パートナー コンプライアンス管理] ページに表示されるようになります。

### <a name="modify-the-configuration-for-a-compliance-partner"></a>コンプライアンス パートナーの構成を変更する

1. [Microsoft エンドポイント マネージャー管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[テナント管理]**  >  **[コネクタとトークン]**  >  **[パートナー コンプライアンス管理]** の順に移動し、変更するパートナー構成を選択します。 構成は、プラットフォームの種類によって並べ替えられます。

3. パートナー構成の **[概要]** ページで、 **[プロパティ]** を選択して、[プロパティ] ページを開きます。このページで割り当てを編集できます。

4. **[プロパティ]** ページで、 **[編集]** を選択して、[割り当て] ビューを開きます。このビューで、この構成を使用するグループを変更できます。

5. **[レビューと保存]** 、 **[保存]** の順に選択して、編集内容を保存します。

6. "*このステップは、VMware Workspace ONE を使用する場合にのみ適用されます*"

   Workspace ONE UEM コンソール内から、Microsoft エンドポイント マネージャー管理センターに保存した変更を、手動で同期する必要があります。 変更を手動で同期するまで、構成の変更は Workspace ONE UEM によって認識されず、新しいグループに割り当てられたユーザーからは、コンプライアンスが正常に報告されません。

   Azure サービスから手動で同期するには:
   1. VMware Workspace ONE UEM コンソールにサインインします。
   2. **[Settings]\(設定\)**  >  **[System]\(システム\)**  >  **[Enterprise Integration]\(エンタープライズ統合\)**  >  **[Directory Services]\(ディレクトリ サービス\)** に移動します。
   3. *[Sync Azure Services]\(Azure サービスの同期\)* で、 **[SYNC]\(同期\)** をクリックします。

      初期構成または前回の手動同期の後に行ったすべての変更が、Azure サービスから UEM に同期されます。  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Intune と連携するようにコンプライアンス パートナーを構成する

デバイス コンプライアンス パートナーが Intune と連携できるようにするには、そのパートナー固有の構成を完了する必要があります。 このタスクの詳細については、該当するパートナーのドキュメントを参照してください。

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>iOS または Android デバイスをそのデバイス コンプライアンス パートナーに登録する

デバイスをデバイス コンプライアンス パートナーに登録する方法については、そのパートナーのドキュメントを参照してください。 パートナーにデバイスを登録し、コンプライアンス データを送信すると、そのコンプライアンス データは Intune に転送され、Azure AD に追加されます。

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>サードパーティのデバイス コンプライアンス パートナーによって管理されるデバイスを監視する

サードパーティのデバイス コンプライアンス パートナーを構成し、それらにデバイスを登録すると、パートナーによって、コンプライアンスの詳細が Intune に転送されます。 Intune によってそのデータが受信された後、デバイスに関する詳細を Azure portal で表示することができます。

Azure portal にサインインし、 **[Azure AD]**  >  **[デバイス]**  > [ **[すべてのデバイス]** ](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/) に移動します。

## <a name="next-steps"></a>次のステップ

サードパーティ パートナーのドキュメントを使用して、デバイスのコンプライアンス ポリシーを作成します。

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
