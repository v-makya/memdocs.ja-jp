---
title: クライアントでトランスポート層セキュリティ (TLS) 1.2 を有効にする方法
titleSuffix: Configuration Manager
description: 構成マネージャー クライアントで TLS 1.2 を有効にする方法に関する情報。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704110"
---
# <a name="how-to-enable-tls-12-on-clients"></a>クライアントで TLS 1.2 を有効にする方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager 環境に対して TLS 1.2 を有効にするときは、サイト サーバーとリモート サイト システムで TLS 1.2 を有効にして古いプロトコルを無効にする前に、まず、クライアントが TLS 1.2 を使用でき、適切に構成されていることを確認します。 クライアントで TLS 1.2 を有効にするには、次の 3 つのタスクを実行します。

- Windows と WinHTTP を更新する
- オペレーティング システム レベルで SChannel のプロトコルとして TLS 1.2 を確実に有効にする
- TLS 1.2 をサポートするように .NET Framework を更新して構成する

Configuration Manager の特定の機能とシナリオに対する依存関係について詳しくは、[TLS 1.2 の有効化](enable-tls-1-2.md)に関する記事をご覧ください。

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a> Windows と WinHTTP を更新する

Windows 8.1、Windows Server 2012 R2、Windows 10、Windows Server 2016、および以降のバージョンの Windows では、WinHTTP 経由のクライアントとサーバー間の通信で TLS 1.2 がネイティブにサポートされています。 

Windows 7 や Windows Server 2012 など、以前のバージョンの Windows では、WinHTTP を使用するセキュリティで保護された通信に対して TLS 1.1 または TLS 1.2 は既定では有効にされていません。 以前のバージョンの Windows の場合、[更新プログラム 3140245](https://support.microsoft.com/help/3140245) をインストールして、次のレジストリ値を有効にします。これにより、WinHTTP 用の既定のセキュリティで保護されたプロトコルの一覧に、TLS 1.1 と TLS 1.2 を追加するように設定することができます。 修正プログラムをインストールしたら、次のレジストリ値を作成します。

> [!IMPORTANT]
> Configuration Manager サーバーで TLS 1.2 を有効にして、古いプロトコルを無効にする "*前*" に、以前のバージョンの Windows が実行されているすべてのクライアントで、これらの設定を有効にします。 そうでない場合、それらが誤って孤立する可能性があります。

`DefaultSecureProtocols` レジストリ設定の値を確認します。例:

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

この値を変更した場合は、コンピューターを再起動してください。

上記の例では、WinHTTP の `DefaultSecureProtocols` 設定に対して値 `0xAA0` が表示されています。 [KB 3140245:Windows の WinHTTP 用の既定のセキュリティで保護されたプロトコルとして TLS 1.1 および TLS 1.2 を有効にするための更新プログラム](https://support.microsoft.com/help/3140245)に関するページに、各プロトコルの 16 進数の値が一覧表示されています。 Windows の既定では、この値は `0x0A0` であり、WinHTTP 用に SSL 3.0 と TLS 1.0 が有効になっています。 上記の例では、これらの既定値を保持しつつ、WinHTTP 用に TLS 1.1 と TLS 1.2 も有効にしています。 この構成により、変更を加えても、まだ SSL 3.0 または TLS 1.0 に依存しているかもしれない他のアプリケーションが切断されることはありません。 TLS 1.1 および TLS 1.2 のみを有効にする場合は、値 `0xA00` を使用できます。 Configuration Manager では、Windows が両方のデバイス間でネゴシエートするための最も安全なプロトコルがサポートされています。

 SSL 3.0 と TLS 1.0 を完全に無効にする場合は、Windows の SChannel の無効なプロトコル設定を使います。 詳細については、「[Schannel.dll で特定の暗号アルゴリズムおよびプロトコルの使用を制限する方法](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)」をご覧ください。

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> オペレーティング システム レベルで SChannel のプロトコルとして TLS 1.2 を確実に有効にする

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> TLS 1.2 をサポートするように .NET Framework を更新して構成する

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>次のステップ

- [サイト サーバーとリモート サイト システムで TLS 1.2 を有効にする](enable-tls-1-2-server.md)
- [TLS 1.2 を有効にしたときの一般的な問題](enable-tls-1-2-troubleshoot.md)

