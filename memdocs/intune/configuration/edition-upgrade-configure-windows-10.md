---
title: Windows 10 デバイス上でのアップグレードまたは S モードの使用 - Microsoft Intune - Azure | Microsoft Docs
description: Microsoft Intune を使用して、Windows 10 デバイスを別のエディションにアップグレードしたり、S モードを切り替えたりします。 管理者はデバイス構成プロファイルを使用して、Windows 10 Professional を Windows 10 Enterprise にアップグレードしたり、S モード モードから切り替えたりできます。 Windows 10 Pro、N Edition、Education、Cloud、Enterprise、Core、Holographic、Mobile については、サポートされるアップグレード パスを参照してください。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ae8b6528-7979-47d8-abe0-58cea1905270
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e18395aae96adec3bf4bbf60bdcccdd205dc90d
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146339"
---
# <a name="upgrade-windows-10-editions-or-switch-out-of-s-mode-on-devices-using-microsoft-intune"></a>Microsoft Intune を使用してデバイス上の Windows 10 エディションをアップグレードするか S モードから切り替える

モバイル デバイス管理 (MDM) ソリューションの一部として、Windows 10 デバイスをアップグレードすることができます。 たとえば、Windows 10 Professional デバイスを Windows 10 Enterprise にアップグレードすることができます。 または、デバイスを S モードから切り替えることができます。

[Windows 10 S モード](https://support.microsoft.com/help/4456067/windows-10-switch-out-of-s-mode) (別の Microsoft web サイトが開きます) は、セキュリティとパフォーマンスを目的として設計されています。 Intune を使用して、S モードから切り替えることができます。 S モードから抜けるという行為は一方向です。 Windows 10 S モードから一度抜けると、戻ることができません。

S モードに関して[よく寄せられる質問](https://support.microsoft.com/help/4020089/windows-10-in-s-mode-faq)を参照してください。

この機能は、以下に適用されます。

- Windows 10 以降
- S モードの場合は Windows 10 1809 以降
- Windows Holographic for Business

これらの機能は Intune で使用できます。また、管理者が構成できます。 Intune では、"構成プロファイル" を使用して、お客様の組織のニーズに合わせてこのような設定を作成およびカスタマイズします。 これらの機能をプロファイルに追加した後は、そのプロファイルをお客様の組織内の Windows 10 デバイスにプッシュまたは展開できます。 プロファイルを展開すると、Intune によってデバイスが自動的にアップグレードされるか、S モードから切り替えられます。

この記事では、サポートされているアップグレード パスの一覧を示し、デバイス構成プロファイルの作成方法を説明します。 また、[Windows 10](edition-upgrade-windows-settings.md) で使用できるすべてのアップグレードと S モード設定についても紹介します。

> [!NOTE]
> 後でポリシーの割り当てを削除しても、デバイス上の Windows のバージョンは元に戻りません。 デバイスは引き続き正常に動作します。

## <a name="prerequisites"></a>[前提条件]

デバイスをアップグレードする前に、次の前提条件が満たされていることを確認します。

- ポリシーで対象とするすべてのデバイスにアップデートされたバージョンの Windows をインストールするための有効なプロダクト キー (Windows 10 Desktop エディションの場合)。 マルチ ライセンス認証キー (MAK) またはキー マネジメント サーバー (KMS) キーのどちらかを使用できます。
- Windows 10 Holographic エディションの場合は、Microsoft ライセンス ファイルを使用できます。 このライセンス ファイルには、ポリシーで対象としているすべてのデバイス上に更新されたエディションをインストールするためのライセンス情報が含まれています。
- ポリシーを割り当てる Windows 10 デバイスが Microsoft Intune に登録されます。 エディションのアップグレード ポリシーは、Intune PC クライアント ソフトウェアを実行する PC で使用できません。

## <a name="supported-upgrade-paths"></a>サポートされるアップグレード パス

Windows 10 エディションのアップグレード プロファイルでサポートされるアップグレード パスを次の表に示します。

| アップグレード前のバージョン | アップグレード後のバージョン |
|---|---|
| Windows 10 Pro | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro Education |
| Windows 10 Pro N エディション | Windows 10 Education N エディション <br/>Windows 10 Enterprise N エディション <br/>Windows 10 Pro Education N エディション | 
| Windows 10 Pro Education | Windows 10 Education | 
| Windows 10 Pro Education N エディション | Windows 10 Education N エディション |
| Windows 10 Cloud | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro <br/>Windows 10 Pro Education | 
| Windows 10 Cloud N エディション | Windows 10 Education N エディション <br/>Windows 10 Enterprise N エディション <br/>Windows 10 Pro N エディション <br/>Windows 10 Pro Education N エディション | 
| Windows 10 Enterprise | Windows 10 Education | 
| Windows 10 Enterprise N エディション | Windows 10 Education N エディション | 
| Windows 10 Core | Windows 10 Education <br/>Windows 10 Enterprise <br/>Windows 10 Pro Education | 
| Windows 10 Core N エディション | Windows 10 Education N エディション <br/>Windows 10 Enterprise N エディション <br/>Windows 10 Pro Education N エディション | 
| Windows 10 Holographic | Windows 10 Holographic for Business |

<!--The following table provides information about the supported upgrade paths for Windows 10 editions in this policy:

![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)  (X) = not supported    
![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)    (green checkmark) = supported    

|Upgrade from edition\Upgrade to edition|Education|Education N|Pro Education|Pro Education N|Enterprise|Enterprise N|Professional|Professional N|Mobile Enterprise|Holographic for Business|
|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|--------|
|Pro|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro Education|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Pro Education N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Cloud|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Cloud N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Enterprise|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Enterprise N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Core|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Core N|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Mobile|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|
|Holographic|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![unsupported](./media/edition-upgrade-configure-windows-10/x_blk.png)|![supported](./media/edition-upgrade-configure-windows-10/check_grn.png) -->

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。
3. 次のプロパティを入力します。

    - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
    - **[プロファイル]** : **[エディションのアップグレード]** を選択します。

4. **[作成]** を選択します。
5. **[Basics]\(基本\)** で次のプロパティを入力します。

    - **名前**:新しいプロファイルのわかりやすい名前を入力します。 たとえば、`Windows 10 edition upgrade profile` や `Windows 10 switch off S mode` などを入力します。
    - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。
7. **[構成設定]** で、構成する設定を入力します。 すべての設定の一覧とその実行内容については、以下を参照してください。

    - [Windows 10 のアップグレードと S モード](edition-upgrade-windows-settings.md)
    - [Windows Holographic for Business](holographic-upgrade.md)

8. **[次へ]** を選択します。

9. **スコープ タグ** (オプション) で、`US-NC IT Team` や `JohnGlenn_ITDepartment` など、特定の IT グループにプロファイルをフィルター処理するためのタグを割り当てます。 スコープ タグの詳細については、[分散 IT に RBAC とスコープのタグを使用する](../fundamentals/scope-tags.md)に関するページを参照してください。

    **[次へ]** を選択します。

10. **[割り当て]** で、プロファイルを受け取るユーザーまたはユーザー グループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

    **[次へ]** を選択します。

11. **[確認と作成]** で、設定を確認します。 **[作成]** を選択すると、変更内容が保存され、プロファイルが割り当てられます。 また、ポリシーがプロファイル リストに表示されます。

次に各デバイスがチェックインするときに、ポリシーが適用されます。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当てた](device-profile-assign.md)後は、[その状態を監視](device-profile-monitor.md)します。

[Windows 10](edition-upgrade-windows-settings.md) デバイスと [Windows Holographic for Business](holographic-upgrade.md) デバイスのアップグレードと S モード設定を確認します。
