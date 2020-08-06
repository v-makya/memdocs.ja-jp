---
title: Intune での Windows 10 の自動登録に関するトラブルシューティング
titleSuffix: Microsoft Intune
description: 自動登録に関するトラブルシューティングの方法について説明します。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 8/3/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: jchombe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 968aa9b2f7127e9b7f092f36a99b491a75f0b78c
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546868"
---
# <a name="troubleshoot-windows-10-group-policy-based-auto-enrollment-in-intune"></a>Intune での Windows 10 グループ ポリシーベースの自動登録に関するトラブルシューティング

グループ ポリシーを使用して、Active Directory (AD) ドメイン参加済みデバイスの MDM への自動登録をトリガーすることができます。 この機能の詳細については、「[グループ ポリシーを使用した Windows 10 デバイスの自動登録](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)」を参照してください。

## <a name="verify-the-configuration"></a>構成を確認する

トラブルシューティングを開始する前に、すべてが正しく構成されていることを確認することをお勧めします。 検証中に問題を解決できない場合は、いくつかの重要なログ ファイルを確認することで、さらにトラブルシューティングを行うことができます。

- デバイスを登録しようとしているユーザーに有効な Intune ライセンスが割り当てられていることを確認します。

   ![Intune ライセンスの確認](./media/troubleshoot-windows-auto-enrollment/intune-license.png)

- Intune にデバイスを登録するすべてのユーザーに対して、自動登録が有効になっていることを確認します。 詳細については、「[Azure AD と Microsoft Intune: 新しいポータルでの自動 MDM 登録](https://docs.microsoft.com/windows/client-management/mdm/azure-ad-and-microsoft-intune-automatic-mdm-enrollment-in-the-new-portal)」を参照してください。

   ![自動登録の確認](./media/troubleshoot-windows-auto-enrollment/verify-auto-enrollment.png)

   - すべてのユーザーに Intune へのデバイスの登録を許可するには、 **[MDM ユーザー スコープ]** が **[すべて]** に設定されていることを確認します。
   - **[MAM ユーザー スコープ]** が **[なし]** に設定されていることを確認します。 そうでない場合、この設定が MDM のスコープよりも優先され、問題が発生します。
   - **[MDM 探索 URL]** が **https://enrollment.manage.microsoft.com/enrollmentserver/discovery** に設定されていることを確認します。

- デバイスで Windows 10 バージョン 1709 以降が実行されていることを確認します。

- デバイスが  **[Hybrid Azure AD Join を使用した]** に設定されていることを確認します。 この設定は、デバイスがドメインと Azure AD の両方に参加済みであることを意味します。

   設定を確認するには、コマンド ラインで **dsregcmd /status** を実行します。 次に、出力で次の状態の値を確認します。

   - デバイスの状態
 
     ```asciidoc
     AzureAdJoined: YES
     DomainJoined: YES
     ```

   - SSO の状態

     ```asciidoc
     AzureAdPrt: YES
     ```

   Azure AD 参加済みデバイスの一覧でもこれと同じ情報が見つかります。

   ![Azure AD 参加済みデバイスの一覧](./media/troubleshoot-windows-auto-enrollment/ad-joined-devices.png)

- Azure AD ブレードの  **[モビリティ (MDM および MAM)]**   の下に、 **[Microsoft Intune]**   と  **[Microsoft Intune Enrollment]\(Microsoft Intune 登録\)** の両方が表示される場合があります。 両方が存在する場合は、必ず  **[Microsoft Intune]** で自動登録の設定を構成してください。

- 次のグループ ポリシーのポリシー設定が、Intune に登録する必要があるすべてのデバイスに正常に展開されていることを確認します。

   **[コンピューターの構成]**  >  **[ポリシー]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[MDM]**  > **既定の Azure AD 資格情報を使用して自動 MDM 登録を有効にする**

   ドメイン管理者に連絡して、グループ ポリシーのポリシー設定が正常に展開されていることを確認することができます。

- デバイスがクラシック PC エージェントを使用して Intune に登録されていないことを確認します。
- Azure AD と Intune で次の設定を確認します。

   **Azure AD のデバイス設定で:**

   ![Azure AD のデバイス設定](./media/troubleshoot-windows-auto-enrollment/device-setting.png)

   - **[ユーザーはデバイスを Azure AD に参加させることができます]** の設定が **[すべて]** に設定されていること。
   - ユーザーが Azure AD に持っているデバイスの数が、 **[ユーザーごとのデバイスの最大数]** のクォータを超えていないこと。
   
   **Intune の登録制限で:**

   - Windows デバイスの登録が許可されていること。

     ![許可された Windows デバイスの登録](./media/troubleshoot-windows-auto-enrollment/restrictions.png)

## <a name="troubleshooting"></a>トラブルシューティング

問題が引き続き発生する場合は、イベント ビューアーの次の場所にあるデバイスの MDM ログを調べてください。

**[アプリケーションとサービス ログ]**  >  **[Microsoft]**  >  **[Windows]**  >  **[DeviceManagement-Enterprise-Diagnostic-Provider]**  >  **[Admin]**

イベント ID 75 (イベント メッセージ "Auto MDM Enroll: Succeeded") を検索します。 このイベントは、自動登録が成功したことを示します。

イベント ID 75 は、次の状況ではログに記録されません。

- 登録が失敗した場合。

  このエラーを確認するには、イベント ID 76 (イベント メッセージ:MDM の自動登録: Failed (Unknown Win32 Error code: 0x8018002b)) を検索します。 このイベントは、自動登録が失敗したことを示します。

  このエラーの解決方法については、「[Microsoft Intune での Windows デバイスの登録に関する問題のトラブルシューティング](https://docs.microsoft.com/intune/troubleshoot-windows-enrollment-errors)」を参照してください。

- 登録がまったくトリガーされませんでした。 この場合、イベント ID 75 とイベント ID 76 はログに記録されません。
  
  自動登録プロセスは、タスク スケジューラの **[Microsoft]**  >  **[Windows]**  >  **[EnterpriseMgmt]** の下にある、"**AAD から MDM への自動登録のために登録クライアントによって作成されたスケジュール**" タスクによってトリガーされます。

  ![登録がトリガーされませんでした](./media/troubleshoot-windows-auto-enrollment/trigger.png)

  このタスクは、**既定の Azure AD 資格情報を使用して自動 MDM 登録を有効にする**グループ ポリシーのポリシー設定がターゲット デバイスに正常に展開されるときに作成されます。 タスクは、5 分ごとに 1 日中実行されるようにスケジュールされています。

  タスクが開始されていることを確認するには、イベント ビューアーの次の場所でタスク スケジューラのイベント ログを確認します。

  **[アプリケーションとサービス ログ] > [Microsoft] > [Windows] > [タスク スケジューラ] > [Operational]**

  スケジューラでタスクがトリガーされると、イベント ID 107 がログに記録されます。

  タスクが完了すると、イベント ID 102 がログに記録されます。 このイベントは、自動登録が成功したかどうかに関係なくログに記録されます。

  > [!NOTE]
  > タスク スケジューラ ログを使用して、自動登録がトリガーされたかどうかを確認できます。 ただし、ログを使用して自動登録が成功したかどうかを判断することはできません。

  次の状況では、AAD タスクから MDM に自動的に登録するために登録クライアントによって作成されたスケジュールが始されない場合があります。

  - デバイスが、既に別の MDM ソリューションに登録されている。 この場合、イベント ID 7016 とエラー コード 2149056522 が **[アプリケーションとサービス ログ]**  >  **[Microsoft]**  >  **[Windows]**  >  **[タスク スケジューラ]**  >  **[Operational]** イベント ログに記録されます。

    この問題を解決するには、MDM からデバイスの登録を解除します。

  - グループ ポリシーの問題が存在する。 この場合は、次のコマンドを実行してグループ ポリシー設定を強制的に更新します。

    **gpupdate /force**

    問題が解決しない場合は、Active Directory で追加のトラブルシューティングを行います。

## <a name="next-steps"></a>次のステップ
[Windows デバイス登録のトラブルシューティング](troubleshoot-windows-enrollment-errors.md)