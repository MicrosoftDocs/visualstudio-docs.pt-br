---
title: Usar modelos no processo de desenvolvimento
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML, using models
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 25debac1e5f2e977e5dd36ec8b4a083a1a362d1b
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967214"
---
# <a name="use-models-in-your-development-process"></a>Usar modelos no processo de desenvolvimento

No Visual Studio, você pode usar um modelo para ajudá-lo a entender e alterar um sistema, aplicativo ou componente. Um modelo pode ajudar a visualizar o mundo em que o sistema funciona, esclarecer as necessidades dos usuários, definem a arquitetura do seu sistema, analisar o código e certifique-se de que seu código atende aos requisitos. Ver [vídeo do Channel 9: melhorar a arquitetura com modelagem](http://go.microsoft.com/fwlink/?LinkID=252078).

Para ver quais versões do Visual Studio dão suporte a cada tipo de modelo, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

Modelos podem ajudá-lo de várias maneiras:

- Desenho de diagramas de modelagem ajuda a esclarecer os conceitos envolvidos em requisitos, arquitetura e design de alto nível. Para obter mais informações, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).

- Trabalhar com modelos pode ajudar você a expor as inconsistências nos requisitos.

- Comunicando-se com modelos ajuda você a se comunicar conceitos importantes menor ambíguo com idioma natural. Para obter mais informações, consulte [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md).

- Às vezes, você pode usar modelos para gerar o código ou outros artefatos como esquemas de banco de dados ou documentos. Por exemplo, os componentes de modelagem do Visual Studio são gerados de um modelo. Para obter mais informações, consulte [gerar e configurar o aplicativo a partir de modelos de](../modeling/generate-and-configure-your-app-from-models.md).

Você pode usar os modelos em uma ampla variedade de processos, desde extreme cerimônia agile para alta.

## <a name="use-models-to-reduce-ambiguity"></a>Usar modelos para reduzir a ambiguidade

Linguagem de modelagem é menos ambígua de linguagem natural e ele é projetado para expressar as ideias necessárias normalmente durante o desenvolvimento de software.

Se o projeto tiver uma equipe pequena, seguindo as práticas do agile, você pode usar modelos para ajudar a esclarecer as histórias de usuários. Em discussões com o cliente sobre suas necessidades, a criação de um modelo pode gerar perguntas úteis muito mais rápido e em uma área mais ampla do produto, que escrever código de pico ou protótipo.

Se seu projeto for grande e inclui as equipes em diferentes partes do mundo, você pode usar modelos para ajudar a se comunicar os requisitos e arquitetura de maneira muito mais eficaz do que no texto sem formatação.

Em ambos os casos a criação de um modelo quase sempre resulta em uma redução significativa no inconsistências e ambiguidades. Participantes diferentes frequentemente têm diferentes Noções básicas do mundo dos negócios em que o sistema funciona e diferentes desenvolvedores frequentemente têm diferentes Noções básicas de como funciona o sistema. Usando um modelo como o foco de uma discussão geral expõe essas diferenças. Para obter mais informações sobre como usar um modelo para reduzir as inconsistências, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).

## <a name="use-models-with-other-artifacts"></a>Usar modelos com outros artefatos

Um modelo não é por si só, uma especificação de requisitos ou uma arquitetura. Ele é uma ferramenta para expressar alguns aspectos dessas coisas mais claramente, mas não todos os conceitos necessários durante o design de software podem ser expresso. Os modelos, portanto, devem ser usados junto com outros meios de comunicação, como o OneNote páginas ou parágrafos, documentos do Microsoft Office, itens de trabalho no Team Foundation ou Notas Autoadesivas na parede de sala do projeto. O último item, além de todos esses tipos de objeto podem ser vinculados a partes de elementos do modelo.

Outros aspectos da especificação que normalmente são usados junto com os modelos incluem o seguinte. Dependendo da escala e o estilo do seu projeto, você pode usar vários desses aspectos ou não usar nenhum:

- Histórias do usuário. Uma história de usuário é uma breve descrição, discutida com usuários e outros participantes, de um aspecto do comportamento do sistema que será entregue em uma das iterações do projeto. Uma história de usuário típico começa "o cliente será capaz de..." Uma história de usuário pode introduzir um grupo de casos de uso ou pode definir as extensões de casos de uso que foram desenvolvidas anteriormente. Definir ou estender os casos de uso ajuda a tornar a história de usuário mais clara.

- Solicitações de alteração. Uma solicitação de alteração em um projeto mais formal é muito semelhante a uma história de usuário em um projeto agile. A abordagem do agile trata todos os requisitos de como as alterações para o que foi desenvolvido em iterações anteriores.

- Use a descrição do caso. Um caso de uso representa uma forma em que um usuário interage com o sistema para atingir uma meta específica. Uma descrição completa inclui a meta, principais e alternativas sequências de eventos e os resultados excepcionais. Um diagrama de caso de uso ajuda a resumir e fornecem uma visão geral dos casos de uso.

- Cenários. Um cenário é uma descrição detalhada bastante de uma sequência de eventos mostrando como o sistema, os usuários e outros sistemas funcionam juntos para fornecer o valor às partes interessadas. Ele pode assumir a forma de um slide show da interface do usuário ou um protótipo da interface do usuário. Ele pode descrever um caso de uso ou uma sequência de casos de uso.

- Glossário. Glossário de requisitos do projeto descreve as palavras com o qual os clientes discutem seu mundo. Os modelos de requisitos e a interface do usuário também devem usar esses termos. Um diagrama de classe pode ajudar a esclarecer as relações entre a maioria desses termos. Criar os diagramas e glossário não só reduz a confusão entre usuários e desenvolvedores, mas também quase sempre expõe mal-entendidos entre os participantes de negócios diferentes.

- Regras de negócio. Muitas regras de negócios podem ser expressos como invariáveis restrições sobre as associações e os atributos no modelo de classe de requisitos e restrições em diagramas de sequência.

- Design de alto nível. Descreve as principais partes e como elas se encaixam. Componente, sequência e diagramas de interface são uma parte importante de um design de alto nível.

- Padrões de design. Descreva as regras de design que são compartilhadas entre as diferentes partes do sistema.

- Especificações de teste. Scripts de teste e os designs para o código de teste podem fazer bom uso de diagramas de atividade e a sequência para descrever as sequências de etapas de teste. Testes de sistema devem ser expressos em termos do modelo de requisitos para que eles podem ser alterados facilmente quando os requisitos mudam.

- Plano de projeto. O plano de projeto ou uma lista de pendências define quando cada recurso será entregue. Você pode definir cada recurso informando quais casos de uso e ela implementa ou estende as regras de negócio. Você pode se referir a casos de uso e as regras de negócios diretamente no plano, ou você pode definir um conjunto de recursos em um documento separado e usar os títulos dos recursos no plano.

## <a name="use-models-in-iteration-planning"></a>Usar modelos no planejamento de iteração

Embora todos os projetos sejam diferentes em seu dimensionamento e a organização, um projeto típico é planejado como uma série de iterações de entre dois e seis semanas. É importante planejar suficiente iterações para permitir que os comentários de iterações iniciais a serem usados para ajustar o escopo e os planos para iterações posteriores.

Você pode encontrar as sugestões a seguir úteis para ajudar a compreender os benefícios da modelagem em um projeto iterativo.

### <a name="sharpen-focus-as-each-iteration-approaches"></a>Ajustar o foco conforme cada iteração se aproxima

Conforme cada iteração se aproxima, use modelos para ajudar a definir o que deve ser entregue ao final da iteração.

- Modele tudo em detalhes nas iterações anteriores. Na primeira iteração, criar um diagrama de classe para os principais itens no glossário de usuário, desenhar um diagrama dos casos de uso importantes e desenhar um diagrama dos principais componentes. Não descreva qualquer um deles separadamente com muitos detalhes, porque o detalhe será alterada posteriormente no projeto. Use os termos definidos nesse modelo para criar uma lista de recursos ou histórias de usuário principal. Atribua os recursos para as iterações para aproximadamente equilibrar a carga de trabalho a estimados em todo o projeto. Essas atribuições serão alterado posteriormente no projeto.

- Tente implementar versões simplificadas de todos os casos de uso mais importantes em uma iteração inicial. Estender esses casos de uso em iterações posteriores. Essa abordagem ajuda a reduzir o risco de descoberta de uma falha nos requisitos ou a arquitetura muito tarde no projeto para fazer a respeito.

- No final de cada iteração, mantenha um workshop de requisitos para definir em detalhes os requisitos ou histórias de usuários que serão desenvolvidas na próxima iteração. Convide usuários e participantes de negócios que podem decidir prioridades, bem como os desenvolvedores e testadores de sistema. Permitir a três horas definir requisitos para uma iteração 2 semanas.

- O objetivo do workshop é concordar com o que será realizado no final da próxima iteração de todos. Use modelos como uma das ferramentas para ajudar a esclarecer os requisitos. A saída do workshop é uma lista de pendências de iteração: ou seja, uma lista de tarefas de desenvolvimento no Team Foundation e conjuntos de testes em [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)].

- O workshop de requisitos, discutiremos o design somente na medida, você precisa determinar as estimativas para as tarefas de desenvolvimento. Caso contrário, mantenha a discussão ao comportamento do sistema que os usuários podem enfrentar diretamente. Manter o modelo de requisitos separado do modelo de arquitetura.

- Stakeholders não técnicos geralmente não têm problemas Noções básicas sobre diagramas UML, com a orientação de você.

### <a name="link-model-to-work-items"></a>Modelo de link a itens de trabalho

Após o workshop de requisitos, elaborar os detalhes do modelo de requisitos e vincule o modelo para tarefas de desenvolvimento. Você pode fazer isso ao vincular itens de trabalho no Team Foundation a elementos no modelo.

Você pode vincular qualquer elemento para itens de trabalho, mas os elementos mais úteis são da seguinte maneira:

- Comentários que descrevem as regras de negócio ou qualidade dos requisitos de serviço. Para obter mais informações, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).

### <a name="link-model-to-tests"></a>Modelo de link para testes

Use o modelo de requisitos para orientar o design dos testes de aceitação. Crie esses testes simultaneamente com o trabalho de desenvolvimento.

Para saber mais sobre essa técnica, consulte [desenvolver testes de um modelo de](../modeling/develop-tests-from-a-model.md).

### <a name="estimate-remaining-work"></a>Estimar o trabalho restante

Um modelo de requisitos pode ajudar a estimar o tamanho total do projeto em relação ao tamanho de cada iteração. Avaliar o número e a complexidade dos casos de uso e classes pode ajudá-lo a estimar o trabalho de desenvolvimento que serão necessário. Quando você tiver concluído as primeiras iterações, uma comparação dos requisitos abordados e os requisitos ainda para cobrir pode fornecer uma medida aproximada do custo e o escopo do resto do projeto.

No final de cada iteração, revise a atribuição de requisitos para iterações futuras. Ele pode ser útil representar o estado do seu software no final da cada iteração como um subsistema de um diagrama de caso de uso. Em suas discussões, você pode mover os casos de uso e usar extensões de caso de um desses subsistemas para outro.

## <a name="levels-of-abstraction"></a>Níveis de abstração

Os modelos têm um intervalo de abstração em relação ao software. Os modelos mais concretos representam diretamente o código do programa e os modelos mais abstratos representam conceitos comerciais que podem ou não podem ser representados no código.

Um modelo pode ser exibido por meio de vários tipos de diagramas. Para obter informações sobre modelos e diagramas, consulte [criar modelos para o aplicativo](../modeling/create-models-for-your-app.md).

Diferentes tipos de diagrama são úteis para descrever o design em diferentes níveis de abstração. Muitos dos tipos de diagrama são úteis em mais de um nível. Esta tabela mostra como cada tipo de diagrama pode ser usado.

|Nível de design|Tipos de diagrama|
|-|-|
|Processo de negócios<br /><br /> Noções básicas sobre o contexto no qual o sistema será usado o ajuda a entender o que os usuários que precisam dele.|-Diagramas de classe conceitual descrevem os conceitos de negócios usados dentro do processo de negócios.|
|Requisitos de usuário<br /><br /> Definição do que os usuários que precisa do seu sistema.|-Regras de negócio e a qualidade dos requisitos de serviço podem ser descritos em documentos separados.|
|Design de nível alto<br /><br /> A estrutura geral do sistema: os principais componentes e como eles acoplar juntos.|-Diagramas de dependência descrevem como o sistema está estruturado em partes interdependentes. Você pode validar o código do programa em diagramas de dependência para garantir que ela adere à arquitetura.|
|Análise de código<br /><br /> Diagramas podem ser gerados a partir do código.|-Diagramas de dependência mostram as dependências entre classes. Código atualizado pode ser validado em relação a um diagrama de dependência.<br />-Diagramas de classe mostram as classes no código.|

## <a name="external-resources"></a>Recursos externos

|**Categoria**|**Links**|
|-|-|
|**Vídeos**|![link para vídeo](../data-tools/media/playvideo.gif) [MSDN vídeos como faço: como criar e usar modelos de UML e diagramas (Visual Studio 2010 Ultimate)](http://go.microsoft.com/fwlink/?LinkId=214460)<br /><br /> ![link para vídeo](../data-tools/media/playvideo.gif) [Channel 9: UML no Visual Studio 2010](http://go.microsoft.com/fwlink/?LinkID=201106)<br /><br /> ![link para vídeo](../data-tools/media/playvideo.gif) [série MSDN How Do I: ferramentas UML e extensibilidade (Visual Studio 2010 Ultimate)](http://go.microsoft.com/fwlink/?LinkID=214467)|
|**Fóruns**|- [Visualização do Visual Studio e ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)<br />- [Visualização do Visual Studio e modelagem (ferramentas DSL) do SDK](http://go.microsoft.com/fwlink/?LinkId=184721)|
|**Blogs**|[Microsoft DevOps](https://blogs.msdn.microsoft.com/devops/)|
|**Artigos técnicos e diários**|[MSDN Architecture Center](http://go.microsoft.com/fwlink/?LinkId=201343)<br /><br /> [Diretrizes de ferramentas de arquitetura do Visual Studio](../modeling/visual-studio-architecture-tooling-guidance.md)|

## <a name="see-also"></a>Consulte também

- [Usar modelos no desenvolvimento Agile](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f)
- [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)
- [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)
- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)
- [Desenvolver testes por meio de um modelo](../modeling/develop-tests-from-a-model.md)
- [Estruturar a solução de modelagem](../modeling/structure-your-modeling-solution.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
