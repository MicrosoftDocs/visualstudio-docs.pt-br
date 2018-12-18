---
title: IScriptNode::CreateChildHandler | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptNode.CreateChildHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptNode::CreateChildHandler
ms.assetid: 4ce5eb10-1a3f-43b0-a4b7-599a397ed3a2
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ff2ba40d1570e23f0256bd34ca8aff0f8d77ce5c
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729556"
---
# <a name="iscriptnodecreatechildhandler"></a>IScriptNode::CreateChildHandler
Adiciona um miniscript como uma instância de filho de um `IScriptNode`.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CreateChildHandler(  
   LPCOLESTR          pszDefaultName,  
   LPCOLESTR          *prgpszNames,  
   ULONG              cpszNames,  
   LPCOLESTR          pszEvent,  
   LPCOLESTR          pszDelimiter,  
   ITypeInfo*         ptiSignature,  
   ULONG              iMethodSignature,  
   ULONG              isn,  
   DWORD              dwCookie,  
   IScriptEntry       **ppse  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszDefaultName`  
 [in] O endereço do nome padrão para associar o miniscript.  
  
 `prgpszNames`  
 [in, size_is (`cpszNames`)] uma lista de identificadores do nome totalmente qualificado no host.  
  
 `cpszNames`  
 [in] O número de identificadores de `prgpszNames` parâmetro.  
  
 `pszEvent`  
 [in] O endereço do buffer que identifica o nome do evento associado com o miniscript.  
  
 `pszDelimiter`  
 [in] O endereço do delimitador final do bloco de script. Para análise, o host normalmente usa um delimitador (como duas aspas simples), para detectar o final do bloco de script.  
  
 O delimitador permite pré-processamento pelo script do mecanismo de criação. Por exemplo, o mecanismo pode substituir uma aspa simples por duas aspas simples para uso como um delimitador. O mecanismo determina como o delimitador é usado.  
  
 Definido como NULL se nenhum delimitador é usado para identificar o fim do bloco de script.  
  
 `ptiSignature`  
 [in] As informações de tipo para um objeto de função.  
  
 `iMethodSignature`  
 [in] O índice da função de `ITypeInfo``ptiSignature` parâmetro.  
  
 `isn`  
 [in] O índice do filho no pai.  
  
 `dwCookie`  
 [in] Um valor definido pelo aplicativo que é usado para associar a entrada com o objeto de host.  
  
 `ppse`  
 [out] O endereço de uma variável que recebe um ponteiro para o `IScriptEntry` interface da instância filho.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Um miniscript Especifica um manipulador de eventos. Esse método cria um miniscript se ele for chamado por um `IScriptNode` objeto que representa uma página da Web. Este método não tem êxito se ele é chamado de outras interfaces.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IScriptNode](../../winscript/reference/iscriptnode-interface.md)   
 [IScriptEntry Interface](../../winscript/reference/iscriptentry-interface.md)