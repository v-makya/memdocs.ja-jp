---
title: 工場出荷時の OEM、または現地保管場所用のイメージの作成
titleSuffix: Configuration Manager
description: 事前設定されたメディアによる展開を使用して、完全にはプロビジョニングされていないコンピューターに OS を展開する際のネットワーク トラフィックを軽減します。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15145cccf73e517d0e49444fbdaf834de342865e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125442"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Configuration Manager を使用した工場出荷時の OEM 用、または現地保管場所用のイメージの作成

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager における事前設定されたメディアによる展開では、完全にはプロビジョニングされていないコンピューターに OS を展開できます。 事前設定されたメディアは、Windows イメージ (WIM) ファイルです。 製造元 (OEM) はそれをベアメタル コンピューターにインストールできます。あるいは運用環境とは別のステージング センターで使用できます。

ブート イメージと OS イメージが展開先のコンピューターに存在するので、この展開の方法はネットワーク トラフィックを軽減します。 事前設定メディアにも含めるようにアプリケーション、パッケージ、ドライバー パッケージを指定できます。 コンピューターに OS がインストールされると、タスク シーケンスではまず、事前設定されたキャッシュにアプリケーション、パッケージ、またはドライバー パッケージがないか確認されます。 必要なコンテンツが見つからない場合、あるいは最新の改訂がオンラインにある場合、タスク シーケンスによって、配布ポイントからコンテンツがダウンロードされます。

事前設定されたメディアは、次の OS の展開シナリオで使用します。

- [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)

- [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md)

いずれかの OS の展開シナリオの手順を完了します。 その後、次のセクションを使用して、事前設定メディアの準備と作成を行います。

## <a name="configure-deployment-settings"></a>展開の設定の構成

展開の **[展開の設定]** ページの **[利用できるようにする項目]** の設定で、次のいずれかのオプションを選択します。

- Configuration Manager クライアント、メディア、PXE

- メディアと PXE のみ

- メディアと PXE のみ (非表示)

## <a name="create-the-prestaged-media"></a>事前設定メディアの作成

OEM または現地保管場所に送信する事前設定メディア ファイルを作成します。 詳細については、[Configuration Manager を使用した事前設定されたメディアの作成](create-prestaged-media.md)に関する記事を参照してください。

## <a name="send-the-prestaged-media-file"></a>事前設定メディアの送信

コンピューター上で事前設定する目的で OEM または現地保管場所にメディアを送信します。 そこで、コンピューター上のフォーマットされたハード ディスクにイメージ ファイルが適用されます。

## <a name="deliver-the-computer"></a>コンピューターの配送

コンピューターをユーザーに届け、初めて電源を入れると:

1. コンピューターは、事前設定されたブート イメージで起動します。

1. 事前設定メディアでハッシュを確認し、それが有効であることを確認します。

1. コンピューターは管理ポイントに接続し、利用できるタスク シーケンスを探し、プロセスを完了します。

## <a name="next-steps"></a>次のステップ

[OS 展開のユーザー エクスペリエンス](../understand/user-experience.md)
