---
title: Windows 自動操縦ポリシーの競合
ms.reviewer: ''
manager: laurawi
description: Windows の自動操縦展開中に発生する可能性のある既知の問題について通知します。
keywords: MDM, セットアップ, Windows, Windows 10, OOBE, 管理, 展開, Autopilot, ZTD, ゼロタッチ, パートナー, MSFB, Intune
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
ms.openlocfilehash: 432656fc46d9b2a6e9cad6c8c9b7e287afc34b7b
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757162"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows 自動操縦-ポリシーの競合

**適用対象**

- Windows 10

Windows 10 で使用できるポリシー設定の数には、ネイティブ MDM ポリシーとグループポリシー (ADMX による) 設定の両方があります。 Windows 10 の動作を変更した結果として、一部の Windows 自動操縦のシナリオで問題が発生することがあります。 これらの問題が発生した場合は、問題を解決するために該当するポリシーを削除します。

<table>
<th>ポリシー<th>詳細情報

<tr><td width="50%">デバイスの制限/<a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">パスワードポリシー</a></td>
<td>パスワードの最小長とパスワードの複雑さ、同様のグループポリシー設定 (自動ログオンを無効にするものを含む) などの特定の<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">Devicelock ポリシー</a>がデバイスに適用され、デバイスの登録ステータスページ (ESP) 中にデバイスが再起動した場合、インボックスエクスペリエンス (OOBE) またはユーザーデスクトップ自動ログオンが失敗する可能性があります。  これは、パスワードが自動的に生成されるキオスクのシナリオに特に当てはまります。</td>

<tr><td width="50%">Windows 10 のセキュリティベースライン/<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理者の昇格時のプロンプト動作</a>
<br>Windows 10 のセキュリティベースライン/<a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">管理者の承認モードが必要</a></td>
<td>デバイス登録ステータスページ (ESP) を使用して OOBE 中にユーザーアカウント制御 (UAC) の設定を変更すると、追加の UAC プロンプトが表示されることがあります。これらのポリシーを適用した後にデバイスを再起動して、有効にすることができます。  この問題を回避するには、デバイスではなくユーザーにポリシーを適用して、後でプロセスで適用できるようにすることができます。</td>

<tr><td width="50%">デバイスの制限/クラウドとストレージ/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Microsoft アカウントサインインアシスタント</a></td>
<td>このポリシーを [無効] に設定すると、Microsoft サインインアシスタントサービス (wlidsvc) が無効になります。  このサービスは、windows 自動操縦によって Windows 自動操縦プロファイルを取得するために必要です。</td>

</table>

## <a name="related-topics"></a>関連トピック

[Windows 自動操縦のトラブルシューティング](troubleshooting.md)
