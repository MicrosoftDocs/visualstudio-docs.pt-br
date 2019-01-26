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
ms.openlocfilehash: f35ae28a1a231721d5ee5616a3b075737c24e629
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54982228"
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
 pvCallerData  
 O `pvCallerData` parâmetro é passado pelo chamador (IDE) para o [SccPopulateList](../extensibility/sccpopulatelist-function.md). O plug-in de controle do código-fonte deve presumir nada sobre o conteúdo desse parâmetro.  
  
 fAddRemove  
 Se `TRUE`, `lpFileName` é um arquivo que deve ser adicionado à lista de arquivos. Se `FALSE`, `lpFileName` é um arquivo que deve ser excluído da lista de arquivos.  
  
 nStatus  
 Status dos `lpFileName` (uma combinação da `SCC_STATUS` bits, consulte [código de Status do arquivo](../extensibility/file-status-code-enumerator.md) para obter detalhes).  
  
 lpFileName  
 Caminho completo do diretório do nome do arquivo para adicionar ou excluir da lista.  
  
## <a name="return-value"></a>Valor retornado  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`TRUE`|O plug-in pode continuar a chamar essa função.|  
|`FALSE`|Houve um problema no lado do IDE (como uma saída de situação de memória). O plug-in deve interromper a operação.|  
  
## <a name="remarks"></a>Comentários  
 Para cada arquivo que deseja que o plug-in de controle do código-fonte para adicionar ou excluir da lista de arquivos, ele chama esta função, passando o `lpFileName`. O `fAddRemove` sinalizador indica um novo arquivo a adicionar à lista ou um arquivo antigo a ser excluído. O `nStatus` parâmetro fornece o status do arquivo. Quando o plug-in de SCC for concluída, adicionando e excluindo arquivos, ele retorna dos [SccPopulateList](../extensibility/sccpopulatelist-function.md) chamar.  
  
> [!NOTE]
>  O `SCC_CAP_POPULATELIST` bit de recurso é necessário para o Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)   
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)   
 [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)