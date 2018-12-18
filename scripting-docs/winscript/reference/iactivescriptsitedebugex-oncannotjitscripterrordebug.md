---
title: IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptSiteDebugEx.OnCanNotJITScriptErrorDebug
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug
ms.assetid: 83f81476-bf12-47f2-897d-1d37d21137d4
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e428f12b3d199603ac341a5e069fcc5ce5d36f93
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725106"
---
# <a name="iactivescriptsitedebugexoncannotjitscripterrordebug"></a>IActiveScriptSiteDebugEx::OnCanNotJITScriptErrorDebug
Informa o host sobre um erro de tempo de execução do script quando o processo de depurar Gerenciador não encontrar um depurador de script apenas no tempo.  
  
 Para implementar um depurador em seu host, você deve tratar [IActiveScriptSiteDebug::OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md). Com base em uma ação do usuário, o host pode anexar o depurador e retorno ou retornar a partir do depurador no OnScriptErrorDebug `pfEnterDebugger` parâmetro. Você também deve implementar essa interface para receber a notificação sobre o erro de tempo de execução, mesmo se não houver nenhum depuradores externos que podem ser interpretadas pelo Gerenciador de processo de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT OnCanNotJITScriptErrorDebug(  
   IActiveScriptErrorDebug*  pErrorDebug  
   BOOL *pfCallOnScriptErrorWhenContinuing  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pErrorDebug`  
 [in] O erro de tempo de execução que ocorreu.  
  
 `pfCallOnScriptErrorWhenContinuingt`  
 [out] Se a chamada [IActiveScriptSiteDebug::OnScriptErrorDebug](../../winscript/reference/iactivescriptsitedebug-onscripterrordebug.md) se o usuário decidir continuar sem depuração.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Você também deve implementar essa interface para receber uma notificação.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptSiteDebugEx Interface](../../winscript/reference/iactivescriptsitedebugex-interface.md)