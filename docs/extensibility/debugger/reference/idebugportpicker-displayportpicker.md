---
description: Exibe a caixa de diálogo especificada que permite ao usuário selecionar uma porta.
title: IDebugPortPicker::D isplayPortPicker | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- DisplayPortPicker
- IDebugPortPicker::DisplayPortPicker
ms.assetid: 08511ef5-be64-4069-b169-a569cc94bc64
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a49c1379d2bb3946f75eddd9d80bdccdb370d3ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072306"
---
# <a name="idebugportpickerdisplayportpicker"></a>IDebugPortPicker::DisplayPortPicker
Exibe a caixa de diálogo especificada que permite ao usuário selecionar uma porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DisplayPortPicker(
   HWND hwndParentDialog,
   BSTR* pbstrPortId
);
```

```csharp
public int DisplayPortPicker(
   int hwndParentDialog,
   out string pbstrPortId
);
```

## <a name="parameters"></a>Parâmetros
`hwndParentDialog`\
no Identificador da caixa de diálogo pai.

`pbstrPortId`\
fora Cadeia de caracteres do identificador de porta.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Um valor de retorno de `S_FALSE` (ou um valor de retorno de `S_OK` com o `BSTR` definido como `NULL` ) indica que o usuário clicou em **Cancelar**.

## <a name="see-also"></a>Confira também
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
