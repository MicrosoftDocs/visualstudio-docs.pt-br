---
description: Representa um provedor de símbolos COM+ com métodos que são específicos do código gerenciado.
title: IDebugComPlusSymbolProvider | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugComPlusSymbolProvider interface
ms.assetid: 5b98e908-fd15-49a6-9010-933c9b948085
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 13541766cdcd6cdd3a0a49673703d6abea82a5c7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094166"
---
# <a name="idebugcomplussymbolprovider"></a>IDebugComPlusSymbolProvider
Representa um provedor de símbolos COM+ com métodos que são específicos do código gerenciado.

## <a name="syntax"></a>Sintaxe

```
IDebugComPlusSymbolProvider : IDebugSymbolProvider
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Embora não haja nenhuma separação entre as interfaces que são úteis para um avaliador de expressão (EE) e aquelas que se destinam a serem usadas por um mecanismo DE depuração (DE), os métodos a seguir provavelmente serão somente juros DE desenvolvedores: AreSymbolsLoaded, GetAddressesInModuleFromPosition, getentrypoint, GetFunctionLineOffset, GetLocalVariableLayout, IsFunctionStale, LoadSymbols, LoadSymbolsFromStream, ReplaceSymbols, UnloadSymbols e UpdateSymbols.

## <a name="methods"></a>Métodos
 Além dos métodos na interface [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) , essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[AreSymbolsLoaded](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-aresymbolsloaded.md)|Determina se os símbolos de depuração são carregados para o módulo especificado, dado o identificador de domínio do aplicativo.|
|[CreateTypeFromPrimitive](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-createtypefromprimitive.md)|Cria um tipo a partir do tipo primitivo especificado.|
|[GetAddressesInModuleFromPosition](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getaddressesinmodulefromposition.md)|Mapeia uma posição de documento no módulo especificado para uma matriz de endereços de depuração.|
|[GetArrayTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getarraytypefromaddress.md)|Recupera informações de tipo sobre a matriz especificada de acordo com seu endereço de depuração.|
|[GetAssemblyName](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getassemblyname.md)|Recupera o nome do assembly de acordo com seu módulo e domínio de aplicativo.|
|[GetAttributedClassesForLanguage](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesforlanguage.md)|Recupera as classes com o atributo especificado que são implementados na linguagem de programação fornecida.|
|[GetAttributedClassesinModule](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getattributedclassesinmodule.md)|Recupera as classes com o atributo especificado em um determinado módulo.|
|[GetEntryPoint](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getentrypoint.md)|Recupera o ponto de entrada do aplicativo.|
|[GetFunctionLineOffset](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getfunctionlineoffset.md)|Recupera o endereço dentro de uma função que representa o deslocamento de linha fornecido.|
|[GetLocalVariablelayout](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getlocalvariablelayout.md)|Recupera o layout de variáveis locais para um conjunto de métodos.|
|[GetNameFromToken](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getnamefromtoken.md)|Retorna o nome associado ao token especificado, dado seu objeto de metadados.|
|[GetSymAttribute](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymattribute.md)|Recupera os símbolos de depuração com o atributo pai fornecido para o módulo especificado.|
|[GetSymUnmanagedReader](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-getsymunmanagedreader.md)|Recupera o leitor de símbolos a ser usado pelo código não gerenciado.|
|[GetTypeFromAddress](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-gettypefromaddress.md)|Recupera para um tipo de símbolo dado seu endereço de depuração.|
|[IsFunctionDeleted](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctiondeleted.md)|Determina se a função no endereço de depuração especificado é excluída.|
|[IsFunctionStale](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-isfunctionstale.md)|Determina se a função no endereço de depuração especificado é considerada obsoleta.|
|[IsHiddenCode](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-ishiddencode.md)|Determina se o código no endereço do depurador especificado está oculto.|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbols.md)|Carrega os símbolos de depuração especificados na memória.|
|[LoadSymbolsFromStream](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-loadsymbolsfromstream.md)|Carrega símbolos de depuração dado o fluxo de dados.|
|[ReplaceSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-replacesymbols.md)|Substitui os símbolos de depuração atuais por aqueles no fluxo de dados especificado.|
|[UnloadSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-unloadsymbols.md)|Descarrega os símbolos de depuração do módulo especificado da memória.|
|[UpdateSymbols](../../../extensibility/debugger/reference/idebugcomplussymbolprovider-updatesymbols.md)|Atualiza os símbolos de depuração na memória com os fluxos de dados especificados.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
