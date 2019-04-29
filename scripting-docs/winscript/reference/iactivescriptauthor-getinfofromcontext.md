---
title: IActiveScriptAuthor::GetInfoFromContext | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IActiveScriptAuthor.GetInfoFromContext
apilocation:
- scrobj.dll
helpviewer_keywords:
- IActiveScriptAuthor::GetInfoFromContext
ms.assetid: 9891b095-6eb5-4473-87c0-c2e5cd2afc1a
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e4fe885e116019608dd8d748c3cbdaff5d31dd2a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62935380"
---
# <a name="iactivescriptauthorgetinfofromcontext"></a>IActiveScriptAuthor::GetInfoFromContext
Retorna informações e as posições de âncora para um determinado caractere de tipo em um bloco de código. Isso fornece informações de membro IntelliSense, listas globais e dicas de parâmetro.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetInfoFromContext(  
   LPCOLESTR  pszCode,  
   ULONG      cchCode,  
   ULONG      ichCurrentPosition,  
   DWORD      dwListTypesRequested,  
   DWORD      *pdwListTypesProvided,  
   ULONG      *pichListAnchorPosition,  
   ULONG      *pichFuncAnchorPosition,  
   MEMBERID   *pmemid,  
   LONG       *piCurrentParameter,  
   IUnknown   **ppunk  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszCode`  
 [in] O endereço da cadeia de caracteres de bloco de código usado para gerar os resultados de informações.  
  
 `cchCode`  
 [in] O tamanho do bloco de código.  
  
 `ichCurrentPosition`  
 [in] Posição do caractere em relação ao início do bloco.  
  
 `dwListTypesRequested`  
 [in] Os tipos de lista solicitados. Pode ser uma combinação dos seguintes valores:  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|SCRIPT_CMPL_NOLIST|0x0000|Nenhuma lista.|  
|SCRIPT_CMPL_MEMBERLIST|0x0001|Lista de membros.|  
|SCRIPT_CMPL_ENUMLIST|0x0002|Lista de enumeração.|  
|SCRIPT_CMPL_PARAMLIST|0x0004|Chame a lista de parâmetros de método.|  
|SCRIPT_CMPL_GLOBALLIST|0x0008|Lista global.|  
  
 O tipo SCRIPT_CMPL_GLOBALLIST é tratado como um item de preenchimento padrão que pode ser combinado usando o operador OR com outros itens de conclusão. O script do mecanismo de criação primeiro tenta preencher as informações de tipo para outros itens de lista de conclusão. Se isso falhar, o mecanismo preenche para SCRIPT_CMPL_GLOBALLIST.  
  
 `pdwListTypesProvided`  
 [out] O tipo de lista fornecida.  
  
 `pichListAnchorPosition`  
 [out] O índice inicial do contexto que contém a posição atual. O índice inicial é relativo ao início do bloco.  
  
 Esse campo é preenchido somente quando `dwListTypesRequested` inclui SCRIPT_CMPL_MEMBERLIST, SCRIPT_CMPL_ENUMLIST ou SCRIPT_CMPL_GLOBALLIST. Para outros tipos de lista solicitada, o resultado será indefinido.  
  
 `pichFuncAnchorPosition`  
 [out] O índice de início da chamada de função que contém a posição atual. O índice inicial é relativo ao início do bloco.  
  
 Esse campo é preenchido somente quando o contexto que contém a posição atual é uma chamada de função e quando `dwListTypesRequested` inclui SCRIPT_CMPL_PARAMLIST. Caso contrário, o resultado será indefinido.  
  
 `pmemid`  
 [out] O MEMBERID da função, conforme definido por um tipo no `IProvideMultipleClassInfo``ppunk` parâmetro out.  
  
 Esse campo é preenchido somente quando `dwListTypesRequested` inclui SCRIPT_CMPL_PARAMLIST.  
  
 `piCurrentParameter`  
 [out] O índice do parâmetro que contém a posição atual. Se a posição atual está no nome da função, -1 será retornado.  
  
 O `piCurrentParameter` valor é preenchido somente quando `dwListTypesRequested` inclui SCRIPT_CMPL_PARAMLIST.  
  
 `ppunk`  
 As informações de tipo, que são fornecidas na forma de um `IProvideMultipleClassInfo` objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Interface IProvideMultipleClassInfo](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.ole.interop.iprovidemultipleclassinfo)   
 [IActiveScriptAuthor Interface](../../winscript/reference/iactivescriptauthor-interface.md)