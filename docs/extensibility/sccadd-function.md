---
description: Essa função adiciona novos arquivos ao sistema de controle do código-fonte.
title: Função SccAdd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccAdd
helpviewer_keywords:
- SccAdd function
ms.assetid: 545268f3-8e83-446a-a398-1a9db9e866e8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f654429f8c3faefe05a6410a3c732a6a4b1d083b
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221717"
---
# <a name="sccadd-function"></a>Função SccAdd
Essa função adiciona novos arquivos ao sistema de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccAdd(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LPCSTR    lpComment,
   LONG*     pfOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 nFiles

no Número de arquivos selecionados a serem adicionados ao projeto atual, conforme fornecido na `lpFileNames` matriz.

 lpFileNames

no Matriz de nomes locais totalmente qualificados de arquivos a serem adicionados.

 lpComment

no O comentário a ser aplicado a todos os arquivos que estão sendo adicionados.

 pfOptions

no Matriz de sinalizadores de comando, fornecida por arquivo.

 pvOptions

no Opções específicas de plug-ins de controle do código-fonte.

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A operação de adição foi bem-sucedida.|
|SCC_E_FILEALREADYEXISTS|O arquivo selecionado já está sob controle do código-fonte.|
|SCC_E_TYPENOTSUPPORTED|O tipo de arquivo (por exemplo, Binary) não é suportado pelo sistema de controle do código-fonte.|
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não oferece suporte a essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção. Uma nova tentativa é recomendada.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar esta operação.|
|SCC_E_NONSPECIFICERROR|Falha não específica; adição não executada.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes da conclusão.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|
|SCC_E_FILENOTEXIST|O arquivo local não foi encontrado.|

## <a name="remarks"></a>Comentários
 As `fOptions` Opções usuais são substituídas aqui por uma matriz, `pfOptions` com uma `LONG` especificação de opção por arquivo. Isso ocorre porque o tipo de arquivo pode variar de arquivo para arquivo.

> [!NOTE]
> É inválido especificar as `SCC_FILETYPE_TEXT` `SCC_FILETYPE_BINARY` Opções e para o mesmo arquivo, mas é válido especificar nenhum. A definição de nenhum é igual à configuração `SCC_FILETYPE_AUTO` . nesse caso, o plug-in de controle do código-fonte detecta automaticamente o tipo de arquivo.

 Abaixo está a lista de sinalizadores usados na `pfOptions` matriz:

|Opção|Valor|Significado|
|------------|-----------|-------------|
|SCC_FILETYPE_AUTO|0x00|O plug-in de controle do código-fonte deve detectar o tipo de arquivo.|
|SCC_FILETYPE_TEXT|0x01|Indica um arquivo de texto ASCII.|
|SCC_FILETYPE_BINARY|0x02|Indica um tipo de arquivo diferente de texto ASCII.|
|SCC_ADD_STORELATEST|0x04|Armazena apenas a cópia mais recente do arquivo, sem deltas.|
|SCC_FILETYPE_TEXT_ANSI|0x08|Trata o arquivo como texto ANSI.|
|SCC_FILETYPE_UTF8|0x10|Trata o arquivo como texto Unicode no formato UTF8.|
|SCC_FILETYPE_UTF16LE|0x20|Trata o arquivo como texto Unicode no formato UTF16 little endian.|
|SCC_FILETYPE_UTF16BE|0x40|Trata o arquivo como texto Unicode no formato UTF16 big endian.|

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
