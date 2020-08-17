---
title: Windows Defender をオンにする | Microsoft Docs
description: Windows Defender をオンにし、会社のリソースにアクセスする方法について説明します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a57010a5c8089b0ac979cf43c3706467d83faea2
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110700"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Windows Defender をオンにし、会社のリソースにアクセスする

組織は、そのリソースにアクセスするデバイスが確実にセキュリティで保護されるようにしたいと考えています。そのために、[Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx) の使用が必要とされる場合があります。 Windows Defender は、Windows に含まれているウイルス対策ソフトウェアであり、ウイルスやその他のマルウェアや脅威からデバイスを保護するのに役立ちます。 

この記事では、組織のウイルス対策の要件を満たすようにデバイスの設定を更新し、アクセスの問題を解決する方法について説明します。 

## <a name="turn-on-windows-defender"></a>Windows Defender をオンにする
ご使用のデバイスで Windows Defender を有効にするには、次の手順を行います。 

1. **[スタート]** メニューを選択します。
2. 検索バーに、「**グループ ポリシー**」と入力します。 次に、表示された結果から **[グループポリシーの編集]** を選択します。 ローカル グループ ポリシー エディターが開きます。
4. **[コンピューターの構成]**  >  **[管理テンプレート]**  >  **[Windows コンポーネント]**  >  **[Windows Defender ウイルス対策]** の順に選択します。 
5. 一覧の一番下までスクロールし、 **[Windows Defender ウイルス対策を無効にします]** を選択します。  
6. **[無効]** または **[未構成]** を選択します。 これらのオプションは名前が Windows Defender を無効にすることを示唆しているため、選択することが直感に反していると思われるかもしれません。 実際にはこれらのオプションは確実に有効にするためのものですので、ご安心ください。 
7. **[適用]**  >  **[OK]** の順に選択します。  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>リアルタイムおよびクラウドによる保護を有効にする

リアルタイムおよびクラウドによる保護を有効にするには、次の手順を行います。 これらのウイルス対策機能を一緒に使用すると、スパイウェアから保護され、マルウェアの問題に対する修正プログラムがクラウド経由で提供されます。 

1. **[スタート]** メニューを選択します。
2. 検索バーに、「**Windows セキュリティ**」と入力します。 一致する結果を選択します。 
3. **[ウイルスと脅威の防止]** を選択します。
4. **[ウイルスと脅威の防止の設定]** の下で、 **[設定の管理]** を選択します。
5. **[リアルタイム保護]** と **[クラウドによる保護]** の下の各スイッチを切り替えて、オンにします。 

画面上にこれらのオプションが見つからない場合は、非表示になっている可能性があります。 表示するには、次の手順を行います。  

1. **[スタート]** メニューを選択します。  
2. 検索バーに、「**グループ ポリシー**」と入力します。 次に、表示された結果から **[グループポリシーの編集]** を選択します。 ローカル グループ ポリシー エディターが開きます。
3. **[コンピューターの構成]**  >  **[管理テンプレート]**  >  **[Windows コンポーネント]**  >  **[Windows セキュリティ]**  >  **[ウイルスと脅威の防止]** の順に選択します。
4. **[Hide the Virus and threat protection area]\(ウイルスと脅威の防止領域を非表示にする\)** を選択します。
5. **[無効]**  >  **[適用]**  >  **[OK]** の順に選択します。  

## <a name="update-your-antivirus-definitions"></a>ウイルス対策定義を更新する
ウイルス対策定義を更新するには、次の手順を行います。  
1. **[スタート]** メニューを選択します。
2. 検索バーに、「**Windows セキュリティ**」と入力します。 一致する結果を選択します。 
3. **[ウイルスと脅威の防止]** を選択します。
4. **[ウイルスと脅威の防止の更新]** の下で、 **[更新プログラムのチェック]** を選択します。 画面上にこのオプションが見つからない場合は、[リアルタイム保護の有効化](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection)に関する箇所の最初の手順セットを完了します。 その後、更新プログラムのチェックを再試行してください。 

## <a name="next-steps"></a>次のステップ  

サポートが必要な場合は、 社内サポートに問い合わせてください。 連絡先情報については、[ポータル サイト Web サイト](https://go.microsoft.com/fwlink/?linkid=2010980)をご確認ください。
