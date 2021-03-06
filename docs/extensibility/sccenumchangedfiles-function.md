---
description: Dada uma lista de arquivos locais, essa função determina quais arquivos são diferentes das versões correspondentes no banco de dados de controle do código-fonte.
title: Função SccEnumChangedFiles | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccEnumChangedFiles
helpviewer_keywords:
- SccEnumChangedFiles function
ms.assetid: 76cac510-107b-4c1a-ba60-9c39b6db2e71
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9349172ac60f1e02f82327424cdbc3a3b1d4f865
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102221529"
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

no O ponteiro de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 recfiles

no Número de nomes de arquivo especificados na `lpFileNames` matriz. Também especifica o tamanho da `plIsFileDifferent` matriz.

 lpFileNames

no Matriz de nomes de arquivos locais a serem verificados.

 plIsFileDifferent

[entrada, saída] Matriz de valores que indica o status de diferença de cada arquivo (a matriz deve ter pelo menos `cFiles` entradas). Zero significa que o arquivo é diferente.

## <a name="return-value"></a>Retornar valor
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Operação concluída com sucesso.|
|SCC_UNSPECIFIEDERROR|Erro genérico.|

## <a name="see-also"></a>Confira também
- [Funções da API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
