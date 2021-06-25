---
title: Enumerador de código de status de arquivo | Microsoft Docs
description: O enumerador SccStatus contém valores constantes que especificam o estado de um arquivo no sistema de controle do código-fonte e são usados por SccQueryInfo e POPLISTFUNC.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- named constants, SccStatus enumerator
- source control plug-ins, file status enumeration
- SccStatus enumerator
- file status code enumerator
ms.assetid: 5c37876b-c83c-4ca1-837b-57cd465a879a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 95de8a29efcd56880cdaf452c9f21b90bba1c5c9
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900961"
---
# <a name="file-status-code-enumerator"></a>Enumerador de código de status de arquivo
O `SccStatus` enumerador contém valores constantes nomeados que especificam o estado de um arquivo no sistema de controle do código-fonte. Essa enumeração é usada pelo [SccQueryInfo](../extensibility/sccqueryinfo-function.md) e pela `POPLISTFUNC` função de retorno de chamada (consulte [POPLISTFUNC](../extensibility/poplistfunc.md) para obter detalhes).

## <a name="syntax"></a>Sintaxe

```
enum SccStatus {
   SCC_STATUS_INVALID          = -1L,
   SCC_STATUS_NOTCONTROLLED    = 0x0000L,
   SCC_STATUS_CONTROLLED       = 0x0001L,
   SCC_STATUS_CHECKEDOUT       = 0x0002L,
   SCC_STATUS_OUTOTHER         = 0x0004L,
   SCC_STATUS_OUTEXCLUSIVE     = 0x0008L,
   SCC_STATUS_OUTMULTIPLE      = 0x0010L,
   SCC_STATUS_OUTOFDATE        = 0x0020L,
   SCC_STATUS_DELETED          = 0x0040L,
   SCC_STATUS_LOCKED           = 0x0080L,
   SCC_STATUS_MERGED           = 0x0100L,
   SCC_STATUS_SHARED           = 0x0200L,
   SCC_STATUS_PINNED           = 0x0400L,
   SCC_STATUS_MODIFIED         = 0x0800L,
   SCC_STATUS_OUTBYUSER        = 0x1000L
   SCC_STATUS_NOMERGE          = 0x2000L
   SCC_STATUS_RESERVED_1       = 0x4000L
   SCC_STATUS_RESERVED_2       = 0x8000L
};
```

## <a name="members"></a>Membros
 Não foi possível obter SCC_STATUS_INVALID status; Não confie nela.

 SCC_STATUS_NOTCONTROLLED arquivo não está no controle do código-fonte.

 SCC_STATUS_CONTROLLED arquivo está sob controle do código-fonte.

 SCC_STATUS_CHECKEDOUT check-out feito pelo usuário atual no disco local.

 O check-out do arquivo do SCC_STATUS_OUTOTHER foi feito por outro usuário.

 O check-out exclusivo do arquivo de SCC_STATUS_OUTEXCLUSIVE foi feito.

 O check-out do arquivo de SCC_STATUS_OUTMULTIPLE é feito por mais de um usuário.

 SCC_STATUS_OUTOFDATE o arquivo não é o mais recente.

 SCC_STATUS_DELETED arquivo foi excluído do projeto.

 SCC_STATUS_LOCKED arquivo está bloqueado; Não há mais nenhuma versão permitida.

 SCC_STATUS_MERGED arquivo foi mesclado, mas ainda não foi corrigido/verificado.

 SCC_STATUS_SHARED arquivo é compartilhado entre projetos.

 SCC_STATUS_PINNED arquivo é compartilhado para uma versão explícita.

 SCC_STATUS_MODIFIED arquivo foi modificado/interrompido/violado.

 O check-out do arquivo do SCC_STATUS_OUTBYUSER foi feito pelo usuário atual.

 SCC_STATUS_NOMERGE arquivo nunca pode ser mesclado com o e não precisa ser salvo antes de um GET.

 SCC_STATUS_RESERVED_1 reservado para uso interno.

 SCC_STATUS_RESERVED_2 reservado para uso interno.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [SccQueryInfo](../extensibility/sccqueryinfo-function.md)
- [POPLISTFUNC](../extensibility/poplistfunc.md)
