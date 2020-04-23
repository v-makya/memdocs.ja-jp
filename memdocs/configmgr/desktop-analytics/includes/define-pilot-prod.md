---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708220"
---
パイロットと運用を区別するには、次の定義を使用します。  

- **パイロット**:より大きなセットに展開する前に検証するデバイスのサブセットです。 Desktop Analytics を使用して、パイロット セットに固有としてデバイスをマークします。 資産がブロックされていない場合、パイロットのデバイスはアップグレードする準備ができています。 ブロックしている資産は、"*重大*" および "*アップグレードできません*" としてマークされています。  

- **Production**:Desktop Analytics に登録されているその他のデバイスはすべて、パイロットに含まれません。 すべての資産がサインオフされている場合、運用デバイスはアップグレードする準備ができています。 Desktop Analytics によって、重大ではない資産は自動的にサインオフされます。  

