---
title: POPLISTFUNC | Microsoft Docs
description: Saiba mais sobre a função de retorno de chamada POPLISTFUNC, que é usada pelo plug-in de controle do código-fonte para atualizar uma lista de arquivos ou diretórios.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- POPDIRLISTFUNC
helpviewer_keywords:
- POPLISTFUNC callback function
ms.assetid: b2199fd5-d707-4628-92dd-e2a01e2f507a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b52ed40397793b44f8a9c7ed9c36aa5996ae0176
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900376"
---
# <a name="poplistfunc"></a>POPLISTFUNC
Esse retorno de chamada é fornecido para o [SccPopulateList](../extensibility/sccpopulatelist-function.md) pelo IDE e é usado pelo plug-in de controle do código-fonte para atualizar uma lista de arquivos ou diretórios (também fornecidos para a `SccPopulateList` função).

 Quando um usuário escolhe o comando **Get** no IDE, o IDE exibe uma caixa de listagem de todos os arquivos que o usuário pode obter. Infelizmente, o IDE não conhece a lista exata de todos os arquivos que o usuário pode obter; somente o plug-in tem essa lista. Se outros usuários tiverem adicionado arquivos ao projeto de controle do código-fonte, esses arquivos deverão aparecer na lista, mas o IDE não saberá sobre eles. O IDE cria uma lista dos arquivos que ele acha que o usuário pode obter. Antes de exibir essa lista para o usuário, ela chama o [SccPopulateList](../extensibility/sccpopulatelist-function.md) `,` concedendo ao plug-in de controle do código-fonte a oportunidade de adicionar e excluir arquivos da lista.

## <a name="signature"></a>Assinatura
 O plug-in de controle do código-fonte modifica a lista chamando uma função implementada por IDE com o seguinte protótipo:

```cpp
typedef BOOL (*POPLISTFUNC) (
   LPVOID pvCallerData,
   BOOL fAddRemove,
   LONG nStatus,
   LPSTR lpFileName
);
```

## <a name="parameters"></a>Parâmetros
 pvCallerData o `pvCallerData` parâmetro passado pelo chamador (IDE) para o [SccPopulateList](../extensibility/sccpopulatelist-function.md). O plug-in de controle do código-fonte deve assumir nada sobre o conteúdo desse parâmetro.

 fAddRemove se `TRUE` , `lpFileName` é um arquivo que deve ser adicionado à lista de arquivos. Se `FALSE` , `lpFileName` é um arquivo que deve ser excluído da lista de arquivos.

 nStatus status `lpFileName` (uma combinação de `SCC_STATUS` bits; consulte o [código de status do arquivo](../extensibility/file-status-code-enumerator.md) para obter detalhes).

 lpFileName caminho completo do diretório do nome do arquivo a ser adicionado ou excluído da lista.

## <a name="return-value"></a>Valor retornado

|Valor|Descrição|
|-----------|-----------------|
|`TRUE`|O plug-in pode continuar chamando essa função.|
|`FALSE`|Houve um problema no lado do IDE (como uma situação de memória insuficiente). O plug-in deve parar a operação.|

## <a name="remarks"></a>Comentários
 Para cada arquivo que o plug-in de controle do código-fonte deseja adicionar ou excluir da lista de arquivos, ele chama essa função, passando o `lpFileName` . O `fAddRemove` sinalizador indica um novo arquivo a ser adicionado à lista ou a um arquivo antigo a ser excluído. O `nStatus` parâmetro fornece o status do arquivo. Quando o plug-in SCC terminar de adicionar e excluir arquivos, ele retornará da chamada [SccPopulateList](../extensibility/sccpopulatelist-function.md) .

> [!NOTE]
> O `SCC_CAP_POPULATELIST` bit de funcionalidade é necessário para o Visual Studio.

## <a name="see-also"></a>Confira também
- [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
- [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)
