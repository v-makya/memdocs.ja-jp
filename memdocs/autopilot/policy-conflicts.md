---
title: Windows 自動操縦ポリシーの競合
ms.reviewer: ''
manager: laurawi
description: Windows の自動操縦展開中に発生する可能性があるポリシーの競合について通知します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: mtniehaus
ms.author: mniehaus
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 1f839f128dc869f7c9a4619237de0c33a21d66e1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606580"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows 自動操縦-ポリシーの競合

**適用対象**

- Windows 10

Windows 10 では、次のような多数のポリシー設定を使用できます。
- ネイティブ MDM ポリシー
- グループポリシー (ADMX による) の設定

一部のポリシー設定では、一部の Windows 自動操縦シナリオで問題が発生する可能性があります。 これらの問題は、ポリシーによって Windows 10 の動作がどのように変化するかによって発生する可能性があります。 これらの問題が見つかった場合は、該当するポリシーを削除して問題を解決します。

<table>
<th>ポリシー<th>詳細情報

<tr><td width="50%">デバイスの制限/ <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">パスワードポリシー</a></td>
<td>デバイス登録ステータスページ (ESP) 中にデバイスが再起動すると、既定のエクスペリエンス (OOBE) またはユーザーデスクトップの自動ログオンが失敗することがあります。 このエラーは、デバイスに特定の <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">Devicelock ポリシー</a> が適用されている場合に発生する可能性があります。 このようなポリシーには次のものがあります。<ul><li>パスワードの最小文字数とパスワードの複雑さ</li><li>同様のグループポリシー設定 (自動ログオンを無効にするものも含む)</li></ul>
このようなエラーは、パスワードが自動的に生成されるキオスクシナリオで特に当てはまります。</td>

<tr><td width="50%">Windows 10 のセキュリティベースライン/ <a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理者の昇格時のプロンプト動作</a>
<br>Windows 10 のセキュリティベースライン/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理者の承認モードが必要</a></td>
<td>デバイス登録ステータスページ (ESP) を使用して、OOBE 中にユーザーアカウント制御 (UAC) の設定を変更すると、より多くのプロンプトが表示される場合があります。 ポリシーが適用された後にデバイスが再起動される場合は、プロンプトが増加する可能性が高くなります。 この問題を回避するには、デバイスではなくユーザーにポリシーを適用して、後でプロセスで適用できるようにすることができます。</td>

<tr><td width="50%">デバイスの制限/クラウドとストレージ/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Microsoft アカウントサインインアシスタント</a></td>
<td>このポリシーを [無効] に設定すると、Microsoft サインインアシスタントサービス (wlidsvc) が無効になります。 このサービスは、windows 自動操縦によって Windows 自動操縦プロファイルを取得するために必要です。</td>

</table>

## <a name="related-topics"></a>関連トピック

[Windows 自動操縦のトラブルシューティング](troubleshooting.md)
