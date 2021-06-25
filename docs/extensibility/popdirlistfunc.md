---
title: POPDIRLISTFUNC | Microsoft Docs
description: Saiba mais sobre a função de retorno de chamada POPDIRLISTFUNC, que é passada para diretórios de atualização para descobrir quais estão sob controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- POPLISTFUNC
helpviewer_keywords:
- POPDIRLISTFUNC callback function
ms.assetid: 0ee90fd2-5467-4154-ab4c-7eb02ac3a14c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c98b35d9f915e16072333c72df2e1e045850f5d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900389"
---
# <a name="popdirlistfunc"></a>POPDIRLISTFUNC
Essa é uma função de retorno de chamada fornecida para a função [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) para atualizar uma coleção de diretórios e (opcionalmente) nomes de arquivos para descobrir quais estão sob controle do código-fonte.

 O `POPDIRLISTFUNC` retorno de chamada deve ser chamado somente para os diretórios e nomes de arquivo (na lista fornecida para a `SccPopulateDirList` função) que estão na verdade no controle do código-fonte.

## <a name="signature"></a>Assinatura

```cpp
typedef BOOL (*POPDIRLISTFUNC)(
   LPVOID pvCallerData,
   BOOL bFolder,
   LPCSTR lpDirectoryOrFileName
);
```

## <a name="parameters"></a>Parâmetros
 pvCallerData

no Valor de usuário fornecido a [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md).

 bFolder

[in] `TRUE` Se o nome no `lpDirectoryOrFileName` for um diretório; caso contrário, o nome será um nome de arquivo.

 lpDirectoryOrFileName

no Caminho local completo para um diretório ou nome de arquivo que está sob controle do código-fonte.

## <a name="return-value"></a>Valor retornado
 O IDE retorna um código de erro apropriado:

|Valor|Descrição|
|-----------|-----------------|
|SCC_OK|Continuar o processamento.|
|SCC_I_OPERATIONCANCELED|Pare o processamento.|
|SCC_E_xxx|Qualquer erro de controle do código-fonte apropriado deve parar de processar.|

## <a name="remarks"></a>Comentários
 Se o `fOptions` parâmetro da `SccPopulateDirList` função contiver o `SCC_PDL_INCLUDEFILES` sinalizador, a lista provavelmente conterá nomes de arquivo, bem como nomes de diretório.

## <a name="see-also"></a>Confira também
- [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)
- [Códigos de erro](../extensibility/error-codes.md)
