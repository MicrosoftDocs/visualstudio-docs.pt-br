---
description: Chamado quando um diretório de depuração foi encontrado no arquivo. exe.
title: IDiaLoadCallback::NotifyDebugDir | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback::NotifyDebugDir method
ms.assetid: bd04e2f6-0dbf-4742-a556-96f2cd99aa19
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ed83b79dea8f488be79a2161968876c9aa2a9a11
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102148279"
---
# <a name="idialoadcallbacknotifydebugdir"></a>IDiaLoadCallback::NotifyDebugDir
Chamado quando um diretório de depuração foi encontrado no arquivo. exe.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT NotifyDebugDir ( 
   BOOL  fExecutable,
   DWORD cbData,
   BYTE  data[]
);
```

#### <a name="parameters"></a>Parâmetros
 `fExecutable`

[in] `TRUE` Se o diretório de depuração for lido a partir de um executável (em vez de um arquivo. dbg).

 `cbData`

no Contagem de bytes de dados no diretório de depuração.

 `data[]`

no Uma matriz que é preenchida com o diretório de depuração.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. O código de retorno é normalmente ignorado.

## <a name="remarks"></a>Comentários
 O método [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) invoca esse retorno de chamada quando ele encontra um diretório de depuração durante o processamento do arquivo executável.

 Esse método remove a necessidade do cliente de fazer a engenharia reversa do arquivo executável e/ou de depuração para dar suporte a informações de depuração diferentes das encontradas no arquivo. pdb. Com esses dados, o cliente pode reconhecer o tipo de informações de depuração disponíveis e se ele reside no arquivo executável ou no arquivo. dbg.

 A maioria dos clientes não precisará desse retorno de chamada, pois o `IDiaDataSource::loadDataForExe` método abre de forma transparente os arquivos. PDB e. dbg quando necessário para atender aos símbolos.

## <a name="see-also"></a>Confira também
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
