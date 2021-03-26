---
description: Lê as instruções a partir da posição atual no fluxo de desmontagem.
title: 'IDebugDisassemblyStream2:: Read | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bcabd0cc42f013b579ee32deeb33d68cd9d45f5d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066913"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
Lê as instruções a partir da posição atual no fluxo de desmontagem.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Read( 
   DWORD                     dwInstructions,
   DISASSEMBLY_STREAM_FIELDS dwFields,
   DWORD*                    pdwInstructionsRead,
   DisassemblyData*          prgDisassembly
);
```

```csharp
int Read( 
   uint                           dwInstructions,
   enum_DISASSEMBLY_STREAM_FIELDS dwFields,
   out uint                       pdwInstructionsRead,
   DisassemblyData[]              prgDisassembly
);
```

## <a name="parameters"></a>Parâmetros
`dwInstructions`\
no O número de instruções a serem desmembradas. Esse valor também é o comprimento máximo da `prgDisassembly` matriz.

`dwFields`\
no Uma combinação de sinalizadores da enumeração [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md) que indica quais campos do `prgDisassembly` devem ser preenchidos.

`pdwInstructionsRead`\
fora Retorna o número de instruções realmente desmontadas.

`prgDisassembly`\
fora Uma matriz de estruturas [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) que é preenchida com o código desmontado, uma estrutura por instrução desmontada. O comprimento dessa matriz é determinado pelo `dwInstructions` parâmetro.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O número máximo de instruções disponíveis no escopo atual pode ser obtido chamando o método [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md) .

 A posição atual na qual a próxima instrução é lida pode ser alterada chamando o método [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md) .

 O `DSF_OPERANDS_SYMBOLS` sinalizador pode ser adicionado ao `DSF_OPERANDS` sinalizador no `dwFields` parâmetro para indicar que os nomes de símbolo devem ser usados ao desmontar as instruções.

## <a name="see-also"></a>Confira também
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
