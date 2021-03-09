---
title: IManagedAddin::Unload
description: Chamado pouco antes de um suplemento do VSTO gerenciado ser descarregado.
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Unload method
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e45fd9e6385388b9c6bc32098cf59799618d511b
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102469704"
---
# <a name="imanagedaddinunload"></a>IManagedAddin::Unload
  Chamado pouco antes de um suplemento do VSTO gerenciado ser descarregado.

## <a name="syntax"></a>Sintaxe

```csharp
HRESULT Unload();
```

## <a name="return-value"></a>Retornar valor
 Um valor HRESULT que indica se o método foi concluído com êxito.

## <a name="remarks"></a>Comentários
 Esse método não é chamado pelas versões atuais do Microsoft Office. Este método está reservado para uso futuro.

## <a name="see-also"></a>Confira também
- [Interface IManagedAddin](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Load](../vsto/imanagedaddin-load.md)
