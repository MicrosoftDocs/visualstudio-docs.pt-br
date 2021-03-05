---
description: Essa função obtém informações de status para um conjunto de arquivos selecionados sob controle do código-fonte.
title: Função SccQueryInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 880cb2cf7db5c7a988d6549865de1864cb799e53
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221490"
---
# <a name="sccqueryinfo-function"></a>Função SccQueryInfo
Essa função obtém informações de status para um conjunto de arquivos selecionados sob controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccQueryInfo(
   LPVOID  pvContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPLONG  lpStatus
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 nFiles

no Número de arquivos especificados na `lpFileNames` matriz e o comprimento da `lpStatus` matriz.

 lpFileNames

no Uma matriz de nomes de arquivos a serem consultados.

 lpStatus

[entrada, saída] Uma matriz na qual o plug-in de controle do código-fonte retorna os sinalizadores de status para cada arquivo. Para obter mais informações, consulte [código de status do arquivo](../extensibility/file-status-code-enumerator.md).

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A consulta foi bem-sucedida.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente causado por problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_PROJNOTOPEN|O projeto não está aberto sob controle do código-fonte.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Se `lpFileName` for uma cadeia de caracteres vazia, no momento não há informações de status para atualizar. Caso contrário, é o nome do caminho completo do arquivo para o qual as informações de status podem ter mudado.

 A matriz de retorno pode ser um bitmask de `SCC_STATUS_xxxx` bits. Para obter mais informações, consulte [código de status do arquivo](../extensibility/file-status-code-enumerator.md). Um sistema de controle do código-fonte pode não dar suporte A todos os tipos de bits. Por exemplo, se `SCC_STATUS_OUTOFDATE` não for oferecido, o bit simplesmente não será definido.

 Ao usar essa função para fazer check-out de arquivos, observe os seguintes `MSSCCI` requisitos de status:

- `SCC_STATUS_OUTBYUSER` é definido quando o usuário atual fez o check-out do arquivo.

- `SCC_STATUS_CHECKEDOUT` Não pode ser definido a menos que `SCC_STATUS_OUTBYUSER` esteja definido.

- `SCC_STATUS_CHECKEDOUT` é definido apenas quando o check-out do arquivo é feito no diretório de trabalho designado.

- Se o check-out do arquivo for feito pelo usuário atual em um diretório diferente do diretório de trabalho, o `SCC_STATUS_OUTBYUSER` será definido, mas `SCC_STATUS_CHECKEDOUT` não será.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)
