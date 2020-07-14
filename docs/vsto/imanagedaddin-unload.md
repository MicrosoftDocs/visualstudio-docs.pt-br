---
title: IManagedAddin::Unload
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Unload method
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 1ec01ebc32472e315fe2c905ecfd2cfef0f4bbe1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541005"
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

## <a name="see-also"></a>Consulte também
- [Interface IManagedAddin](../vsto/imanagedaddin-interface.md)
- [IManagedAddin::Load](../vsto/imanagedaddin-load.md)
