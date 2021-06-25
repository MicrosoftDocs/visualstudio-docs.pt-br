---
description: Essa função examina uma lista de diretórios totalmente qualificados para seu status atual.
title: Função SccDirQueryInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDirQueryInfo
helpviewer_keywords:
- SccDirQueryInfo function
ms.assetid: 459e2d99-573d-47c4-b834-6d82c5e14162
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9a3e65fa03c7fc2b6a8ce83ba2bb39250547aadb
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904611"
---
# <a name="sccdirqueryinfo-function"></a>Função SccDirQueryInfo
Essa função examina uma lista de diretórios totalmente qualificados para seu status atual.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccDirQueryInfo(
LPVOID  pContext,
LONG    nDirs,
LPCSTR* lpDirNames,
LPLONG  lpStatus
);
```

### <a name="parameters"></a>Parâmetros
 pContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 nDirs

no O número de diretórios selecionados a serem consultados.

 lpDirNames

no Uma matriz de caminhos totalmente qualificados dos diretórios a serem consultados.

 lpStatus

[entrada, saída] Uma estrutura de matriz para o plug-in de controle do código-fonte para retornar os sinalizadores de status (consulte o [código de status do diretório](../extensibility/directory-status-code-enumerator.md) para obter detalhes).

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A consulta foi bem-sucedida.|
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não oferece suporte a essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 A função preenche a matriz de retorno com um bitmask de bits da `SCC_DIRSTATUS` família (consulte o [código de status do diretório](../extensibility/directory-status-code-enumerator.md)), uma entrada para cada diretório fornecido. A matriz de status é alocada pelo chamador.

 O IDE usa essa função antes que um diretório seja renomeado para verificar se o diretório está sob controle do código-fonte consultando se ele tem um projeto correspondente. Se o diretório não estiver no controle do código-fonte, o IDE poderá fornecer o aviso apropriado ao usuário.

> [!NOTE]
> Se um plug-in de controle do código-fonte optar por não implementar um ou mais dos valores de status, os bits não implementados deverão ser definidos como zero.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Código de status do diretório](../extensibility/directory-status-code-enumerator.md)
