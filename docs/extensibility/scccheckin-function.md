---
description: Essa função faz check-out de arquivos extraídos anteriormente no sistema de controle do código-fonte, armazenando as alterações e criando uma nova versão.
title: Função SccCheckin | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d324c03096df5178decd6f6954928df3f2c6b9aa
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904741"
---
# <a name="scccheckin-function"></a>Função SccCheckin
Essa função faz check-out de arquivos extraídos anteriormente no sistema de controle do código-fonte, armazenando as alterações e criando uma nova versão. Essa função é chamada com uma contagem e uma matriz de nomes dos arquivos nos quais será feito o check-in.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccCheckin (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPSTR*    lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in SCC pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 nFiles

no Número de arquivos selecionados para fazer check-in.

 lpFileNames

no Matriz de nomes de caminho locais totalmente qualificados dos arquivos nos quais fazer check-in.

 lpComment

no Comentário a ser aplicado a cada um dos arquivos selecionados que estão sendo verificados. Esse parâmetro é `NULL` se o plug-in de controle do código-fonte solicitar um comentário.

 fOptions

no Sinalizadores de comando, 0 ou `SCC_KEEP_CHECKEDOUT` .

 pvOptions

no Opções específicas de plug-in SCC.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O check-in do arquivo foi realizado com êxito.|
|SCC_E_FILENOTCONTROLLED|O arquivo selecionado não está no controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR|Falha não específica. O check-in do arquivo não foi feito.|
|SCC_E_NOTCHECKEDOUT|O usuário não fez o check-out do arquivo; portanto, não é possível verificá-lo.|
|SCC_E_CHECKINCONFLICT|O check-in não pôde ser executado porque:<br /><br /> -Outro usuário fez o check-in antecipado e `bAutoReconcile` foi falso.<br /><br /> – ou –<br /><br /> -A mesclagem automática não pode ser feita (por exemplo, quando os arquivos são binários).|
|SCC_E_VERIFYMERGE|O arquivo foi mesclado automaticamente, mas não foi verificado na verificação de usuário pendente.|
|SCC_E_FIXMERGE|O arquivo foi mesclado automaticamente, mas não foi verificado devido a um conflito de mesclagem que deve ser resolvido manualmente.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes da conclusão.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|
|SCC_E_FILENOTEXIST|O arquivo local não foi encontrado.|

## <a name="remarks"></a>Comentários
 O comentário se aplica a todos os arquivos cujo check-in está sendo feito. O argumento comment pode ser uma `null` cadeia de caracteres; nesse caso, o plug-in de controle do código-fonte pode solicitar ao usuário uma cadeia de caracteres de comentário para cada arquivo.

 O `fOptions` argumento pode receber um valor do `SCC_KEEP_CHECKEDOUT` sinalizador para indicar a intenção do usuário de verificar o arquivo e conferir novamente.

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
