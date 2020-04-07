---
title: Microsoft Intune - Azure で macOS のエンドポイント保護を追加する | Microsoft Docs
description: macOS デバイスで、ゲートキーパーを利用し、Mac App Store など、アプリをインストールできる場所を決定します。 他にも、ファイアウォールを有効にして (あるいは構成して) 特定のアプリを許可または禁止したり、ステルス モードを利用したり、さらには Microsoft Intune を利用し、特定の種類の着信接続をブロックしたりします。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e857cdd7028851f14f607739ba7e37c744fa2f1
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359463"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Intune の macOS エンドポイント保護設定  

この記事では、macOS を稼働しているデバイスに対して構成できるすべてのエンドポイント保護設定について説明します。 これらの設定を構成するには、Intune の[エンドポイント保護](endpoint-protection-configure.md)用の macOS デバイス構成プロファイルを使用します。  

## <a name="before-you-begin"></a>始める前に

[macOS Endpoint Protection プロファイルを作成します](endpoint-protection-configure.md)。

## <a name="gatekeeper"></a>ゲートキーパー  

- **これらの場所からダウンロードされたアプリを許可します**  
  アプリのダウンロード元の場所に応じて、デバイスで起動できるアプリを制限します。 その目的は、マルウェアからデバイスを保護し、信頼しているソースからのアプリだけを許可することです。  

  - **未構成**  
  - **Mac App Store**  
  - **[Mac App Store and identified developers]\(Mac App Store と確認済みの開発者\)**  
  - **[どこでも]**  

  **既定値**:未構成  

- **ユーザーはゲートキーパーをオーバーライドできます**  
  ユーザーがゲートキーパー設定をオーバーライドすることを禁止し、Control キーを押しながらクリックしてアプリをインストールすることを防止します。 有効にすると、ユーザーはあらゆるアプリを Control キーを押しながらクリックし、インストールできます。  
 
  - **[未構成]** - ユーザーは、Ctrl キーを押しながらクリックしてアプリをインストールできます。  
  - **[ブロック]** - ユーザーが Ctrl キーを押しながらクリックしてアプリをインストールできないようにします。  

  **既定値**:未構成  

## <a name="firewall"></a>ファイアウォール  

ファイアウォールを利用し、ポート別ではなく、アプリケーション別に接続を制御します。 アプリケーション別の設定を利用することで、ファイアウォール保護の長所を簡単に引き出すことができます。 また、正しいアプリのために開いているネットワーク ポートが望ましくないアプリに支配されるのを防ぎます。  

**全般**
- **ファイアウォール**  
  ファイアウォールを有効にして、使用する環境における着信接続の処理方法を構成します。  
  - **未構成**  
  - **有効化**  

  **既定値**:未構成  

- **着信接続**  
  DHCP、Bonjour、IPSec など、基本的なインターネット サービスに必要な接続を除き、すべての着信接続をブロックします。 この機能によって、ファイル共有や画面共有など、あらゆるすべての共有サービスもブロックされます。 共有サービスを利用している場合、この設定を *[未構成]* にしてください。  
  - **未構成**  
  - **ブロック**  

  **既定値**:未構成  

**特定のアプリの着信接続を許可またはブロックします。**  

  - **許可されたアプリ**  
    着信接続を受け入れることが明示的に許可されているアプリを選択します。  

  - **ブロックされたアプリ**  
    着信接続をブロックする必要があるアプリを選択します。  

  - **ステルス モード**  
    コンピューターがプローブ要求に応答するのを防ぐには、ステルス モードを有効にします。 デバイスは引き続き、許可されているアプリに関する着信要求に応答します。 ICMP (ping) などの予期しない要求は無視されます。  
    - **未構成**  
    - **有効化**  

    **既定値**:未構成  

## <a name="filevault"></a>FileVault  
Apple FileVault の設定の詳細については、Apple Developer コンテンツの「[FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault)」を参照してください。 

> [!IMPORTANT]  
> macOS 10.15 では、FileVault の構成にはユーザーが承認した MDM 登録が必要です。 

- **FileVault**  
  macOS 10.13 以降が実行されるデバイスでは、XTS-AES 128 と FileVault を使用するフル ディスク暗号化を "*有効*" にすることができます。  
  - **未構成**  
  - **有効化**  

  **既定値**:未構成  

  - **回復キーの種類**  
    "*個人用キー*" 回復キーがデバイスに対して作成されます。 個人用キーに関する次の設定を構成します。  

    - **[個人用回復キーの場所]** - 個人用回復キーを取得できる方法と場所をユーザーに対して説明する短いメッセージを指定します。 このテキストは、ユーザーがログイン画面でパスワードを忘れた場合に表示される個人用回復キーの入力をユーザーに求めるメッセージに挿入されます。  

    - **[個人用回復キーの交換]** - デバイスの個人用回復キーを交換する頻度を指定します。 既定値の **[未構成]** または **1** から **12** か月の値を選択できます。  

  - **サインアウト時のプロンプトを無効にする**  
    ユーザーがサインアウトするときに FileVault を有効にするように要求するプロンプトを表示しないようにします。無効に設定すると、サインアウト時のプロンプトは無効になり、代わりにユーザーがサインインするときにメッセージが表示されます。  
    - **未構成**  
    - **[無効]** - サインアウト時のプロンプトを無効にします。

    **既定値**:未構成  

  - **バイパスを許可する回数**  
  ユーザーのサインインに FileVault が必要となる前に、FileVault を有効にするプロンプトをユーザーが無視できる回数を設定します。 

    - **[未構成]** - 次のサインインが許可される前に、デバイスの暗号化が必要です。  
    - **1** から **10** - ユーザーは、デバイスの暗号化を要求する前に、1 から 10 回までプロンプトを無視できます。  
    - **[制限なし、常に通知]** - ユーザーは FileVault を有効にするように求められますが、暗号化は必要ありません。  
 
    **既定値**:*不定* - *[サインアウト時のプロンプトを無効にする]* を **[未構成]** に設定すると、この設定の既定値は **[未構成]** になります。 *[サインアウト時のプロンプトを無効にする]* を **[無効]** に設定すると、この設定の既定値は **1** になり、 **[未構成]** はオプションに含まれなくなります。

Intune での FileVault の詳細については、「[FileVault 回復キー](encryption-monitor.md#filevault-recovery-keys)」を参照してください。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](../configuration/device-profile-assign.md)、[その状態を監視](../configuration/device-profile-monitor.md)します。

[Windows 10 以降のデバイス](endpoint-protection-windows-10.md)で Endpoint Protection を構成することもできます。
