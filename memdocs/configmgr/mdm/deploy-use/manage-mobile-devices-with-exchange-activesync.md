---
title: Exchange でのデバイスの管理
titleSuffix: Configuration Manager
description: Configuration Manager で Exchange Server コネクタを使用してモバイルデバイスを管理します。
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724806"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Exchange と Configuration Manager を使用したデバイス管理

*適用対象:Configuration Manager (Current Branch)*

ActiveSync プロトコルを使用して Exchange Server に接続するモバイルデバイスがある場合は、Configuration Manager で Exchange Server コネクタを使用して、これらのデバイスを管理できます。 コネクタは、オンプレミスの Exchange Server または Exchange Online の両方で動作します。 Configuration Manager コンソールを使用して、Exchange モバイルデバイス管理機能を構成します。 たとえば、複数の Exchange サーバーのリモートデバイスワイプと設定の制御です。

![Configuration Manager を使用した Exchange Server コネクタの論理図](media/configmgr-with-exchange.png)  

このコネクタを使用してモバイルデバイスを管理すると、Configuration Manager クライアントがインストールされず、MDM 経由でデバイスが登録されません。 Exchange Server の管理機能は、これらの他のオプションと比較して制限されています。 たとえば、ソフトウェアをインストールしたり、構成項目を使用してこれらのデバイスを構成したりすることはできません。 詳細については、「 [Configuration Manager のデバイス管理ソリューションの選択](../../core/plan-design/choose-a-device-management-solution.md)」を参照してください。  

## <a name="policies"></a>ポリシー

コネクタを使用すると、Configuration Manager によってモバイルデバイスの設定が構成されます。 デバイスは、既定の Exchange ActiveSync メールボックスポリシーを使用しません。 次のグループで使用する設定を定義します。

- **全般**
- **パスワード**
- **電子メール管理**
- **Security**
- **Application**

たとえば、**パスワード**グループでは、次の設定を構成できます。

- モバイルデバイスにパスワードが必要かどうか
- パスワードの最小文字数
- パスワードの複雑さ
- パスワードの回復が許可されているかどうか

グループで 1 つでも設定を行うと、Configuration Manager がグループのすべてのモバイル デバイス用設定を管理します。 グループの設定を構成しなかった場合、Exchange は引き続きモバイルデバイスの設定を管理します。 Exchange サーバーで構成し、ユーザーに割り当てる Exchange ActiveSync メールボックスポリシーは、引き続き適用されます。

## <a name="access-rules-and-remote-actions"></a>アクセス規則とリモート操作

Exchange Server コネクタを構成して、Exchange のアクセスルールを管理することもできます。 これらのアクセス規則には、モバイルデバイスの許可、ブロック、検疫が含まれます。 Configuration Manager コンソールを使用してモバイルデバイスをリモートでワイプできます。また、ユーザーは、アプリケーションカタログを使用してモバイルデバイスをリモートでワイプできます。

ユーザーのモバイルデバイスは、管理時にアプリケーションカタログに自動的に表示され、Exchange Server はオンプレミスにあります。 Exchange Online を使用するときにモバイルデバイスがアプリケーションカタログに表示されるようにするには、ユーザーとデバイスのアフィニティを手動で構成します。 詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。

> [!TIP]  
> モバイルデバイスを別のユーザーに転送する場合は、新しい所有者がデバイスで Exchange アカウントを構成する前に、Configuration Manager コンソールからモバイルデバイスを削除します。

## <a name="prerequisites"></a>前提条件

> [!IMPORTANT]  
> このコネクタをインストールする前に、使用しているバージョンの Exchange が Configuration Manager でサポートされていることを確認してください。 詳細については、「[サポートされている構成-Exchange Server コネクタ](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS)」を参照してください。  

### <a name="permissions-to-configure-the-connector"></a>コネクタを構成するためのアクセス許可

Configuration Manager で Exchange Server コネクタを構成するには、次のセキュリティのアクセス許可が必要です。

- Exchange Server コネクタを追加、変更、削除する: **サイト** オブジェクトの **変更** のアクセス許可。  

- モバイル デバイス設定を構成する: **サイト** オブジェクトの **ModifyConnectorPolicy** のアクセス許可。  

たとえば、**完全管理者**の組み込みロールには、これらの必要なアクセス許可が含まれます。  

### <a name="permissions-to-manage-mobile-devices"></a>モバイルデバイスを管理するためのアクセス許可

モバイルデバイスを管理するには、次のセキュリティのアクセス許可が必要です。  

- モバイル デバイスをワイプする: **コレクション** オブジェクトの **リソースの削除** 。  

- ワイプ コマンドを取り消す: **コレクション** オブジェクトの **リソースの変更** 。  

- モバイル デバイスを許可またはブロックする: **コレクション** オブジェクトの **リソースの変更**  

たとえば、 **Operations Administrator**の組み込みロールには、これらの必要なアクセス許可が含まれています。

詳細については、「[役割に基づいた管理の構成](../../core/servers/deploy/configure/configure-role-based-administration.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

> [!div class="nextstepaction"]
> [Exchange connector をインストールして構成する](install-configure-exchange-connector.md)
