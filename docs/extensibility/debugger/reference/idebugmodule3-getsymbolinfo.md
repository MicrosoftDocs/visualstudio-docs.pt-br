---
description: Recupera uma lista de caminhos que são pesquisados em busca de símbolos, bem como os resultados da pesquisa de cada caminho.
title: 'IDebugModule3:: GetSymbolInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::GetSymbolInfo
helpviewer_keywords:
- GetSymbolInfo method
- IDebugModule3::GetSymbolInfo method
ms.assetid: dda5e8e1-6878-4aa9-9ee4-e7d0dcc11210
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9cc4c8d7c88e4b973ad7055327da73472a6ed4d2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065522"
---
# <a name="idebugmodule3getsymbolinfo"></a>IDebugModule3::GetSymbolInfo
Recupera uma lista de caminhos que são pesquisados em busca de símbolos, bem como os resultados da pesquisa de cada caminho.

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

## <a name="parameters"></a>Parâmetros
`dwFields`\
no Uma combinação de sinalizadores da enumeração [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md) especificando quais campos do `pInfo` devem ser preenchidos.

`pInfo`\
fora Uma estrutura de [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md) cujos membros devem ser preenchidos com as informações especificadas. Se esse for um valor nulo, esse método retornará `E_INVALIDARG` .

## <a name="return-value"></a>Valor Retornado
Se o método tiver sucesso, ele retornará `S_OK` ; caso contrário, ele retornará um código de erro.

> [!NOTE]
> A cadeia de caracteres retornada (na `MODULE_SYMBOL_SEARCH_INFO` estrutura) pode estar vazia mesmo se `S_OK` for retornada. Nesse caso, não havia informações de pesquisa a serem retornadas.

## <a name="remarks"></a>Comentários
Se o `bstrVerboseSearchInfo` campo da `MODULE_SYMBOL_SEARCH_INFO` estrutura não estiver vazio, ele conterá uma lista de caminhos pesquisados e os resultados dessa pesquisa. A lista é formatada com um caminho, seguido por uma elipse ("..."), seguida pelo resultado. Se houver mais de um par de resultados de caminho, cada par será separado por um par "\r\n" (retorno de carro/alimentação de discagem). O padrão tem a seguinte aparência:

\<path>...\<result> \r\n \<path> . \<result> .. \r\n \<path> ...\<result>

Observe que a última entrada não tem uma sequência \r\n.

## <a name="example"></a>Exemplo
Neste exemplo, esse método retorna três caminhos com três resultados de pesquisa diferentes. Cada linha é encerrada com um par de retorno de carro/alimentação de linha. A saída de exemplo apenas imprime os resultados da pesquisa como uma única cadeia de caracteres.

> [!NOTE]
> Um resultado de status é tudo imediatamente após o "..." até o fim da linha.

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

**c:\symbols\user32.pdb... Arquivo não encontrado.** 
 **c:\winnt\symbols\user32.pdb... A versão não corresponde.** 
 **\\\symbols\symbols\user32.dll \0a8sd0ad8ad\user32.pdb... Símbolos carregados.**

## <a name="see-also"></a>Confira também

- [SYMBOL_SEARCH_INFO_FIELDS](../../../extensibility/debugger/reference/symbol-search-info-fields.md)
- [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
