---
description: Essa função recupera do controle do código-fonte cada um dos arquivos especificados sem interação do usuário.
title: Função SccBackgroundGet | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 316a02e84b4d51f309aecdd98d0409c85ccbdbef
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901234"
---
# <a name="sccbackgroundget-function"></a>Função SccBackgroundGet
Essa função recupera do controle do código-fonte cada um dos arquivos especificados sem interação do usuário.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccBackgroundGet(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LONG    dwFlags,
   LONG    dwBackgroundOperationID
);
```

### <a name="parameters"></a>Parâmetros
 pContext

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 nFiles

[in] Número de arquivos especificados na `lpFileNames` matriz.

 lpFileNames

[in, out] Matriz de nomes de arquivos a serem recuperados.

> [!NOTE]
> Os nomes devem ser nomes de arquivo locais totalmente qualificados.

 dwFlags

[in] Sinalizadores de comando ( `SCC_GET_ALL` , `SCC_GET_RECURSIVE` ).

 dwBackgroundOperationID

[in] Um valor exclusivo associado a esta operação.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Operação concluída com sucesso.|
|SCC_E_BACKGROUNDGETINPROGRESS|Uma recuperação em segundo plano já está em andamento (o plug-in de controle do código-fonte deve retornar isso somente se ele não dá suporte a operações simultâneas em lote).|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes de ser concluída.|

## <a name="remarks"></a>Comentários
 Essa função sempre é chamada em um thread diferente do que carregou o plug-in de controle do código-fonte. Essa função não deve retornar até que seja feita; no entanto, ele pode ser chamado várias vezes com várias listas de arquivos, tudo ao mesmo tempo.

 O uso do `dwFlags` argumento é o mesmo que o [SccGet](../extensibility/sccget-function.md).

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
