---
description: Recupera os arquivos de origem por compiland e nome.
title: IDiaSession::findFile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findFile method
ms.assetid: a215dc21-b316-40d7-9923-55bfa014976b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: af547f9e504e9d832968bd18a370cb43e816e786
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159002"
---
# <a name="idiasessionfindfile"></a>IDiaSession::findFile
Recupera os arquivos de origem por compiland e nome.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findFile ( 
   IDiaSymbol*           pCompiland,
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumSourceFiles** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `pCompiland`

no Um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o compiland a ser usado como um contexto para a pesquisa. Defina esse parâmetro como `NULL` para localizar os arquivos de origem em todos os compilandos.

 `name`

no Especifica o nome do arquivo de origem a ser recuperado. Defina esse parâmetro como `NULL` para todos os arquivos de origem a serem recuperados.

 `option`

no Especifica as opções de comparação aplicadas à pesquisa de nomes. Os valores da enumeração de [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md) podem ser usados sozinhos ou em combinação.

 `ppResult`

fora Retorna um objeto [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md) que contém uma lista dos arquivos de origem recuperados.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="example"></a>Exemplo

```C++
IDiaEnumSourceFiles* pEnum;
pSession->findFile( NULL, L"sourcefile.cpp", nsFNameExt, &pEnum );
```

## <a name="see-also"></a>Confira também
- [IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md)
