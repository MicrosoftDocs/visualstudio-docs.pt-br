---
description: Esse método é chamado para exibir o valor especificado.
title: IDebugCustomViewer::D isplayvalue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer::DisplayValue
helpviewer_keywords:
- IDebugCustomViewer::DisplayValue
ms.assetid: 7a538248-5ced-450e-97cd-13fabe35fb1c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 238bb4f9b453513f2fdcccb628eacdfc9ef4ae2b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173475"
---
# <a name="idebugcustomviewerdisplayvalue"></a>IDebugCustomViewer::DisplayValue
Esse método é chamado para exibir o valor especificado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DisplayValue(
   HWND             hwnd,
   DWORD            dwID,
   IUnknown *       pHostServices,
   IDebugProperty3* pDebugProperty);
);
```

```csharp
int DisplayValue(
   IntPtr          hwnd,
   uint            dwID,
   object          pHostServices,
   IDebugProperty3 pDebugProperty
);
```

## <a name="parameters"></a>Parâmetros
`hwnd`\
no Janela pai

`dwID`\
no ID para visualizadores personalizados que dão suporte a mais de um tipo.

`pHostServices`\
[in] Reservado. Sempre definido como nulo.

`pDebugProperty`\
no Interface que pode ser usada para recuperar o valor a ser exibido.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro.

## <a name="remarks"></a>Comentários
 A exibição é "modal", pois esse método criará a janela necessária, exibirá o valor, aguardará a entrada e fechará a janela, tudo antes de retornar ao chamador. Isso significa que o método deve lidar com todos os aspectos da exibição do valor da propriedade, desde a criação de uma janela para saída até a espera da entrada do usuário, a destruição da janela.

 Para dar suporte à alteração do valor no objeto [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) fornecido, você pode usar o método [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md) — se o valor puder ser expresso como uma cadeia de caracteres. Caso contrário, é necessário criar uma interface personalizada — exclusiva para o avaliador de expressão que implementa esse `DisplayValue` método — no mesmo objeto que implementa a `IDebugProperty3` interface. Essa interface personalizada forneceria métodos para alterar os dados de um tamanho ou complexidade arbitrária.

## <a name="see-also"></a>Confira também
- [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)
