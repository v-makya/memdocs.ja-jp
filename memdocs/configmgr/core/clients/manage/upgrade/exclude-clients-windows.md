---
title: Windows をクライアント アップグレードから除外する
titleSuffix: Configuration Manager
description: Windows クライアントを Configuration Manager のアップグレードから除外する方法について説明します。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58a7741bb628a0c8fb346c8f61b446301b138d80
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696850"
---
# <a name="how-to-exclude-clients-from-upgrade-in-configuration-manager"></a>クライアントを Configuration Manager のアップグレードから除外する方法

*適用対象:Configuration Manager (Current Branch)*

クライアントのコレクションを、更新されたクライアントのバージョンの自動インストールから除外できます。 この除外は、クライアントをアップグレードする際により注意が必要なコンピューターのコレクションに使用します。 除外されるコレクション内にあるクライアントでは、更新されたクライアント ソフトウェアのインストールの要求が無視されます。

この除外は、以下の手法に適用されます。

- 自動アップグレード
- ソフトウェアの更新に基づいたアップグレード
- ログオン スクリプト
- グループ ポリシー

> [!NOTE]
> ユーザー インターフェイスにどの方法でもクライアントがアップグレードされないことが示されますが、これらの設定をオーバーライドするために使用できる 2 つの方法があります。 クライアント プッシュまたは手動クライアント インストールを使用して、この構成をオーバーライドします。 詳しくは、「[除外したクライアントをアップグレードする方法](#bkmk_override)」をご覧ください。

## <a name="configure-exclusion"></a><a name="bkmk_exclude"></a> 除外の構成

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動します。 **[サイトの構成]** を展開し、 **[サイト]** ノードを選択してから、リボンの **[階層設定]** を選択します。

2. **[クライアント アップグレード]** タブに切り替えます。

3. **[指定したクライアントをアップグレードから除外する]** オプションを選択します。 次に、除外する **[除外コレクション]** を選択します。 除外するコレクションを 1 つだけ選択できます。

4. **[OK]** を選択して閉じ、構成を保存します。

![自動アップグレード除外の設定](media/automatic_upgrade_exclusion.png)

除外されるコレクション内のクライアントによってポリシーが更新された後、クライアントの更新プログラムは自動的にインストールされません。 詳細については、「[Windows コンピューター用クライアントをアップグレードする方法](upgrade-clients-for-windows-computers.md)」を参照してください。

> [!NOTE]
> 除外されたクライアントでも Ccmsetup はダウンロードされて実行されますが、アップグレードされません。

除外コレクションからクライアントを削除すると、次の自動アップグレード サイクルまで自動的にアップグレードされません。

## <a name="how-to-upgrade-an-excluded-client"></a><a name="bkmk_override"></a> 除外したクライアントをアップグレードする方法

デバイスが、アップグレードから除外したコレクションのメンバーである場合でも、次のいずれかの方法を使用してクライアントをアップグレードできます。

- **クライアント プッシュ インストール**:Ccmsetup では、クライアント プッシュ インストールが許可されます。これが直接的な意図であるためです。 このメソッドを使用すると、クライアントをコレクションから削除せずにアップグレードしたり、コレクション全体を除外から除去したりできます。

- **手動クライアント インストール**:次の Ccmsetup コマンドライン パラメーターを使用して、除外されたクライアントを手動でアップグレードします: **/IgnoreSkipUpgrade**

    除外されるコレクションのメンバーであるクライアントを手動でアップグレードしようとする場合にこのパラメーターを使用しないと、クライアントはアップグレードされません。 詳細については、[構成マネージャー クライアントの手動インストール方法](../../deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)に関するセクションをご覧ください。

## <a name="see-also"></a>関連項目

- [クライアントをアップグレードする](upgrade-clients.md)

- [Windows コンピューターにクライアントを展開する方法](../../deploy/deploy-clients-to-windows-computers.md)

- [拡張相互運用性クライアント](../../../understand/interoperability-client.md)
