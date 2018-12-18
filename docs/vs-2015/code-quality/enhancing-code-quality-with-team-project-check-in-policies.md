---
title: Melhorando a qualidade do código com políticas de Check-in do projeto de equipe | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code quality, using check-in policies
- team-based development, enhancing code quality
ms.assetid: 0ab72c33-148a-4a8a-a7bf-046995514c84
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c48a4e9cb68997903eed017637c9f00db88261a5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49299020"
---
# <a name="enhancing-code-quality-with-team-project-check-in-policies"></a>Melhorando a qualidade do código com políticas de check-in do projeto de equipe
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você usa o controle de versão do Team Foundation (TFVC), você pode criar políticas de check-in para seus projetos de equipe. para impor práticas que levam a um código melhor e mais eficiente do desenvolvimento de grupo. Políticas de check-in são regras que são definidas no nível de projeto de equipe e aplicadas em computadores de desenvolvedor, antes que o código tem permissão para fazer check-in.  
  
 Você pode especificar essas políticas de check-in do projeto equipe:  
  
-   **Compilações**: requer que as quebras de compilação que foram criadas durante um build devem ser corrigidas antes de um novo check-in.  
  
-   **Comentários do conjunto de alterações**: requer que os usuários forneçam comentários ao fazer check-in de alterações.  
  
-   **Análise de código**: requer que a análise de código seja executada antes do check-in.  
  
-   **Itens de trabalho**: requer que um ou mais itens de trabalho pode ser associado com o check-in.  
  
> [!IMPORTANT]
>  Para usar políticas de check-in, você deve estar conectado para [!INCLUDE[vststfsLong](../includes/vststfslong-md.md)].  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|Tarefa|Conteúdo de suporte|  
|----------|------------------------|  
|**Criar e usar políticas de check-in:** criar políticas de check-in usando as configurações de projeto de equipe do [!INCLUDE[esprscc](../includes/esprscc-md.md)].|[Definir e impor restrições de qualidade](http://msdn.microsoft.com/library/bdc5666e-6cf0-45b2-a0a1-133c3f61e852)|  
|**Criar e usar diretivas do check-in de análise de código:** você pode escolher entre um conjunto padrão de regras de análise de código, ou você pode criar um conjunto personalizado.|[Criando e usando políticas de check-in de análise de código](../code-quality/creating-and-using-code-analysis-check-in-policies.md)|  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tarefa|Conteúdo de suporte|  
|----------|------------------------|  
|**Configurar seu ambiente de desenvolvimento:** antes de criar ou modificar o código, você deve configurar seus ambientes de desenvolvimento e teste usando o código-fonte apropriado. Se você estiver trabalhando com bancos de dados, você também deve ter acesso à sua representação off-line.|[Como configurar ambientes de desenvolvimento](http://msdn.microsoft.com/en-us/7b686610-d379-4ca0-9608-73ef0e576e3a)|  
|**Usar análise de código no processo de desenvolvimento:** membros da equipe executam análise de código em seus computadores de desenvolvimento. No Visual Studio, os desenvolvedores configurar e executar execuções de análise de código para projetos de código individuais, exibir em analisar os problemas encontrados pelas execuções e criar itens de trabalho para avisos.|[Analisando a qualidade do aplicativo](../code-quality/analyzing-application-quality-by-using-code-analysis-tools.md)|  
|**Criar e executar testes de unidade:** testes de unidade fornecem aos desenvolvedores e testadores uma maneira rápida de procurar por erros lógicos nos métodos de classes em projetos c#, Visual Basic .NET e C++. Um teste de unidade pode ser criado uma vez e executado sempre que esse código-fonte é alterado para certificar-se de que nenhum erro é introduzido.|[Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)|  
|**Acompanhar itens de trabalho e defeitos:** você pode usar itens de trabalho para acompanhar e gerenciar seu trabalho e informações sobre seu projeto de equipe. Um item de trabalho é um banco de dados que [!INCLUDE[esprfound](../includes/esprfound-md.md)] usa para controlar a atribuição e o andamento do trabalho. Você pode usar diferentes tipos de itens de trabalho para acompanhar tipos diferentes de trabalho, como requisitos de cliente, bugs do produto e tarefas de desenvolvimento.|[Acompanhar trabalho e gerenciar o fluxo de trabalho &#91;redirecionado&#93;](http://msdn.microsoft.com/en-us/d2d8637d-0ef8-4ca3-874e-a04713344032)|  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="guidance"></a>Diretrizes  
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](http://go.microsoft.com/fwlink/?LinkID=255188)



