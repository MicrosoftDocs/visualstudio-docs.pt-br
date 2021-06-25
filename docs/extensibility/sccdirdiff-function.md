---
description: Essa função exibe as diferenças entre o diretório local atual no disco do cliente e o projeto correspondente no controle do código-fonte.
title: Função SccDirDiff | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccDirDiff
helpviewer_keywords:
- SccDirDiff function
ms.assetid: 26c9ba92-e3b9-4dd2-bd5e-76b17745e308
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e938cdaedf8541d787673371cfce3d07e005711f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904637"
---
# <a name="sccdirdiff-function"></a>Função SccDirDiff
Essa função exibe as diferenças entre o diretório local atual no disco do cliente e o projeto correspondente no controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccDirDiff(
   LPVOID    pContext,
   HWND      hWnd,
   LPCSTR    lpDirName,
   LONG      dwFlags,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>Parâmetros
 pContext

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 lpDirName

[in] Caminho totalmente qualificado para o diretório local para o qual mostrar uma diferença visual.

 dwFlags

[in] Sinalizadores de comando (consulte a seção Comentários).

 pvOptions

[in] Opções específicas do plug-in de controle do código-fonte.

## <a name="return-value"></a>Valor retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|O diretório no disco é o mesmo que o projeto no controle do código-fonte.|
|SCC_I_FILESDIFFER|O diretório no disco é diferente do projeto no controle do código-fonte.|
|SCC_I_RELOADFILE|Um arquivo ou projeto precisa ser recarregado.|
|SCC_E_FILENOTCONTROLLED|O diretório não está sob controle do código-fonte.|
|SCC_E_NOTAUTHORIZED|O usuário não tem permissão para executar essa operação.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção. Uma nova tentativa é recomendada.|
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|Falha não específica.|
|SCC_E_FILENOTEXIST|Não foi possível encontrar o diretório local.|

## <a name="remarks"></a>Comentários
 Essa função é usada para instruir o plug-in de controle do código-fonte a exibir ao usuário uma lista de alterações em um diretório especificado. O plug-in abre sua própria janela, em um formato de sua escolha, para exibir as diferenças entre o diretório do usuário no disco e o projeto correspondente sob controle de versão.

 Se um plug-in for compatível com a comparação de diretórios, ele deverá dar suporte à comparação de diretórios em uma base de nome de arquivo, mesmo que as opções de "comparação rápida" não sejam compatíveis.

|`dwFlags`|Interpretação|
|---------------|--------------------|
|SCC_DIFF_IGNORECASE|Comparação que não diferencia maiúsculas de minúsculas (pode ser usada para comparação rápida ou visual).|
|SCC_DIFF_IGNORESPACE|Ignora o espaço em branco (pode ser usado para comparação rápida ou visual).|
|SCC_DIFF_QD_CONTENTS|Se for suportado pelo plug-in de controle do código-fonte, compara silenciosamente o diretório byte byte.|
|SCC_DIFF_QD_CHECKSUM|Se o plug-in tiver suporte, o comparará silenciosamente o diretório por meio de uma verificação ou, se não tiver suporte, retornará para SCC_DIFF_QD_CONTENTS.|
|SCC_DIFF_QD_TIME|Se o plug-in tiver suporte, o comparará silenciosamente o diretório por meio de seu timestamp ou, se não tiver suporte, retornará SCC_DIFF_QD_CHECKSUM ou SCC_DIFF_QD_CONTENTS.|

> [!NOTE]
> Essa função usa os mesmos sinalizadores de comando que [o SccDiff](../extensibility/sccdiff-function.md). No entanto, um plug-in de controle do código-fonte pode optar por não dar suporte à operação de "comparação rápida" para diretórios.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
