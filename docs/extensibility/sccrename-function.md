---
description: Essa função renomeia um arquivo no sistema de controle do código-fonte.
title: Função SccRename | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: fb3fa392cd4ed31d907fe5913f8d7965a20df05b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900454"
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

[in] A estrutura de contexto de plug-in do controle do código-fonte.

 hWnd

[in] Um alça para a janela IDE que o plug-in de controle do código-fonte pode usar como um pai para qualquer caixa de diálogo que ele fornece.

 Lpfilename

[in] O nome de arquivo totalmente qualificado do arquivo que está sendo renomeado.

 lpNewName

[in] O novo nome totalmente qualificado. Se o caminho do diretório for diferente, o arquivo foi movido de um subdiretório para outro.

## <a name="return-value"></a>Valor Retornado
 Espera-se que a implementação do plug-in de controle do código-fonte dessa função retorne um dos seguintes valores:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|A operação de renomeação foi concluída com êxito.|
|SCC_E_PROJNOTOPEN|O projeto não está aberto sob controle do código-fonte.|
|SCC_E_FILENOTCONTROLLED|O arquivo não está sob controle do código-fonte.|
|SCC_E_ACCESSFAILURE|Houve um problema ao acessar o sistema de controle do código-fonte, provavelmente devido a problemas de rede ou contenção.|
|SCC_E_NOTAUTHORIZED|O usuário não está autorizado a concluir essa operação.|
|SCC_E_COULDNOTCREATEPROJECT|Não foi possível criar o projeto como parte do processo de renomeação.|
|SCC_E_OPNOTPERFORMED|A operação não foi executada.|
|SCC_E_NONSPECIFICERROR|Ocorreu um erro não especificado ou geral.|

## <a name="remarks"></a>Comentários
 Essa função pode ser usada para renomear um arquivo ou movê-lo de um local para outro no sistema de controle do código-fonte. O plug-in de controle do código-fonte não deve tentar acessar o arquivo no disco. É responsabilidade do IDE renomear o arquivo local.

## <a name="see-also"></a>Confira também
- [Funções de API de plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)
