---
title: Microsoft Intune でデバイスをロックする - Azure | Microsoft Docs
description: PIN またはパスワードで保護されているデバイスをロックするには、Microsoft Intune のリモート ロック アクションを使用します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 3b67f285-229d-4a0f-ae34-0402a20b4518
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6cafadbecbb0e0f0287b8a6ac4db5a1168e5e84
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83983096"
---
# <a name="remotely-lock-devices-with-intune"></a>デバイスを Intune でリモートからロックする

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

**リモート ロック** デバイス アクションは、デバイスをロックします。 デバイスのロックを解除するには、そのデバイスの所有者がパスコードを入力する必要があります。 PIN またはパスワードが設定されているデバイスをリモートでロックすることができます。 PIN またはパスワードがないデバイスは、リモートでロックできません。

## <a name="supported-platforms"></a>サポートされているプラットフォーム

**リモート ロック**は、次のプラットフォームでサポートされます。

- Android
- Android エンタープライズ キオスク デバイス
- Android エンタープライズ仕事用プロファイル デバイス
- iOS
- macOS
- Windows 10 Mobile
- Windows Phone 8.1 以降

**リモート ロック**は、以下ではサポートされません。
- Windows 10 Desktop

> [!NOTE]
> macOS デバイスの場合は、6 桁の回復用 PIN を設定します。 デバイスがロックされているときは、別のデバイス アクションが送信されるまで、 **[デバイス概要]** にその PIN が表示されます。 PIN はリモート ロック コマンドが送信されてから 7 日間しか利用できないため、必ず書き留めておいてください。 7 日後、Intune に その PIN は存在しなくなります。 また、元の PIN を使用してデバイスのロックを正常に解除するまで、同じデバイスに対してこのコマンドを再度起動しないでください。 このコマンドを送信して、PIN を書き留める必要があり、それを使用して macOS デバイスに正常にアクセスするまではこのコマンドを同じデバイスに再度送信しないでください。  


## <a name="remote-lock-a-device"></a>デバイスのリモート ロック

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。
3. **[デバイス]**  >  **[すべてのデバイス]** の順に選択します。
4. デバイスの一覧でデバイスを選択し、 **[リモート ロック]** アクションを選択します。

## <a name="next-steps"></a>次のステップ

- このアクションのステータスを表示するには、 **[Microsoft Intune]**  >  **[デバイス]**  >  **[デバイス アクション]** の順に選択します。 
- デバイスの管理に役立つその他のアクションについては、[使用できるアクション](device-management.md)に関するページを参照してください。
