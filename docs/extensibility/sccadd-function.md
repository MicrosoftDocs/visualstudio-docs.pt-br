---
description: Essa função adiciona novos arquivos ao sistema de controle do código-fonte.
title: Função SccAdd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccAdd
helpviewer_keywords:
- SccAdd function
ms.assetid: 545268f3-8e83-446a-a398-1a9db9e866e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7f73a91f7f801ca89a633f1722e0c4d1183fb3dc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904845"
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

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 nFiles

[in] Número de arquivos selecionados para serem adicionados ao projeto atual, conforme determinado na `lpFileNames` matriz.

 lpFileNames

[in] Matriz de nomes locais totalmente qualificados de arquivos a serem adicionados.

 lpComment

[in] O comentário a ser aplicado a todos os arquivos que estão sendo adicionados.

 pfOptions

[in] Matriz de sinalizadores de comando, fornecidos por arquivo.

 pvOptions

[in] Opções específicas do plug-in de controle do código-fonte.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A operação de adoção foi bem-sucedida.|
|SCC_E_FILEALREADYEXISTS|O arquivo selecionado já está sob controle do código-fonte.|
|SCC_E_TYPENOTSUPPORTED|O tipo do arquivo (por exemplo, binário) não é suportado pelo sistema de controle do código-fonte.|
|SCC_E_OPNOTSUPPORTED|O sistema de controle do código-fonte não dá suporte a essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_NONSPECIFICERROR|Falha não específica; add não executado.|
|SCC_I_OPERATIONCANCELED|A operação foi cancelada antes da conclusão.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|
|SCC_E_FILENOTEXIST|O arquivo local não foi encontrado.|

## <a name="remarks"></a>Comentários
 O normal `fOptions` é substituído aqui por uma matriz, , por uma `pfOptions` `LONG` especificação de opção por arquivo. Isso porque o tipo de arquivo pode variar de arquivo para arquivo.

> [!NOTE]
> É inválido especificar as opções `SCC_FILETYPE_TEXT` e para o mesmo `SCC_FILETYPE_BINARY` arquivo, mas é válido especificar nenhum deles. A configuração de nenhum dos dois é igual à configuração , caso em que o plug-in do controle do código-fonte faz a detecção automática `SCC_FILETYPE_AUTO` do tipo de arquivo.

 Abaixo está a lista de sinalizadores usados na `pfOptions` matriz:

|Opção|Valor|Significado|
|------------|-----------|-------------|
|SCC_FILETYPE_AUTO|0x00|O plug-in de controle do código-fonte deve detectar o tipo de arquivo.|
|SCC_FILETYPE_TEXT|0x01|Indica um arquivo de texto ASCII.|
|SCC_FILETYPE_BINARY|0x02|Indica um tipo de arquivo diferente do texto ASCII.|
|SCC_ADD_STORELATEST|0x04|Armazena apenas a cópia mais recente do arquivo, sem deltas.|
|SCC_FILETYPE_TEXT_ANSI|0x08|Trata o arquivo como texto ANSI.|
|SCC_FILETYPE_UTF8|0x10|Trata o arquivo como texto Unicode no formato UTF8.|
|SCC_FILETYPE_UTF16LE|0x20|Trata o arquivo como texto Unicode no formato UTF16 Little Endian.|
|SCC_FILETYPE_UTF16BE|0x40|Trata o arquivo como texto Unicode no formato UTF16 Big Endian.|

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
