---
title: IDebugExpressionEvaluator::Parse | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugExpressionEvaluator::Parse
helpviewer_keywords:
- IDebugExpressionEvaluator::Parse method
ms.assetid: e6e31b3a-63a7-4293-bcda-267eb78dffb6
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0f389cd10178a5a5e72f3cb3f909c1fb067baa5e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884272"
---
# <a name="idebugexpressionevaluatorparse"></a>IDebugExpressionEvaluator::Parse
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Esse método converte uma cadeia de caracteres de expressão em uma expressão analisada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT Parse(   
   LPCOLESTR                upstrExpression,  
   PARSEFLAGS               dwFlags,  
   UINT                     nRadix,  
   BSTR*                    pbstrError,  
   UINT*                    pichError,  
   IDebugParsedExpression** ppParsedExpression  
);  
```  
  
```csharp  
int Parse(  
   string                     upstrExpression,   
   enum_PARSEFLAGS            dwFlags,   
   uint                       nRadix,   
   out string                 pbstrError,   
   out uint                   pichError,   
   out IDebugParsedExpression ppParsedExpression  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `upstrExpression`  
 [in] A cadeia de caracteres de expressão a ser analisado.  
  
 `dwFlags`  
 [in] Uma coleção de [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md) constantes que determinam como a expressão deve ser analisados.  
  
 `nRadix`  
 [in] Base a ser usado para interpretar todas as informações numéricas.  
  
 `pbstrError`  
 [out] Retorna o erro como texto legível por humanos.  
  
 `pichError`  
 [out] Retorna a posição do caractere do início do erro na cadeia de caracteres de expressão.  
  
 `ppParsedExpression`  
 [out] Retorna a expressão analisada em um [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Esse método produz uma expressão analisada, não um valor real. Uma expressão analisada está pronta para ser avaliada, ou seja, convertido em um valor.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)   
 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)   
 [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)

