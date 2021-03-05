---
description: Essa função Desfaz uma operação de check-out anterior, restaurando assim o conteúdo do arquivo ou dos arquivos selecionados para o estado anterior ao check-out.
title: Função SccUncheckout | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 33e0c4904a92d71e000d8c911d551eb8d0aab621
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221347"
---
# <a name="sccuncheckout-function"></a>Função SccUncheckout
Essa função Desfaz uma operação de check-out anterior, restaurando assim o conteúdo do arquivo ou dos arquivos selecionados para o estado anterior ao check-out. Todas as alterações feitas no arquivo desde que o check-out são perdidas.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccUncheckout (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
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

no Matriz de nomes de caminho locais totalmente qualificados de arquivos para os quais desfazer um check-out.

 fOptions

no Sinalizadores de comando (não usados).

 pvOptions

no Opções específicas de plug-ins de controle do código-fonte.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A ação de desfazer o check-out foi bem-sucedida.|
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está no controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR|Falha não específica. Desfazer o check-out não teve sucesso.|
|SCC_E_NOTCHECKEDOUT|O usuário não fez check-out do arquivo.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_E_PROJNOTOPEN|O projeto não foi aberto do controle do código-fonte.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes da conclusão.|

## <a name="remarks"></a>Comentários
 Após essa operação, os `SCC_STATUS_CHECKEDOUT` `SCC_STATUS_MODIFIED` sinalizadores e serão limpos para os arquivos nos quais o check-out de desfazer foi executado.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
