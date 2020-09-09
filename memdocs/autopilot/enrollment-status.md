---
title: Windows 自動操縦の登録ステータスページ
ms.reviewer: ''
manager: laurawi
description: 登録ステータスページの機能、構成の概要を示します。
keywords: 自動操縦プラグアンド忘れ、Windows 10
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: a7d368aef0b10fbe78e2c4ca141a39aa4ed6d803
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606603"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Windows 自動操縦の登録ステータスページ

**適用対象**

-  Windows 10 バージョン 1803 以降 

ユーザーが初めてデバイスにサインインすると、登録ステータスページ (ESP) にデバイスの構成の進行状況が表示されます。 また、ESP は、ユーザーが初めてデスクトップにアクセスできるようになる前に、デバイスが予期された状態であることを確認します。

ESP は、アプリケーション、セキュリティポリシー、証明書、およびネットワーク接続のインストールを追跡します。 管理者は、ライセンスを付与された Intune ユーザーに ESP プロファイルを展開し、ESP プロファイル内で特定の設定を構成できます。 これらの設定のいくつかを次に示します。
- 指定されたアプリケーションを強制的にインストールします。
- ユーザーがトラブルシューティングログを収集できるようにします。
- デバイスの設定が失敗した場合にユーザーが行えることを指定する。

詳細については、「 [Intune で登録ステータスページ](/intune/windows-enrollment-status)を設定する方法」を参照してください。  
 
![登録状態ページ](images/enrollment-status-page.png)
 

## <a name="more-information"></a>詳細情報

登録ステータスページの構成の詳細については、 [Microsoft Intune のドキュメント](/intune/windows-enrollment-status)を参照してください。<br>
基になる実装の詳細については、 [DMClient CSP のドキュメントの Firstsyncstatus の詳細](/windows/client-management/mdm/dmclient-csp)を参照してください。<br>
アプリのインストールのブロックの詳細については、次を参照してください。
- [登録ステータスページを使用してアプリのインストールをブロックして](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page)います。
- [サポートヒント: OFFICE C2R のインストールは、ESP 中に追跡されるようになりました](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514)。
