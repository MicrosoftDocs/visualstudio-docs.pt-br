---
title: POPLISTFUNC | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- POPDIRLISTFUNC
helpviewer_keywords:
- POPLISTFUNC callback function
ms.assetid: b2199fd5-d707-4628-92dd-e2a01e2f507a
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 83e54cf1b0e6f15b1a6c5dc0af379a8b88bd77f4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63434233"
---
# <a name="poplistfunc"></a>POPLISTFUNC
Esse retorno de chamada é fornecido para o [SccPopulateList](../extensibility/sccpopulatelist-function.md) pelo IDE e é usado pelo controle de fonte de plug-in para atualizar uma lista de arquivos ou diretórios (também é fornecido para o `SccPopulateList` função).

 Quando um usuário escolhe o **obter** de comando no IDE, o IDE exibirá uma caixa de listagem de todos os arquivos que o usuário pode obter. Infelizmente, o IDE não sabe a lista exata de todos os arquivos que o usuário pode obter; somente o plug-in tem essa lista. Se outros usuários tem adicionado os arquivos para o projeto de controle do código-fonte, esses arquivos devem aparecer na lista, mas o IDE não sabe sobre eles. O IDE compila uma lista dos arquivos que ele achar que o usuário pode obter. Antes de exibir essa lista para o usuário, ele chama o [SccPopulateList](../extensibility/sccpopulatelist-function.md) `,` dando o plug-in de controle do código-fonte a oportunidade de adicionar e excluir arquivos na lista.

## <a name="signature"></a>Assinatura
 O plug-in de controle do código-fonte modifica a lista, chamando uma função implementado pelo IDE com o seguinte protótipo:

```cpp
typedef BOOL (*POPLISTFUNC) (
   LPVOID pvCallerData,
   BOOL fAddRemove,
   LONG nStatus,
   LPSTR lpFileName
);
```

## <a name="parameters"></a>Parâmetros
 pvCallerData a `pvCallerData` parâmetro é passado pelo chamador (IDE) para o [SccPopulateList](../extensibility/sccpopulatelist-function.md). O plug-in de controle do código-fonte deve presumir nada sobre o conteúdo desse parâmetro.

 fAddRemove se `TRUE`, `lpFileName` é um arquivo que deve ser adicionado à lista de arquivos. Se `FALSE`, `lpFileName` é um arquivo que deve ser excluído da lista de arquivos.

 nStatus Status de `lpFileName` (uma combinação da `SCC_STATUS` bits, consulte [código de Status do arquivo](../extensibility/file-status-code-enumerator.md) para obter detalhes).

 caminho completo do diretório de lpFileName do nome do arquivo para adicionar ou excluir da lista.

## <a name="return-value"></a>Valor retornado

|Valor|Descrição|
|-----------|-----------------|
|`TRUE`|O plug-in pode continuar a chamar essa função.|
|`FALSE`|Houve um problema no lado do IDE (como uma saída de situação de memória). O plug-in deve interromper a operação.|

## <a name="remarks"></a>Comentários
 Para cada arquivo que deseja que o plug-in de controle do código-fonte para adicionar ou excluir da lista de arquivos, ele chama esta função, passando o `lpFileName`. O `fAddRemove` sinalizador indica um novo arquivo a adicionar à lista ou um arquivo antigo a ser excluído. O `nStatus` parâmetro fornece o status do arquivo. Quando o plug-in de SCC for concluída, adicionando e excluindo arquivos, ele retorna dos [SccPopulateList](../extensibility/sccpopulatelist-function.md) chamar.

> [!NOTE]
> O `SCC_CAP_POPULATELIST` bit de recurso é necessário para o Visual Studio.

## <a name="see-also"></a>Consulte também
- [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)
- [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)
- [SccPopulateList](../extensibility/sccpopulatelist-function.md)
- [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)