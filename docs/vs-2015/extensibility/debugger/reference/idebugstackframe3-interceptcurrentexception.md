---
title: IDebugStackFrame3::InterceptCurrentException | Microsoft Docs
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
- IDebugStackFrame3::InterceptCurrentException
helpviewer_keywords:
- IDebugStackFrame3::InterceptCurrentException
ms.assetid: 116c7324-7645-4c15-b484-7a5cdd065ef5
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0dde6935a343d7ba915bd7d3954c4462056be851
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781641"
---
# <a name="idebugstackframe3interceptcurrentexception"></a>IDebugStackFrame3::InterceptCurrentException
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Chamado pelo depurador no quadro de pilhas atual quando quer interceptar a exceção atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT InterceptCurrentException(  
   INTERCEPT_EXCEPTION_ACTION dwFlags,  
   UINT64*                    pqwCookie  
);  
```  
  
```csharp  
int InterceptCurrentException(  
   uint dwFlags,   
   out  ulong pqwCookie  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwFlags`  
 [in] Especifica as ações diferentes. Atualmente, apenas o [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md) valor `IEA_INTERCEPT` tem suporte e deve ser especificado.  
  
 `pqwCookie`  
 [out] Valor exclusivo que identifica uma exceção específica.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará S_OK; Caso contrário, retornará um código de erro.  
  
 A seguir estão os retornos de erro mais comuns.  
  
|Erro|Descrição|  
|-----------|-----------------|  
|`E_EXCEPTION_CANNOT_BE_INTERCEPTED`|A exceção atual não pode ser interceptada.|  
|`E_EXCEPTION_CANNOT_UNWIND_ABOVE_CALLBACK`|O quadro atual da execução não tiver sido pesquisados à procura um manipulador ainda.|  
|`E_INTERCEPT_CURRENT_EXCEPTION_NOT_SUPPORTED`|Esse método não tem suporte para este quadro.|  
  
## <a name="remarks"></a>Comentários  
 Quando uma exceção é lançada, o depurador assume o controle de tempo de execução nos pontos-chave durante o processo de tratamento de exceções. Durante esses momentos cruciais, o depurador pode pedir o quadro de pilhas atual se o quadro Quer interceptar a exceção. Dessa forma, uma exceção interceptada é essencialmente um manipulador de exceção do sistema em funcionamento para um quadro de pilha, mesmo que esse quadro de pilha não tem um manipulador de exceção (por exemplo, um bloco try/catch no código do programa).  
  
 Quando o depurador quer saber se a exceção deve ser interceptada, ele chama esse método no objeto de quadro de pilha atual. Esse método é responsável por gerenciar todos os detalhes da exceção. Se o [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md) interface não está implementada ou a `InterceptStackException` método retorna qualquer erro e, em seguida, o depurador continua o processamento de exceção normalmente.  
  
> [!NOTE]
>  Exceções podem ser interceptadas apenas em código gerenciado, ou seja, quando o programa que está sendo depurado está em execução em tempo de execução .NET. Obviamente, os implementadores de linguagem de terceiros podem implementar `InterceptStackException` em seus próprios mecanismos de depuração se desejarem.  
  
 Depois que a interceptação for concluída, uma [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) é sinalizado.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)   
 [INTERCEPT_EXCEPTION_ACTION](../../../extensibility/debugger/reference/intercept-exception-action.md)   
 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)

