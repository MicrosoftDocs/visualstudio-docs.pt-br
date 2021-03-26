---
description: Retorna informações que permitem a construção de uma mensagem de erro legível por humanos.
title: 'IDebugErrorEvent2:: GetErrorMessage | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2::GetErrorMessage
helpviewer_keywords:
- IDebugErrorEvent2::GetErrorMessage
ms.assetid: 9e3b0d74-a2dd-4eaa-bd95-21b2f9c79409
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a0ab15c0f232695dbc017d80f666154e5c35a8fd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065769"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
Retorna informações que permitem a construção de uma mensagem de erro legível por humanos.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetErrorMessage(
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrErrorFormat,
   HRESULT*     hrErrorReason,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetErrorMessage(
   out enum_MESSAGETYPE   pMessageType,
   out string             pbstrErrorFormat,
   out int                phrErrorReason,
   out uint               pdwType,
   out string             pbstrHelpFileName,
   out uint               pdwHelpId
);
```

## <a name="parameters"></a>Parâmetros
`pMessageType`\
fora Retorna um valor da enumeração [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) , que descreve o tipo de mensagem.

`pbstrErrorFormat`\
fora O formato da mensagem final para o usuário (consulte "Comentários" para obter detalhes).

`hrErrorReason`\
fora O código de erro para a mensagem é sobre.

`pdwType`\
fora Severidade do erro (use as constantes MB_XXX para `MessageBox` ; por exemplo, `MB_EXCLAMATION` ou `MB_WARNING` ).

`pbstrHelpFileName`\
fora Caminho para um arquivo de ajuda (definido como um valor nulo se não houver nenhum arquivo de ajuda).

`pdwHelpId`\
fora ID do tópico da ajuda a ser exibido (definido como 0 se não houver nenhum tópico da ajuda).

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A mensagem de erro deve ser formatada ao longo das linhas de `"What I was doing.  %1"` . O `"%1"` seria então substituído pelo chamador pela mensagem de erro derivada do código de erro (que é retornado em `hrErrorReason` ). O `pMessageType` parâmetro informa ao chamador como a mensagem de erro final deve ser exibida.

## <a name="see-also"></a>Confira também
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
