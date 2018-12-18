---
title: O que&#39;s novo design no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- what's new [VIsual Studio ALM], architecture and modeling
- architecture [Visual Studio Ultimate], modeling
- modeling software [Visual Studio ALM], What's New
ms.assetid: 36ab5c17-6dc0-4075-a28e-a0fa49b11260
caps.latest.revision: 34
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: ee504d0054c52649d48676451168e7dea171b6af
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51771283"
---
# <a name="whats-new-for-design-in-visual-studio"></a>Novidades no design no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
Esta versão do Visual Studio inclui os seguintes aprimoramentos para ajudá-lo a entender melhor e criar o código.

 **Gráficos de dependência e mapas de código**

 No Visual Studio Enterprise, quando você quiser entender dependências específicas em seu código, exiba-os Criando mapas de código. Em seguida, você pode navegar essas relações usando o mapa, que aparece ao lado de seu código. Mapas de código também podem ajudar a manter o controle de seu local no código enquanto você trabalha ou depura código, portanto, você lerá menos códigos enquanto aprende mais sobre o design do seu código.

 Na versão final (RTM), fizemos os menus de atalho para elementos de código e links muito mais fácil de usar, agrupando comandos em seções relacionadas ao selecionar, edição, gerenciamento de grupos e alterando o layout do conteúdo do grupo. Observe também que os projetos de teste são exibidos em um estilo diferente de outros projetos e que atualizamos os ícones de elementos no mapa para versões mais adequadas.

 ![Mostrar itens selecionados em um novo mapa de códigos](../ide/media/codemapsshowonnewmap.png "CodeMapsShowOnNewMap")

 Outros aprimoramentos incluem:

- **Diagramas de cima para baixo melhorados**. Para médias e grandes soluções do Visual Studio, agora você pode usar um menu de arquitetura simplificado para obter um código mais útil mapas para sua solução. Os assemblies da sua solução são agrupados pelas pastas de solução, para que você possa vê-los no contexto e aproveitar o esforço feito para estruturar a solução. Você verá imediatamente projeto e referências de assembly e, em seguida, os tipos de link que aparecem. Além disso, os assemblies externos à solução são agrupados de forma mais compacta.

- **Projetos de teste têm estilo diferente e podem ser filtrados**. Você pode agora mais fácil e rapidamente identificar os projetos de teste no mapa porque eles têm estilos diferentes. Eles também podem ser filtrados para que você possa se concentrar no código de trabalho do aplicativo.

- **Links de dependência externa de simplificado**. Links de dependência não mais representam a herança de System. Object, System. ValueType, System. Enum e System. Delegate, que facilita ver dependências externas no mapa de códigos.

- **'Drill-in into dependency links' leva os filtros em consideração**. Você obtém um diagrama simples e útil quando expande para compreender as contribuições para um link de dependência. O diagrama é menos desorganizado e leva em consideração as opções que você selecionou de filtragem de link.

- **Elementos de código são adicionados a um mapa de código com seus contexto**. Como os diagramas agora aparecem com contexto (até assembly e solução de pasta que você pode filtrar as se necessário), que você conseguir diagramas mais eficientes ao arrastar e soltar elementos de código do Gerenciador de soluções, o modo de exibição de classe, o Pesquisador de objetos; ou, quando selecionar elementos no Gerenciador de soluções e selecionando mostram no mapa de códigos.

- **Obtenha mapas de código reativos mais rapidamente**. Arrastar e soltar operações produzem um resultado imediato, e os links entre os nós são criados com muito mais rapidamente, sem afetar as operações posteriores iniciadas pelo usuário, como expandir um nó ou solicitar mais nós. Quando você cria mapas de código sem compilar a solução, todos os casos de canto, como quando os assemblies não são compilados — agora são processados.

- **Ignorar a recompilação de sua solução.** Fornece um melhor desempenho durante a criação e edição de diagramas.

- **Filtrar nós de elemento de código e grupos**. Você organizar rapidamente seus mapas ao exibir ou ocultar elementos de código com base em sua categoria, bem como pelo agrupamento de elementos de código por pastas de solução, assemblies, namespaces, pastas de projeto e tipos.

- **Filtre relações para tornar os diagramas mais fáceis de ler**. Filtragem de link agora também se aplica para cruzar os links de grupo, o que torna o trabalho com a janela de filtros menos intrusivo que do que era nas versões anteriores.

- **Criar diagramas da exibição de classe e Pesquisador de objetos**. Arraste e solte arquivos e assemblies em um novo ou um mapa existente do windows de modo de exibição de classe e Pesquisador de objetos.

  Ver [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md).

  **Outras alterações de design e modelagem nesta versão:**

- **Diagramas de camada**. Atualize esses diagramas usando o modo de exibição de classe e Pesquisador de objetos. Para atender aos requisitos de design de software, use diagramas de camada para descrever as dependências desejadas para seu software. Mantenha o código consistente com esse design, localizando o código que não atende a essas restrições e validando códigos futuros com essa linha de base.

- **Diagramas de UML**. Você não pode mais criar diagramas de classe UML e diagramas de sequência do código. Mas você ainda criar esses diagramas usando novos elementos UML.

- **Gerenciador de arquitetura**. Não há mais você pode usar o Architecture Explorer para criar diagramas. Mas você ainda pode usar o Gerenciador de soluções.

##  <a name="VersionSupport"></a> Suporte de edição para a arquitetura e ferramentas de modelagem

Visual Studio 2015 está disponível em várias edições. Nem todos eles oferecem suporte para a arquitetura e ferramentas de modelagem. A tabela a seguir mostra a disponibilidade de cada ferramenta.

|**Recurso**|**Enterprise**|**Professional**|**Comunidade**|**Express**|
|-----------------|--------------------|----------------------|-------------------|-----------------|
|**Mapas de código**|Sim|Só dá suporte à leitura e filtragem de mapas de código, adicionar novos nós genéricos e criando um novo gráfico direcionado a partir de uma seleção.|-|-|
|**Diagramas de classe UML**|Sim|-|-|-|
|**Diagramas de sequência UML**|Sim|-|-|-|
|**Diagramas de caso de uso UML**|Sim|-|-|-|
|**Diagramas de atividade UML**|Sim|-|-|-|
|**Diagramas de componente UML**|Sim|-|-|-|
|**Diagramas de camada**|Sim|-|-|-|
|**Gráficos direcionados** (diagramas DGML)|Sim|Sim|-|-|
|**Clone de código**|Sim|-|-|-|