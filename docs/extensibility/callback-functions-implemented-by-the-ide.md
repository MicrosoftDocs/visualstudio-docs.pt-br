---
title: Funções de retorno de chamada implementadas pelo IDE | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: c76a9ef3ab81cf764d5f82fdfb9c8d6a86f24bee
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39232475"
---
# <a name="callback-functions-implemented-by-the-ide"></a>Funções de retorno de chamada implementadas pelo IDE
Para fazer a integração com o ambiente de desenvolvimento integrado (IDE) como perfeita possível e para fornecer uma experiência unificada do usuário final, o plug-in de controle de origem pode usar funções de retorno de chamada que são implementadas pelo IDE. O plug-in pode chamar essas funções em momentos apropriados durante uma operação de controle do código-fonte para passar informações para o IDE; o IDE pode exibir essas informações como os elementos incorporados na sua interface do usuário nativa. O usuário tem uma experiência menos fragmentada neste cenário que se o plug-in empregados sua própria interface do usuário.  
  
 É o arquivo de cabeçalho necessários *scc.h*. O local padrão é *\Program Files\VSIP 8.0\EnvSDK\common\inc\\*. Ele também está na pasta VSIP que tem o exemplo de plug-in de controle do código-fonte em *\Program Files\VSIP 8.0\MSSCCI\\*.  
  
## <a name="in-this-section"></a>Nesta seção  
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)  
 Descreve a função de retorno de chamada que é usada pelo [SccOpenProject](../extensibility/sccopenproject-function.md) para exibir mensagens de controle de fonte de plug-in por meio do IDE.  
  
 [POPLISTFUNC](../extensibility/poplistfunc.md)  
 Descreve a função de retorno de chamada que é usada pelo [SccPopulateList](../extensibility/sccpopulatelist-function.md) quando o IDE não tem acesso completo a informações que estão disponíveis somente para o plug-in, como uma lista completa dos arquivos sob controle de versão de controle de origem.  
  
 [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md)  
 Descreve a função de retorno de chamada que é usada pelas [SccQueryChanges](../extensibility/sccquerychanges-function.md) operação.  
  
 [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md)  
 Descreve a função de retorno de chamada que é usada pelas [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) operação.  
  
 [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md)  
 Descreve a função de retorno de chamada definida por uma chamada para o [SccSetOption](../extensibility/sccsetoption-function.md) que permite que o plug-in para se comunicar alterações de nome de volta para o IDE de controle de origem.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [SccOpenProject](../extensibility/sccopenproject-function.md)  
 Abre um projeto.  
  
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)  
 Examina a lista de arquivos para seu status atual. Além disso, usa o `pfnPopulate` função para notificar o chamador quando um arquivo não coincide com os critérios para o `nCommand`.  
  
 [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)  
 Examina uma lista de diretórios e arquivos em um projeto ou projetos que estão sob controle do código-fonte. Cada nome de arquivo e diretório encontrado é passado para uma função de retorno de chamada.  
  
 [SccQueryChanges](../extensibility/sccquerychanges-function.md)  
 Examina as alterações de nome que foram feitas em uma lista de arquivos. Cada nome de arquivo é passado para uma função de retorno de chamada juntamente com seu status de alteração.  
  
 [SccSetOption](../extensibility/sccsetoption-function.md)  
 Define uma ampla variedade de opções. Cada opção começa com `SCC_OPT_xxx` e tem seu próprio conjunto definido de valores.  
  
 [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)  
 Descreve o conteúdo da seção de referência do SDK do plug-in de controle de origem.