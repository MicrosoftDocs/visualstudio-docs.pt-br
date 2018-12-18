---
title: Analisar e modelar sua arquitetura | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, exploring code
- Visual Studio Ultimate, visualizing code
- diagrams - modeling
- Visual Studio ALM, modeling
- application, design
- architecture
- code visualization
- application design
- applications, architecture
- code exploration
- Visual Studio ALM, exploring code
- modeling
- application architecture
- application, modeling
- applications, modeling
- architecture [Visual Studio ALM], modeling
- application modeling
- Visual Studio Ultimate, modeling
- architecture [Visual Studio Ultimate], modeling
- application, architecture
- Visual Studio ALM, visualizing code
- applications, designing
ms.assetid: c9f04cfa-72bd-419d-a952-616eed01472e
caps.latest.revision: 129
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 1b7d7f9f478e85229eaa72ab04d12b6b542cbab5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781030"
---
# <a name="analyze-and-model-your-architecture"></a>Analisar e modelar a sua arquitetura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Verifique se que o aplicativo atende aos requisitos de usuário usando a arquitetura do Visual Studio e ferramentas para projetar e modelar seu aplicativo de modelagem. Entenda o código existente do programa com mais facilidade usando o Visual Studio para visualizar a estrutura do código, o comportamento e relações.  
  
 Crie modelos em diferentes níveis de detalhe em todo o ciclo de vida do aplicativo como parte de seu processo de desenvolvimento. Acompanhe requisitos, tarefas, casos de teste, bugs e outros trabalhos associados com seus modelos vinculando os elementos de modelo a itens de trabalho do Team Foundation Server e ao plano de desenvolvimento. Ver [cenário: alterar o design usando visualização e modelagem](../modeling/scenario-change-your-design-using-visualization-and-modeling.md).  
  
 Para ver quais versões do Visual Studio dão suporte a cada recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)  
  
## <a name="to"></a>Para  
  
|||  
|-|-|  
|**Visualizar código**:<br /><br /> -Consulte a organização e os relacionamentos do código Criando mapas de código. Visualize dependências entre assemblies, namespaces, classes, métodos e assim por diante.<br />-Consulte a estrutura de classes e membros para um projeto específico com a criação de diagramas de classe do código.<br />-Encontre conflitos entre o código e seu design com a criação de diagramas de camada para validar o código.<br /><br /> **Observação**: nesta versão do Visual Studio, o termo *mapa de códigos* é usado no lugar de *grafo de dependência*. O termo *graph* quando usada sozinha geralmente se refere a um diagrama DGML ou de gráfico direcionado (ou documento). Mapas de código são um tipo especializado de diagrama DGML.|-   [Visualizar código](../modeling/visualize-code.md)<br />-   [Trabalhando com Classes e outros tipos (Designer de classe)](../ide/working-with-classes-and-other-types-class-designer.md)<br />-   [Vídeo: Entender suas dependências de código por meio da visualização (Channel 9)](http://go.microsoft.com/fwlink/?LinkID=252065)<br />-   [Vídeo: Visualizar o impacto de uma alteração (Channel 9)](http://go.microsoft.com/fwlink/?LinkID=252068)|  
|**Descrever e comunicar requisitos do usuário**:<br /><br /> -Esclarecer as histórias de usuários, as regras de negócio e outros requisitos e ajudar a garantir sua consistência ao desenhar diagramas UML como caso de uso, atividade e diagramas de classe.|-   [Criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md)<br />-   [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)<br />-   [Vídeo: Aperfeiçoar a arquitetura por meio de modelagem (Channel 9)](http://go.microsoft.com/fwlink/?LinkID=252078)|  
|**Definir a arquitetura**:<br /><br /> -A estrutura em larga escala do seu sistema de software e os padrões de design do modelo ao desenhar diagramas de sequência, classe e componente UML.<br />-Definir e impor restrições sobre dependências entre os componentes do seu código com a criação de diagramas de camada.|-   [Criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md)<br />-   [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)<br />-   [Vídeo: Aperfeiçoar a arquitetura por meio de modelagem (Channel 9)](http://go.microsoft.com/fwlink/?LinkID=252078)<br />-   [Vídeo: Usar diagramas de camada para projetar e validar sua arquitetura (Channel 9)](http://go.microsoft.com/fwlink/?LinkID=252073)|  
|**Validar o sistema com os requisitos e se destina a design:**<br /><br /> -Defina testes de aceitação ou testes de sistema com base em modelos de requisitos. Isso cria uma forte relação entre os testes e requisitos dos seus usuários e ajuda a atualizar o sistema mais facilmente quando os requisitos são alterados.<br />-Validar dependências de código com diagramas de camada que descrevem a arquitetura pretendida e evitar alterações entrarem em conflito com o design.|-   [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)<br />-   [Vídeo: Usar diagramas de camada para projetar e validar sua arquitetura (Channel 9)](http://go.microsoft.com/fwlink/?LinkID=252073)|  
|**Compartilhar modelos, diagramas e mapas de código usando o controle de versão do Team Foundation**:<br /><br /> -Coloque mapas de código, diagramas de camada sob o controle de versão do Team Foundation, diagramas de UML e projetos de modelagem para que você pode compartilhá-los.|Quando você tiver vários usuários que trabalham com estes itens sob controle de versão do Team Foundation, use estas diretrizes para ajudar a evitar problemas de controle de versão:<br /><br /> -   [Gerenciar modelos e diagramas com controle de versão](../modeling/manage-models-and-diagrams-under-version-control.md)|  
|**Gerar ou configurar as partes do seu aplicativo de UML ou linguagens específicas de domínio**:<br /><br /> -Tornar o seu design mais responsivos a alterações de requisitos e facilmente variável em uma linha de produtos.|-   [Gerar e configurar seu aplicativo a partir de modelos](../modeling/generate-and-configure-your-app-from-models.md)|  
|**Personalizar modelos e diagramas**:<br /><br /> -Adaptem modelos para como seu projeto usa-os ao definir propriedades adicionais para elementos UML, restrições de validação para certificar-se de que seus modelos em conformidade com suas regras de negócio e comandos de menu adicionais e itens de caixa de ferramentas.<br />-Crie seus próprios linguagens específicas de domínio.|-   [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)<br />-   [SDK de modelagem para Visual Studio - linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|  
|**Gerar texto usando modelos T4**:<br /><br /> -Usar blocos de texto e a lógica de controle dentro de modelos para gerar arquivos baseados em texto.|-   [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)|  
  
## <a name="types-of-models-and-their-uses"></a>Tipos de modelos e seus usos  
  
|**O tipo de modelo e usos típicos**|  
|-------------------------------------|  
|**Mapas de código**<br /><br /> Mapas de código ajudam você a ver a organização e relações em seu código.<br /><br /> Usos típicos:<br /><br /> -Examine o código do programa para que você possa entender melhor a sua estrutura e suas dependências, como atualizá-lo e estimar o custo de alterações propostas.<br /><br /> Consulte:<br /><br /> -   [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />-   [Usar mapas de códigos para depurar seus aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [Localizar possíveis problemas usando analisadores de mapa de código](../modeling/find-potential-problems-using-code-map-analyzers.md)|  
|**Diagrama de camada**<br /><br /> Diagramas de camada permitem que você definir a estrutura de um aplicativo como um conjunto de blocos com dependências explícitas ou camadas. Você pode executar a validação para detectar conflitos entre dependências no código e descritos em um diagrama de camada.<br /><br /> Usos típicos:<br /><br /> -Estabilize a estrutura do aplicativo por meio de várias alterações ao longo do ciclo de vida.<br />-Descobrir conflitos de dependência não intencionais, antes de fazer check-in de alterações no código.<br /><br /> Consulte:<br /><br /> -   [Criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)<br />-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)|  
|**Modelo UML**<br /><br /> Um modelo UML inclui várias exibições, incluindo a classe, componente, caso de uso, atividade e diagramas de sequência. Você pode personalizar o UML de acordo com seu domínio de aplicativo. Por exemplo, você pode anexar marcas, informações adicionais e restrições para os elementos de modelo. Você também pode definir as ferramentas que operam nos modelos. Ver [criar modelos para o aplicativo](../modeling/create-models-for-your-app.md).<br /><br /> Usos típicos:<br /><br /> -Descrevem requisitos e design. Você pode aplicar rapidamente UML para o desenvolvimento de qualquer aplicativo. Ver [usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md).<br />– Gere ou configurar testes ou partes de um aplicativo. Algum trabalho é necessária para personalizar a notação e desenvolver os modelos de geração ou o aplicativo configurável. Ver [gerar e configurar o aplicativo a partir de modelos de](../modeling/generate-and-configure-your-app-from-models.md).<br />-Para descrição geral e para geração de código e configuração em projetos menores.|  
|**Linguagem específica de domínio (DSL)**<br /><br /> Uma DSL é uma notação de design para uma finalidade específica. No Visual Studio, é geralmente gráfica.<br /><br /> Usos típicos:<br /><br /> – Gere ou configurar as partes do aplicativo. Trabalho é necessário para desenvolver as ferramentas e a notação. O resultado pode ser mais adequado ao seu domínio do que uma personalização de UML.<br />-Para projetos grandes ou em linhas de produtos em que o investimento em DSL e suas ferramentas de desenvolvimento é retornado por seu uso em mais de um projeto.<br /><br /> Consulte:<br /><br /> -   [SDK de modelagem para Visual Studio - linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|  
  
## <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?  
  
|||  
|-|-|  
|**Fóruns**|-   [Visualização do Visual Studio e ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visualização do Visual Studio e modelagem (ferramentas DSL) do SDK](http://go.microsoft.com/fwlink/?LinkId=184721)|  
  
## <a name="see-also"></a>Consulte também  
 [O que há de novo](../modeling/what-s-new-for-design-in-visual-studio.md)   
 [DevOps e gerenciamento de ciclo de vida do aplicativo](http://msdn.microsoft.com/library/74a1f71d-7f23-4c71-8fd7-89ede614fab6)



