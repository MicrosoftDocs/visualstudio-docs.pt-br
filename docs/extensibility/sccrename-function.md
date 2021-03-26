---
description: Essa função renomeia um arquivo no sistema de controle do código-fonte.
title: Função SccRename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccRename
helpviewer_keywords:
- SccRename function
ms.assetid: b467ade6-a1db-4c0b-b60f-7850ec4f79eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d9d42e796f1ec2176e9de79ca392aab070581324
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073827"
---
# <a name="sccrename-function"></a>Função SccRename
Essa função renomeia um arquivo no sistema de controle do código-fonte.

## <a name="syntax"></a>Sintaxe

```cpp
SCCRTN SccRename(
   LPVOID pvContext,
   HWND   hWnd,
   LPCSTR lpFileName,
   LPCSTR lpNewName
);
```

#### <a name="parameters"></a>Parâmetros
 pvContext

no A estrutura de contexto do plug-in de controle do código-fonte.

 hWnd

no Um identificador para a janela do IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornecer.

 lpFileName

no O nome de arquivo totalmente qualificado do arquivo que está sendo renomeado.

 lpNewName

no O novo nome totalmente qualificado. Se o caminho do diretório for diferente, o arquivo terá sido movido de um subdiretório para outro.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação de plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A operação de renomeação foi concluída com êxito.|
|SCC_E_PROJNOTOPEN|O projeto não está aberto sob controle do código-fonte.|
|SCC_E_FILENOTCONTROLLED|O arquivo não está no controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou de contenção.|
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado a concluir esta operação.|
|SCC_E_COULDNOTCREATEPROJECT|Não foi possível criar o projeto como parte do processo de renomeação.|
|SCC_E_OPNOTPERFORMED|A operação não foi executada.|
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado ou geral.|

## <a name="remarks"></a>Comentários
 Essa função pode ser usada para renomear um arquivo ou movê-lo de um local para outro no sistema de controle do código-fonte. O plug-in de controle do código-fonte não deve tentar acessar o arquivo no disco. É responsabilidade do IDE renomear o arquivo local.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
