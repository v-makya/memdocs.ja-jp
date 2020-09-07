---
title: Intune エンドポイント セキュリティのファイアウォール設定 | Microsoft Docs
description: Microsoft Intune の Windows および macOS 用のエンドポイント セキュリティ ファイアウォール ポリシー設定
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 10d9320932e7835b8c2ecac46e35ea5a57375904
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068135"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Intune でのエンドポイント セキュリティのファイアウォール ポリシー設定

[エンド ポイント セキュリティ ポリシー](../protect/endpoint-security-policy.md)の一部として、Intune のエンドポイント セキュリティ ノードでの "*ファイアウォール*" ポリシーのプロファイルで構成できる設定を表示します。

サポートされているプラットフォームとプロファイル

- **macOS**:
  - プロファイル: **macOS ファイアウォール**

- **Windows 10 以降**:
  - プロファイル: **Microsoft Defender ファイアウォール**

## <a name="macos-firewall-profile"></a>macOS ファイアウォールのプロファイル

### <a name="firewall"></a>ファイアウォール

次の設定は、[macOS ファイアウォールのエンドポイント セキュリティ ポリシー](../protect/endpoint-security-firewall-policy.md)として構成されます。

- **ファイアウォールを有効にする**

  - **[未構成]** ("*既定値*")
  - **はい** - ファイアウォールを有効にします。
  
  *[はい]* に設定すると、つぎの設定を構成できます。  

  - **すべての着信接続をブロックする**

    - **[未構成]** ("*既定値*")
    - **はい** - DHCP、Bonjour、IPSec など、基本的なインターネット サービスに必要な接続を除き、すべての着信接続をブロックします。 この設定では、すべての共有サービスがブロックされます。

  - **ステルス モードを有効にする**

    - **[未構成]** ("*既定値*")
    - **はい** - コンピューターがプローブ要求に応答するのをブロックします。 その場合でも、コンピューターは承認されたアプリの着信要求には応答します。

  - **ファイアウォール アプリ** - ドロップダウンを展開してから **[追加]** を選択して、アプリを指定し、さらにアプリの着信接続のための規則を指定します。
    - **着信接続を許可する**
      - 未構成
      - ブロックする
      - Allow

    - **バンドル ID** - ID によってアプリが識別されます。 例: *com.apple.app*

## <a name="microsoft-defender-firewall-profile"></a>Microsoft Defender ファイアウォール プロファイル

### <a name="microsoft-defender-firewall"></a>Microsoft Defender ファイアウォール

次の設定は、[Windows 10 ファイアウォールのエンドポイント セキュリティ ポリシー](../protect/endpoint-security-firewall-policy.md)として構成されます。

- **ステートフル ファイル転送プロトコル (FTP) を無効にする**  
  CSP:[MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **未構成** ("*既定値*") - ファイアウォールでは FTP を使用して、セカンダリ ネットワーク接続が検査およびフィルター処理されます。これにより、ご利用のファイアウォール規則は無視される可能性があります。
  - **あり**
  
- **セキュリティ アソシエーションが削除されるまでのアイドル状態の秒数**  
  CSP:[MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  ネットワーク トラフィックが表示されなくなった後に、セキュリティ アソシエーションを保持する期間として、3600 秒から 300 秒までの時間を指定します。
  
  値を何も指定しない場合、300 秒のアイドル期間を経て、セキュリティ アソシエーションはシステムによって削除されます。
  
- **事前共有キーのエンコード**  
  CSP:[MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  *UTF-8* を必要としない場合、事前共有キーが最初に UTF-8 を使用してエンコードされます。 その後、デバイス ユーザーは別のエンコード方法を選択できます。

  - **[未構成]** ("*既定値*")
  - **なし**
  - **UTF8**

- **ファイアウォール IPsec の除外による近隣探索の許可**  
  CSP:[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **[未構成]** ("*既定値*")
  - **はい** - ファイアウォール IPsec の除外による近隣探索の許可

- **ファイアウォール IPsec の除外により ICMP を許可する**  
  CSP:[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **[未構成]** ("*既定値*")
  - **はい** - ファイアウォール IPsec の除外により ICMP を許可する

- **ファイアウォール IPsec の除外によるルーター発見の許可**  
  CSP:[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **[未構成]** ("*既定値*")
  - **はい** - ファイアウォール IPsec の除外によるルーター発見の許可

- **ファイアウォール IPsec の除外による DHCP の許可**  
  CSP:[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **[未構成]** ("*既定値*")
  - **はい** - ファイアウォール IPsec の除外による DHCP の許可

- **証明書失効リスト (CRL) の検証**  
  CSP:[MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   証明書失効リスト (CRL) の検証をどのように適用するかを指定します。
  - **未構成** ("*既定値*") - クライアントの既定値は、CRL 検証を無効にするためのものです。
  - **なし**
  - **試行回数**
  - **必要**

- **サポートしていない認証スイートのみを無視するようにキー モジュールに求める**  
  CSP:[MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **[未構成]** ("*既定値*")
  - **はい** - サポートされていない認証スイートがキー モジュールによって無視されます。

- **[パケット キュー]**  
  CSP:[MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  IPsec トンネル ゲートウェイのシナリオで、暗号化された受信とクリア テキストの転送について受信側のソフトウェアのスケーリングを有効にする方法を指定します。 これにより、パケットの順序が確実に保持されます。
  - **未構成** ("*既定値*") - パケット キューはクライアントの既定値に戻され、無効になります。
  - **[無効]**
  - **インバウンドをキューに入れる**
  - **アウトバウンドをキューに入れる**
  - **両方をキューに入れる**

- **ドメイン ネットワークに対して Microsoft Defender ファイアウォールを有効にする**  
  CSP:[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **未構成** (*既定値*) - クライアントは既定値に戻ります。これは、ファイアウォールを有効にするためのものです。
  - **はい** - **ドメイン** のネットワークの種類に対する Microsoft Defender ファイアウォールが有効にされ、適用されます。
  - **いいえ** - ファイアウォールを無効にします。

- **プライベート ネットワークに対して Microsoft Defender ファイアウォールを有効にする**  
  CSP:[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **未構成** ("*既定値*") - クライアントは既定値に戻ります。これは、ファイアウォールを有効にするためのものです。
  - **はい** - **プライベート** のネットワークの種類に対する Microsoft Defender ファイアウォールが有効にされ、適用されます。
  - **いいえ** - ファイアウォールを無効にします。

- **パブリック ネットワークに対して Microsoft Defender ファイアウォールを有効にする**  
  CSP:[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **未構成** ("*既定値*") - クライアントは既定値に戻ります。これは、ファイアウォールを有効にするためのものです。
  - **はい** - **パブリック**のネットワークの種類に対する Microsoft Defender ファイアウォールが有効にされ、適用されます。
  - **いいえ** - ファイアウォールを無効にします。

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Microsoft Defender ファイアウォール規則

"*このプロファイルはプレビュー段階です*"。

次の設定は、[Windows 10 ファイアウォールのエンドポイント セキュリティ ポリシー](../protect/endpoint-security-firewall-policy.md)として構成されます。

#### <a name="windows-firewall-rule"></a>Windows ファイアウォール規則

- **名前**  
  使用する規則にフレンドリ名を指定します。 規則の一覧にはこの名前が表示されるので、識別しやすくなります。

- **説明**  
  規則の説明を入力します。

- **方向**  
  - **未構成** ("*既定値*") - この規則の既定値は送信トラフィックです。
  - **Out** - この規則は送信トラフィックに適用される
  - **In** - この規則は受信トラフィックに適用されます。

- **操作**  
  - **未構成** ("*既定値*") - 規則では既定でトラフィックが許可されます。
  - **ブロック済み** - 構成した "*方向*" のトラフィックがブロックされます。
  - **許可済み** - 構成した "*方向*" のトラフィックが許可されます。

- **[ネットワークの種類]**  
  規則が属するネットワークの種類を指定します。 次の 1 つまたは複数を選択できます。 オプションを選択しない場合、すべてのネットワークの種類に規則が適用されます。
  - **ドメイン**
  - **プライベート**
  - **パブリック**
  - **未構成**

- **パッケージ ファミリ名**  
  [Get-AppxPackage](/previous-versions//hh856044(v=technet.10))

  PowerShell から Get-AppxPackage コマンドを実行して、パッケージ ファミリ名を取得できます。

- **ファイル パス**  
  CSP:[FirewallRules/FirewallRuleName/App/FilePath](/windows/client-management/mdm/firewall-csp#filepath)

  アプリのファイル パスを指定するには、クライアント デバイス上のアプリの場所を入力します。 例: `C:\Windows\System\Notepad.exe` または `%WINDIR%\Notepad.exe`

- **サービス名**  
  [FirewallRules/FirewallRuleName/App/ServiceName](/windows/client-management/mdm/firewall-csp#servicename)

  アプリケーションではなくサービスによってトラフィックの送受信が行われる場合は、Windows サービスの短い名前を使用します。 サービスの短い名前を取得するには、PowerShell から `Get-Service` コマンドを実行します。

- **プロトコル**  
  CSP:[FirewallRules/FirewallRuleName/Protocol](/windows/client-management/mdm/firewall-csp#protocol)

  このポート規則のプロトコルを指定します。
  - *TCP(6)* や *UDP(17)* などのトランスポート層プロトコルでは、ポートまたはポート範囲を指定できます。
  - カスタム プロトコルについては、IP プロトコルを表す *0* から *255* の数値を入力します。
  - 何も指定されていない場合、規則の既定値は **[任意]** となります。

- **[インターフェイスの種類]**  
  規則が属するインターフェイスの種類を指定します。 次の 1 つまたは複数を選択できます。 オプションを選択しない場合、すべてのインターフェイスの種類に規則が適用されます。
  - **[リモート アクセス]**
  - **[ワイヤレス]**
  - **[ローカル エリア ネットワーク]**
  - **未構成**

- **許可されているユーザー**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  この規則に対して承認されたローカル ユーザーのリストを指定します。 このポリシー内の "*サービス名*" が Windows サービスとして設定されている場合、許可されているユーザーの一覧を指定することはできません。 許可されているユーザーが指定されていない場合、既定値は *[すべてのユーザー]* になります。

- **任意のローカル アドレス**  
  **未構成** ("*既定値*") - サポートするアドレスの範囲を構成するには、以下の設定 *[ローカル アドレス範囲]* * を使用します。
  - **はい** - 任意のローカル アドレスをサポートし、アドレス範囲は構成しません。

- **ローカル アドレス範囲**  
  CSP:[FirewallRules/FirewallRuleName/LocalAddressRanges](/windows/client-management/mdm/firewall-csp#localaddressranges)  

  この規則のローカル アドレス範囲を管理します。 次の操作を行います。
  - 1 つまたは複数のアドレスを、規則の対象となるローカル アドレスのコンマ区切りリストとして**追加**します。
  - ローカル アドレス範囲として使用するアドレスの一覧が含まれる .csv ファイルを**インポート**します。
  - .csv ファイルとしてローカル アドレス範囲の現行一覧を**エクスポート**します。

  有効なエントリ (トークン) には、次のオプションが含まれています。
  - **アスタリスク** - アスタリスク (\*) は任意のローカル アドレスを示します。 存在する場合、アスタリスクを、含める唯一のトークンとする必要があります。
  - **サブネット** - サブネット マスクまたはネットワーク プレフィックス表記を使用してサブネットを指定します。 サブネット マスクもネットワーク プレフィックスも指定されていない場合、サブネット マスクの既定値は 255.255.255.255 となります。
  - **有効な IPv6 アドレス**
  - **IPv4 アドレス範囲** - IPv4 範囲は、スペースを含めずに "*開始アドレス - 終了アドレス*" の形式とする必要があります。ここで、開始アドレスは終了アドレスよりも小さくします。
  - **IPv6 アドレス範囲** - IPv6 範囲は、スペースを含めずに "*開始アドレス - 終了アドレス*" の形式とする必要があります。ここで、開始アドレスは終了アドレスよりも小さくします。

  値が指定されていない場合、この設定では既定値として *[任意のアドレス]* が使用されます。

- **任意のリモート アドレス**  
  **未構成** ("*既定値*") - サポートするアドレスの範囲を構成するには、以下の設定 *[リモート アドレス範囲]* * を使用します。
  - **はい** - 任意のリモート アドレスをサポートし、アドレス範囲は構成しません。

- **リモート アドレス範囲**  
  CSP:[FirewallRules/FirewallRuleName/RemoteAddressRanges](/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  この規則のリモート アドレス範囲を管理します。 次の操作を行います。
  - 1 つまたは複数のアドレスを、規則の対象となるリモート アドレスのコンマ区切りリストとして**追加**します。
  - リモート アドレス範囲として使用するアドレスの一覧が含まれる .csv ファイルを**インポート**します。
  - .csv ファイルとしてリモート アドレス範囲の現行一覧を**エクスポート**します。

  有効なエントリ (トークン) には次のものが含まれます。大文字と小文字は区別されません。
  - **アスタリスク** - アスタリスク (\*) は任意のリモート アドレスを示します。 存在する場合、アスタリスクを、含める唯一のトークンとする必要があります。
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** - Windows 1809 以降を実行しているデバイスでサポートされています。
  - **RmtIntranet** - Windows 1809 以降を実行しているデバイスでサポートされています。
  - **Ply2Renders** - Windows 1809 以降を実行しているデバイスでサポートされています。
  - **LocalSubnet** - ローカル サブネット上の任意のローカル アドレスを示します。
  - **サブネット** - サブネット マスクまたはネットワーク プレフィックス表記を使用してサブネットを指定します。 サブネット マスクもネットワーク プレフィックスも指定されていない場合、サブネット マスクの既定値は 255.255.255.255 となります。
  - **有効な IPv6 アドレス**
  - **IPv4 アドレス範囲** - IPv4 範囲は、スペースを含めずに "*開始アドレス - 終了アドレス*" の形式とする必要があります。ここで、開始アドレスは終了アドレスよりも小さくします。
  - **IPv6 アドレス範囲** - IPv6 範囲は、スペースを含めずに "*開始アドレス - 終了アドレス*" の形式とする必要があります。ここで、開始アドレスは終了アドレスよりも小さくします。

  値が指定されていない場合、この設定では既定値として *[任意のアドレス]* が使用されます。

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>次のステップ

[ファイアウォールのエンドポイント セキュリティ ポリシー](../protect/endpoint-security-firewall-policy.md)