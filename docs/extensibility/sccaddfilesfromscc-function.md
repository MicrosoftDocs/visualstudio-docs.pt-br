---
description: Essa função adiciona uma lista de arquivos do controle do código-fonte ao projeto aberto no momento.
title: Função SccAddFilesFromSCC | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccAddFilesFromSCC
helpviewer_keywords:
- SccAddFilesFromSCC function
ms.assetid: f21a3500-ade8-4dd8-8647-10e2179be9c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fa08ec93383fa661d1e2dd055b3139b2ba90f34
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904858"
---
# <a name="sccaddfilesfromscc-function"></a>Função SccAddFilesFromSCC
Essa função adiciona uma lista de arquivos do controle do código-fonte ao projeto aberto no momento.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccAddFilesFromSCC(
   LPVOID  pContext,
   HWND    hWnd,
   LPSTR   lpUser,
   LPSTR   lpAuxProjPath,
   LONG    cFiles,
   LPCSTR* lpFilePaths,
   LPCSTR  lpDestination,
   LPCSTR  lpComment,
   LPBOOL  pbResults
);
```

### <a name="parameters"></a>Parâmetros
 pContext

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 lpUser

[in, out] O nome de usuário (até SCC_USER_SIZE, incluindo o terminador nulo).

 lp LpProjPath

[in, out] Cadeia de caracteres auxiliar que identifica o projeto (até `SCC_PRJPATH_` SIZE, incluindo o terminador nulo).

 cFiles

[in] Número de arquivos determinados por `lpFilePaths` .

 lpFilePaths

[in, out] Matriz de nomes de arquivo a adicionar ao projeto atual.

 lpDestination

[in] O caminho de destino em que os arquivos devem ser gravados.

 lpComment

[in] O comentário a ser aplicado a cada um dos arquivos que estão sendo adicionados.

 pbResults

[in, out] Matriz de sinalizadores que são definidos para indicar êxito (não zero ou TRUE) ou falha (zero ou FALSE) para cada arquivo (o tamanho da matriz deve ser pelo menos `cFiles` longo).

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_E_PROJNOTOPEN|O projeto não está aberto.|
|SCC_E_OPNOTPERFORMED|A conexão não é para o mesmo projeto especificado por `lpAuxProjPath.`|
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado a atualizar o banco de dados.|
|SCC_E_NONSPECIFICERROR|Erro desconhecido.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
