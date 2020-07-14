---
title: Analise e modele sua arquitetura | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e00735a180ec951a8afced0f5c74f7a9466e50b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534089"
---
# <a name="analyze-and-model-your-architecture"></a>Analisar e modelar a sua arquitetura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Verifique se seu aplicativo atende aos requisitos de usuário usando ferramentas de arquitetura e modelagem do Visual Studio para criar e modelar seu aplicativo. Entenda o código do programa existente mais facilmente usando o Visual Studio para visualizar a estrutura, o comportamento e as relações do código.

 Crie modelos em diferentes níveis de detalhes ao longo do ciclo de vida do aplicativo como parte do seu processo de desenvolvimento. Acompanhe os requisitos, as tarefas, os casos de teste, os bugs e outros trabalhos associados aos seus modelos vinculando elementos de modelo a Team Foundation Server itens de trabalho e seu plano de desenvolvimento. Consulte [cenário: alterar o design usando visualização e modelagem](../modeling/scenario-change-your-design-using-visualization-and-modeling.md).

 Para ver quais versões do Visual Studio oferecem suporte a cada recurso, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="to"></a>Para

|Cenário|Artigos|
|-|-|
|**Visualizar código**:<br /><br /> -Consulte a organização do código e as relações Criando mapas de código. Visualize dependências entre assemblies, namespaces, classes, métodos e assim por diante.<br />-Consulte a estrutura de classe e os membros de um projeto específico Criando diagramas de classe do código.<br />-Encontre conflitos entre seu código e seu design criando diagramas de camada para validar o código.<br /><br /> **Observação**: nesta versão do Visual Studio, o termo *mapa de código* é usado no lugar do *grafo de dependência*. O termo *grafo* quando usado sozinha geralmente refere-se a um gráfico direcionado ou diagrama DGML (ou documento). Mapas de código são um tipo especializado de diagrama DGML.|-   [Visualizar código](../modeling/visualize-code.md)<br />-   [Trabalhando com classes e outros tipos (Designer de Classe)](../ide/working-with-classes-and-other-types-class-designer.md)<br />-   [Vídeo: entenda suas dependências de código por meio de visualização (canal 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Understand-your-code-dependencies-through-visualization)<br />-   [Vídeo: Visualizar o impacto de uma alteração (canal 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Visualize-the-impact-of-a-change)|
|**Descrever e comunicar os requisitos de usuário**:<br /><br /> -Esclareça histórias de usuários, regras de negócios e outros requisitos e ajude a garantir sua consistência, desenhando diagramas UML como casos de uso, atividade e diagramas de classe.|-   [Criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md)<br />-   [Requisitos de usuário de modelo](../modeling/model-user-requirements.md)<br />-   [Vídeo: melhorar a arquitetura por meio de modelagem (canal 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Improving-architecture-through-modeling)|
|**Defina a arquitetura**:<br /><br /> -Modelar a estrutura em larga escala do seu sistema de software e os padrões de design por desenho de diagramas UML, classes e componentes de sequência.<br />-Definir e impor restrições em dependências entre os componentes do seu código Criando diagramas de camada.|-   [Criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md)<br />-   [Modele a arquitetura de seu aplicativo](../modeling/model-your-app-s-architecture.md)<br />-   [Vídeo: melhorar a arquitetura por meio de modelagem (canal 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Improving-architecture-through-modeling)<br />-   [Vídeo: Use diagramas de camada para projetar e validar sua arquitetura (canal 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture)|
|**Valide seu sistema com os requisitos e o design pretendido:**<br /><br /> -Definir testes de aceitação ou testes de sistema com base nos modelos de requisitos. Isso cria uma relação forte entre os testes e os requisitos dos seus usuários e ajuda a atualizar o sistema mais facilmente quando os requisitos mudam.<br />– Valide dependências de código com diagramas de camada que descrevem a arquitetura desejada e evite alterações que possam entrar em conflito com o design.|-   [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)<br />-   [Vídeo: Use diagramas de camada para projetar e validar sua arquitetura (canal 9)](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture)|
|**Compartilhe modelos, diagramas e mapas de código usando o controle de versão do Team Foundation**:<br /><br /> -Coloque mapas de código, modelagem de projetos, diagramas UML e diagramas de camada sob o controle de versão do Team Foundation para que você possa compartilhá-los.|Quando você tiver vários usuários que trabalham com esses itens sob o controle de versão do Team Foundation, use estas diretrizes para ajudá-lo a evitar problemas de controle de versão:<br /><br /> -   [Gerenciar modelos e diagramas sob controle de versão](../modeling/manage-models-and-diagrams-under-version-control.md)|
|**Gere ou configure partes do seu aplicativo de UML ou de linguagens específicas de domínio**:<br /><br /> -Tornar seu design mais responsivo às alterações de requisitos e facilmente uma variável em uma linha de produtos.|-   [Gerar e configurar seu aplicativo com base em modelos](../modeling/generate-and-configure-your-app-from-models.md)|
|**Personalizar modelos e diagramas**:<br /><br /> – Adapte modelos de como seu projeto os utiliza definindo propriedades adicionais para elementos UML, restrições de validação para garantir que seus modelos estejam em conformidade com suas regras de negócio, além de comandos de menu e itens de caixa de ferramentas adicionais.<br />-Crie suas próprias linguagens específicas de domínio.|-   [Estender diagramas e modelos UML](../modeling/extend-uml-models-and-diagrams.md)<br />-   [SDK de modelagem para Visual Studio-linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**Gerar texto usando modelos T4**:<br /><br /> -Use blocos de texto e lógica de controle dentro de modelos para gerar arquivos baseados em texto.|-   [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)|

## <a name="types-of-models-and-their-uses"></a>Tipos de modelos e seus usos

|**Tipo de modelo e usos típicos**|
|-------------------------------------|
|**Mapas de código**<br /><br /> Os mapas de código ajudam você a ver a organização e as relações em seu código.<br /><br /> Usos típicos:<br /><br /> -Examine o código do programa para que você possa entender melhor sua estrutura e suas dependências, como atualizá-lo e estimar o custo das alterações propostas.<br /><br /> Consulte:<br /><br /> -   [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />-   [Usar mapas de código para depurar seus aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [Localizar possíveis problemas usando analisadores de mapa de código](../modeling/find-potential-problems-using-code-map-analyzers.md)|
|**Diagrama de camada**<br /><br /> Os diagramas de camada permitem que você defina a estrutura de um aplicativo como um conjunto de camadas ou blocos com dependências explícitas. Você pode executar a validação para descobrir conflitos entre dependências no código e as dependências descritas em um diagrama de camada.<br /><br /> Usos típicos:<br /><br /> – Estabilizar a estrutura do aplicativo por meio de várias alterações ao longo de sua vida.<br />-Descobrir conflitos de dependências não intencionais antes de fazer check-in de alterações no código.<br /><br /> Consulte:<br /><br /> -   [Crie diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)<br />-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)|
|**modelo UML**<br /><br /> Um modelo UML inclui vários modos de exibição, incluindo classe, componente, casos de uso, atividade e diagramas de sequência. Você pode personalizar o UML para se adequar ao domínio do aplicativo. Por exemplo, você pode anexar marcas, informações adicionais e restrições aos elementos do modelo. Você também pode definir ferramentas que operam nos modelos. Consulte [criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md).<br /><br /> Usos típicos:<br /><br /> -Descrever os requisitos e o design. Você pode aplicar o UML rapidamente ao desenvolvimento de qualquer aplicativo. Consulte [usar modelos em seu processo de desenvolvimento](../modeling/use-models-in-your-development-process.md).<br />-Gerar ou configurar testes ou partes de um aplicativo. Alguns trabalhos são necessários para personalizar a notação e desenvolver os modelos de geração ou o aplicativo configurável. Consulte [gerar e configurar seu aplicativo com base em modelos](../modeling/generate-and-configure-your-app-from-models.md).<br />-Para descrição geral e para geração de código ou configuração em projetos menores.|
|**DSL (linguagem específica de domínio)**<br /><br /> Uma DSL é uma notação que você cria para uma finalidade específica. No Visual Studio, geralmente é gráfico.<br /><br /> Usos típicos:<br /><br /> – Gerar ou configurar partes do aplicativo. O trabalho é necessário para desenvolver a notação e as ferramentas. O resultado pode ser uma melhor opção para seu domínio do que uma personalização de UML.<br />-Para projetos grandes ou em linhas de produtos em que o investimento no desenvolvimento da DSL e suas ferramentas são retornados por seu uso em mais de um projeto.<br /><br /> Consulte:<br /><br /> -   [SDK de modelagem para Visual Studio-linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|

## <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?

|Recurso|Links|
|-|-|
|**Fóruns**|-   [Ferramentas de modelagem & de visualização do Visual Studio](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />-   [SDK de modelagem de & de visualização do Visual Studio (ferramentas DSL)](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|

## <a name="see-also"></a>Consulte Também

- [O que há de novo para modelagem no Visual Studio 2015](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps e gerenciamento de ciclo de vida do aplicativo](https://msdn.microsoft.com/library/74a1f71d-7f23-4c71-8fd7-89ede614fab6)
