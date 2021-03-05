---
description: Recupera uma lista de fontes que foram colocadas no repositório de símbolos por provedores de atributos ou outros componentes do processo de compilação.
title: IDiaSession::findInjectedSource | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findInjectedSource method
ms.assetid: 907531b6-1ef8-4153-986d-b72611a1632d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e1604bf91f70f2973dcd394f81569b5ee04e9a99
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147845"
---
# <a name="idiasessionfindinjectedsource"></a>IDiaSession::findInjectedSource
Recupera uma lista de fontes que foram colocadas no repositório de símbolos por provedores de atributos ou outros componentes do processo de compilação.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findInjectedSource ( 
   LPCOLESTR                 srcFile,
   IDiaEnumInjectedSources** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 srcFile

no Nome do arquivo de origem para pesquisa.

 ppResult

fora Retorna um objeto [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) que contém uma lista de todas as fontes injetadas.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
