---
title: IDebugDocumentPosition2::GetRange | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugDocumentPosition2::GetRange
helpviewer_keywords:
- IDebugDocumentPosition2::GetRange
ms.assetid: 91a06ee7-253a-4215-be22-04bf57305aa8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 839e6be66ead2a5c76047f40de6142c669667673
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49882417"
---
# <a name="idebugdocumentposition2getrange"></a>IDebugDocumentPosition2::GetRange
Obtém o intervalo para essa posição do documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetRange(   
   TEXT_POSITION* pBegPosition,  
   TEXT_POSITION* pEndPosition  
);  
```  
  
```csharp  
int GetRange(   
   TEXT_POSITION[] pBegPosition,  
   TEXT_POSITION[] pEndPosition  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pBegPosition`  
 [no, out] Um [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) estrutura será preenchida com a posição inicial. Defina este argumento como um valor nulo se essa informação não é necessária.  
  
 `pEndPosition`  
 [no, out] Um [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) estrutura será preenchida com a posição final. Defina este argumento como um valor nulo se essa informação não é necessária.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 O intervalo especificado em uma posição de documento para um ponto de interrupção de local é usado pelo mecanismo de depuração (DE) para procurar uma instrução que contribui, na verdade, o código com antecedência. Por exemplo, considere o seguinte código:  
  
```  
Line 5: // comment  
Line 6: x = 1;  
```  
  
 Linha 5 contribui com nenhum código para o programa que está sendo depurado. Se quiser que o depurador que define o ponto de interrupção na linha 5 DE para pesquisar adiante uma certa quantidade para a primeira linha que contribui com o código, o depurador seria especificar um intervalo que inclui linhas de candidato adicional em que um ponto de interrupção pode ser colocado corretamente. O DE, em seguida, pesquisaria para frente por meio dessas linhas até que ela encontrou uma linha que poderia aceitar um ponto de interrupção.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)