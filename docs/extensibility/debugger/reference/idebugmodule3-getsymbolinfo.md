---
title: IDebugModule3::GetSymbolInfo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugModule3::GetSymbolInfo
helpviewer_keywords:
- GetSymbolInfo method
- IDebugModule3::GetSymbolInfo method
ms.assetid: dda5e8e1-6878-4aa9-9ee4-e7d0dcc11210
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2e121434f5db1edc1e4c13df3e832cba5be7d471
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49876120"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
Recupera uma lista de caminhos que são pesquisados para símbolos, bem como os resultados da pesquisa de cada caminho.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetSymbolInfo(  
   SYMBOL_SEARCH_INFO_FIELDS  dwFields,  
   MODULE_SYMBOL_SEARCH_INFO* pInfo  
);  
```  
  
```csharp  
int GetSymbolInfo(  
   enum_SYMBOL_SEARCH_INFO_FIELDS dwFields,   
   MODULE_SYMBOL_SEARCH_INFO[]    pinfo  
);  
  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwFields`  
 [in] Uma combinação de sinalizadores do [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) enumeração que especifica quais campos de `pInfo` devem ser preenchidos.  
  
 `pInfo`  
 [out] Um [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) estrutura cujos membros são a ser preenchida com as informações especificadas. Se isso for um valor nulo, esse método retorna `E_INVALIDARG`.  
  
## <a name="return-value"></a>Valor de retorno  
 Se o método for bem-sucedido, ele retorna `S_OK`; caso contrário, ele retorna um código de erro.  
  
> [!NOTE]
>  A cadeia de caracteres retornada (na `MODULE_SYMBOL_SEARCH_INFO` estrutura) pode estar vazio, mesmo se `S_OK` é retornado. Nesse caso, não houve nenhuma informação de pesquisa para retornar.  
  
## <a name="remarks"></a>Comentários  
 Se o `bstrVerboseSearchInfo` campo do `MODULE_SYMBOL_SEARCH_INFO` estrutura não estiver vazia, ele contém uma lista de caminhos pesquisados e os resultados da pesquisa. A lista é formatada com um caminho, seguido por um sinal de reticências (""...), seguido pelo resultado. Se houver mais de um par de resultado do caminho, em seguida, cada par é separado por um par de "\r\n" (carro-retorno/avanço de linha). O padrão tem esta aparência:  
  
 \<caminho >... \<resultado > \r\n\<caminho >... \<resultado > \r\n\<caminho >... \<resultado >  
  
 Observe que a última entrada não tem uma sequência \r\n.  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, esse método retorna três caminhos com três resultados de pesquisa diferentes. Cada linha é encerrada com um par carro-retorno/avanço de linha. A saída de exemplo apenas imprime os resultados da pesquisa como uma única cadeia de caracteres.  
  
> [!NOTE]
>  Um resultado de status é tudo o que imediatamente após o ""... até o final da linha.  
  
```cpp  
void ShowSymbolSearchResults(IDebugModule3 *pIDebugModule3)  
{  
    MODULE_SYMBOL_SEARCH_INFO ssi = { 0 };  
    HRESULT hr;  
    hr = pIDebugModule3->GetSymbolInfo(SSIF_VERBOSE_SEARCH_INFO,&ssi);  
    if (SUCCEEDED(hr)) {  
        CComBSTR searchInfo = ssi.bstrVerboseSearchInfo;  
        if (searchInfo.Length() != 0) {  
            std::wcout << (wchar_t *)(BSTR)searchInfo;  
            std::wcout << std::endl;  
        }  
    }  
}  
```  
  
 **c:\symbols\user32.PDB... Arquivo não encontrado.**  
**c:\winnt\symbols\user32.PDB... Versão não corresponde.**  
**\\\symbols\symbols\user32.dll\0a8sd0ad8ad\user32.PDB... Os símbolos carregados.**   
## <a name="see-also"></a>Consulte também  
 [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)   
 [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)   
 [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)