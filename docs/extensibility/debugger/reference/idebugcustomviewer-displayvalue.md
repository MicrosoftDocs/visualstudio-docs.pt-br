---
title: IDebugCustomViewer::DisplayValue | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugCustomViewer::DisplayValue
helpviewer_keywords:
- IDebugCustomViewer::DisplayValue
ms.assetid: 7a538248-5ced-450e-97cd-13fabe35fb1c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 44295cb6cc3635d099a93ef62c7d4ae4e2bdd4cd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49833831"
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
  
#### <a name="parameters"></a>Parâmetros  
 `hwnd`  
 [in] Janela pai  
  
 `dwID`  
 [in] ID para visualizadores personalizados que dão suporte a mais de um tipo.  
  
 `pHostServices`  
 [in] Reservado. Sempre definido como null.  
  
 `pDebugProperty`  
 [in] Interface que pode ser usado para recuperar o valor a ser exibido.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará o código de erro.  
  
## <a name="remarks"></a>Comentários  
 A exibição é "modal" em que esse método criar a janela necessária, exibir o valor, aguarda a entrada e fechar a janela, todos antes de retornar ao chamador. Isso significa que o método deve tratar todos os aspectos de exibir o valor da propriedade, desde a criação de uma janela de saída, para aguardar entrada do usuário, a destruição de janela.  
  
 Para dar suporte à alteração do valor na determinada [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) objeto, você pode usar o [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md) método — se o valor pode ser expresso como uma cadeia de caracteres. Caso contrário, será necessário criar uma interface personalizada — exclusiva para o avaliador de expressão implementar isso `DisplayValue` método — no mesmo objeto que implementa o `IDebugProperty3` interface. Essa interface personalizada fornece métodos para alterar os dados de um tamanho arbitrário ou complexidade.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [SetValueAsStringWithError](../../../extensibility/debugger/reference/idebugproperty3-setvalueasstringwitherror.md)