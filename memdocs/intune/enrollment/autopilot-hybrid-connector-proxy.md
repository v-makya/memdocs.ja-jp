---
title: Active Directory 用の Intune コネクタのプロキシ設定を構成する
description: 既存のオンプレミス プロキシ サーバーと連携するように Active Directory 用の Intune コネクタを構成する方法について説明します。
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9c7300c03ce0ba703f423aa420e9e47534ef2968
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908685"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>既存のオンプレミス プロキシ サーバーと連携する

この記事では、送信プロキシ サーバーと連携するように Active Directory 用の Intune コネクタを構成する方法について説明します。 ネットワーク環境に既存のプロキシがあるお客様を対象としています。

既定では、Active Directory 用の Intune コネクタにより、Web プロキシの自動検出 (WPAD) を使用して、ネットワーク上のプロキシ サーバーの自動検出が試みられます。 これがネットワーク上で構成されている場合、追加の構成は必要ない可能性があります。  変更が必要な場合は、以下のセクションで、[プロキシ設定を構成するための標準的な .NET Framework 機能](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)を利用して既定の設定をオーバーライド方法について説明します。  そのドキュメントでは、その他のオプションについて説明されています。

コネクタのしくみの詳細については、「[Azure AD アプリケーション プロキシ コネクタを理解する](/azure/active-directory/manage-apps/application-proxy-connectors)」を参照してください。

## <a name="completely-bypass-outbound-proxies"></a>送信プロキシを完全にバイパスする

コネクタがオンプレミス プロキシをバイパスして確実に Azure サービスに直接接続するようにコネクタを構成できます。 保守する構成が 1 つ少なくなるため、ネットワーク ポリシーで許可されている限り、この方法をお勧めします。

コネクタの送信プロキシの使用を無効にするには、\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config ファイルを編集し、次のコード サンプルに示すセクションにプロキシ アドレスとプロキシ ポートを追加します。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Connector Updater サービスも確実にプロキシをバイパスするようにするには、C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config にも同様の変更を加えます。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

既定の .config ファイルに戻す必要がある場合に備えて、必ず元のファイルのコピーを作成してください。

構成ファイルを変更したら、Intune コネクタ サービスを再起動する必要があります。 

1. **services.msc** を開きます。
2. **Intune ODJConnector サービス**を検索して選択します。
3. **[再起動]** を選択します。

![サービスの再起動のスクリーンショット](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>代替プロキシ サーバーを指定する

Active Directory 用の Intune コネクタで別のプロキシ サーバー (認証をバイパスするものなど) を使用する必要がある場合は、同様の方法で指定できます。 これを行うには、\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config ファイルを編集し、次のコード サンプルで示すセクションにプロキシ アドレスとプロキシ ポートを追加します。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

Connector Updater サービスも確実にプロキシをバイパスするようにするには、C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config にも同様の変更を加えます。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

既定の .config ファイルに戻す必要がある場合に備えて、必ず元のファイルのコピーを作成してください。

構成ファイルを変更したら、Intune コネクタ サービスを再起動する必要があります。 

1. **services.msc** を開きます。
2. **Intune ODJConnector サービス**を検索して選択します。
3. **[再起動]** を選択します。

![サービスの再起動のスクリーンショット](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>次のステップ

[デバイスの管理](../remote-actions/device-management.md)