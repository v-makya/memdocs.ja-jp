---
title: ハイブリッド MDM はどうなりましたか?
titleSuffix: Configuration Manager
description: Configuration Manager でのハイブリッドモバイルデバイス管理 (MDM) の廃止について説明します。
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e9e0da6d-bd5a-48d9-930a-e74b34b9286c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d07a014cdcb3f371a90028ec09be3c0c939b8424
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724656"
---
# <a name="what-happened-to-hybrid-mdm"></a>ハイブリッド MDM はどうなりましたか?

*適用対象:Configuration Manager (Current Branch)*

> [!WARNING]
> Microsoft は、2019年9月1日以降、ハイブリッド MDM サービスオファリングを廃止しました。 残りのハイブリッド MDM デバイスは、ポリシー、アプリ、またはセキュリティ更新プログラムを受信しません。

## <a name="remove-hybrid-mdm"></a>ハイブリッド MDM の削除

ご利用の Configuration Manager サイトに Microsoft Intune サブスクリプションがあった場合は、それを削除する必要があります。

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[クラウド サービス]** を展開し、**[Microsoft Intune サブスクリプション]** ノードを選択します。 既存の Intune サブスクリプションを削除します。

1. **Microsoft Intune サブスクリプションの削除ウィザード**で、 **Microsoft Intune サブスクリプションを Configuration Manager から削除**するオプションを選択し、[**次へ**] をクリックします。

1. ウィザードを完了します。

## <a name="deprecation-announcement"></a>廃止に関するお知らせ

次の注意事項は、元の非推奨のアナウンスです。

> [!NOTE]  
> 2018 年 8 月 14 日の時点では、ハイブリッド モバイル デバイス管理は[非推奨の機能](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)です。 2019 年 2 月末に予定されている 1902 Intune サービス リリース以降、新規のお客様は新しいハイブリッド接続を作成できなくなります。
> <!--Intune feature 2683117-->  
> 1 年以上前に Azure で利用できるようになってから、Intune には、お客様からの要望や市場の発展に従って何百もの新しいサービス機能が追加されています。 ハイブリッド モバイル デバイス管理 (MDM) で提供されるものよりはるかに多くの機能が用意されています。 Azure での Intune では、エンタープライズ モビリティのニーズに対していっそう統合された効率的な管理エクスペリエンスが提供されています。
>
> その結果、ほとんどのお客様は、ハイブリッド MDM ではなく Azure での Intune を選択されています。 クラウドに移行するお客様の増加により、ハイブリッド MDM を使用するお客様の数は減り続けています。 そのため、2019 年 9 月 1 日をもって、Microsoft はハイブリッド MDM サービスの提供を終了します。
>
> この変更は、オンプレミスの Configuration Manager または [Windows 10 デバイスの共同管理](../../comanage/overview.md)には影響しません。 ハイブリッド MDM を使用しているかどうかわからない場合は、Configuration Manager コンソールの [**管理**] ワークスペースで [ **Cloud Services**] を展開し、[ **Microsoft Intune サブスクリプション**] を選択します。 Microsoft Intune のサブスクリプションが設定されている場合、そのテナントはハイブリッド MDM 用に構成されています。
>
> **ユーザーへの影響**
>
> - ハイブリッド MDM の使用は来年はサポートされます。 機能の主要なバグの修正プログラムは引き続き受け取ります。 iOS 12 への登録など、新しい OS バージョンでの既存機能はサポートされます。 ハイブリッド MDM には新機能は追加されません。  
>
> - ハイブリッド MDM 提供終了前に Azure での Intune に移行する場合、エンドユーザーに対する影響はありません。  
>
> - 2019 年 9 月 1 日をもって、残っているハイブリッド MDM のデバイスは、ポリシー、アプリ、またはセキュリティの更新プログラムを受け取らなくなります。  
>
> - ライセンスは同じままです。 Azure での Intune のライセンスは、ハイブリッド MDM に含まれています。  
>
> - Configuration Manager のオンプレミス MDM 機能は非推奨とされます。 Configuration Manager バージョン1810以降では、Intune に接続せずにオンプレミスの MDM を使用することができます。 詳細については、「[新しいオンプレミス MDM デプロイでは Intune 接続が](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm)不要になりました。」を参照してください。
>
> - Configuration Manager のオンプレミスの条件付きアクセス機能も、ハイブリッド MDM では非推奨とされます。 Configuration Manager クライアントで管理されているデバイスで条件付きアクセスを使用する場合は、移行する前に保護されていることを確認してください。
>     1. Azure で条件付きアクセスポリシーを設定する
>     2. Intune ポータルでコンプライアンスポリシーを設定する
>     3. ハイブリッド移行を完了し、MDM 機関を Intune に設定する
>     4. 共同管理を有効にする
>     5. コンプライアンスポリシーの共同管理ワークロードを Intune に移動する
>
>     詳細については、「[共同管理での条件付きアクセス](../../comanage/quickstart-conditional-access.md)」を参照してください。
>
> **この変更に対して必要な準備**
>
> - ConfigMgr コンソールから Azure への MDM の移行の計画を開始してください。 Microsoft IT を含む多くのお客様は、このプロセスを既に行っています。 詳しくは、[Microsoft のケース スタディ](https://aka.ms/Intune_MSFT)に関するページをご覧ください。  
>
> - 詳しくは、レコードまたは FastTrack のパートナーにお問い合わせください。 [FastTrack for Microsoft 365](https://aka.ms/hybrid_fasttrack) は、ハイブリッド MDM から Azure での Intune への移行に役立ちます。
>
> 詳細については、 [Intune サポートブログの投稿](https://aka.ms/hybrid_notification)を参照してください。

## <a name="next-steps"></a>次のステップ

MDM デバイスの管理に関してサポートされている機能の詳細については、次の記事を参照してください。

- [Microsoft Intune とは](https://docs.microsoft.com/intune/what-is-intune)
- [オンプレミス MDM とは](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Exchange でのデバイスの管理](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
