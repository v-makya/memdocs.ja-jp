---
title: Windows 自動操縦の登録ステータスページ
ms.reviewer: ''
manager: laurawi
description: 登録ステータスページの機能、構成の概要を示します。
keywords: 自動操縦プラグアンド忘れ、Windows 10
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
ms.openlocfilehash: dd60c47e0e22aa24cf1d4d4df3324f3b1bfed21c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908256"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Windows 自動操縦の登録ステータスページ

**適用対象**

-   Windows 10 バージョン 1803 以降 

[登録ステータス] ページ (ESP) には、MDM で管理されているユーザーが初めてデバイスにサインインしたときの、完全なデバイス構成プロセスの状態が表示されます。  ESP は、ユーザーが初めてデスクトップにアクセスできるようになる前に、デバイスのプロビジョニングの進行状況を把握し、デバイスが組織の目的の状態を満たしていることを確認するのに役立ちます。

ESP は、アプリケーション、セキュリティポリシー、証明書、およびネットワーク接続のインストールを追跡します。  Intune を使用すると、管理者は、ライセンスを付与された Intune ユーザーに ESP プロファイルを展開し、ESP プロファイル内で特定の設定を構成できます。これらの設定のいくつかを次に示します。指定したアプリケーションを強制的にインストールし、ユーザーがトラブルシューティングログを収集できるようにし、デバイスのセットアップが失敗したときにユーザーが実行できる操作を指定します。  詳細については、「 [Intune で登録ステータスページ](/intune/windows-enrollment-status)を設定する方法」を参照してください。   
 
 ![登録状態ページ](images/enrollment-status-page.png)
 

## <a name="more-information"></a>詳細情報

登録ステータスページの構成の詳細については、 [Microsoft Intune のドキュメント](/intune/windows-enrollment-status)を参照してください。<br>
基になる実装の詳細については、 [DMClient CSP のドキュメントの Firstsyncstatus の詳細](/windows/client-management/mdm/dmclient-csp)を参照してください。<br>
アプリのインストールのブロックの詳細については、次を参照してください。
- [登録ステータスページを使用してアプリのインストールをブロックして](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page)います。
- [サポートヒント: OFFICE C2R のインストールは、ESP 中に追跡されるようになりました](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514)。