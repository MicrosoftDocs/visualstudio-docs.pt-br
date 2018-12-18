---
title: Plug-ins de controle de origem | Microsoft Docs
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
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e7c51efc30251a177e07b7acf3e4c62821cb9488
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745449"
---
# <a name="source-control-plug-ins"></a>Plug-ins de controle do código-fonte
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A seção de referência do SDK de plug-in de controle do código-fonte contém a especificação de interface completa que permite que os sistemas de controle de origem sejam integrados [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Especifica a sintaxe e semântica das várias funções e tipos de dados que o plug-in de controle de origem deve implementar a interface com o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Funções de API do plug-in de controle do código-fonte](../extensibility/source-control-plug-in-api-functions.md)  
 Lista as funções que devem ser implementadas pelo plug-in de controle da fonte para estar em conformidade com a API de plug-in de controle do código-fonte.  
  
 [Funções de retorno de chamada implementadas pelo IDE](../extensibility/callback-functions-implemented-by-the-ide.md)  
 Descreve as funções que o plug-in de controle de origem usa para passar informações de volta para o IDE enquanto certos comandos são executados.  
  
 [Enumeradores](../extensibility/enumerators.md)  
 Lista os tipos de dados de enumerador na API de plug-in de controle de origem que o plug-in de controle do código-fonte deve conhecer.  
  
 [Sinalizadores de recurso](../extensibility/capability-flags.md)  
 Descreve o `SCC_CAP_xxx` sinalizadores, que são indicam os recursos de um provedor.  
  
 [Sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md)  
 Sinalizadores de listas que são úteis no contexto de comandos específicos.  
  
 [Códigos de erro](../extensibility/error-codes.md)  
 Lista de valores de erro comuns retornados por funções como `SCCTRN`.  
  
 [Cadeias de caracteres usadas como chaves para localizar um plug-in de controle do código-fonte](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)  
 Descreve as chaves para acessar o registro para localizar o controle de fonte de plug-in.  
  
 [Arquivo MSSCCPRJ.SCC](../extensibility/mssccprj-scc-file.md)  
 Descreve um arquivo do lado do cliente que contém informações opacas para o IDE, mas que é usado pelo plug-in de controle da fonte para localizar a solução ou projeto no controle de versão.  
  
 [Práticas recomendadas para implementar um plug-in de controle do código-fonte](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md)  
 Fornece uma coleção de lembretes técnicas importantes lembrar-se enquanto você estiver implementando a API de plug-in de controle do código-fonte.  
  
 [Restrições aos comprimentos de cadeia de caracteres](../extensibility/restrictions-on-string-lengths.md)  
 Descreve as limitações na API de plug-in de controle do código-fonte em comprimentos de cadeias de caracteres usadas em várias funções.  
  
 [Glossário](../extensibility/source-control-plug-in-glossary.md)  
 Fornece termos úteis e suas definições para ler a documentação do SDK de plug-in de controle do código-fonte.  
  
 [Como desativar avisos de compatibilidade para plug-ins de controle do código-fonte](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md)  
 Descreve como desabilitar avisos.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Exemplo de plug-in de controle do código-fonte](http://msdn.microsoft.com/en-us/61de7d2b-71db-451e-8e3e-d41b11c7a4ca)  
 Fornece um exemplo da funcionalidade de plug-in de controle do código-fonte.  
  
 [Guia de teste para plug-ins de controle do código-fonte](../extensibility/internals/test-guide-for-source-control-plug-ins.md)  
 Descreve os procedimentos de teste relacionados a um plug-in de controle de origem.  
  
 [Criar um plug-in de controle do código-fonte](../extensibility/internals/creating-a-source-control-plug-in.md)  
 Discute como criar um plug-in de controle de fonte que fornece funcionalidade de controle do código-fonte enquanto você estiver usando o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] interface de usuário de controle do código-fonte (UI).  
  
 [Referência do SDK do Visual Studio](../extensibility/visual-studio-sdk-reference.md)  
 Apresenta uma lista de tópicos de referência.

