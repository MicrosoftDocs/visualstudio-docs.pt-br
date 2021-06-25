---
description: Dada uma lista de arquivos locais, essa função determina quais arquivos são diferentes das versões correspondentes no banco de dados de controle do código-fonte.
title: Função SccEnumChangedFiles | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2b0707c049013fd3a0272d1f024e4fdbc342bab1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904533"
---
# <a name="sccenumchangedfiles-function"></a>Função SccEnumChangedFiles
Dada uma lista de arquivos locais, essa função determina quais arquivos são diferentes das versões correspondentes no banco de dados de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccEnumChangedFiles(
   LPVOID  pContext,
   HWND    hWnd,
   LONG    cFiles,
   LPCSTR* lpFileNames,
   LONG*   plIsFileDifferent
);
```

### <a name="parameters"></a>Parâmetros
 pContext

[in] O ponteiro de contexto do plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 cFiles

[in] Número de nomes de arquivo especificados na `lpFileNames` matriz. Também especifica o tamanho da `plIsFileDifferent` matriz.

 lpFileNames

[in] Matriz de nomes de arquivo local a verificar.

 plIsFileDifferent

[in, out] Matriz de valores que indicam o status de diferença de cada arquivo (a matriz deve ter pelo menos `cFiles` entradas). Diferente de zero significa que o arquivo é diferente.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Operação concluída com sucesso.|
|SCC_UNSPECIFIEDERROR|Erro genérico.|

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
