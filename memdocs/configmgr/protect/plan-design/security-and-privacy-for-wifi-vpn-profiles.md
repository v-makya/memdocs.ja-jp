---
title: Wi-Fi および VPN プロファイルのセキュリティとプライバシー
titleSuffix: Configuration Manager
description: Configuration Manager でデバイスの Wi-Fi および VPN プロファイルを管理する場合のセキュリティのベスト プラクティスについて説明します。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705980"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager の Wi-Fi および VPN プロファイルのセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

## <a name="security-recommendations"></a>セキュリティに関する推奨事項

デバイスの Wi-Fi および VPN プロファイルを管理する際は、次のセキュリティのベスト プラクティスに従ってください。

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>使用する Wi-Fi および VPN インフラストラクチャとクライアントのオペレーティング システムでサポートできる最も安全なオプションを選択します。

Wi-Fi および VPN プロファイルは、デバイスで既にサポートしている Wi-Fi および VPN 設定を中央から配付して管理するのに便利です。 Configuration Manager では、Wi-Fi および VPN 機能は追加されません。 デバイスとインフラストラクチャのセキュリティに関する推奨事項を特定し、実装して、それに従ってください。

## <a name="privacy-information"></a>プライバシーに関する情報

Wi-Fi および VPN プロファイルを使用して、Wi-Fi および VPN サーバーに接続するようにクライアント デバイスを構成することができます。 次に、Configuration Manager を使用して、プロファイルが適用された後に、それらのデバイスが準拠しているかどうかを評価します。 コンプライアンス対応情報は、管理ポイントからサイト サーバーに送信され、サイト データベースに保存されます。 情報は、デバイスによって管理ポイントに送信される際は暗号化されますが、サイト データベースに保存されるときは暗号化されません。 データベースに保存された情報は、 **"期限切れの構成管理データの削除"** というメンテナンス タスクで削除されるまで維持されます。 情報が削除される既定の期限は 90 日ですが、変更することができます。 コンプライアンス情報は、Microsoft に送信されません。

既定では、デバイスで Wi-Fi および VPN プロファイルを評価しません。 また、プロファイルを構成してから、プロファイルをユーザーに展開する必要があります。  

Wi-Fi または VPN プロファイルを構成する前に、プライバシー要件について検討してください。  
