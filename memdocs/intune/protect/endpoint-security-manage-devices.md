---
title: Microsoft Intune でエンドポイント セキュリティを使用してデバイスを管理する |Microsoft Docs
description: セキュリティ管理者がエンドポイント セキュリティ ノードを使用してデバイスを確認し、Microsoft Endpoint Manager でデバイスを管理するための操作を行う方法について説明します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 8171eb3cf484c61e2b99046b36553a633d92044e
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431463"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Microsoft Intune でエンドポイント セキュリティを使用してデバイスを管理する

セキュリティ管理者は、Microsoft Endpoint Manager 管理センターの *[すべてのデバイス]* ビューを使用してデバイスを確認し、デバイスを管理するための操作を行います。 このビューには、Azure Active Directory (Azure AD) のすべてのデバイスの一覧が表示されます。 これには、Intune によって管理されるデバイス、Configuration Manager によって管理されるデバイス、Intune と Configuration Manager の両方で[共同管理](https://docs.microsoft.com/configmgr/comanage/overview)されるデバイスが含まれます。 Azure AD に統合されている場合、デバイスはクラウドとオンプレミスのインフラストラクチャに存在する可能性があります。

 ビューを見つけるには、[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)を開き、 **[エンドポイント セキュリティ]**  >  **[すべてのデバイス]** を選択します。

初期の *[すべてのデバイス]* ビューにはデバイスが表示され、それぞれに関する重要な情報が表示されます。

- デバイスの管理方法
- 準拠状態
- オペレーティング システムの詳細
- デバイスが最後にチェックインされた日時
- その他

![管理センターの [すべてのデバイス] ビュー](./media/endpoint-security-manage-devices/all-device-view.png)

デバイスの詳細を表示しているときに、ドリルダウンするデバイスを選択して詳細情報を確認できます。

## <a name="available-details-by-management-type"></a>管理の種類別の使用可能な詳細情報

Microsoft Endpoint Manager 管理センターでデバイスを表示しているときに、デバイスの管理方法を確認してください。 管理ソースは、管理センターに表示される情報と、デバイスを管理するために使用できる操作に影響を与えます。

次のフィールドを確認してみましょう。

- **管理者** – この列は、デバイスの管理方法を示します。 [管理者] には次のようなオプションがあります。

  - **MDM** - これらのデバイスは Intune によって管理されます。 コンプライアンス データは、Intune によって収集され、管理センターに報告されます。

  - **ConfigMgr** – "*テナントのアタッチ*" を使用して、Configuration Manager で管理するデバイスを追加すると、これらのデバイスは Microsoft Endpoint Manager 管理センターに表示されます。 これらのデバイスを管理するには、デバイスによって Configuration Manager クライアントが実行され、デバイスが次の状態である必要があります。

    - ワークグループ内にある (AAD に参加している、およびその他)
    - ドメインに参加している
    - ハイブリッド AAD に参加している (AD と AAD に参加している)

    Configuration Manager によって管理されるデバイスのコンプライアンス状態は、Microsoft Endpoint Manager 管理センターに表示されません。

    詳細については、Configuration Manager ドキュメントの[テナントのアタッチを有効にする](https://docs.microsoft.com/configmgr/tenant-attach/device-sync-actions)方法に関するページを参照してください。

  - **MDM/ConfigMgr エージェント** – これらのデバイスは、Intune と Configuration Manager 間の共同管理下にあります。

    共同管理を使用すると、[さまざまな共同管理ワークロードを選択](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)して、Configuration Manager または Intune によって管理される側面を決定できます。 これらの選択は、デバイスで適用されるポリシーと、コンプライアンス データを管理センターに報告する方法に影響を与えます。

    たとえば、Intune を使用して、ウイルス対策、ファイアウォール、および暗号化のポリシーを構成できます。 これらのポリシーの種類は、*Endpoint Protection* のポリシーと見なされます。 共同管理されているデバイスで Configuration Manager のポリシーではなく Intune のポリシーを使用するには、Endpoint Protection の共同管理スライダーを *[Intune]* または *[パイロット Intune]* に設定します。 スライダーが [Configuration Manager] に設定されている場合、デバイスでは代わりに Configuration Manager のポリシーと設定が使用されます。

- **コンプライアンス**:コンプライアンスは、デバイスに割り当てられているコンプライアンス ポリシーに照らして評価されます。 これらのポリシーのソースとコンソール内の情報は、デバイスの管理方法 (Intune による管理、Configuration Manager による管理、または共同管理) によって異なります。 共同管理されるデバイスでコンプライアンスを報告するには、デバイスのコンプライアンスの共同管理スライダーを [Intune] または [パイロット Intune] に設定します。  

  デバイスの管理センターにコンプライアンスが報告されたら、詳細情報にドリルダウンしてさらに詳細を表示できます。 デバイスが準拠していない場合は、詳細情報にドリルダウンして、準拠していないポリシーに関する情報を表示します。 この情報は、デバイスのコンプライアンスを調査して支援するのに役立ちます。

- **最後のチェックイン**:このフィールドは、デバイスで最後に状態が報告された時刻を示します。

## <a name="review-a-devices-policy"></a>デバイス ポリシーの確認

デバイスの一覧を表示しているときに、デバイスを選択してその詳細情報を確認するには、そのデバイスの *概要*ページを開きます。

デバイスの [概要] ページで **[Endpoint security configuration]\(エンドポイントのセキュリティ構成\)** を選択して、そのデバイスに適用されるエンドポイント セキュリティ ポリシーを表示できます。 MDM と Intune によって管理されているデバイスでは、ポリシーの詳細を表示できます。

![エンドポイント セキュリティ ポリシーの詳細の表示](./media/endpoint-security-manage-devices/view-policy-details.png)

Configuration Manager によって管理されているデバイスでは、ポリシーの詳細は表示されません。 これらのデバイスの追加情報を表示するには、Configuration Manager コンソールを使用します。

## <a name="remote-actions-for-devices"></a>デバイスのリモート操作

リモート操作とは、Microsoft Endpoint Manager 管理センターからデバイスに対して開始または適用できる操作のことです。 デバイスの詳細を表示すると、デバイスに適用されるリモート操作にアクセスできます。

リモート操作は、デバイスの*概要*ページの上部に表示されます。 画面の領域が制限されているために表示できない操作は、右側の省略記号を選択すると表示できます。

![追加の操作の表示](./media/endpoint-security-manage-devices/view-additional-actions.png)

使用可能なリモート操作は、デバイスの管理方法によって異なります。

- **Intune**:デバイス プラットフォームに適用されるすべての [Intune のリモート操作](../remote-actions/device-management.md)を使用できます。  
- **Configuration Manager**:Configuration Manager の次の操作を使用できます。

  - コンピューター ポリシーの同期
  - ユーザー ポリシーの同期
  - アプリの評価サイクル

- **共同管理**: Intune のリモート操作と Configuration Manager の操作の両方にアクセスできます。

Intune の一部のリモート操作では、デバイスをセキュリティで保護したり、デバイス上にある可能性のあるデータを保護したりできます。 リモート操作を使用すると、次のことができます。

- デバイスのロック
- デバイスのリセット
- 会社データの削除
- スケジュールされた実行以外のマルウェアのスキャン
- BitLocker キーのローテーション

Intune の次のリモート操作は、セキュリティ管理者にとって重要であり、[完全な一覧](../remote-actions/device-inventory.md#view-the-device-details)のサブセットです。 すべての操作がすべてのデバイス プラットフォームで使用できるわけではありません。 以下のリンクをクリックすると、各操作の詳細情報にアクセスできます。

- [デバイスの同期](../remote-actions/device-sync.md) – デバイスが Intune ですぐにチェックインされるようにします。 デバイスがチェックインされると、割り当てられた保留中の操作またはポリシーを受け取ります。  

- [再起動](../remote-actions/device-restart.md) – 5 分以内に Windows 10 デバイスを強制的に再起動します。 デバイスの所有者に再起動の自動通知が行われないため、作業内容が失われる可能性があります。

- [クイック スキャン](../configuration/device-restrictions-windows-10.md) – Defender で、デバイスのクイック スキャンを実行してマルウェアがないか確認し、結果を Intune に送信します。 クイック スキャンでは、レジストリ キーや既知の Windows スタートアップ フォルダーなど、マルウェアが登録されている可能性がある一般的な場所が確認されます。

- [フル スキャン](../configuration/device-restrictions-windows-10.md) – Defender で、デバイスのスキャンを実行してマルウェアがないか確認し、結果を Intune に送信します。 フル スキャンでは、マルウェアが登録されている可能性がある一般的な場所が確認され、デバイス上のすべてのファイルとフォルダーもスキャンされます。

- Windows Defender セキュリティ インテリジェンスの更新 – デバイスで Microsoft Defender ウイルス対策のマルウェア定義を更新します。 この操作ではスキャンは開始されません。

- [BitLocker キーの交換](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) – Windows 10 バージョン 1909 以降を実行するデバイスの BitLocker 回復キーをリモートで交換します。

また、 **[デバイスの一括操作]** を使用して、複数のデバイスに対する "*インベントリからの削除*" や "*ワイプ*" などのいくつかの操作を同時に管理することもできます。 [一括操作](../remote-actions/bulk-device-actions.md)は、 *[すべてのデバイス]* ビューで使用できます。 プラットフォーム、操作を選択し、最大 100 のデバイスを指定します。

![一括操作の選択](./media/endpoint-security-manage-devices/select-bulk-actions.png)

デバイス用に管理するオプションは、Intune でデバイスがチェックインされるまで有効になりません。

## <a name="next-steps"></a>次のステップ

[Intune でエンドポイント セキュリティを管理する](../protect/endpoint-security.md)