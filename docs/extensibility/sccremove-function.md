---
description: Essa função exclui arquivos do sistema de controle do código-fonte.
title: Função SccRemove | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccRemove
helpviewer_keywords:
- SccRemove function
ms.assetid: 20830fdc-c0e9-4a5f-bf60-33f28874442f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f4a608b3556040033d9f51535ad29d0abf5d4e35
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904120"
---
# <a name="sccremove-function"></a>Função SccRemove
Essa função exclui arquivos do sistema de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccRemove(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 nFiles

no Número de arquivos especificados na `lpFileNames` matriz.

 lpFileNames

no Matriz de nomes de caminho locais totalmente qualificados de arquivos a serem removidos.

 lpComment

no O comentário a ser aplicado a cada arquivo que está sendo removido.

 fOptions

no Sinalizadores de comando (não utilizados).

 pvOptions

no Opções específicas de plug-ins de controle do código-fonte.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A remoção foi bem-sucedida.|
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está no controle do código-fonte.|
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não oferece suporte a essa operação.|
|SCC_E_ISCHECKEDOUT|Não é possível remover um arquivo porque um usuário o fez check-out no momento.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_E_NONSPECIFICERROR|Falha não específica; o arquivo não foi removido.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes da conclusão.|

## <a name="remarks"></a>Comentários
 Essa função remove os arquivos do sistema de controle do código-fonte, mas não os exclui do disco rígido local do usuário.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
