---
title: Função SccWillCreateSccFile | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccWillCreateSccFile
helpviewer_keywords:
- SccWillCreateSccFile function
ms.assetid: 0d7542f0-4351-41b3-b24c-960ab99c05a1
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1fa85c8a96f17508d2e2e53a8d14444dd857dad0
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56715161"
---
# <a name="sccwillcreatesccfile-function"></a>Função SccWillCreateSccFile
Esta função determina se o plug-in de controle do código-fonte suporta a criação do MSSCCPRJ. Arquivos SCC para cada um dos arquivos de determinado.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccWillCreateSccFile(
   LPVOID  pContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPBOOL  pbSccFiles
);
```

#### <a name="parameters"></a>Parâmetros
 pContext

[in] O ponteiro de contexto de plug-in de controle do código-fonte.

 nFiles

[in] O número de nomes de arquivos incluídos na `lpFileNames` matriz, bem como o comprimento do `pbSccFiles` matriz.

 lpFileNames

[in] Uma matriz de nomes de arquivo totalmente qualificado para verificar (matriz deve ser alocada pelo chamador).

 pbSccFiles

[no, out] Matriz na qual armazenar os resultados.

## <a name="return-value"></a>Valor de retorno
 A implementação de plug-in de controle do código-fonte desta função deve retornar um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Êxito.|
|SCC_E_INVALIDFILEPATH|Um dos caminhos na matriz é inválido.|
|SCC_E_NONSPECIFICERROR|Falha não específica.|

## <a name="remarks"></a>Comentários
 Essa função é chamada com uma lista de arquivos para determinar se o plug-in de controle do código-fonte fornece suporte no MSSCCPRJ. Arquivos SCC para cada um dos arquivos de determinado (para obter mais informações sobre o MSSCCPRJ. Arquivos SCC, consulte [MSSCCPRJ. Arquivos SCC](../extensibility/mssccprj-scc-file.md)). Plug-ins de controle de origem pode declarar se eles têm a capacidade de criar MSSCCPRJ. Arquivos SCC, declarando `SCC_CAP_SCCFILE` durante a inicialização. O plug-in retorna `TRUE` ou `FALSE` por arquivo no `pbSccFiles` matriz para indicar quais arquivos de determinado têm MSSCCPRJ. Suporte do SCC. Se o plug-in retorna um código de êxito da função, os valores na matriz de retorno são respeitados. Em caso de falha, a matriz é ignorada.

## <a name="see-also"></a>Consulte também
- [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
- [Arquivo MSSCCPRJ.SCC](../extensibility/mssccprj-scc-file.md)