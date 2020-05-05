---
title: ユーザーによるデバイスの登録方法
titleSuffix: Configuration Manager
description: Configuration Manager で、ユーザーがオンプレミスモバイルデバイス管理 (MDM) にデバイスを登録する方法について説明します。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724886"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Configuration Manager でユーザーがオンプレミス MDM にデバイスを登録する方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager オンプレミスモバイルデバイス管理 (MDM) を使用すると、ユーザーは自分のデバイスを登録できます。 前提条件が 2 つあります。

- クライアント設定を使用して、登録するアクセス許可をユーザーに付与します。

- 必要な信頼されたルート証明書をデバイスにインストールします。

登録をセットアップする方法の詳細については、「[オンプレミス MDM のデバイス登録の設定](../get-started/set-up-device-enrollment-on-premises-mdm.md)」を参照してください。

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>Windows 10 の登録

1. Windows 10 コンピューターで、 **[設定]** に移動します。

1. [**アカウント**] を選択し、[**職場または学校にアクセス**する] を選択します。

1. [**接続**] を選択し、ユーザープリンシパル名 (UPN) を入力して、[**続行**] を選択します。 UPN は、電子メールアドレスと同じにすることができますjdoe@contoso.com。たとえば、のようになります。

1. 登録プロキシポイントの完全修飾ドメイン名 (FQDN) を入力し、[**続行**] を選択します。

1. パスワードを入力し、[**サインイン**] を選択します。

1. Windows では、この操作のサインイン情報を記憶する必要がないため、[**スキップ**] を選択します。

しばらくすると、デバイスは Configuration Manager に登録されます。

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>Windows 10 Mobile の登録

1. Windows 10 Mobile デバイスで、 **[設定]** に移動します。

1. [**アカウント**] を選択し、[**職場のアクセス**] を選択します。

1. **[接続]** を選択します。

1. UPN と登録プロキシポイントの FQDN を入力します。 [**接続**] を選択します。

1. 次の画面で、UPN とパスワードを入力し、[**サインイン**] を選択します。

しばらくすると、デバイスは Configuration Manager に登録されます。 **[Done]** を選択します。

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>登録の確認

Configuration Manager コンソールを使用して、デバイスが正常に登録されていることを確認します。 Configuration Manager コンソールで、**[資産とコンプライアンス]** ワークスペースに移動し、**[デバイス]** を選択します。 デバイスの一覧で、登録されているデバイスを参照または検索します。
