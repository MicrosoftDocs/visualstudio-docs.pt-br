---
description: Obtém informações estendidas para a propriedade.
title: 'IDebugProperty2:: GetExtendedInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 004c7d545dbaaa20016fd94febe999420305fc7a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171493"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
Obtém informações estendidas para a propriedade.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetExtendedInfo ( 
   REFGUID* guidExtendedInfo,
   VARIANT* pExtendedInfo
);
```

```csharp
int GetExtendedInfo ( 
   ref Guid guidExtendedInfo,
   out object pExtendedInfo
);
```

## <a name="parameters"></a>Parâmetros
`guidExtendedInfo`\
no GUID que determina o tipo de informações estendidas a serem recuperadas. Consulte Comentários para obter detalhes.

`pExtendedInfo`\
fora Retorna um `VARIANT` (C++) ou um objeto (C#) que pode ser usado para recuperar as informações de propriedade estendida. Por exemplo, esse parâmetro pode retornar uma `IUnknown` interface que pode ser consultada para uma interface [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) . Consulte Comentários para obter detalhes.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro. Retorna `S_GETEXTENDEDINFO_NO_EXTENDEDINFO` se não houver informações estendidas a serem recuperadas.

## <a name="remarks"></a>Comentários
 Esse método existe para a finalidade de recuperar informações que não se prestam para serem recuperadas chamando o método [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) .

 Os GUIDs a seguir são normalmente reconhecidos por esse método (os valores GUID são especificados para C#, pois o nome não está disponível em nenhum assembly). GUIDs adicionais podem ser criados para uso interno.

|Nome|GUID|Descrição|
|----------|----------|-----------------|
|guidDocument|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|Retorna uma `IUnknown` interface para o documento. Normalmente, a interface [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) pode ser obtida por meio desta `IUnknown` interface.|
|guidCodeContext|{e2fc65e-56ce-11d1-b528-00aax004a8797}|Retorna uma `IUnknown` interface para o contexto do documento. Normalmente, a interface [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) pode ser obtida por meio desta `IUnknown` interface.|
|guidCustomViewerSupported|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|Retorna uma cadeia de caracteres que contém o CLSID de um visualizador personalizado, normalmente implementado por um avaliador de expressão.|
|guidExtendedInfoSlot|{6df235ad-82c6-4292-9c97-7389770bc42f}|Retorna um número de 32 bits que representa o número de slot desejado se essa propriedade representar um endereço local de código gerenciado.|
|guidExtendedInfoSignature|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|Retorna uma cadeia de caracteres que contém a assinatura da variável associada ao objeto de propriedade.|

## <a name="see-also"></a>Confira também
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
