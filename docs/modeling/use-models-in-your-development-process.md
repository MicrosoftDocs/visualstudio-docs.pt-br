---
title: Usar modelos no processo de desenvolvimento
description: Saiba que, Visual Studio, você pode usar um modelo para ajudá-lo a entender e alterar um sistema, aplicativo ou componente.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UML, using models
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 095a6f17691d3265320a7b77905f70903bec1cb5
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388497"
---
# <a name="use-models-in-your-development-process"></a>Usar modelos no processo de desenvolvimento

No Visual Studio, você pode usar um modelo para ajudá-lo a entender e alterar um sistema, aplicativo ou componente. Um modelo pode ajudá-lo a visualizar o mundo no qual seu sistema funciona, esclarecer as necessidades dos usuários, definir a arquitetura do sistema, analisar o código e garantir que seu código atenda aos requisitos. Consulte [Vídeo do Channel 9: melhorar a arquitetura por meio da modelagem](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Improving-architecture-through-modeling).

Para ver quais versões do Visual Studio dar suporte a cada tipo de modelo, consulte [Suporte de versão para ferramentas de arquitetura e modelagem](../modeling/analyze-and-model-your-architecture.md#VersionSupport).

Os modelos podem ajudá-lo de várias maneiras:

- Desenhar diagramas de modelagem ajuda a esclarecer os conceitos envolvidos em requisitos, arquitetura e design de alto nível. Para obter mais informações, consulte [Requisitos do usuário do modelo.](../modeling/model-user-requirements.md)

- Trabalhar com modelos pode ajudá-lo a expor inconsistências nos requisitos.

- A comunicação com modelos ajuda você a comunicar conceitos importantes de forma menos ambígua do que com a linguagem natural. Para obter mais informações, [consulte Modelar a arquitetura do aplicativo.](../modeling/model-your-app-s-architecture.md)

- Às vezes, você pode usar modelos para gerar código ou outros artefatos, como esquemas de banco de dados ou documentos. Por exemplo, os componentes de modelagem Visual Studio são gerados de um modelo. Para obter mais informações, [consulte Gerar e configurar seu aplicativo de modelos](../modeling/generate-and-configure-your-app-from-models.md).

Você pode usar modelos em uma ampla variedade de processos, da extrema ágil à alta.

## <a name="use-models-to-reduce-ambiguity"></a>Usar modelos para reduzir a ambiguidade

A linguagem de modelagem é menos ambígua do que a linguagem natural e foi projetada para expressar as ideias normalmente necessárias durante o desenvolvimento de software.

Se seu projeto tiver uma pequena equipe seguindo as práticas agile, você poderá usar modelos para ajudá-lo a esclarecer histórias de usuários. Em discussões com o cliente sobre suas necessidades, a criação de um modelo pode gerar perguntas úteis muito mais rapidamente e em uma área mais ampla do produto, do que escrever código de pico ou protótipo.

Se seu projeto for grande e incluir equipes em diferentes partes do mundo, você poderá usar modelos para ajudar a comunicar os requisitos e a arquitetura com muito mais eficiência do que em texto sem-texto.

Em ambos os casos, a criação de um modelo quase sempre resulta em uma redução significativa em inconsistências e ambiguidades. Diferentes stakeholders frequentemente têm diferentes noções básicas sobre o mundo dos negócios em que o sistema funciona, e desenvolvedores diferentes frequentemente têm diferentes noções básicas sobre como o sistema funciona. O uso de um modelo como o foco de uma discussão geralmente expõe essas diferenças. Para obter mais informações sobre como usar um modelo para reduzir inconsistências, consulte [Requisitos do usuário do modelo.](../modeling/model-user-requirements.md)

## <a name="use-models-with-other-artifacts"></a>Usar modelos com outros artefatos

Um modelo não é por si só uma especificação de requisitos ou uma arquitetura. É uma ferramenta para expressar alguns aspectos dessas coisas com mais clareza, mas nem todos os conceitos necessários durante o design de software podem ser expressos. Portanto, os modelos devem ser usados junto com outros meios de comunicação, como páginas ou parágrafos do OneNote, Microsoft Office documentos, itens de trabalho no Team Foundation ou anotações autodetertivas na parede da sala do projeto. Além do último item, todos esses tipos de objeto podem ser vinculados a elementos partes do modelo.

Outros aspectos da especificação que normalmente são usados junto com modelos incluem o seguinte. Dependendo da escala e do estilo do seu projeto, você pode usar vários desses aspectos ou não usar nenhum:

- Histórias de usuários. Uma história de usuário é uma breve descrição, discutida com usuários e outros stakeholders, de um aspecto do comportamento do sistema que será entregue em uma das i iterações do projeto. Uma história de usuário típica começa "O cliente poderá...." Uma história de usuário pode introduzir um grupo de casos de uso ou pode definir extensões de casos de uso que foram desenvolvidos anteriormente. Definir ou estender os casos de uso ajuda a tornar a história do usuário mais clara.

- Solicitações de alteração. Uma solicitação de alteração em um projeto mais formal é muito semelhante a uma história de usuário em um projeto agile. A abordagem ágil trata todos os requisitos como alterações no que foi desenvolvido em idições anteriores.

- Descrição do caso de uso. Um caso de uso representa uma maneira na qual um usuário interage com o sistema para atingir uma meta específica. Uma descrição completa inclui a meta, sequências principais e alternativas de eventos e resultados excepcionais. Um diagrama de caso de uso ajuda a resumir e fornecer uma visão geral dos casos de uso.

- Cenários. Um cenário é uma descrição bastante detalhada de uma sequência de eventos que mostra como o sistema, os usuários e outros sistemas trabalham juntos para fornecer valor aos stakeholders. Ele pode assumir a forma de uma apresentação de slides da interface do usuário ou um protótipo da interface do usuário. Ele pode descrever um caso de uso ou uma sequência de casos de uso.

- Glossário. O glossário de requisitos do projeto descreve as palavras com as quais os clientes discutem seu mundo. Os modelos de interface do usuário e requisitos também devem usar esses termos. Um diagrama de classe pode ajudar a esclarecer as relações entre a maioria desses termos. A criação de diagramas e glossário não apenas reduz as inidentidades entre usuários e desenvolvedores, mas também quase sempre expõe mal-entendidos entre diferentes stakeholders de negócios.

- Regras de negócio. Muitas regras de negócio podem ser expressas como restrições invariantes nas associações e atributos no modelo de classe requirements e como restrições em diagramas de sequência.

- Design de alto nível. Descreve as partes principais e como elas se encaixam. Diagramas de componente, sequência e interface são uma parte importante de um design de alto nível.

- Padrões de design. Descreva as regras de design que são compartilhadas entre as diferentes partes do sistema.

- Especificações de teste. Os scripts de teste e os designs do código de teste podem fazer bom uso de diagramas de atividade e sequência para descrever sequências de etapas de teste. Os testes do sistema devem ser expressos em termos do modelo de requisitos para que possam ser alterados facilmente quando os requisitos mudarem.

- Plano de projeto. O plano de projeto ou a pendência define quando cada recurso será entregue. Você pode definir cada recurso informando quais casos de uso e regras de negócios ele implementa ou estende. Você pode consultar os casos de uso e as regras de negócio diretamente no plano ou pode definir um conjunto de recursos em um documento separado e usar os títulos de recurso no plano.

## <a name="use-models-in-iteration-planning"></a>Usar modelos no planejamento de iteração

Embora todos os projetos sejam diferentes em sua escala e organização, um projeto típico é planejado como uma série de ierções entre duas e seis semanas. É importante planejar ierções suficientes para permitir que os comentários de ierções in antecipadas sejam usados para ajustar o escopo e os planos para ierações posteriores.

Você pode achar as sugestões a seguir úteis para ajudar a perceber os benefícios da modelagem em um projeto iterativo.

### <a name="sharpen-focus-as-each-iteration-approaches"></a>Focar o foco à medida que cada iteração se aproxima

À medida que cada iteração se aproxima, use modelos para ajudar a definir o que deve ser entregue no final da iteração.

- Não modele tudo em detalhes nas i iterações in antecipadas. Na primeira iteração, crie um diagrama de classe para os itens principais no glossário do usuário, desenhe um diagrama dos principais casos de uso e desenhe um diagrama dos principais componentes. Não descreva nenhum deles em detalhes, pois os detalhes serão mais adiante no projeto. Use os termos definidos neste modelo para criar uma lista de recursos ou histórias de usuários principais. Atribua os recursos a i iterações para equilibrar aproximadamente a carga de trabalho estimada em todo o projeto. Essas atribuições serão mudadas posteriormente no projeto.

- Tente implementar versões simplificadas de todos os casos de uso mais importantes em uma iteração antecipada. Estenda esses casos de uso em ierações posteriores. Essa abordagem ajuda a reduzir o risco de descobrir uma falha nos requisitos ou na arquitetura muito tarde no projeto para fazer qualquer coisa sobre isso.

- Próximo ao final de cada iteração, mantenha um workshop de requisitos para definir em detalhes os requisitos ou as histórias do usuário que serão desenvolvidos na próxima iteração. Convidar usuários e stakeholders empresariais que podem decidir prioridades, bem como desenvolvedores e testadores de sistema. Permita três horas para definir requisitos para uma iteração de duas semanas.

- O objetivo do workshop é que todos concordem com o que será feito ao final da próxima iteração. Use modelos como uma das ferramentas para ajudar a esclarecer os requisitos. A saída do workshop é uma lista de pendências de iteração: ou seja, uma lista de tarefas de desenvolvimento no Team Foundation e nos suites de teste no [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] .

- No workshop de requisitos, discuta o design apenas na medida em que você precisar determinar estimativas para as tarefas de desenvolvimento. Caso contrário, mantenha a discussão sobre o comportamento do sistema que os usuários podem experimentar diretamente. Mantenha o modelo de requisitos separado do modelo de arquitetura.

- Os stakeholders não técnicos geralmente não têm problemas para entender diagramas UML, com algumas diretrizes suas.

### <a name="link-model-to-work-items"></a>Vincular modelo a itens de trabalho

Após o workshop de requisitos, elabore os detalhes do modelo de requisitos e vincule o modelo às tarefas de desenvolvimento. Você pode fazer isso vinculando itens de trabalho no Team Foundation a elementos no modelo.

Você pode vincular qualquer elemento a itens de trabalho, mas os elementos mais úteis são os seguinte:

- Comentários que descrevem regras de negócios ou requisitos de qualidade de serviço. Para obter mais informações, consulte [Requisitos do usuário do modelo.](../modeling/model-user-requirements.md)

### <a name="link-model-to-tests"></a>Vincular modelo a testes

Use o modelo de requisitos para orientar o design dos testes de aceitação. Crie esses testes simultaneamente com o trabalho de desenvolvimento.

Para saber mais sobre essa técnica, confira [Desenvolver testes de um modelo](../modeling/develop-tests-from-a-model.md).

### <a name="estimate-remaining-work"></a>Estimar o trabalho restante

Um modelo de requisitos pode ajudar a estimar o tamanho total do projeto em relação ao tamanho de cada iteração. Avaliar o número e a complexidade dos casos de uso e classes pode ajudá-lo a estimar o trabalho de desenvolvimento que será necessário. Quando você tiver concluído as primeiras ierções, uma comparação dos requisitos abordados e os requisitos que ainda serão abordados poderá dar uma medida aproximada do custo e do escopo do restante do projeto.

Próximo ao final de cada iteração, revise a atribuição de requisitos para imissões futuras. Pode ser útil representar o estado do software no final de cada iteração como um subsistema em um diagrama de caso de uso. Em suas discussões, você pode mover casos de uso e usar extensões de caso de um desses subsistemas para outro.

## <a name="levels-of-abstraction"></a>Níveis de abstração

Os modelos têm uma variedade de abstração em relação ao software. Os modelos mais concretos representam diretamente o código do programa e os modelos mais abstratos representam conceitos de negócios que podem ou não ser representados no código.

Um modelo pode ser exibido por meio de vários tipos de diagramas. Para obter informações sobre modelos e diagramas, [consulte Criar modelos para seu aplicativo.](../modeling/create-models-for-your-app.md)

Diferentes tipos de diagrama são úteis para descrever o design em diferentes níveis de abstração. Muitos dos tipos de diagrama são úteis em mais de um nível. Esta tabela mostra como cada tipo de diagrama pode ser usado.

|Nível de design|Tipos de diagrama|
|-|-|
|Processo empresarial<br /><br /> Entender o contexto no qual seu sistema será usado ajuda você a entender o que os usuários precisam dele.|– Diagramas de classe conceituais descrevem os conceitos de negócios usados no processo empresarial.|
|Requisitos do usuário<br /><br /> Definição do que os usuários precisam do seu sistema.|- Regras de negócios e requisitos de qualidade de serviço podem ser descritos em documentos separados.|
|Design de alto nível<br /><br /> A estrutura geral do sistema: os principais componentes e como eles se reúnem.|– Diagramas de dependência descrevem como o sistema é estruturado em partes interdependentes. Você pode validar o código do programa em relação a diagramas de dependência para garantir que ele adere à arquitetura.|
|Análise de código<br /><br /> Diagramas podem ser gerados a partir do código.|– Diagramas de dependência mostram as dependências entre classes. O código atualizado pode ser validado em relação a um diagrama de dependência.<br />– Diagramas de classe mostram as classes no código.|

## <a name="external-resources"></a>Recursos externos

|**Categoria**|**Links**|
|-|-|
|**Vídeos**|![link para vídeos ](../data-tools/media/playvideo.gif) [do MSDN How Do I Videos: How to Create and Use UML Models and Diagrams (Visual Studio 2010 Ultimate)](/previous-versions/visualstudio/visual-studio-2010/dd831853(v=vs.100))<br /><br /> ![link para o ](../data-tools/media/playvideo.gif) [vídeo Channel 9: UML com Visual Studio 2010](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-1-brainstorming-a-project)<br /><br /> ![link para o vídeo ](../data-tools/media/playvideo.gif) [MSDN How Do I Series: UML Tools and Extensibility (Visual Studio 2010 Ultimate)](/previous-versions/visualstudio/visual-studio-2010/dd831853(v=vs.100))|
|**Fóruns**|- [Visual Studio ferramentas & de modelagem](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [Visual Studio visualização & SDK de Modelagem (Ferramentas DSL)](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|
|**Blogs**|[Microsoft DevOps](https://devblogs.microsoft.com/devops/)|
|**Artigos técnicos e diários**|[Centro de Arquitetura do MSDN](/previous-versions/dn630665(v=msdn.10))|

## <a name="see-also"></a>Confira também

- [Usar modelos no desenvolvimento Agile](/previous-versions/ff398061(v=vs.140))
- [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)
- [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)
- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)
- [Desenvolver testes por meio de um modelo](../modeling/develop-tests-from-a-model.md)
- [Estruturar a solução de modelagem](../modeling/structure-your-modeling-solution.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]