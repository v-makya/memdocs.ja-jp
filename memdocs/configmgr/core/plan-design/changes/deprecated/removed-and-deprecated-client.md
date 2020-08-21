---
title: クライアントの非推奨機能
titleSuffix: Configuration Manager
description: Configuration Manager でサポートされなくなったクライアント オペレーティング システムについて説明します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 604ab835-bce3-4fe3-a7f3-3f059cfc0ecf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1c5ef0b1065c98cb558c7000677e85cbfb798af6
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129088"
---
# <a name="removed-and-deprecated-items-for-configuration-manager-clients"></a>削除され、非推奨になった Configuration Manager クライアントの項目

*適用対象:Configuration Manager (Current Branch)*

この記事では、Configuration Manager クライアントのサポート対象から削除されたか、今後の更新で削除される予定 (非推奨) の製品およびオペレーティング システムについて説明します。 Configuration Manager の使用に影響する可能性のある将来の変更について早期に注意するものです。  

この情報は将来、変更される可能性があります。 非推奨の機能、製品、オペレーティング システムにはここで取り上げられていないものもある可能性があります。  

## <a name="deprecated-client-operating-systems"></a>非推奨のクライアント オペレーティング システム  

特に明記されていない限り、Configuration Manager クライアントとしてサポートされている各 OS は、その OS バージョンの "*延長サポート終了日*" までサポートされます。 延長サポート終了日の詳細については、「[Microsoft サポート ライフ サイクル](https://support.microsoft.com/lifecycle)」を参照してください。 OS の Configuration Manager のサポートが延長サポート終了日より前に終了する場合、この記事で紹介するのは、そのオペレーティング システムの廃止日とサポート削除日になります。  

<!-- 
The following OS versions are deprecated as a Configuration Manager client. You can still use them now, but Microsoft plans to end support in the future.

|OS version|Deprecation first announced|Support removed|  
|-|-|-|
 -->

## <a name="unsupported-client-operating-systems"></a>サポートされていないクライアント オペレーティング システム

次の OS バージョンはサポートされなくなりました。

|OS バージョン|最初に非推奨と発表|サポートの削除|  
|-|-|-|
|Windows CE 7.0|2019 年 7 月 19 日|バージョン 2006|
|Windows 10 Mobile|2019 年 7 月 19 日|バージョン 2006|
|Windows 10 Mobile Enterprise|2019 年 7 月 19 日|バージョン 2006|
|Windows 7||2020 年 1 月 14 日|
|Windows Server 2008||2020 年 1 月 14 日|
|Windows Server 2008 R2||2020 年 1 月 14 日|
|Linux および UNIX|2018 年 3 月 22 日|バージョン 1902|
|Windows 8: Professional、Enterprise|2016 年 1 月 12 日|バージョン 1802|
|Windows Embedded 8 Pro|2016 年 1 月 12 日|バージョン 1802|
|Windows Embedded 8 Industry|2016 年 1 月 12 日|バージョン 1802|
|Windows XP Embedded <br><br> XP ベースの Embedded オペレーティング システムがすべて含まれます。|2015 年 7 月 10 日|バージョン 1702|
|Windows Vista|2015 年 7 月 10 日|バージョン 1511|
|Windows Server 2003 R2|2015 年 7 月 10 日|バージョン 1511|
|Windows Server 2003|2015 年 7 月 10 日|バージョン 1511|
|Windows XP|2015 年 7 月 10 日|バージョン 1511|  
|macOS X  10.6 - 10.8|2015 年 7 月 10 日|バージョン 1511|  
|Windows Mobile 6.0 - 6.5|2015 年 7 月 10 日|バージョン 1511|  
|Nokia Symbian Belle|2015 年 7 月 10 日|バージョン 1511|  
|Windows CE 5.0 - 6.0|2015 年 7 月 10 日|バージョン 1511|  

## <a name="see-also"></a>関連項目

詳細については、以下の記事を参照してください。

- [クライアントとデバイスに対してサポートされる OS のバージョン](../../configs/supported-operating-systems-for-clients-and-devices.md)

- [マイクロソフト サポート ライフサイクル](https://support.microsoft.com/lifecycle)

- [Configuration Manager の Current Branch バージョンのサポート](../../../servers/manage/current-branch-versions-supported.md)
