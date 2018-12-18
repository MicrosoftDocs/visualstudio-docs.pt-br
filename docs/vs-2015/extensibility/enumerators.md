---
title: Enumeradores | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
caps.latest.revision: 20
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 90ba436dcfbd09c29f68bff056e315f057e1a983
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810267"
---
# <a name="enumerators"></a>Enumeradores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta seção lista os tipos de dados em que a API de plug-in de controle do código-fonte que o plug-in de controle do código-fonte deve saber sobre enumerador.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Código de comando](../extensibility/command-code-enumerator.md)  
 Enumera as opções para o [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) e [SccPopulateList](../extensibility/sccpopulatelist-function.md) funções.  
  
 [Message](../extensibility/message-enumerator.md)  
 Enumera os sinalizadores usados para o retorno de chamada, impressão [LPTEXTOUTPROC](../extensibility/lptextoutproc.md).  
  
 [Código de status do arquivo](../extensibility/file-status-code-enumerator.md)  
 Contém valores constantes nomeados que especificam o estado de um arquivo sob controle do código-fonte.  
  
 [Código de status do diretório](../extensibility/directory-status-code-enumerator.md)  
 Contém valores constantes nomeados que especificam o estado de um diretório sob controle do código-fonte.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Criar um plug-in de controle do código-fonte](../extensibility/internals/creating-a-source-control-plug-in.md)  
 Define o SDK do plug-in de controle de origem e descreve os recursos incluídos.  
  
 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)  
 Solicita ao usuário para opções avançadas para o comando fornecido.  
  
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)  
 Examina a lista de arquivos para seu status atual. Além disso, usa o `pfnPopulate` função para notificar o chamador quando um arquivo não coincide com os critérios para o `nCommand`.  
  
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)  
 Descreve a função de retorno de chamada que é usada pelo [SccOpenProject](../extensibility/sccopenproject-function.md) para exibir mensagens de controle de fonte de plug-in por meio do IDE.  
  
 [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)  
 Fornece uma lista completa de todos os elementos na API de plug-in de controle de origem.

