---
title: モバイル デバイス管理機関の設定
titleSuffix: Microsoft Intune
description: Intune でモバイル デバイス管理機関を設定します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e1ac5180a30959618f37d909511785b4de1c407
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88591243"
---
# <a name="set-the-mobile-device-management-authority"></a>モバイル デバイス管理機関の設定

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

モバイル デバイス管理 (MDM) 機関の設定によって、デバイスの管理方法が決まります。 IT 管理者が MDM 機関を設定してからでないと、ユーザーは管理対象のデバイスを登録できません。

可能な構成は以下のとおりです。

- **Intune スタンドアロン** - Azure Portal を利用して構成する、クラウドのみの管理。 Intune で提供される機能がすべて含まれます。 [Intune コンソールで MDM 機関を設定](#set-mdm-authority-to-intune)します。

- **Intune 共同管理** - Intune クラウド ソリューションと Windows 10 用 Configuration Manager デバイスの統合。 Configuration Manager コンソールを使用して Intune を構成します。 [Intune へのデバイスの自動登録を構成します](https://docs.microsoft.com/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune)。 

- **Basic Mobility and Security for Office 365** - この構成を有効にしている場合、MDM 機関は "Office 365" に設定されます。 Intune の使用を開始するには、Intune のライセンスを購入する必要があります。

- **Basic Mobility and Security for Office 365 共存** - Basic Mobility and Security for Office 365 を既に使用している場合は自分のテナントに Intune を追加し、管理機関をユーザーごとに Intune または Basic Mobility and Security for Office 365 に設定し、その MDM 登録デバイスの管理に使用されるサービスを指示できます。 各ユーザーの管理機関は、ユーザーに割り当てられたライセンスに基づいて定義されます。ユーザーに Microsoft 365 Basic または Standard のライセンスのみが与えられている場合、そのデバイスは Basic Mobility and Security for Office 365 によって管理されます。 ユーザーが Intune の権利を与えるライセンスを所持している場合、そのユーザーのデバイスは Intune によって管理されます。 以前は Basic Mobility and Security for Office 365 によって管理されていたユーザーに、Intune の権利を与えるライセンスを追加すると、そのユーザーのデバイスは Intune の管理に切り替わります。 ユーザーを Intune に切り替える前に、Intune の構成をユーザーに割り当てて Basic Mobility and Security for Office 365 を置き換えるようにしてください。そうしないと、デバイスで Basic Mobility and Security for Office 365 の構成が失われ、Intune から置き換えとなるものが受信されません。

## <a name="set-mdm-authority-to-intune"></a>MDM 機関を Intune に設定する

1911 サービス リリース以降を使用しているテナントの場合、MDM 機関は自動的に Intune に設定されます。

1911 より前のサービス リリースを使用しているテナントで、MDM 機関をまだ設定していない場合は、次の手順に従います。

1. [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) で、オレンジのバナーを選択して **[モバイル デバイス管理機関]** の設定を開きます。 オレンジのバナーは、MDM 機関をまだ設定していない場合にのみ表示されます。
2. **[モバイル デバイス管理機関]** で、次の選択肢から MDM 機関を選択します。
  - **Intune MDM 機関**
  - **なし**

  ![Intune のモバイル デバイス管理機関設定画面のスクリーンショット](./media/mdm-authority-set/set-mdm-auth.png)

  MDM 機関が Intune に正しく設定されたことを示すメッセージが表示されます。

### <a name="workflow-of-intune-administration-ui"></a>Intune 管理 UI のワークフロー
Android または Apple デバイスの管理が有効になっていると、Intune では、それぞれのデバイスを管理するために、デバイスとユーザー情報を送信し、これらのサード パーティ サービスと統合できるようにします。

データを共有することに同意するシナリオは、次の場合に含まれます。
- Android 仕事用プロファイルを有効にする。
- Apple MDM プッシュ通知証明書を有効にしてアップロードする
- Device Enrollment Program、School Manager および Volume Purchasing Program など、Apple の任意のサービスを有効にする

いずれの場合も、同意はモバイル デバイス管理サービスの実行に厳密に関連します。 たとえば、IT 管理者が Google または Apple デバイスの登録を許可されていることを確認します。 新しいワークフローが公開されたとき、どの情報が共有されるかを示すドキュメントは、次の場所から入手することができます。
- [Intune から Google に送られるデータ](https://aka.ms/Data-intune-sends-to-google)
- [Intune から Apple に送られるデータ](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>主な考慮事項
新しい MDM 機関に切り替えた後、多くの場合、デバイスがチェックインしてサービスと同期されるまでに移行時間 (最大 8 時間) があります。 変更後も引き続き登録済みデバイスが管理および保護されるように、新しい MDM 機関で設定を構成する必要があります。 
- デバイスの既存の設定が新しい MDM 機関の設定 (Intune スタンドアロン) に置き換わるように、変更後にご使用のデバイスをサービスに接続する必要があります。
- MDM 機関を変更した後も、前の MDM 機関からの基本的な設定の一部 (プロファイルなど) が、最大 7 日間、またはデバイスが最初にサービスに接続するまで、デバイスに残ります。 できるだけ早く新しい MDM 機関でアプリと設定 (ポリシー、プロファイル、アプリなど) を構成し、既存の登録済みデバイスを持つユーザーが含まれているユーザー グループにその設定を展開することをお勧めします。 MDM 機関の変更後、デバイスがサービスに接続すると、新しい MDM 機関の新しい設定がすぐに送信されるので、管理と保護の中断を回避できます。
- 関連付けられているユーザーがいない (通常は iOS/iPadOS の Device Enrollment Program または一括登録シナリオの場合) デバイスは、新しい MDM 機関に移行されません。 これらのデバイスでは、新しい MDM 機関への移行を支援してもらうためにサポートを要請する必要があります。

## <a name="coexistence"></a>Coexistence

共存を有効にすると、既存のユーザーに対して Basic Mobility and Security を引き続き使用しながら、新しい一連のユーザーに対して Intune を使用できます。 ユーザーを介して Intune によって管理されるデバイスを制御します。 ユーザーに Intune ライセンスが割り当てられている場合、またはユーザーが Configuration Manager で Intune 共同管理を使用している場合、登録されている彼らのデバイスはすべて Intune によって管理されます。 それ以外の場合、ユーザーは Basic Mobility and Security によって管理されます。

共存を有効にするための主要な手順は次の 3 つです。
1. 準備
2. Intune MDM 機関を追加する
3. ユーザーとデバイスの移行 (オプション)。

### <a name="preparation"></a>準備

Basic Mobility and Security との共存を有効にする前に、次の点を考慮してください。
- Intune で管理する予定のユーザーに対して、十分な Intune 対応のライセンスがあることを確認します。
- Intune 対応のライセンスが割り当てられているユーザーを確認します。 共存を有効にした後、Intune 対応のライセンスが既に割り当てられているユーザーは自分のデバイスを Intune に切り替えることができます。 予期しないデバイス切り替えを回避するために、共存を有効にするまでは、Intune 対応のライセンスを割り当てないことをお勧めします。
- Intune ポリシーを作成して展開することで、Office 365 Security & Compliance ポータルを通して最初に展開したデバイス セキュリティ ポリシーを置き換えます。 この置き換えは、Basic Mobility and Security から Intune に移行させる予定のすべてのユーザーに対しても行う必要があります。 それらのユーザーに Intune ポリシーが割り当てられていない場合、共存が有効にされると、彼らは Basic Mobility and Security の設定を失ってしまう可能性があります。 これらの設定は、マネージド電子メール プロファイルのように、置き換えないと失われます。

### <a name="add-intune-mdm-authority"></a>Intune MDM 機関を追加する

共存を有効にするには、ご利用の環境の MDM 機関として Intune を追加する必要があります。

1. Azure AD グローバルまたは Intune サービス管理者権限を使用して、endpoint.microsoft.com にサインインします。
2. **[デバイス]** に移動します。
3. **[MDM 機関の追加] ブレード**が表示されます。
4. MDM 機関を *Office 365* から *Intune* に切り替えてから共存を有効にするには、 **[Intune MDM 機関]**  >  **[追加]** の順に選択します。
  ![[MDM 機関の追加] 画面のスクリーンショット](./media/mdm-authority-set/add-mdm-authority.png)

### <a name="migrate-users-and-devices-optional"></a>ユーザーとデバイスの移行 (オプション)

Intune MDM 機関が有効になると、共存がアクティブ化され、Intune を使用してユーザーの管理を開始できるようになります。 オプションとして、これまで Basic Mobility and Security で管理されていたデバイスを Intune による管理に移行したい場合は、該当するユーザーに Intune 対応のライセンスを割り当てます。 ユーザーのデバイスは、次回の MDM チェックイン時に Intune に切り替わります。 Basic Mobility and Security を通してこれらのデバイスに適用されていた設定は、もはや適用されなくなり、デバイスから削除されます。

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>MDM 証明書の有効期限が切れた後のモバイル デバイスのクリーンアップ

MDM 証明書は、モバイル デバイスが Intune サービスと通信しているときに自動的に更新されます。 モバイル デバイスがワイプされたり、一定の時間 Intune サービスとモバイル デバイスが通信できなかったりすると、MDM 証明書は更新されません。 デバイスは、MDM 証明書の有効期限が切れてから 180 日後に、Azure Portal から削除されます。

## <a name="remove-mdm-authority"></a>MDM 機関を削除する

MDM 機関を [不明] に戻すことはできません。 MDM 機関は、登録されたデバイスからどのポータルにレポートするか (Microsoft Intune または Basic Mobility and Security for Office 365) を特定するサービスによって利用されます。

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>MDM 機関を変更した後の注意点

- テナントの MDM 機関が変更されたことを Intune サービスが検出すると、登録されているすべてのデバイスに、サービスにチェックインして同期することを促す通知メッセージが送信されます (この通知は定期的にスケジュールされているチェックインとは別になります)。 そのため、テナントの MDM 機関が Intune スタンドアロンから変更された後は、電源が入っていてオンラインのすべてのデバイスがサービスに接続し、新しい MDM 機関を受信して、新しい MDM 機関によって管理されるようになります。 これらのデバイスの管理と保護は中断されません。
- MDM 機関の変更中 (または変更直後) にデバイスの電源が入り、オンラインだった場合でも、デバイスが新しい MDM 機関のサービスに登録されるまでに最大 8 時間の遅れがあります (次の定期的なチェックインのタイミングによって異なります)。  

 > [!IMPORTANT]  
 > MDM 機関を変更してから、更新された APNs 証明書が新しい機関にアップロードされるまで、iOS/iPadOS デバイスの新しいデバイスの登録とデバイスのチェックインは失敗します。 そのため、MDM 機関を変更した後は、できるだけ早く APNs 証明書を確認し、新しい機関にアップロードすることが重要です。

- ユーザーが新しい MDM 機関にすぐに変更するには、デバイスからサービスへのチェックインを手動で開始します。 ポータル サイト アプリを使用して、デバイス コンプライアンス チェックを開始することで、ユーザーはこの変更を簡単に実行できます。
- MDM 機関の変更後、デバイスがチェックインしてサービスと同期した後に、動作が正常であることを確認するには、新しい MDM 機関でそのデバイスを探します。
- MDM 機関の変更中にデバイスがオフラインだったときから、デバイスがサービスにチェックインするまでは中間期間があります。 この中間期間にも確実にデバイスが保護され利用できるように、次のプロファイルが最大 7 日間 (またはデバイスが新しい MDM 機関に接続し、新しい設定を受信して既存の設定が上書きされるまで)、デバイスに残ります。
   - 電子メール プロファイル
   - VPN プロファイル
   - 証明書プロファイル
   - Wi-Fi プロファイル
   - 構成プロファイル
- 新しい MDM 機関に変更した後は、Microsoft Intune 管理コンソールのコンプライアンス データが正確に報告されるまでに最大 1 週間かかる可能性があります。 ただし、Azure Active Directory とデバイスのコンプライアンス状態は正確なので、デバイスは引き続き保護されます。
- 既存の設定を上書きするための新しい設定は、古い設定が確実に上書きされるように、古い設定と同じ名前にする必要があります。 そうしないと、デバイスのプロファイルとポリシーが重複する可能性があります。  

 > [!TIP]  
 > ベスト プラクティスとして、MDM 機関の変更が完了した直後に、すべての管理設定、構成、展開を作成することをお勧めします。 こうすることで、中間期間にもデバイスを保護し、アクティブに管理することができます。

- MDM 機関を変更した後に、次の手順を実行して、新しいデバイスが新しい機関に正常に登録されたことを確認します。  
 - 新しいデバイスを登録する
 - 新しく登録されたデバイスが、新しい MDM 機関に表示されることを確認します。
 - 管理コンソールからデバイスに対して、リモート ロックなどのアクションを実行します。 成功した場合、そのデバイスは新しい MDM 機関で管理されていることを示します。
- 特定のデバイスで問題がある場合、できるだけ早くデバイスを新しい機関に接続し、管理対象にするには、そのデバイスの登録を解除してから再登録します。

## <a name="next-steps"></a>次のステップ

MDM 機関が設定されると、[デバイスの登録](../enrollment/device-enrollment.md)を開始することができます。
