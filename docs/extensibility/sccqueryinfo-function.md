---
description: Essa função obtém informações de status para um conjunto de arquivos selecionados no controle do código-fonte.
title: Função SccQueryInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 369bbd8d783e5d33ea1519b7ad8a4a37476dc62b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904133"
---
# <a name="sccqueryinfo-function"></a>Função SccQueryInfo
Essa função obtém informações de status para um conjunto de arquivos selecionados no controle do código-fonte.

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

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 nFiles

[in] Número de arquivos especificados na `lpFileNames` matriz e o comprimento da `lpStatus` matriz.

 lpFileNames

[in] Uma matriz de nomes de arquivos a serem consultados.

 lpStatus

[in, out] Uma matriz na qual o plug-in de controle do código-fonte retorna os sinalizadores de status para cada arquivo. Para obter mais informações, consulte [Código de status do arquivo](../extensibility/file-status-code-enumerator.md).

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A consulta foi bem-sucedida.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente causado por problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_PROJNOTOPEN|O projeto não está aberto sob controle do código-fonte.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Se `lpFileName` for uma cadeia de caracteres vazia, atualmente não há nenhuma informação de status a ser atualizada. Caso contrário, será o nome de caminho completo do arquivo para o qual as informações de status podem ter sido alteradas.

 A matriz de retorno pode ser um bitmask de `SCC_STATUS_xxxx` bits. Para obter mais informações, consulte [Código de status do arquivo](../extensibility/file-status-code-enumerator.md). Um sistema de controle do código-fonte pode não dar suporte a todos os tipos de bits. Por exemplo, se `SCC_STATUS_OUTOFDATE` não for oferecido, o bit não será definido.

 Ao usar essa função para fazer check-out de arquivos, observe os seguintes `MSSCCI` requisitos de status:

- `SCC_STATUS_OUTBYUSER` é definido quando o usuário atual fez check-out do arquivo.

- `SCC_STATUS_CHECKEDOUT` não pode ser definido, a menos `SCC_STATUS_OUTBYUSER` que esteja definido.

- `SCC_STATUS_CHECKEDOUT` só é definido quando o arquivo faz check-out no diretório de trabalho designado.

- Se o arquivo for verificado pelo usuário atual em um diretório diferente do diretório de trabalho, `SCC_STATUS_OUTBYUSER` será definido, mas `SCC_STATUS_CHECKEDOUT` não será.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)
