---
title: 共同管理によるリモート アクション
titleSuffix: Configuration Manager
description: 共同管理対象デバイスに対して Intune からリモート操作を実行する
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075321"
---
# <a name="remote-actions-with-co-management"></a>共同管理によるリモート アクション

置き場所や接続の時間帯に関係なく、管理しているあらゆるデバイスに到達できることを確認する必要があります。 また、ユーザーが生産性を維持するために必要なものをすべて各ユーザーに提供し、同時にアプリとデータを保護する必要があります。 Intune でサポートされているデバイス アクションを利用することで、このような非常に重要な機能を離れた場所から実行できます。

次のビデオでは、プリンシパル プログラム マネージャーの Heidi Cheng とシニア プログラム マネージャーの Danny Guillory が共同管理によるリモート アクションについて説明し、デモを行います。

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>利点

リモート デバイス アクションを利用することで、個人データに干渉することなく、管理者としてデバイスを制御できます。 リモート デバイス アクションによって以下のことが可能になります。 
- 紛失したデバイスまたは盗難にあったデバイスに記録されている会社のデータを削除する  
- デバイスの名前を変更する  
- デバイスを再起動する  
- デバイス インベントリをレビューする  
- デバイスをリモート コントロールする  
- "新たに開始" 再起動でプレインストールされている OEM アプリを消去する  
- Windows 10 デバイスを工場出荷時の設定に戻す  

このような機能は、電子メールに保存されているものであれ、OneDrive に保存されているものであれ、デバイスに保存されている会社のデータを保護するための重要かつ簡単な手段となります。

これらのアクションに関する詳細については、「[利用できるリモート アクション](#available-remote-actions)」を参照してください。 



## <a name="case-studies"></a>導入事例

世界的なコンサルティング会社である Avanade は定期的にリモート アクションを利用し、30,000 人の社員に支給しているデバイスを管理しています。 [最近のブログ投稿](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/)で Avanade の CIO は次のように述べています。

> *Intune のこの機能を導入したことですぐに現れた効果は、コンピューター上の Windows をリモート リセットできるようになったことでした。これは弊社にとって重要なことです。外回りの多い会社ではコンピューターの紛失や盗難が当たり前ですから。* 
> *この機能がなかったら、カスタムの ConfigMgr パッケージを作成し、保守管理しなければならなかったはずです。*

リモート アクションの利用方法については、「[行えるデバイス アクション](../../intune/remote-actions/device-management.md#available-device-actions)」を参照してください。


## <a name="value-proposition"></a>価値提案

Configuration Manager デバイスを共同管理すると、Configuration Manager にはネイティブで与えられていない機能がすぐに加わることになります。 これで Intune でサポートされているあらゆるリモート アクションを実行できます。 

共同管理を利用することで、Configuration Manager デバイスは他の Intune 管理デバイスと同じになります。 たとえば、クラウドで常時存在を確認できるため、インターネット アクセスがある限り、デバイスに接触できます。 こうしたアクションを実行するとき、共同管理を有効にする以外の追加手順はありません。

ユーザーは自動登録プロセスを意識することがないので、生産性が妨げられません。 ユーザー側ではいかなる操作も必要ありません。


### <a name="available-remote-actions"></a>利用できるリモート アクション

Configuration Manager で[共同管理を有効に](how-to-enable.md)したら、Intune から次のリモート アクションを使用します。

#### <a name="remove-devices"></a>デバイスを削除する
- **インベントリからの削除**:このアクションでは、管理対象のアプリとデータ (該当する場合)、設定、そのデバイスに割り当てられていた電子メール プロファイルが削除されます。 デバイスはその後、Intune の管理から削除されます。 このプロセスは、次回、デバイスがチェックインし、リモート アクション "インベントリからの削除" を受信したときに行われます。 "インベントリからの削除" 機能では、ユーザーの個人データはデバイスに残ります。  

- **ワイプ**:このアクションでは、デバイスがリセットされ、工場出荷時の設定に戻ります。 **登録状態とユーザー アカウントを保持する**オプションを選択した場合、ユーザー データは保存されます。 そのオプションを選択しない場合、ドライブは安全に消去されます。  

- **削除**:Azure portal で Intune からデバイスを削除する場合、特定のデバイス ウィンドウからそのデバイスを削除します。 次回、デバイスがチェックインしたとき、デバイスに組織データが格納されていれば、それが削除されます。  

詳細については、「[ワイプ、インベントリからの削除、デバイス登録の手動解除を使用し、デバイスを削除する](../../intune/remote-actions/devices-wipe.md)」を参照してください。

#### <a name="selective-wipe"></a>選択的ワイプ
<!--SCCMDocs issue 973-->
**[アプリの選択的ワイプ]** を選択すると、個人データを削除することなく会社のアプリ データが削除されます。 デバイスの紛失や盗難が報告されたとき、このアクションを使用します。 

詳細については、「Intune で管理されているアプリから会社のデータをワイプする方法」 (../../intune/apps/apps-selective-wipe.md) を参照してください。

#### <a name="sync"></a>同期
デバイス アクション "**同期**" を実行すると、選択したデバイスが直後に Intune にチェックインします。 チェックインしたデバイスは、保留中のアクションやポリシーがデバイスに割り当てられている場合、それを直後に受信します。

この機能により、割り当てたポリシーをすぐに検証し、問題を解決できます。スケジュールされている次のチェックインまで待つ必要がありません。

詳細については、「[デバイスを Intune と同期して最新のポリシーとアクションを取得する](../../intune/remote-actions/device-sync.md)」を参照してください。

#### <a name="restart"></a>再起動
デバイス アクション "**再起動**" では、選択したデバイスが再起動されます。 このアクションは、再起動が保留になっているがユーザーがそれを実行できないときに便利です。

詳細については、「[Intune でデバイスをリモートで再起動する](../../intune/remote-actions/device-restart.md)」を参照してください。

#### <a name="fresh-start"></a>新たに開始
デバイス アクション "**新たに開始**" では、Windows 10 バージョン 1703 以降で実行されているデバイスにアプリがインストールされていれば、そのアプリが削除されます。 "新たに開始" では、新しいデバイスに通常インストールされているプレインストール (OEM) アプリを削除できます。

ユーザー データを保持しないことを選択した場合、デバイスはその開封時の状態に復元されます。 Azure AD と MDM の登録が解除されます。

デバイスに入れるアプリに関して基準を既に決定している場合、基準に一致しないアプリがこのアクションで消去されます。

詳細については、「[[新たに開始] を使用して Intune が稼働する Windows 10 デバイスをリセットする](../../intune/remote-actions/device-fresh-start.md)」を参照してください。 

#### <a name="remote-control"></a>リモート コントロール
Intune で管理されているデバイスは [TeamViewer](https://www.teamviewer.com/) でリモート管理できます。 TeamViewer はサードパーティ製のプログラムであり、別途入手する必要があります。

詳細については、「[TeamViewer を使用して、Intune デバイスをリモートで管理する](../../intune/remote-actions/teamviewer-support.md)」を参照してください。



## <a name="configure"></a>構成

TeamViewer によるリモート コントロールを除き、[共同管理を有効に](how-to-enable.md)した後は、他に何も設定しなくても Intune で上記のリモート デバイス アクションを使用できます。

TeamViewer によるリモート コントロールの詳細については、「[TeamViewer を使用して、Intune デバイスをリモートで管理する](../../intune/remote-actions/teamviewer-support.md)」を参照してください。
