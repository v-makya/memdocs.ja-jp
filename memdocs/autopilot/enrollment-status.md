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
ms.openlocfilehash: 129023d73f7a0ed458c351e8b2bcfd482a201c23
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757218"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Windows 自動操縦の登録ステータスページ

**適用対象**

-   Windows 10 バージョン 1803 以降 

[登録ステータス] ページ (ESP) には、MDM で管理されているユーザーが初めてデバイスにサインインしたときの、完全なデバイス構成プロセスの状態が表示されます。  ESP は、ユーザーが初めてデスクトップにアクセスできるようになる前に、デバイスのプロビジョニングの進行状況を把握し、デバイスが組織の目的の状態を満たしていることを確認するのに役立ちます。

ESP は、アプリケーション、セキュリティポリシー、証明書、およびネットワーク接続のインストールを追跡します。  Intune を使用すると、管理者は、ライセンスを付与された Intune ユーザーに ESP プロファイルを展開し、ESP プロファイル内で特定の設定を構成できます。これらの設定のいくつかを次に示します。指定したアプリケーションを強制的にインストールし、ユーザーがトラブルシューティングログを収集できるようにし、デバイスのセットアップが失敗したときにユーザーが実行できる操作を指定します。  詳細については、「 [Intune で登録ステータスページ](https://docs.microsoft.com/intune/windows-enrollment-status)を設定する方法」を参照してください。   
 
 ![登録状態ページ](images/enrollment-status-page.png)
 

## <a name="more-information"></a>詳細情報

登録ステータスページの構成の詳細については、 [Microsoft Intune のドキュメント](https://docs.microsoft.com/intune/windows-enrollment-status)を参照してください。<br>
基になる実装の詳細については、 [DMClient CSP のドキュメントの Firstsyncstatus の詳細](https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp)を参照してください。<br>
アプリのインストールのブロックの詳細については、次を参照してください。
- [登録ステータスページを使用してアプリのインストールをブロックして](https://blogs.technet.microsoft.com/mniehaus/2018/12/06/blocking-for-app-installation-using-enrollment-status-page/)います。
- [サポートヒント: OFFICE C2R のインストールは、ESP 中に追跡されるようになりました](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514)。
