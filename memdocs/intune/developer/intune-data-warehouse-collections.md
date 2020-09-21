---
title: Intune データ ウェアハウスのコレクション
titleSuffix: Microsoft Intune
description: Intune データ ウェアハウスのコレクションでは、データ ウェアハウス API に関する詳細が提供されます。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/08/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 29f09230-dc56-43db-b599-d961967bda49
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0a9ecebd86404d4218142d1a3acb591974b027d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608085"
---
# <a name="intune-data-warehouse-collections"></a>Intune データ ウェアハウスのコレクション

以下の Intune データ ウェアハウスのコレクションでは、データ ウェアハウス API のエンティティの v1.0 コレクションのプロパティ、説明、例が提供されます。 

## <a name="apprevisions"></a>appRevisions
**appRevision** エンティティには、アプリのすべてのバージョンがリストされています。

|          プロパティ          |                                      [説明]                                      |                例               |
|----------------------------|---------------------------------------------------------------------------------------|--------------------------------------|
| appKey                     | アプリを示す一意識別子。                                                         | 123                                  |
| applicationId              | アプリを示す一意識別子 - AppKey に似ていますが、このキーはナチュラルです。        | b66bc706-ffff-7437-0340-032819502773 |
| revision                   | バイナリのアップロード中に管理者が挙げたバージョン。                   | 2                                    |
| title                      | アプリのタイトル。                                                                     | Excel                                |
| publisher                  | アプリの発行者。                                                                 | Microsoft                            |
| uploadState                | アプリのアップロード状態。                                                              | 1                                    |
| appTypeKey                 | AppType の参照 (次のセクションに説明あり)。                            | 1                                    |
| vppProgramTypeKey          | VppProgramType の参照 (下に説明あり)。                                        | 30876                                |
| creationTime               | このリビジョンが作成された日時。                                            | 11/23/2016 0:00                      |
| modifiedTime               | このリビジョンに関連する事項が最後に変更された日時。                            | 11/23/2016 0:00                      |
| サイズ                       | バイナリのサイズ (バイト単位)。                                                          | 120,392,000                          |
| startDateInclusiveUTC      | このアプリ リビジョンがデータ ウェアハウスで作成されたときの UTC 日時。      | 11/23/2016 0:00                      |
| endDateExclusiveUTC        | このアプリ リビジョンが推奨されなくなったときの UTC 日時。                        | 11/23/2016 0:00                      |
| isCurrent                  | データ ウェアハウスにおいて、このアプリ バージョンが現行のものであるかどうかを示します。         | 真/偽                           |
| rowLastModifiedDateTimeUTC | このアプリ バージョンがデータ ウェアハウスで最後に変更されたときの UTC 日時。 | 11/23/2016 0:00                      |

## <a name="apptypes"></a>appTypes
**appType** エンティティには、アプリのインストール ソースがリストされています。

|   プロパティ  |        [説明]        |
|-------------|---------------------------|
| appTypeID   | 種類の ID           |
| appTypeKey  | キーの代理キー |
| appTypeName | アプリの種類                  |

### <a name="example"></a>例

| AppTypeID |                名前               |                     [説明]                     |
|-----------|-----------------------------------|-----------------------------------------------------|
| 0         | Android ストア アプリ               | Android ストア アプリ。                             |
| 1         | Android LOB アプリ                 | Android の基幹業務アプリ。                  |
| 2         | 管理対象 Android ストア アプリ (MAM) | 管理が有効になっている Android ストア アプリ。 |
| 3         | iOS ストア アプリ                   | iOS ストア アプリ。                                 |
| 4         | iOS LOB アプリ                     | iOS の基幹業務アプリ。                      |
| 5         | 管理対象 iOS ストア アプリ (MAM)     | 管理が有効になっている iOS ストア アプリ。       |
| 6         | Microsoft 365 Apps for enterprise        | Windows 10 用の Microsoft 365 アプリ。     |
| 7         | Web アプリ                         | Web アプリ。                                        |
| 8         | Windows Phone 8.1 ストア アプリ     | Windows Phone 8.1 ストア アプリ。                    |
| 9         | Windows ストア アプリ               | Windows ストア アプリ。                              |
| 10        | Windows LOB アプリ                | Windows AppX 基幹業務アプリ。              |
| 11        | Windows Mobile MSI              | MSI の基幹業務アプリ。                      |
| 12        | Windows Phone LOB アプリ           | Windows Phone 基幹業務アプリ。             |

## <a name="compliancepolicystatusdeviceactivities"></a>compliancePolicyStatusDeviceActivities
次の表は、コンプライアンス ポリシーのデバイスへの割り当ての状態をまとめたものです。 見つかったコンプライアンスの状態ごとにデバイスの数を一覧表示します。

|    プロパティ   |                                                                                      [説明]                                                                                     |  例 |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey       | コンプライアンス ポリシーの概要が作成されたときの日付キー。                                                                                                                   | 20161204 |
| unknown       | 何らかの理由でオフラインになっているか、Intune または Azure AD との通信に失敗したデバイスの数。                                                                           | 5        |
| notApplicable | 管理者が適用対象とするデバイス コンプライアンス ポリシーが適用されないデバイスの数。                                                                                     | 201      |
| 対応     | 管理者が適用対象とする 1 つ以上のデバイス コンプライアンス ポリシーが正常に適用されているデバイスの数。                                                                        | 4083     |
| inGracePeriod | 準拠していないが、管理者によって定義された猶予期間内にあるデバイスの数。                                                                                  | 57       |
| nonCompliant  | 管理者が適用対象とする 1 つ以上のデバイス コンプライアンス ポリシーの適用に失敗した、または管理者が適用対象とするポリシーにユーザーが準拠していないデバイスの数。 | 43       |
|    error      |    Intune または Azure AD との通信に失敗し、エラー メッセージが返されたデバイスの数。                                                                          |    3     |

## <a name="compliancepolicystatusdeviceperpolicyactivities"></a>compliancePolicyStatusDevicePerPolicyActivities
次の表は、デバイスへのコンプライアンス ポリシーの割り当ての状態をポリシーごとおよびポリシーの種類ベースごとにまとめたものです。 割り当てられたコンプライアンス ポリシーごとに、各コンプライアンスの状態で見つかったデバイスの数を一覧表示します。

|      プロパティ     |                                                                                      [説明]                                                                                     |  例 |
|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| dateKey           | コンプライアンス ポリシーの概要が作成されたときの日付キー。                                                                                                                   | 20161219 |
| policyKey         | 概要の作成対象のコンプライアンス ポリシーのキー。                                                                                                                   | 10178    |
| policyPlatformKey | 概要の作成対象のコンプライアンス ポリシーのプラットフォームの種類のキー。                                                                                            | 5        |
| unknown           | 何らかの理由でオフラインになっているか、Intune または Azure AD との通信に失敗したデバイスの数。                                                                           | 13       |
| notApplicable     | 管理者が適用対象とするデバイス コンプライアンス ポリシーが適用されないデバイスの数。                                                                                     | 3        |
| 対応         | 管理者が適用対象とする 1 つ以上のデバイス コンプライアンス ポリシーが正常に適用されているデバイスの数。                                                                        | 45       |
| inGracePeriod     | 準拠していないが、管理者によって定義された猶予期間内にあるデバイスの数。                                                                                  | 3        |
| nonCompliant      | 管理者が適用対象とする 1 つ以上のデバイス コンプライアンス ポリシーの適用に失敗した、または管理者が適用対象とするポリシーにユーザーが準拠していないデバイスの数。 | 7        |
| error             | Intune または Azure AD との通信に失敗し、エラー メッセージが返されたデバイスの数。                                                                             | 3        |
## <a name="compliancestates"></a>complianceStates

|      プロパティ      |                       [説明]                      |
|--------------------|--------------------------------------------------------|
| complianceStatus   | mdmStatusKey に関するデバイスの対応状態       |
| complianceStateKey | デバイスと対応状態を一致させるコンプライアンス キー |
| complianceStateID  | この対応状態を照合する ID                |

### <a name="example"></a>例

|  complianceStatus  |                       [説明]                      |
|--------------------|--------------------------------------------------------|
|    Unknown         |    不明。                                                                        |
|    [準拠]       |    準拠。                                                                      |
|    非準拠    |       デバイスは準拠しておらず、会社のリソースからブロックされています。             |
|    競合        |    他の規則と競合しています。                                                      |
|    エラー           |       エラー。                                                                       |
|    ConfigManager   |    Config Manager によって管理されています。                                                      |
|    InGracePeriod   |       デバイスは非対応ですが、まだ会社のリソースにアクセスできます          |

## <a name="dates"></a>dates
**date** エンティティは、複数のデータ ウェアハウス エンティティ全体で参照される日付を示します。

|     プロパティ    |                       [説明]                      |    例    |
|-----------------|--------------------------------------------------------|---------------|
| dateKey         | データ ウェアハウス内のこの日付を示す一意識別子。 | 20160703      |
| fullDate        | この日付を完全な日時形式で表した日付。        | 7/3/2016 0:00 |
| dayOfWeek       | 曜日                                            | 1             |
| dayOfMonth      | 月の日付                                           | 3             |
| dayOfYear       | 年の通算日                                            | 185           |
| weekOfYear      | 年の通算週                                           | 28            |
| monthOfYear     | 月                                      | 7             |
| calendarQuarter | カレンダーの四半期                                       | 3             |
| calendarYear    | カレンダーの年                                          | 2016          |
| dateKey         | データ ウェアハウス内のこの日付を示す一意識別子。 | 20160703      |
| fullDate        | この日付を完全な日時形式で表した日付。        | 7/3/2016 0:00 |
| dayOfWeek       | 曜日                                            | 1             |
| dayOfMonth      | 月の日付                                           | 3             |
| dayOfYear       | 年の通算日                                            | 185           |
| weekOfYear      | 年の通算週                                           | 28            |
| monthOfYear     | 月                                      | 7             |
| calendarQuarter | カレンダーの四半期                                       | 3             |
| calendarYear    | カレンダーの年                                          | 2016          |

## <a name="devicecategories"></a>deviceCategories

|      プロパティ      |                                    [説明]                                   |                例               |
|--------------------|----------------------------------------------------------------------------------|--------------------------------------|
| deviceCategoryID   | デバイス カテゴリの一意識別子。                                       | fb415ba2-7c08-41f6-a5e5-685b50da2c4c |
| deviceCategoryKey  | データ ウェアハウスでのデバイス カテゴリを示す一意識別子 - 代理キー | 1                                    |
| deviceCategoryName | デバイス カテゴリの表示名。                                            | スマートフォン                          |

## <a name="deviceconfigurationprofiledeviceactivities"></a>deviceConfigurationProfileDeviceActivities
**DeviceConfigurationProfileDeviceActivity** エンティティには、成功、保留中、失敗、エラー状態のデバイス数/日が表示されます。 この数は、エンティティに割り当てられているデバイス構成プロファイルを反映しています。 たとえば、割り当てられているすべてのポリシーでデバイスが成功状態の場合、その日の成功カウンターが 1 つ増えます。 成功状態のプロファイルとエラー状態のプロファイルという 2 つのプロファイルがデバイスに割り当てられている場合、エンティティは成功カウンターを増やし、デバイスをエラー状態にします。 エンティティには、過去 30 日間の各状態のデバイス数/日が表示されます。

|  プロパティ |                                          [説明]                                          |  例 |
|-----------|-----------------------------------------------------------------------------------------------|----------|
| dateKey   | デバイス構成プロファイルのチェックインがデータ ウェアハウスに記録されたときの日付キー。 | 20160703 |
| pending   | 保留状態の一意のデバイス数。                                                    | 123      |
| 成功 | 成功状態の一意のデバイス数。                                                    | 12       |
| error     | エラー状態の一意のデバイス数。                                                      | 10       |
| 失敗    | 失敗状態の一意のデバイス数。                                                     | 2        |

## <a name="deviceconfigurationprofileuseractivities"></a>deviceConfigurationProfileUserActivities 
**DeviceConfigurationProfileUserActivity** エンティティには、成功、保留中、失敗、エラー状態のユーザー数/日が表示されます。 この数は、エンティティに割り当てられているデバイス構成プロファイルを反映しています。 たとえば、割り当てられているすべてのポリシーでユーザーが成功状態の場合、その日の成功カウンターが 1 つ増えます。 ユーザーに、成功状態のプロファイルとエラー状態のプロファイルの 2 つのプロファイルが割り当てられている場合、エラー状態のユーザーがカウントされます。 **DeviceConfigurationProfileUserActivity** エンティティには、過去 30 日間の各状態のユーザー数/日が表示されます。 

| プロパティ  | [説明]  | 例  |
|------------|----------------------------------------------------------------------------------------------|-----------|
| dateKey  | デバイス構成プロファイル チェックインがデータ ウェアハウスに記録されたときの日付キー。  | 20160703  |
| pending  | 保留状態の一意のユーザー数。  | 123  |
| 成功  | 成功状態の一意のユーザー数。  | 12  |
| error  | エラー状態の一意のユーザー数。  | 10  |
| 失敗  | 失敗状態の一意のユーザー数。  | 2  |

## <a name="devicepropertyhistories"></a>devicePropertyHistories

|          プロパティ          |                                                                                      [説明]                                                                                     |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| dateKey                    | 日付テーブルの参照であり、日を示します。                                                                                                                                          |
| deviceKey                  | データ ウェアハウスでのデバイスの一意識別子 - 代理キー。 これは、Intune デバイス ID が含まれるデバイス テーブルの参照です。                               |
| deviceName                 | デバイスに名前を付けられるプラットフォーム上にあるデバイスの名前。 その他のプラットフォームの場合、Intune がその他のプロパティから名前を作成します。 この属性は一部のデバイスでは利用できません。 |
| deviceRegistrationStateKey | このデバイスのデバイス登録状態属性のキー。                                                                                                                    |
| ownerTypeKey               | このデバイスの所有者の種類属性のキー: 会社、個人、不明                                                                                                  |
| managementStateKey         | このデバイスに関連付けられている管理状態を示すキーであり、リモート アクションの最新の状態を示すか、脱獄/ルート化状態を示します。                                                |
| azureADRegistered          | デバイスが Azure Active Directory に登録されているかどうか。                                                                                                                             |
| complianceStateKey         | ComplianceState へのキー。                                                                                                                                                            |
| oSVersion                  | OS のバージョン。                                                                                                                                                                          |
| jailBroken                 | デバイスが脱獄またはルート化されているかどうか。                                                                                                                                         |
| deviceCategoryKey          | このデバイスのデバイス カテゴリ属性のキー。                                                                                                                                    |
| physicalMemoryInBytes      | 物理メモリ (バイト単位)。                                                                                                                                    |
| totalStorageSpaceInBytes      | 記憶域の合計容量 (バイト単位)。                                                                                                                                    |


## <a name="deviceregistrationstates"></a>deviceRegistrationStates
**DeviceRegistrationState** エンティティは、他のデータ ウェアハウス コレクションにより参照される登録の種類を表します。 

|           プロパティ          |                                     説明                                     |
|-----------------------------|-------------------------------------------------------------------------------------|
| deviceRegistrationStateID   | 登録状況の一意識別子                                            |
| deviceRegistrationStateKey  | データ ウェアハウスにおける登録状況を示す一意識別子 - 代理キー |
| deviceRegistrationStateName | 登録状況                                                                  |
|    notRegistered                     |    未登録                                                                                                                                                                  |
|    registered                        |       登録済み                                                                                                                                                                   |
|    revoked                           |       状態は IT 管理者がクライアントをブロックしたことを意味します。クライアントのブロックを解除できます。 デバイスは、ワイプした後やインベントリから削除した後にも取り消し済み状態になります。        |
|    keyConflict                       |    キー競合                                                                                                                                                                    |
|    approvalPending                   |    承認保留中                                                                                                                                                                |
|    certificateReset                  |    証明書のリセット                                                                                                                                                               |
|    notRegisteredPendingEnrollment    |    未登録で登録保留中                                                                                                                                               |
|    unknown                           |    状態が不明                                                                                                                                                                   |

## <a name="devices"></a>デバイス
**device** エンティティには、管理中のすべての登録済みデバイスとそれに対応するプロパティが一覧表示されます。

|          プロパティ          |                                                                                       [説明]                                                                                      |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| deviceKey                  | データ ウェアハウスにおけるデバイスを示す一意識別子 - 代理キー。                                                                                                               |
| deviceId                   | デバイスの一意識別子。                                                                                                                                                     |
| deviceName                 | デバイスに名前を付けられるプラットフォーム上にあるデバイスの名前。 その他のプラットフォームの場合、Intune がその他のプロパティから名前を作成します。 この属性は一部のデバイスで利用できません。 |
| deviceTypeKey              | このデバイスの種類属性のキー。                                                                                                                                    |
| deviceRegistrationState    | このデバイスのクライアント登録状態属性のキー。                                                                                                                      |
| ownerTypeKey               | このデバイスの所有者の種類属性のキー: 会社、個人、不明。                                                                                                    |
| enrolledDateTime           | このデバイスが登録された日時。                                                                                                                                         |
| ethernetMacAddress           | このデバイスの一意のネットワーク識別子。                                                                                                                                         |
| lastSyncDateTime           | Intune によるデバイス チェックインで最後に確認されているもの。                                                                                                                                              |
| managementAgentKey         | このデバイスに関連付けられている管理エージェントのキー。                                                                                                                             |
| managementStateKey         | このデバイスに関連付けられている管理状態を示すキーであり、リモート アクションの最新の状態を示すか、脱獄/ルート化状態を示します。                                                |
| azureADDeviceId            | このデバイスの Azure deviceID。                                                                                                                                                  |
| azureADRegistered          | デバイスが Azure Active Directory に登録されているかどうか。                                                                                                                             |
| deviceCategoryKey          | このデバイスに関連付けられているカテゴリのキー。                                                                                                                                     |
| deviceEnrollmentType       | このデバイスに関連付けられている登録の種類を示すキーであり、登録の方法を示します。                                                                                             |
| complianceStateKey         | このデバイスに関連付けられているコンプライアンスの状態のキー。                                                                                                                             |
| office365Version           | デバイスにインストールされている Microsoft 365 のバージョン。                                                                                                                             |
| oSVersion                  | デバイスのオペレーティング システムのバージョン。                                                                                                                                                |
| easDeviceId                | デバイスの Exchange ActiveSync ID。                                                                                                                                                  |
| serialNumber               | SerialNumber                                                                                                                                                                           |
| userId                     | デバイスに関連付けられているユーザーの一意識別子。                                                                                                                           |
| rowLastModifiedDateTimeUTC | このデバイスがデータ ウェアハウスで最後に変更されたときの UTC 日時。                                                                                                       |
| manufacturer               | デバイスの製造元                                                                                                                                                             |
| 対象となるのは、モデル                      | デバイスのモデル                                                                                                                                                                    |
| operatingSystem            | デバイスのオペレーティング システム。 Windows、iOS、iPadOS など                                                                                                                                   |
| isDeleted                  | デバイスを削除されているかどうかを示すバイナリ。                                                                                                                                 |
| androidSecurityPatchLevel  | Android セキュリティ パッチ レベル                                                                                                                                                           |
| mEID                       | MEID                                                                                                                                                                                   |
| isSupervised               | デバイスの監視状態                                                                                                                                                               |
| freeStorageSpaceInBytes    | 記憶域の空き容量 (バイト単位)                                                                                                                                                                 |
| encryptionState            | デバイスの暗号化の状態。                                                                                                                                                      |
| subscriberCarrier          | デバイスの通信事業者                                                                                                                                                       |
| phoneNumber                | デバイスの電話番号                                                                                                                                                             |
| iMEI                       | IMEI                                                                                                                                                                                   |
| cellularTechnology         | デバイスの携帯電話テクノロジ。                                                                                                                                                    |
| wiFiMacAddress             | Wi-Fi MAC。                                                                                                                                                                              |
| windowsOsEdition             | Windows オペレーティング システムのエディション。                                                                                                                                                                              |


## <a name="devicetypes"></a>deviceTypes
**deviceType** エンティティは、他のデータ ウェアハウス エンティティによって参照されるデバイスの種類を表します。 デバイスの種類により、一般的に、デバイスのモデル、メーカー、あるいは両方の組み合わせが説明されます。

|    プロパティ    |                                  [説明]                                 |
|----------------|------------------------------------------------------------------------------|
| deviceTypeID   | デバイスの種類を示す一意識別子                                       |
| deviceTypeKey  | データ ウェアハウスにおけるデバイスの種類を示す一意識別子 - 代理キー |
| deviceTypeName | デバイスの種類                                                                |

### <a name="example"></a>例

| deviceTypeID |        名前       |                      説明                      |
|--------------|-------------------|-------------------------------------------------------|
| -1           | 利用不可   | デバイスの種類は使用できません。                     |
| 0            | デスクトップ           | Windows デスクトップ デバイス                              |
| 1            | Windows           | Windows デバイス                                      |
| 2            | WinMO6            | Windows Mobile 6.0 デバイス                           |
| 3            | Nokia             | Nokia デバイス                                        |
| 4            | WindowsPhone      | Windows Phone デバイス                                |
| 5            | Mac               | Mac デバイス                                          |
| 6            | WinCE             | Windows CE デバイス                                   |
| 7            | WinEmbedded       | Windows Embedded デバイス                             |
| 8            | IPhone            | iPhone デバイス                                       |
| 9            | IPad              | iPad デバイス                                         |
| 10           | IPod              | iPod デバイス                                         |
| 11           | Android           | デバイス管理者によって管理された Android デバイス   |
| 12           | ISocConsumer      | iSoc Consumer デバイス                                |
| 13           | Unix              | Unix デバイス                                         |
| 14           | MacMDM            | 組み込み MDM エージェントによって管理された OS X デバイス |
| 15           | HoloLens          | HoloLens デバイス                                       |
| 16           | SurfaceHub        | Surface Hub デバイス                                  |
| 17           | AndroidForWork    | Android Profile Owner によって管理された Android デバイス  |
| 18           | AndroidEnterprise | Android エンタープライズ デバイス。                          |
| 100          | Blackberry        | Blackberry デバイス                                   |
| 101          | Palm              | Palm デバイス                                         |
| 255          | Unknown           | デバイスの種類が不明                                 |

## <a name="deviceenrollmenttypes"></a>deviceEnrollmentTypes
**deviceEnrollmentType** エンティティは、デバイスが登録された方法を示します。 登録の種類により、登録の方法が保存されます。 例には、登録のさまざまな種類とその意味が一覧表示されています。

|         プロパティ         |                                    [説明]                                    |
|--------------------------|-----------------------------------------------------------------------------------|
| deviceEnrollmentTypeID   | 登録種類の一意識別子。                                       |
| deviceEnrollmentTypeKey  | データ ウェアハウスにおける登録の種類の一意識別子 - 代理キー。 |
| deviceEnrollmentTypeName | 登録種類の名前。                                                           |

### <a name="example"></a>例

| enrollmentTypeID |                名前                |                                        説明                                       |
|------------------|------------------------------------|------------------------------------------------------------------------------------------|
| 0                | Unknown                            | 登録の種類が収集されませんでした                                                      |
| 1                | UserEnrollment                     | BYOD チャネルによるユーザー主導登録。                                           |
| 2                | DeviceEnrollmentManager            | デバイス登録マネージャー アカウントでのユーザー登録。                              |
| 3                | AppleBulkWithUser                  | ユーザー チャレンジでの Apple 一括登録。 (DEP、Apple Configurator)                   |
| 4                | AppleBulkWithoutUser               | ユーザー チャレンジではない Apple 一括登録。   (DEP、Apple Configurator、Mobile Config) |
| 5                | WindowsAzureADJoin                 | Windows 10 Azure AD 参加。                                                                |
| 6                | WindowsBulkUserless                | 証明書を使用した ICD での Windows 10 一括登録。                               |
| 7                | WindowsAutoEnrollment              | Windows 10 自動登録。   (職場アカウントを追加)                                    |
| 8                | WindowsBulkAzureDomainJoin         | Windows 10 一括 Azure AD 参加。                                                           |
| 9                | WindowsCoManagement                | AutoPilot またはグループ ポリシーによってトリガーされた Windows 10 共同管理。                       |
| 10               | WindowsAzureADJoinsUsingDeviceAuth | デバイス認証を使用した Windows 10 Azure AD 参加。                                            |

## <a name="enrollmentactivities"></a>enrollmentActivities 
**EnrollmentActivity** エンティティは、デバイス登録のアクティビティを示します。

| プロパティ                      | [説明]                                                               |
|-------------------------------|---------------------------------------------------------------------------|
| dateKey                       | この登録アクティビティが記録された日付のキー。               |
| deviceEnrollmentTypeKey       | 登録の種類のキー。                                        |
| deviceTypeKey                 | デバイスの種類のキー。                                                |
| enrollmentEventStatusKey      | 登録の成功または失敗を示す状態のキー。    |
| enrollmentFailureCategoryKey  | 登録エラー カテゴリのキー (登録が失敗した場合)。        |
| enrollmentFailureReasonKey    | 登録エラーの理由のキー (登録が失敗した場合)。          |
| osVersion                     | デバイスのオペレーティング システムのバージョン。                               |
| count                         | 上記の分類に一致する登録アクティビティの合計数。  |

## <a name="enrollmenteventstatuses"></a>enrollmentEventStatuses 
**EnrollmentEventStatus** エンティティは、デバイス登録の結果を示します。

| プロパティ                   | [説明]                                                                       |
|----------------------------|-----------------------------------------------------------------------------------|
| enrollmentEventStatusKey   | データ ウェアハウスでの登録状態の一意識別子 (代理キー)  |
| enrollmentEventStatusName  | 登録状態の名前。 以下の例を参照してください。                            |

### <a name="example"></a>例

| enrollmentEventStatusName  | 説明                            |
|----------------------------|----------------------------------------|
| 成功                    | 成功したデバイスの登録         |
| Failed                     | 失敗したデバイスの登録             |
| 利用不可              | 登録状態は利用できません。  |

## <a name="enrollmentfailurecategories"></a>enrollmentFailureCategories 
**EnrollmentFailureCategory** エンティティは、デバイスの登録が失敗した理由を示します。 

| プロパティ                       | [説明]                                                                                 |
|--------------------------------|---------------------------------------------------------------------------------------------|
| enrollmentFailureCategoryKey   | データ ウェアハウスでの登録の失敗カテゴリの一意識別子 (代理キー)  |
| enrollmentFailureCategoryName  | 登録エラーのカテゴリの名前。 以下の例を参照してください。                            |

### <a name="example"></a>例

| enrollmentFailureCategoryName   | [説明]                                                                                                   |
|---------------------------------|---------------------------------------------------------------------------------------------------------------|
| 適用しない                  | 登録エラーのカテゴリは適用されません。                                                            |
| 利用不可                   | 登録エラーのカテゴリは利用できません。                                                             |
| Unknown                         | 不明なエラー。                                                                                                |
| 認証                  | 認証に失敗しました。                                                                                        |
| 承認                   | 呼び出しは認証されましたが、登録する権限がありません。                                                         |
| AccountValidation               | 登録用のアカウントの検証に失敗しました (アカウントはブロックされ、登録は有効になっていません)。                      |
| UserValidation                  | ユーザーを検証できませんでした (ユーザーが存在しておらず、ライセンスが欠落しています)。                                           |
| DeviceNotSupported              | デバイスがモバイル デバイス管理でサポートされていません。                                                         |
| InMaintenance                   | アカウントがメンテナンス中です。                                                                                    |
| BadRequest                      | クライアントによって、サービスで認識/サポートされていない要求が送信されました。                                        |
| FeatureNotSupported             | この登録で使用される機能が、このアカウントでサポートされていません。                                        |
| EnrollmentRestrictionsEnforced  | 管理者が構成した登録制限によって、この登録がブロックされました。                                          |
| ClientDisconnected              | クライアントがタイムアウトになったか、エンドユーザーによって登録が中断されました。                                                        |
| UserAbandonment                 | エンドユーザーによって登録が中止されました。 (エンドユーザーはオンボードを開始しましたが、適切なタイミングでそれを完了できませんでした)  |

## <a name="enrollmentfailurereasons"></a>enrollmentFailureReasons  
**EnrollmentFailureReason** エンティティは、特定のエラー カテゴリ内のデバイス登録エラーのより詳細な理由を示します。  

| プロパティ                     | [説明]                                                                               |
|------------------------------|-------------------------------------------------------------------------------------------|
| enrollmentFailureReasonKey   | データ ウェアハウスでの登録エラーの理由の一意識別子 (代理キー)  |
| enrollmentFailureReasonName  | 登録エラーの理由の名前。 以下の例を参照してください。                            |

### <a name="example"></a>例

| enrollmentFailureReasonName      | 説明                                                                                                                                                                                            |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 適用しない                   | 登録エラーの理由は適用されません。                                                                                                                                                       |
| 利用不可                    | 登録エラーの理由は利用できません。                                                                                                                                                        |
| Unknown                          | 不明なエラー。                                                                                                                                                                                         |
| UserNotLicensed                  | ユーザーが Intune で見つからなかったか、有効なライセンスを持っていません。                                                                                                                                     |
| UserUnknown                      | ユーザーが Intune に認識されていません。                                                                                                                                                                           |
| BulkAlreadyEnrolledDevice        | デバイスを登録できるのは 1 人のユーザーのみです。 このデバイスは以前に別のユーザーによって登録されています。                                                                                                                |
| EnrollmentOnboardingIssue        | Intune モバイル デバイス管理 (MDM) 機関がまだ構成されていません。                                                                                                                                 |
| AppleChallengeIssue              | iOS 管理プロファイルのインストールに遅延が生じたか、失敗しました。                                                                                                                                         |
| AppleOnboardingIssue             | Intune に登録するには、Apple MDM プッシュ証明書が必要です。                                                                                                                                       |
| DeviceCap                        | ユーザーが、最大許容数を超えるデバイスを登録しようとしました。                                                                                                                                        |
| AuthenticationRequirementNotMet  | Intune 登録サービスでこの要求を承認できませんでした。                                                                                                                                            |
| UnsupportedDeviceType            | このデバイスは Intune 登録のための最小要件を満たしていません。                                                                                                                                  |
| EnrollmentCriteriaNotMet         | 構成された登録制限規則により、このデバイスの登録に失敗しました。                                                                                                                          |
| BulkDeviceNotPreregistered       | このデバイスの International Mobile Equipment Identifier (IMEI) またはシリアル番号が見つかりませんでした。  この識別子がない場合、デバイスは、現在ブロックされている個人所有デバイスとして認識されます。  |
| FeatureNotSupported              | ユーザーが、すべての顧客に対してまだリリースされていないか、Intune 構成と互換性のない機能にアクセスしようとしました。                                                            |
| UserAbandonment                  | エンドユーザーによって登録が中止されました。 (エンドユーザーはオンボードを開始しましたが、適切なタイミングでそれを完了できませんでした)                                                                                           |
| APNSCertificateExpired           | 期限切れの Apple MDM プッシュ証明書では、Apple デバイスを管理できません。                                                                                                                            |

## <a name="intunemanagementextensions"></a>intuneManagementExtensions
**intuneManagementExtension** には、1 日あたりの各 Windows 10 デバイスでの **intuneManagementExtension** 正常性がリストされています。 過去 60 日間のデータが保持されます。

|       プロパティ      |                          説明                          | 例 |
|---------------------|---------------------------------------------------------------|---------|
| dateKey             | 日付の一意識別子。                                | 123     |
| tenantKey           | テナントの一意識別子。                              | 456     |
| deviceKey           | デバイスの一意識別子。                              | 789     |
| extensionVersionKey | IntuneManagementExtension バージョンの一意識別子。 | 1       |
| extensionStateKey   | ヘルス状態の一意識別子。                            | 2       |

## <a name="intunemanagementextensionhealthstates"></a>intuneManagementExtensionHealthStates
**IntuneManagementExtensionHealthState** には、**IntuneManagementExtension** のべての可能な正常性状態がリストされています。

|      プロパティ     |                   説明                  | 例 |
|-------------------|------------------------------------------------|---------|
| extensionStateKey | 正常性状態の一意識別子。           | 2       |
| extensionState    | IntuneManagementExtension の正常性状態。 | Healthy |

## <a name="intunemanagementextensionversions"></a>intuneManagementExtensionVersions
**IntuneManagementExtensionVersion** エンティティには、**IntuneManagementExtension** で使用されるすべてのバージョンがリストされています。

|       プロパティ      |                          説明                          | 例 |
|---------------------|---------------------------------------------------------------|---------|
| extensionVersionKey | IntuneManagementExtension バージョンの一意識別子。 | 1       |
| extensionVersion    | 4 桁のバージョン番号。                                   | 1.0.2.0 |

## <a name="mamapplications"></a>MamApplications

**MamApplication** エンティティは、企業内登録なしで、モバイル アプリケーション管理 (MAM) 経由で管理される基幹業務 (LOB) アプリを一覧表示します。

| プロパティ | 説明 | 例 |
|---------|------------|--------|
| mamApplicationKey |MAM アプリケーションの一意識別子。 | 432 |
| mamApplicationName |MAM アプリケーションの名前。 |MAM Application Example Name |
| mamApplicationId |MAM アプリケーションのアプリケーション ID。 | 123 |
| isDeleted |この MAM アプリ レコードが更新されているかどうかを示します。 <br>True - MAM アプリには新しいレコードがあり、そのフィールドはこのテーブルで更新されています。 <br>False - この MAM アプリの最新のレコード。 |真/偽 |
| startDateInclusiveUTC |この MAM アプリがデータ ウェアハウスで作成されたときの UTC 日時。 |11/23/2016 12:00:00 AM |
| deletedDateUTC |IsDeleted が True に変更されたときの UTC 日時。 |11/23/2016 12:00:00 AM |
| rowLastModifiedDateTimeUTC |この MAM アプリがデータ ウェアハウスで最後に変更されたときの UTC 日時。 |11/23/2016 12:00:00 AM |


## <a name="mamapplicationinstances"></a>MamApplicationInstances

**MamApplicationInstance** エンティティは、デバイス別ユーザー別の単一インスタンスとして、管理されているモバイル アプリケーション管理 (MAM) アプリを一覧表示します。 エンティティ内に一覧表示されているユーザーとデバイスはすべて、少なくとも 1 つの MAM ポリシーが割り当てられ、保護されます。


|          プロパティ          |                                                                                                  説明                                                                                                  |               例                |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
|   applicationInstanceKey   |                                                               データ ウェアハウスにおける MAM アプリ インスタンスを示す一意識別子 - 代理キー。                                                                |                 123                  |
|           userId           |                                                                              この MAM アプリをインストールしたユーザーのユーザー ID。                                                                              | b66bc706-ffff-7437-0340-032819502773 |
|   applicationInstanceId    |                                              MAM アプリ インスタンスを示す一意識別子 - ApplicationInstanceKey に似ていますが、識別子はナチュラル キーです。                                              | b66bc706-ffff-7437-0340-032819502773 |
| mamApplicationId | この MAM アプリケーション インスタンスの作成に使用された MAM アプリケーションのアプリケーション ID。   | 11/23/2016 12:00:00 AM   |
|     applicationVersion     |                                                                                     この MAM アプリのアプリケーション バージョン。                                                                                      |                  2                   |
|        createdDate         |                                                                 MAM アプリ インスタンスのこのレコードが作成された日付 値は null を取ることができます。                                                                 |        11/23/2016 12:00:00 AM        |
|          platform          |                                                                          この MAM アプリがインストールされているデバイスのプラットフォーム。                                                                           |                  2                   |
|      platformVersion       |                                                                      この MAM アプリがインストールされているデバイスのプラットフォーム バージョン。                                                                       |                 2.2                  |
|         sdkVersion         |                                                                            この MAM アプリをラップした MAM SDK バージョン。                                                                            |                 3.2                  |
| mamDeviceId | MAM アプリケーションのインスタンスが関連付けられているデバイスのデバイス ID。   | 11/23/2016 12:00:00 AM   |
| mamDeviceType | MAM アプリケーション インスタンスが関連付けられているデバイスのデバイスの種類。   | 11/23/2016 12:00:00 AM   |
| mamDeviceName | MAM アプリケーション インスタンスが関連付けられているデバイスのデバイス名。   | 11/23/2016 12:00:00 AM   |
|         isDeleted          | この MAM アプリ インスタンス レコードが更新されているかどうかを示します。 <br>True - この MAM アプリ インスタンスには新しいレコードがあり、そのフィールドはこのテーブルで更新されています。 <br>False - この MAM アプリ インスタンスの最新のレコード。 |              真/偽              |
|   startDateInclusiveUtc    |                                                              この MAM アプリ インスタンスがデータ ウェアハウスで作成されたときの UTC 日時。                                                               |        11/23/2016 12:00:00 AM        |
|       deletedDateUtc       |                                                                             IsDeleted が True に変更されたときの UTC 日時。                                                                              |        11/23/2016 12:00:00 AM        |
| rowLastModifiedDateTimeUtc |                                                           この MAM アプリ インスタンスがデータ ウェアハウスで最後に変更されたときの UTC 日時。                                                            |        11/23/2016 12:00:00 AM        |

## <a name="mamcheckins"></a>MamCheckins

**MamCheckin** エンティティは、モバイル アプリケーション管理 (MAM) アプリ インスタンスが Intune サービスでチェックインしたときに集められたデータを表します。 

> [!Note]  
> アプリ インスタンスが一日に複数回チェックインするとき、データ ウェアハウスは単一チェックインとしてそれを保存します。

| プロパティ | 説明 | 例 |
|---------|------------|--------|
| dateKey |MAM アプリ チェックインがデータ ウェアハウスに記録されたときの日付キー。 | 20160703 |
| applicationInstanceKey |この MAM アプリ チェックインに関連付けられているアプリ インスタンスのキー。 | 123 |
| userKey |この MAM アプリ チェックインに関連付けられているユーザーのキー。 | 4323 |
| mamApplicationKey |MAM アプリケーションのチェックインに関連付けられているアプリケーションのアプリケーション キー。 | 432 |
| deviceHealthKey |この MAM アプリ チェックインに関連付けられている DeviceHealth のキー。 | 321 |
| platformKey |この MAM アプリ チェックインに関連付けられているデバイスのプラットフォームを表します。 |123 |
| lastCheckInDate |この MAM アプリが最後にチェックインした日時 値は null を取ることができます。 |11/23/2016 12:00:00 AM |

## <a name="mamdevicehealths"></a>MamDeviceHealths

**MamDeviceHealth** エンティティは、モバイル アプリケーション管理 (MAM) ポリシーが展開されているデバイスを表します。脱獄されているものも含まれます。

| プロパティ | 説明 | 例 |
|---------|------------|--------|
| deviceHealthKey |データ ウェアハウスにおけるデバイスとそれに関連付けられている正常性を示す一意識別子 - 代理キー。 |123 |
| deviceHealth |デバイスとそれに関連付けられている正常性を示す一意識別子 - DeviceHealthKey に似ていますが、この識別子はナチュラル キーです。 |b66bc706-ffff-7777-0340-032819502773 |
| deviceHealthName |デバイスの状態を表します。 <br>利用不可 - このデバイスの情報はありません。 <br>正常 - デバイスは脱獄されていません。 <br>異常 - デバイスは脱獄されています。 |利用不可、正常、異常 |
| rowLastModifiedDateTimeUtc |この特定の MAM デバイス正常性がデータ ウェアハウスで最後に変更されたときの UTC 日時。 |11/23/2016 12:00:00 AM |

## <a name="mamplatforms"></a>MamPlatforms

**MamPlatform** エンティティは、モバイル アプリケーション管理 (MAM) アプリがインストールされたプラットフォームの名前と種類を一覧表示します。


|          プロパティ          |                                    説明                                    |                         例                         |
|----------------------------|-----------------------------------------------------------------------------------|---------------------------------------------------------|
|        platformKey         |     データ ウェアハウスにおけるプラットフォームを示す一意識別子 - 代理キー。      |                           123                           |
|          platform          | プラットフォームを示す一意識別子 - PlatformKey に似ていますが、ナチュラル キーです。 |                           123                           |
|        platformName        |                                   プラットフォームの名前                                   | 利用不可 <br>なし <br>Windows <br>IOS <br>Android。 |
| rowLastModifiedDateTimeUtc | このプラットフォームがデータ ウェアハウスで最後に変更されたときの UTC 日時。  |                 11/23/2016 12:00:00 AM                  |

## <a name="managementagenttypes"></a>managementAgentTypes
**managementAgentType** エンティティは、デバイスの管理に使用されるエージェントを表します。

|         プロパティ        |                                       [説明]                                       |
|-------------------------|-----------------------------------------------------------------------------------------|
| managementAgentTypeID   | 管理エージェントの種類を示す一意識別子。                                         |
| managementAgentTypeKey  | データ ウェアハウスにおける管理エージェントの種類を示す一意識別子 - 代理キー。 |
| managementAgentTypeName | デバイスの管理に利用されているエージェントの種類を示します。                              |

### <a name="example"></a>例

| ManagementAgentTypeID |                名前               |                                  説明                                 |
|-----------------------|-----------------------------------|------------------------------------------------------------------------------|
| 1                     | EAS                               | デバイスは Exchange Active Sync で管理されています                         |
| 2                     | MDM                               | デバイスは MDM エージェントで管理されています                                   |
| 3                     | EasMdm                            | デバイスは Exchange Active Sync と MDM エージェントの両方で管理されています        |
| 4                     | IntuneClient                      | デバイスは Intune PC エージェントで管理されています                               |
| 5                     | EasIntuneClient                   | デバイスは Exchange Active Sync と Intune PC エージェントの両方で管理されています |
| 8                     | ConfigManagerClient               | デバイスは Configuration Manager エージェントで管理されています     |
| 10                    | ConfigurationManagerClientMdm     | デバイスは Configuration Manager と MDM で管理されています。                    |
| 11                    | ConfigurationManagerCLientMdmEas  | デバイスは Configuration Manager、MDM、Exchange Active Sync で管理されています。               |
| 16                    | Unknown                           | 管理エージェントの種類は不明です                                              |
| 32                    | Jamf                              | デバイスの属性は、Jamf からフェッチされます。                               |
| 64                    | GoogleCloudDevicePolicyController |  デバイスは、Google の CloudDPC によって管理されています。                                 |

## <a name="managementstates"></a>managementStates
**ManagementState** エンティティは、デバイスの状態に関する詳細を提供します。 リモート アクションが適用され、デバイスが脱獄またはルート化されているとき、詳細が役立ちます。

|       プロパティ      |                                     [説明]                                    |
|---------------------|------------------------------------------------------------------------------------|
| managementStateID   | 管理状態を示す一意識別子。                                       |
| managementStateKey  | データ ウェアハウスにおける管理状態を示す一意識別子 - 代理キー。 |
| managementStateName | このデバイスに適用されるリモート アクションの状態を示します。                 |

### <a name="example"></a>例

| managementStateID |      名前      |                                                   説明                                                   |
|-------------------|----------------|-----------------------------------------------------------------------------------------------------------------|
| 0                 | 管理対象        | 保留なしのリモート アクションにより管理。                                                                       |
| 1                 | RetirePending  | インベントリから削除するコマンドがデバイスに対して保留になっています。                                                             |
| 2                 | RetireFailed   | インベントリから削除するコマンドをデバイスに実行したところ、失敗しました。                                                                      |
| 3                 | WipePending    | ワイプ コマンドがデバイスに対して保留になっています。                                                               |
| 4                 | WipeFailed     | ワイプ コマンドをデバイスに実行したところ、失敗しました。                                                                        |
| 5                 | Unhealthy      | 正常ではない状態。                                                                                              |
| 6                 | DeletePending  | 削除コマンドがデバイスに対して保留になっています。                                                             |
| 7                 | RetireIssued   | インベントリから削除するコマンドがデバイスに発行されています。                                                               |
| 8                 | WipeIssued     | ワイプ コマンドが発行されています。                                                                               |
| 9                 | WipeCanceled   | ワイプ コマンドが取り消されています。                                                                               |
| 10                | RetireCanceled | インベントリから削除するコマンドが取り消されています。                                                                             |
| 11                | Discovered     | Intune がデバイスを新たに検出しました。最初のチェックイン後、状態は管理対象に変更されます。 |

## <a name="mobileappinstallstates"></a>mobileAppInstallStates
MobileAppInstallState エンティティは、デバイス、ユーザー、またはその両方を含むグループに割り当てられた後のモバイル アプリケーションのインストール状態を表します。

|       プロパティ      |                        [説明]                       |
|---------------------|----------------------------------------------------------|
| appInstallStateKey  | アカウントにおけるアプリのインストール状態の一意の ID。 |
| appInstallState     | アプリのインストール状態の列挙値。                     |
| appInstallStateName | アプリのインストール状態の名前。                           |

## <a name="mobileappinstallstatuscounts"></a>mobileAppInstallStatusCounts
Microsoft Intune によるモバイル アプリケーション管理を使用している特定のターゲット デバイスの種類に対するモバイル アプリのインストール状態を表します。

|      プロパティ      |                                                          [説明]                                                          |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------|
| dateKey            | アプリのインストール状態が記録されたときの日付のキー。                                                                     |
| appKey             | AppRevision のインスタンスの識別に使用する、モバイル アプリのキー。                                                          |
| deviceTypeKey      | モバイル アプリケーションに関連付けられているデバイス種類のキー。                                                              |
| appInstallStateKey | MobileAppInstallState のインスタンスの識別に使用する、アプリのインストール状態のキー。                                         |
| errorCode          | アプリのインストーラー、モバイル プラットフォーム、またはアプリのインストールと関わりがあるサービスによって返されるエラー コード。 |
| count              | 総数。                                                                                                                  |

## <a name="ownertypes"></a>ownerTypes
**ownerType** エンティティは、デバイスの種類として企業所有、個人所有、不明のいずれかを示します。

|    プロパティ   |                                                                                     説明                                                                                    |           例          |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------|
| ownerTypeID   | 所有者の種類を示す一意識別子。                                                                                                                                               |                            |
| ownerTypeKey  | データ ウェアハウスにおける所有者の種類を示す一意識別子 - 代理キー。                                                                                                       |                            |
| ownerTypeName | デバイスの所有者の種類を表します。Corporate - 会社が所有するデバイスです。  Personal - 個人が所有するデバイスです (BYOD)。   Unknown - このデバイスの情報はありません。 | 会社、個人、不明 |

> [!Note]  
> デバイスに対して動的グループを作成する場合の AzureAD の `ownerTypeName` フィルターでは、値 `deviceOwnership` を `Company` として設定する必要があります。 詳細については、「[デバイスのルール](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices)」を参照してください。 

## <a name="policies"></a>policies
**Policy** エンティティには、デバイス構成プロファイル、アプリ構成プロファイル、およびコンプライアンス ポリシーが表示されます。 モバイル デバイス管理 (MDM) を含むポリシーを社内のグループに割り当てることができます。

|          プロパティ          |                                                                       説明                                                                      |                例               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| policyKey                  | データ ウェアハウス内のポリシーを表す一意のキー。                                                                                              | 123                                  |
| policyId                   | データ ウェアハウス内のポリシーを示す一意識別子。                                                                                                 | b66bc706-ffff-7437-0340-032819502773 |
| policyName                 | ポリシーの名前。                                                                                                                                    | "Windows 10 Baseline"                |
| policyVersion              | ポリシーのバージョン。 ポリシーを編集または変更すると、新しいバージョンが作成されます。                                                             | 1, 2, 3                              |
| isDeleted                  | ポリシー レコードが更新されているかどうかを示します。  True - ポリシーには、フィールドが更新された新しいレコードがあります。  False - ポリシーの最新のレコードです。 | 真/偽                           |
| startDateInclusiveUTC      | ポリシーがデータ ウェアハウスで作成されたときの UTC 日時。                                                                              | 11/23/2016 0:00                      |
| deletedDateUTC             | IsDeleted が True に変更されたときの UTC 日時。                                                                                                   | 11/23/2016 0:00                      |
| rowLastModifiedDateTimeUTC | ポリシーがデータ ウェアハウスで最後に変更されたときの UTC 日時。                                                                        | 11/23/2016 0:00                      |

## <a name="policydeviceactivities"></a>policyDeviceActivities
次の表に、成功、保留中、失敗、またはエラー状態のデバイス数/日の一覧を示します。 数は、ポリシーの種類のプロファイルごとのデータを反映しています。 たとえば、割り当てられているすべてのポリシーでデバイスが成功状態の場合、その日の成功カウンターが 1 つ増えます。 成功状態のプロファイルとエラー状態のプロファイルという 2 つのプロファイルがデバイスに割り当てられている場合、エンティティは成功カウンターを増やし、デバイスをエラー状態にします。 **policyDeviceActivity** エンティティには、過去 30 日間の各状態のデバイス数/日が表示されます。

|  プロパティ |                                           説明                                           |        例        |
|-----------|-------------------------------------------------------------------------------------------------|-----------------------|
| dateKey   | デバイス構成プロファイル チェックインがデータ ウェアハウスに記録されたときの日付キー。 | 20160703              |
| pending   | 保留状態の一意のデバイス数。                                                    | 123                   |
| 成功 | 成功状態の一意のデバイス数。                                                    | 12                    |
| policyKey | ポリシー キーとポリシーを結合して、policyName を取得できます。                                  | Windows 10 ベースライン |
| error     | エラー状態の一意デバイスの数。                                                      | 10                    |
| 失敗    | 失敗状態の一意デバイスの数。                                                     | 2                     |

## <a name="policyplatformtypes"></a>policyPlatformTypes

|        プロパティ        |                      説明                      |     例    |
|------------------------|-------------------------------------------------------|----------------|
| policyPlatformTypeKey  | ポリシー プラットフォームの種類の一意キー。        | 20170519       |
| policyPlatformTypeId   | ポリシー プラットフォームの種類の一意の ID。 | 1              |
| policyPlatformTypeName | ポリシー プラットフォームの種類の名前。              | AndroidForWork |

## <a name="policytypeactivities"></a>policyTypeActivities
**PolicyTypeActivity** エンティティには、成功、保留中、失敗、またはエラー状態のデバイスの累積数が表示されます。 デバイス構成プロファイル、アプリ構成プロファイル、またはコンプライアンス ポリシーについて、これらの状態が 1 日単位で表示されます。

|    プロパティ   |                                          説明                                          |           例           |
|---------------|-----------------------------------------------------------------------------------------------|-----------------------------|
| dateKey       | デバイス構成プロファイル チェックインがデータ ウェアハウスに記録されたときの日付キー。 | 20160703                    |
| policyKey     | ポリシー キーとポリシーを結合して、policyName を取得できます。                                | Windows 10 baseline         |
| policyTypeKey | ポリシー キーの種類とポリシーの種類を結合してポリシーの種類名を取得できます。             | Windows10 のコンプライアンス ポリシー |
| pending       | 保留状態の一意のデバイス数。                                                    | 123                         |
| 成功     | 成功状態の一意のデバイス数。                                                    | 12                          |
| error         | エラー状態の一意のデバイス数。                                                      | 10                          |
| 失敗        | 失敗状態の一意のデバイス数。                                                     | 2                           |

## <a name="policytypes"></a>policyTypes
**PolicyType** エンティティには、デバイス構成プロファイル、アプリ構成プロファイル、およびコンプライアンス ポリシーの種類が表示されます。 モバイル デバイス管理 (MDM) を含むポリシーを社内のグループに割り当てることができます。

|    プロパティ    |                       説明                      |            例            |
|----------------|--------------------------------------------------------|-------------------------------|
| policyTypeId   | ソース システムのポリシーを示す一意識別子。  | 123                           |
| policyTypeKey  | データ ウェアハウス内のポリシーを示す一意識別子。 | 1                             |
| policyTypeName | ポリシーの種類の名前                               | Windows 10 のコンプライアンス ポリシー。 |

## <a name="policyuseractivities"></a>policyUserActivities
次の表に、成功、保留中、失敗、またはエラー状態のユーザー数/日の一覧を示します。 数は、ポリシーの種類のプロファイルごとのデータを反映しています。 たとえば、割り当てられているすべてのポリシーでユーザーが成功状態の場合、その日の成功カウンターが 1 つ増えます。 ユーザーに、成功状態のプロファイルとエラー状態のプロファイルの 2 つのプロファイルが割り当てられている場合、エラー状態のユーザーがカウントされます。 **PolicyUserActivity** エンティティには、過去 30 日間の各状態のユーザー数/日が表示されます。

|  プロパティ |                                          説明                                          |       例       |
|-----------|-----------------------------------------------------------------------------------------------|---------------------|
| dateKey   | デバイス構成プロファイルのチェックインがデータ ウェアハウスに記録されたときの日付キー。 | 20160703            |
| pending   | 保留状態の一意のデバイス数。                                                    | 123                 |
| 成功 | 成功状態の一意のデバイス数。                                                    | 12                  |
| policyKey | ポリシー キーとポリシーを結合して、policyName を取得できます。                                | Windows 10 baseline |
| error     | エラー状態の一意のデバイス数。                                                      | 10                  |

## <a name="termsandconditions"></a>termsAndConditions
**termsAndConditions** エンティティは、特定の使用条件 (T&C) ポリシーのメタデータと内容を表します。 T&C ポリシーの内容は、ユーザーが初めて Intune に登録しようとしたとき、およびそれ以降に管理者が再承認を必要とする部分を編集するときに、ユーザーに対して提示されます。 デバイスを Intune に登録するためにユーザーが同意する必要のあるプロビジョニングを管理者が通信できるようにします。

|    プロパティ        |    説明    |    例        |
|----------------------------------|-----------------------------------------------------------------------------------------------|-----------------------------------------------------------|
|    termsAndConditionsKey    |    "userTermsAndConditionsAcceptances" コレクション内のエントリに対応するキー    |    123    |
|    termsAndCondidionsId    |    この termsAndConditions エントリの ID    |    276edcb7-7440-4339-b6c5-8b6fc556fee6    |
|    termsAndConditionsVersion    |    この使用条件エントリのバージョン    |    1    |
|    name    |    この termsAndConditions エントリの名前。        |    Intune 使用条件     |
|    description    |    これらの使用条件の説明。     |         |
|    title    |    これらの使用条件のタイトル。     |    デバイス管理の会社のポリシー        |
|    summaryOfTerms    |    ユーザーに提供される条件の概要。     |    使用条件に同意します。    |
|    termsAndConditionsBodyText    |    これらの使用条件のテキストの本文。       |    *デバイスの暗号化* 6 桁の PIN の強制    |
|    isDeleted    |    この値を削除するかどうかの true または false の値。     |    False    |
|    startDateInclusiveUTC    |    これらの使用条件の開始日。     |    8/23/2018 4:01:34 AM    |
|    endDateEclusiveUTC    |    これらの使用条件の終了日。     |    12/31/9999 12:00:00 AM    |

## <a name="userdeviceassociations"></a>userDeviceAssociations
**UserDeviceAssociation** エンティティには、組織内のユーザー デバイスの関連付けが含まれています。

|        名前        |                                             説明                                            |     例     |
|--------------------|----------------------------------------------------------------------------------------------------|-----------------|
| userKey            | データ ウェアハウス内のユーザーを示す一意識別子   (代理キー)。                            | 123             |
| deviceKey          | データ ウェアハウス内のデバイスを示す一意識別子。                                             | 123             |
| createdDateTimeUTC | ユーザー デバイスの関連付けが作成されたときの日時。 UTC 形式を使用します。                     | 11/23/2016 0:00 |
| isDeleted          | ユーザーがそのデバイスを登録解除し、その関連付けが最新でなくなったことを示します。 | 真/偽      |
| endedDateTimeUTC   | IsDeleted が True に変更されたときの UTC 日時。                                               | 6/23/2017 0:00  |

## <a name="users"></a>ユーザー
**user** エンティティには、社内のすべての Azure Active Directory (Azure AD) ユーザーと割り当てられているライセンスがリストされています。

**user** エンティティ コレクションにはユーザー データが含まれています。 これらのレコードには、ユーザーが削除されている場合でも、データ コレクション期間中のユーザーの状態が含まれます。 たとえば、ユーザーが Intune に追加され、過去 1 か月の過程で削除されたとします。 このユーザーがレポートの時点では存在しない一方で、ユーザーと状態は先月のデータに存在します。 データ内のユーザーの履歴における存在の期間を示すレポートを作成できます。

|          プロパティ          |                                                                                                           説明                                                                                                          |                例               |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| userKey                    | データ ウェアハウス内のユーザーを示す一意識別子 - 代理キー。                                                                                                                                                         | 123                                  |
| userId                     | ユーザーを示す一意識別子 - UserKey と似ていますが、ナチュラル キーです。                                                                                                                                                    | b66bc706-ffff-7437-0340-032819502773 |
| userEmail                  | ユーザーの電子メール アドレス。                                                                                                                                                                                                     | John@constoso.com                    |
| userPrincipalName                        | ユーザーのユーザー プリンシパル名。                                                                                                                                                                                               | John@constoso.com                    |
| displayName                | ユーザーの表示名。                                                                                                                                                                                                      | John                                 |
| intuneLicensed             | ユーザーに Intune のライセンスがあるかどうかを示します。                                                                                                                                                                              | 真/偽                           |
| isDeleted                  | そのユーザーのすべてのライセンスの期限が切れているかどうか、および、そのユーザーがそのため Intune から削除されたかどうかを示します。 1 つのレコードでは、このフラグは変更されません。 代わりに、新しいユーザー状態用の新しいレコードが作成されます。 | 真/偽                           |
| rowLastModifiedDateTimeUTC | レコードがデータ ウェアハウスで最後に変更されたときの UTC 日時                                                                                                                                                 | 11/23/2016 0:00                      |

## <a name="usertermsandconditionsacceptances"></a>userTermsAndConditionsAcceptances
**userTermsAndConditionsAcceptance** エンティティは、特定のユーザーによる特定の使用条件 (T&C) ポリシーの同意状態を表します。 ユーザーは、Intune ポータル サイトへのアクセスを維持するには、条件の最新バージョンに同意する必要があります。

|    プロパティ    |    説明    |    例    |
|-------------------------------|--------------------------------------------------------------------------------|----------------------------|
|    dateKey    |    "dates" コレクション内の日付値に対応するキー。     |    20180823    |
|    userKey    |    "users" コレクション内のユーザーにマッピングするユーザー キー。     |    20000    |
|    termsAndConditionsKey    |    "termsAndConditions" コレクション内のエントリに対応するキー    |    1    |
|    acceptedDateTimeUTC    |    ユーザーがこれらの使用条件を受け入れた日時    |    8/23/2018 4:01:34 AM    |
|    lastModifiedDateTimeUTC    |    このエントリが最後に変更された日時。     |    8/23/2018 4:01:34 AM    |

## <a name="vppprogramtypes"></a>vppProgramTypes 
**vppProgramType** エンティティには、アプリの VPP プログラムの種類がリストされています。

|      プロパティ      |          [説明]         |
|--------------------|------------------------------|
| vppProgramTypeID   | 種類の ID。           |
| vppProgramTypeKey  | キーの代理キー。 |
| vppProgramTypeName | VPP プログラムの種類。          |

### <a name="example"></a>例

|             VppProgramID             |         名前        | 説明                |
|--------------------------------------|---------------------|----------------------------|
| 3DDA2474-470B-4503-9830-2665C21C1945 | Microsoft           | Microsoft の VPP プログラム。 |
| 00000000-0000-0000-0000-000000000000 | まだ利用できません | 既定値、No VPP。   |
| B54814E0-68EA-4BA4-8088-B5AAB58E737B | Apple               | Apple の VPP プログラム。     |

## <a name="next-steps"></a>次のステップ

Intune データ ウェアハウスについて詳しくは、「[データ ウェアハウス データ モデル](reports-ref-data-model.md)」をご覧ください。