---
description: Essa função recupera do controle do código-fonte cada um dos arquivos especificados sem interação do usuário.
title: Função SccBackgroundGet | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccBackgroundGet
helpviewer_keywords:
- SccBackgroundGet function
ms.assetid: 69817e52-b9ac-4f4d-820b-2cc9c384f0dc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4df0866458f04081c82796767808194b292866a1
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102220918"
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

no O ponteiro de contexto do plug-in de controle do código-fonte.

 nFiles

no Número de arquivos especificados na `lpFileNames` matriz.

 lpFileNames

[entrada, saída] Matriz de nomes de arquivos a serem recuperados.

> [!NOTE]
> Os nomes devem ser nomes de filelocais totalmente qualificados.

 dwFlags

no Sinalizadores de comando ( `SCC_GET_ALL` , `SCC_GET_RECURSIVE` ).

 dwBackgroundOperationID

no Um valor exclusivo associado a esta operação.

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Operação concluída com sucesso.|
|SCC_E_BACKGROUNDGETINPROGRESS|Uma recuperação em segundo plano já está em andamento (o plug-in de controle do código-fonte deve retornar somente se não oferecer suporte a operações simultâneas em lote).|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes de ser concluída.|

## <a name="remarks"></a>Comentários
 Essa função é sempre chamada em um thread diferente daquele que carregou o plug-in de controle do código-fonte. Essa função não deve retornar até que seja concluída; no entanto, ele pode ser chamado várias vezes com várias listas de arquivos, tudo ao mesmo tempo.

 O uso do `dwFlags` argumento é o mesmo que o [SccGet](../extensibility/sccget-function.md).

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [SccGet](../extensibility/sccget-function.md)
