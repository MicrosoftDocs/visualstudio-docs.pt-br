---
title: IDiaLoadCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLoadCallback interface
ms.assetid: 2f18c64c-2cf0-43fc-a447-21e82702ca2a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 435dc337ea3f1caad2ad99031d9be872d80337e2
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85466717"
---
# <a name="idialoadcallback"></a>IDiaLoadCallback
Recebe retornos de chamada do procedimento de localização de símbolo de DIA, permitindo assim que uma interface do usuário relate o progresso da tentativa de localização.

## <a name="syntax"></a>Syntax

```
IDiaLoadCallback : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Os métodos a seguir são expostos por essa interface:

|Método|Descrição|
|------------|-----------------|
|[IDiaLoadCallback::NotifyDebugDir](../../debugger/debug-interface-access/idialoadcallback-notifydebugdir.md)|Chamado quando um diretório de depuração foi encontrado no arquivo. exe.|
|[IDiaLoadCallback::NotifyOpenDBG](../../debugger/debug-interface-access/idialoadcallback-notifyopendbg.md)|Chamado quando um arquivo Candidate. dbg é aberto.|
|[IDiaLoadCallback::NotifyOpenPDB](../../debugger/debug-interface-access/idialoadcallback-notifyopenpdb.md)|Chamado quando um arquivo Candidate. pdb é aberto.|
|[IDiaLoadCallback::RestrictRegistryAccess](../../debugger/debug-interface-access/idialoadcallback-restrictregistryaccess.md)|Determina se as consultas do registro podem ser usadas para localizar caminhos de pesquisa de símbolos.|
|[IDiaLoadCallback::RestrictSymbolServerAccess](../../debugger/debug-interface-access/idialoadcallback-restrictsymbolserveraccess.md)|Determina se o acesso é permitido para um servidor de símbolos para resolver símbolos.|

## <a name="remarks"></a>Comentários
 O aplicativo cliente implementa essa interface e fornece uma referência a ela na chamada para o método [IDiaDataSource:: loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md) .

 Para obter restrições adicionais que podem ser impostas em um processo de carregamento, consulte a interface [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: dia2. h

 Biblioteca: diaguids. lib

 DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaDataSource::loadDataForExe](../../debugger/debug-interface-access/idiadatasource-loaddataforexe.md)
- [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)
- [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)
- [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)