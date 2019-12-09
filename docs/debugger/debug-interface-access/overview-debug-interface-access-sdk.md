---
title: Visão geral (debug interface Access SDK) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- user-defined types
- .dbg files
- modules
- interfaces [DIA SDK]
- DBG files
- procedures [DIA SDK]
- executable files
- COM objects, in DIA SDK
- compilands
- executable images
ms.assetid: 720b4479-a8bc-4fec-860e-80c1a0780405
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1e4269c620247f256d2cfae2e84b76ff60fcf9ba
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738602"
---
# <a name="overview-debug-interface-access-sdk"></a>Visão geral (SDK de Acesso à Interface de Depuração)
Use o DIA SDK para acessar as informações de depuração da Microsoft. O DIA SDK fornece um conjunto de API baseado em COM que elimina a necessidade de reescrever seu código sempre que a Microsoft alterar o formato das informações de depuração. O DIA SDK também permite que você leia a partir de um conjunto selecionado de versões anteriores de informações de depuração, localizadas nos arquivos. PDB e. dbg gerados pelo [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] versões 5,0 e posteriores.

 Cada interface na DIA SDK representa um objeto COM diferente, exceto quando declarado de outra forma. Interfaces adicionais e, portanto, objetos adicionais, são criadas por meio de consultas explícitas, como [IDiaDataSource:: openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md) ou [IDiaSession:: findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md), em vez de chamar `QueryInterface` em ponteiros de interface existentes.

## <a name="see-also"></a>Consulte também
- [IDiaDataSource::openSession](../../debugger/debug-interface-access/idiadatasource-opensession.md)
- [IDiaSession::findChildren](../../debugger/debug-interface-access/idiasession-findchildren.md)