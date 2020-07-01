---
title: Surface ドライバーの更新プログラムの管理
titleSuffix: Configuration Manager
description: Configuration Manager では、Surface デバイスに展開するために、Surface ドライバーの更新プログラムが同期されます。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: 04793a053e85be051ce9ffafd2f15d274cf166f0
ms.sourcegitcommit: c7afcc3a2232573091c8f36d295a803595708b6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84973079"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Configuration Manager を使用して Surface ドライバーを管理する

*適用対象:System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を使用すると、Surface デバイスのドライバーを同期し、ソフトウェア更新プログラムのように展開することができます。 この機能によって、Surface デバイスで、利用可能な最新のドライバーを確実に実行することができます。 この同期は、バージョン 1706 でプレリリース機能として初めて導入され、1710 で機能になりました。 <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Surface ドライバーを同期するための前提条件

- インターネットに接続された最上位のソフトウェアの更新ポイント。
- すべてのソフトウェアの更新ポイントで、累積的な更新プログラム KB4025339 以降がインストールされた Windows Server 2016 を実行する必要があります。
- Configuration Manager では、このオプション機能は既定で無効です。 この機能は、使用する前に有効にします。 詳細については、「[Enable optional features from updates](../../core/servers/manage/install-in-console-updates.md#bkmk_options)」 (更新プログラムのオプション機能の有効化) を参照してください。<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Surface ドライバーの同期を有効にする

Surface ドライバーの同期を有効にするには、次の手順を実行します。

1. Configuration Manger コンソールを最上位サイト サーバーに接続します。
1. **[管理]**  >  **[サイトの構成]**  >  **[サイト]** の順に移動し、最上位サイトをクリックします。
1. リボンで **[設定]**  >  **[サイト コンポーネントの構成]**  >  **[ソフトウェアの更新ポイント]** の順に選択します。
1. **[分類]** タブをクリックしてから、 **[Microsoft Surface のドライバーとファームウェアの更新プログラムを含める]** のチェックボックスをオンにして、 **[適用]** をクリックします。

     ![ソフトウェアの更新ポイントのプロパティから Surface ドライバーを有効にする](media/enable-surface-driver-sync.png)

1. [ソフトウェアの更新ポイント コンポーネントのプロパティ] で、 **[製品]** タブをクリックします。詳細については、「[Surface ドライバーの製品](#bkmk_prod)」および「[Surface モデル](#bkmk_models)」セクションをご覧ください。
1. Surface ドライバーをサポートする、Windows 10 の各バージョンの製品を選択します。 ドライバーの製品には、それぞれ 2 つの異なるバージョンがあることがわかります。

   - Windows 10 "*バージョンの*" **Update and later Servicing Drivers**
   - Windows 10 "*バージョンの*" **Update and later Upgrade & Servicing Drivers**。

     ![Windows 10 バージョンのドライバーの製品一覧](media/surface-driver-products-sup.png)

1. 製品の選択が完了したら、 **[OK]** をクリックします。
1. [ソフトウェアの更新ポイントを同期](../get-started/synchronize-software-updates.md)して、Surface ドライバーを Configuration Manager に取り込みます。
1. Surface ドライバーが同期されたら、他の更新プログラムを展開するときと同じ方法で展開します。

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a> Surface ドライバーの製品

ほとんどのドライバーは、以下の製品グループに属しています。

- Windows 10 and later version drivers
- Windows 10 and later Upgrade & Servicing Drivers
- Windows 10 Anniversary Update and Later Servicing Drivers
- Windows 10 Anniversary Update and Later Upgrade & Servicing Drivers
- Windows 10 Creators Update and Later Servicing Drivers
- Windows 10 Creators Update and Later Upgrade & Servicing Drivers
- Windows 10 Fall Creators Update and Later Servicing Drivers
- Windows 10 Fall Creators Update and Later Upgrade & Servicing Drivers
- Windows 10 S and Later Servicing Drivers
- Windows 10 S Version 1709 and Later Servicing Drivers for testing
- Windows 10 S Version 1709 and Later Upgrade & Servicing Drivers for testing
- Windows 10 S Version 1803 and Later Servicing Drivers
- Windows 10 S Version 1803 and Later Upgrade & Servicing Drivers
- Windows 10 S version 1809 and later, Servicing Drivers
- Windows 10 S version 1809 and later, Upgrade & Servicing Drivers
- Windows 10 S version 1903 and later, Servicing Drivers
- Windows 10 S version 1903 and later, Upgrade & Servicing Drivers
- Windows 10 Version 1803 and Later Servicing Drivers
- Windows 10 Version 1803 and Later Upgrade & Servicing Drivers
- Windows 10 version 1809 and later, Servicing Drivers
- Windows 10 Version 1809 and later, Upgrade & Servicing Drivers
- Windows 10 version 1903 and later, Servicing Drivers
- Windows 10 Version 1903 and later, Upgrade & Servicing Drivers

> [!NOTE]
> ほとんどの Surface ドライバーは、複数の Windows 10 製品グループに属しています。 ここに記載されているすべての製品を選択する必要はありません。 更新プログラム カタログに設定する製品の数を減らすために、ご自分の環境で同期のために必要な製品のみを選択することをお勧めします。

## <a name="surface-models"></a><a name="bkmk_models"></a> Surface モデル

以下の表に、各 Surface モデルと、Configuration Manager でドライバーをインストールできる Windows 10 のバージョンを示します。 Surface ドライバーの更新プログラムは、Microsoft Update カタログに公開された当日に Configuration Manager で使用することはできません。 Configuration Manager では、インポートされる Surface ドライバーについての独自のリストが保持されます。 Windows 10 S 製品が必要なデバイスについての記載があります。 Microsoft では、毎月第 2 火曜日に Surface ドライバーを許可リストに追加して、Configuration Manager に同期できるようにすることを目標としています。 詳細については、[よく寄せられる質問](#bkmk_faq)をご覧ください。

</br>

|Surface モデル|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|はい| はい| はい |はい|はい|
|Surface Pro 4|はい| はい| はい |はい|はい|
|Surface Pro 6|該当なし| はい| はい |はい|はい|
|Surface Pro 7|該当なし| 該当なし| 該当なし |はい|はい|
|Surface Pro X|該当なし| 該当なし| 該当なし |はい|はい|
|Surface Book|はい| はい| はい |はい|はい|
|Surface Book 2|はい| はい| はい |はい|はい|
|Surface Book 3|該当なし| 該当なし| 該当なし |はい|はい|
|Surface Laptop|はい (製品 "Windows 10 S version 1709 and later Servicing drivers" が選択されている場合)| はい (製品 "Windows 10 S version 1803 and later Servicing drivers" が選択されている場合)|はい (製品 "Windows 10 S version 1809 and later Upgrade & Servicing drivers" が選択されている場合)|はい (製品 "Windows 10 S version 1903 and later Upgrade & Servicing drivers" が選択されている場合)|はい (製品 "Windows 10 S version 1903 and later Upgrade & Servicing drivers" が選択されている場合)|
|Surface Laptop 2|該当なし| はい |はい|はい|はい|
|Surface Laptop 3|該当なし| 該当なし|該当なし|はい |はい|
|Surface Go|該当なし| はい (製品 "Windows 10 S version 1803 and later Servicing drivers" が選択されている場合)|はい (製品 "Windows 10 S version 1809 and later Upgrade & Servicing drivers" が選択されている場合)|はい (製品 "Windows 10 S version 1903 and later Upgrade & Servicing drivers" が選択されている場合)|はい (製品 "Windows 10 S version 1903 and later Upgrade & Servicing drivers" が選択されている場合)|
|Surface Go 2|該当なし| 該当なし| はい |はい|はい (製品 "Windows 10 S version 1903 and later Upgrade & Servicing drivers" が選択されている場合)|
|Surface Studio|はい| はい| はい |はい|はい|
|Surface Studio 2|該当なし| はい| はい |はい|はい|

## <a name="verify-the-configuration"></a>構成を確認する

ソフトウェアの更新ポイントが正しく構成されていることを確認するには、**WsyncMgr.log** と **WCM.log** を使用します。

1. WsyncMgr.log を開き、次のログ エントリを確認します。

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. 次のいずれかのエントリが **WsyncMgr.log** に記録されている場合は、ソフトウェアの更新ポイントのプロパティで **[Microsoft Surface のドライバーとファームウェアの更新プログラムを含める]** オプションを選択したことを再確認してください。
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. **WCM.log** を開き、次のエントリに似た項目を探します。
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   このエントリは、ソフトウェアの更新ポイント サーバーによって現在同期されている、すべての製品グループと分類を一覧表示した XML 要素です。 選択した製品が見つからない場合は、ソフトウェアの更新ポイント用の製品が保存されていることを再確認してください。
1. 次の同期が完了するまで待機することもできます。 その後、Surface ドライバーとファームウェアの更新プログラムが、Configuration Manager コンソールの [ソフトウェア更新プログラム] に一覧表示されているかどうかを確認します。 たとえば、コンソールには次のような情報が表示される場合があります。![Configuration Manger コンソールでの同期された Surface ドライバー](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> よく寄せられる質問 (FAQ)

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>この記事の手順に従った後も、Surface ドライバーがまだ同期されていません。 これはなぜでしょうか。

Microsoft Update ではなく、上流の Windows Server Update Services (WSUS) サーバーから同期する場合は、上流の WSUS サーバーが、Surface ドライバーの更新プログラムをサポートし、同期するように構成されていることを確認してください。 すべての下流のサーバーは、上流の WSUS サーバーのデータベースに存在している更新プログラムに制限されます。

WSUS には、ドライバーとして分類されている更新プログラムが 68,000 個以上あります。 Surface と関係ないドライバーが Configuration Manager に同期されないようにするため、Microsoft では、許可リストに対してドライバーの同期がフィルター処理されます。 新しい許可リストが発行されて Configuration Manager に取り込まれると、次の同期の後に新しいドライバーがコンソールに追加されます。 Microsoft では、毎月第 2 火曜日に Surface ドライバーを許可リストに追加して、Configuration Manager に同期できるようにすることを目標としています。

Configuration Manager 環境がオフラインの場合は、お客様が Configuration Manager に[サービス更新プログラム](../../core/servers/manage/use-the-service-connection-tool.md)をインポートするたびに、新しい許可リストがインポートされます。 また、Configuration Manager コンソールに更新プログラムが表示されるようになる前に、ドライバーを含む[新しい WSUS カタログ](../get-started/synchronize-software-updates-disconnected.md)をインポートする必要があります。 スタンドアロンの WSUS 環境には Configuration Manager SUP よりも多くのドライバーが含まれているため、オンライン機能を備えた Configuration Manager 環境を確立し、Surface ドライバーを同期するように構成することをお勧めします。 これにより、オフライン環境によく似た、より小さな WSUS エクスポートが提供されます。

Configuration Manager 環境がオンラインであり、新しい更新プログラムを検出できる場合は、リストの更新が自動的に受信されます。 想定したドライバーが表示されない場合は、WCM.log と WsyncMgr.log で同期エラーを確認してください。

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>自分の Configuration Manager 環境はオフラインですが、Surface ドライバーを手動で WSUS にインポートすることはできますか。

いいえ。 更新プログラムが WSUS にインポートされていても、許可リストに表示されていない場合は、更新プログラムが展開用に Configuration Manager コンソールにインポートされることはありません。 [サービス接続ツール](../../core/servers/manage/use-the-service-connection-tool.md)を使用して Configuration Manager にサービスの更新プログラムをインポートし、許可リストを更新する必要があります。

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>Surface ドライバーとファームウェアの更新プログラムを展開するには、他にどのような方法がありますか。

代替チャネルを使用して Surface ドライバーとファームウェアの更新プログラムを展開する方法の詳細については、[Surface ドライバーとファームウェアの更新プログラムの管理](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates)に関する記事をご覧ください。 .msi または .exe ファイルをダウンロードしてから、従来のソフトウェア展開チャネルを使用して展開する場合は、「[Configuration Manager を使用して Surface のファームウェアを更新された状態に維持する](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager)」をご覧ください。

## <a name="next-steps"></a>次のステップ

Surface ドライバーの詳細については、次の記事を参照してください。

- [Surface と System Center Configuration Manager に関する考慮事項](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Surface の更新履歴](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Surface デバイス用の最新のファームウェアとドライバーをダウンロードする](https://docs.microsoft.com/surface/deploy-the-latest-firmware-and-drivers-for-surface-devices)
