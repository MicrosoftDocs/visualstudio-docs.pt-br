---
title: 'Idiaframedata:: execute | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaFrameData::execute method
ms.assetid: 7a6c7d03-1ff1-4059-bd54-5f407eeebc26
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 66b8f904ac8add69db0c6d1760b5427cb8c802ae
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49918333"
---
# <a name="idiaframedataexecute"></a>IDiaFrameData::execute
Executa o desenrolamento de pilha e retorna os resultados em uma interface de quadro de movimentação de pilha.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT execute (   
   IDiaStackWalkFrame* frame  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `frame`  
 [in] Uma [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) o objeto que mantém o estado de registradores do quadro.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro. A tabela a seguir mostra os possíveis valores retornados para esse método.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|E_DIA_INPROLOG|Não é possível executar um quadro de pilha no código de prólogo.|  
|E_DIA_SYNTAX|Erro encontrado no programa de quadro de análise.|  
|E_DIA_FRAME_ACCESS|Não é possível a registros de acesso ou memória.|  
|E_DIA_VALUE|Erro no cálculo de um valor (por exemplo, a divisão por zero).|  
  
## <a name="remarks"></a>Comentários  
 Este método é chamado durante a depuração para desenrolar a pilha. O [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md) objeto é implementado pelo aplicativo cliente para receber atualizações para os registros e fornecer métodos usados pelo `execute` método.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)