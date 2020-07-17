---
title: 構成基準を展開する
titleSuffix: Configuration Manager
description: 構成基準を展開し、構成基準の展開の定義や、展開に対する構成基準の追加や削除を行います。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 94a5d0af5636236ffba3f15c05823ead083f2948
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240271"
---
# <a name="how-to-deploy-configuration-baselines-in-configuration-manager"></a>Configuration Manager での構成基準の展開方法

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager の構成基準は、1 つまたは複数のユーザーまたはデバイスのコレクションに展開する必要があります。これにより、これらのコレクションに含まれるクライアント デバイスは、構成基準に対する自らのコンプライアンスを評価できるようになります。  

構成基準の展開を定義するには、 **[構成基準の展開]** ダイアログ ボックスを使用します。このダイアログ ボックスでは、展開からの構成基準の追加と削除や評価スケジュールの指定などを行います。  

## <a name="deploy-a-configuration-baseline"></a>構成基準の展開  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]**  >  **[コンプライアンス設定]**  >  **[構成基準]** の順にクリックします。  

3.  **構成基準** 一覧で、展開にする構成基準を選択し、、 **ホーム**  タブで、 **展開** グループで、 **展開**です。  

4.  **構成基準の展開**  ダイアログ ボックスで、展開する構成基準の選択、 **使用可能な構成基準**  ボックスの一覧です。 クリックして **追加** に追加する、 **構成基準を選択した**  ボックスの一覧です。  

    > [!IMPORTANT]  
    >  展開された構成基準に追加されている構成項目を変更する場合に、その次にスケジュールされた評価時間まで更新された構成項目は対応評価されません。  

5.  次の追加情報を指定します。  

    -   **[サポートされている場合は対応していない規則を修復する]** – Windows Management Instrumentation (WMI)、レジストリ、スクリプト、および、Configuration Manager が登録したモバイル デバイスのすべての設定が対応しない規則があれば、自動的に修復します。  

    -   **[メンテナンス期間以外の修復を許可する]** – このオプションを有効にすると、構成基準の展開先のコレクションにメンテナンス期間が設定されていても、コンプライアンス設定がメンテナンス期間外に値を修復します。 メンテナンス期間について詳しくは、「[メンテナンス期間を使用する方法](../../core/clients/manage/collections/use-maintenance-windows.md)」を参照してください。  

6.  **[アラートを生成する]** – 構成基準のコンプライアンスが、指定した日付と時刻までに指定した割合に達しなかった場合に生成されるアラートを構成します。 アラートを System Center Operations Manager に送信するかどうかも指定できます。  

7.  **[コレクション]** - **[参照]** をクリックして、構成基準を展開するコレクションを選択します。  

8.  **[この構成基準のコンプライアンス評価スケジュールを指定してください]** – 展開された構成基準をクライアント コンピューターで評価するスケジュールを指定します。 簡易スケジュールまたはカスタム スケジュールを使用できます。  

    > [!NOTE]  
    >  構成基準がコンピューターに展開された場合、スケジュールされた開始時間から 2 時間以内にコンプライアンスが評価されます。 ユーザーに展開された場合、ユーザーがログオンするとコンプライアンスが評価されます。  

9. をクリックして **ok** を閉じる、 **構成基準の展開**  ダイアログ ボックスと、展開を作成します。 展開の監視方法の詳細については、「[Monitor compliance settings](monitor-compliance-settings.md)」 (コンプライアンス設定の監視) をご覧ください。  
