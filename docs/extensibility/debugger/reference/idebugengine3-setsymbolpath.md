---
description: Define o caminho ou caminhos que são pesquisados para símbolos de depuração.
title: 'IDebugEngine3:: SetSymbolPath | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetSymbolPath
helpviewer_keywords:
- IDebugEngine3::SetSymbolPath
ms.assetid: 47b48f84-8a96-401f-84df-0baa8a96d26e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f3bc24aa6ae07505f4f1fce16593f11e44e752a9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066107"
---
# <a name="idebugengine3setsymbolpath"></a>IDebugEngine3::SetSymbolPath
Define o caminho ou caminhos que são pesquisados para símbolos de depuração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetSymbolPath (
   LPOLESTR            szSymbolSearchPath,
   LPOLESTR            szSymbolCachePath,
   LOAD_SYMBOLS_FLAGS  Flags
);
```

```csharp
int SetSymbolPath(
   string                    szSymbolSearchPath,
   string                    szSymbolCachePath,
   enum_LOAD_SYMBOLS_FLAGS   Flags
);
```

## <a name="parameters"></a>Parâmetros

`szSymbolSearchPath`\
no Cadeia de caracteres que contém o caminho de pesquisa de símbolo ou caminhos. Consulte "Comentários" para obter detalhes. Não pode ser nulo.

`szSymbolCachePath`\
no Cadeia de caracteres que contém o caminho local onde os símbolos podem ser armazenados em cache. Não pode ser nulo.

`Flags`\
no Não usado; sempre definido como 0.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A cadeia `szSymbolSearchPath` de caracteres é uma lista de um ou mais caminhos, separados por ponto-e-vírgula, para procurar por símbolos. Esses caminhos podem ser um caminho local, um caminho de estilo UNC ou uma URL. Esses caminhos também podem ser uma combinação de tipos diferentes. Se o caminho for UNC (por exemplo, \\ \Symserver\Symbols), o mecanismo de depuração deverá determinar se o caminho é para um servidor de símbolos e deve ser capaz de carregar símbolos desse servidor, armazenando-os no caminho especificado por `szSymbolCachePath` .

 O caminho do símbolo também pode conter um ou mais locais de cache. Os caches são listados em ordem de prioridade, com o cache de prioridade mais alta primeiro e separados por símbolos *. Por exemplo:

```
\\symbols\symbols;\\someotherserver\symbols;c:\symbols\httpsymbols*https://msdl.microsoft.com
```

 O método [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md) executa a carga real dos símbolos.

## <a name="see-also"></a>Confira também
- [LoadSymbols](../../../extensibility/debugger/reference/idebugengine3-loadsymbols.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
