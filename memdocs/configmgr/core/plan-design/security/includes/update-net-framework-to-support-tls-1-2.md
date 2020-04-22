---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: b21365d0c355adab6819e13537c1b25316583ec2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704090"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>.NET のバージョンの確認

最初に、インストールされている .NET のバージョンを確認します。 詳細については、「[インストールされている Microsoft .NET Framework のバージョンおよび Service Pack のレベルを確認する方法](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso)」をご覧ください。

### <a name="install-net-updates"></a>.NET の更新プログラムのインストール

強力な暗号化を有効にできるように、.NET の更新プログラムをインストールします。 .NET Framework の一部のバージョンでは、強力な暗号化を有効にするために更新プログラムが必要となる場合があります。 次のガイドラインを使用してください。

- NET Framework 4.6.2 以降では TLS 1.1 と TLS 1.2 がサポートされています。 レジストリ設定を確認してください。ただし、追加の変更は必要ありません。

- TLS 1.1 および TLS 1.2 をサポートするには、NET Framework 4.6 以前のバージョンを更新してください。 詳細については、「[.NET Framework のバージョンおよび依存関係](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies)」をご覧ください。

- Windows 8.1 または Windows Server 2012 上で .NET Framework 4.5.1 または 4.5.2 を使用している場合は、[ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=42883)から関連する更新プログラムと詳細を入手することもできます。


### <a name="configure-for-strong-cryptography"></a>強力な暗号化の構成

強力な暗号化をサポートするように .NET Framework を構成します。 `SchUseStrongCrypto` レジストリ設定を `DWORD:00000001` に設定します。 この値により、RC4 ストリーム暗号が無効になります。また、再起動が必要です。 この設定の詳細については、「[Microsoft セキュリティ アドバイザリ 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358)」をご覧ください。

TLS 1.2 が有効なシステムを備えたネットワーク間で通信を行う任意のコンピューター上で、必ず以下のレジストリ キーを設定してください。 たとえば、構成マネージャー クライアント、サイト サーバーにインストールされていないリモート サイト システムの役割、サイト サーバー自体などです。

32 ビット OS 上で実行されている 32 ビット アプリケーション、および 64 ビット OS 上で実行されている 64 ビット アプリケーションの場合は、次のサブキーの値を更新します。

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

64 ビット OS 上で実行されている 32 ビット アプリケーションの場合は、次のサブキーの値を更新します。

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto` 設定により、.NET で TLS 1.1 および TLS 1.2 を使えるようになります。 `SystemDefaultTlsVersions` 設定により、.NET で OS 構成を使えるようになります。 詳細については、[.NET Framework での TLS のベスト プラクティス](https://docs.microsoft.com/dotnet/framework/network-programming/tls)に関するページをご覧ください。
