---
description: Essa função desfaz uma operação de check-out anterior, restaurando assim o conteúdo do arquivo ou arquivos selecionados para o estado antes do check-out.
title: Função SccUncheckout | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccUncheckout
helpviewer_keywords:
- SccUncheckout function
ms.assetid: 6d498b70-29c7-44b7-ae1c-7e99e488bb09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3a382a112b5a11acc36c52735c949ebef71052ec
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904081"
---
# <a name="sccuncheckout-function"></a>Função SccUncheckout
Essa função desfaz uma operação de check-out anterior, restaurando assim o conteúdo do arquivo ou arquivos selecionados para o estado antes do check-out. Todas as alterações feitas no arquivo desde o check-out são perdidas.

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

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 nFiles

[in] Número de arquivos especificados na `lpFileNames` matriz.

 lpFileNames

[in] Matriz de nomes de caminho local totalmente qualificados de arquivos para os quais desfazer um check-out.

 fOptions

[in] Sinalizadores de comando (não usados).

 pvOptions

[in] Opções específicas do plug-in de controle do código-fonte.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Desfazer o check-out foi bem-sucedido.|
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está sob controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR|Falha não específica. Desfazer o check-out não foi bem-sucedido.|
|SCC_E_NOTCHECKEDOUT|O usuário não tem o arquivo verificado.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_PROJNOTOPEN|O projeto não foi aberto do controle do código-fonte.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes da conclusão.|

## <a name="remarks"></a>Comentários
 Após essa operação, os sinalizadores e serão limpos para os arquivos nos quais `SCC_STATUS_CHECKEDOUT` `SCC_STATUS_MODIFIED` o check-out de desfazer foi executado.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
