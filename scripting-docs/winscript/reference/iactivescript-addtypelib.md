---
title: IActiveScript::AddTypeLib | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScript.AddTypeLib
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScript_AddTypeLib
ms.assetid: 8e507ea8-c80a-471c-b482-ae753c6e8595
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a2be7cf033b4b5dd4d99b19a3b71ed53e32af855
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24640866"
---
# <a name="iactivescriptaddtypelib"></a>IActiveScript::AddTypeLib
Adiciona uma biblioteca de tipos para o espaço de nome para o script. Isso é semelhante de `#include` diretiva em C/C++. Ele permite que um conjunto de itens predefinidos, como definições de classe, `typedefs`e constantes a serem adicionadas ao ambiente de tempo de execução disponível para o script nomeadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT AddTypeLib(  
    REFGUID guidTypeLib,  // CLSID of type library  
    DWORD dwMaj,          // major version number  
    DWORD dwMin,          // minor version number  
    DWORD dwFlags         // option flags  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `guidTypeLib`  
 [in] CLSID do tipo de biblioteca para adicionar.  
  
 `dwMaj`  
 [in] Número de versão principal.  
  
 `dwMin`  
 [in] Número de versão secundária.  
  
 `dwFlags`  
 [in] Sinalizadores de opção. Pode ser o seguinte:  
  
|Valor|Significado|  
|-----------|-------------|  
|SCRIPTTYPELIB_ISCONTROL|A biblioteca de tipos descreve um controle ActiveX usado pelo host.|  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um dos seguintes valores:  
  
|Valor de retorno|Significado|  
|------------------|-------------|  
|`S_OK`|Êxito.|  
|`E_INVALIDARG`|Um argumento era inválido.|  
|`E_UNEXPECTED`|A chamada não era esperada (por exemplo, o mecanismo de script ainda não foi carregado ou inicializado).|  
|`TYPE_E_CANTLOADLIBRARY`|Não foi possível carregar a biblioteca de tipo especificado.|  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScript](../../winscript/reference/iactivescript.md)