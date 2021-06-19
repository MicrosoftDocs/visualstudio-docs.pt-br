---
title: Ferramentas de modelagem de & de análise de arquitetura
description: Projete e modele seu aplicativo para garantir que seu aplicativo atenda aos requisitos de arquitetura.
ms.custom: SEO-VS-2020
ms.date: 06/04/2021
ms.topic: overview
helpviewer_keywords:
- diagrams - modeling
- architecture
- code visualization
- application design
- code exploration
- modeling
- application architecture
- architecture [Visual Studio ALM], modeling
- application modeling
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 542b74e7d3bb73847303fa4215651eea7e110e91
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384870"
---
# <a name="analyze-and-model-your-architecture"></a>Analisar e modelar a sua arquitetura

Verifique se seu aplicativo atende aos requisitos de arquitetura usando ferramentas de arquitetura e modelagem do Visual Studio para criar e modelar seu aplicativo.

1. Entenda melhor o código de programa existente [visualizando a](visualize-code.md) estrutura, o comportamento e as relações de código com mapas de código e diagramas de dependência.
    - Consulte a organização do código e as relações Criando **mapas de código**. 
    - Visualize dependências entre assemblies, namespaces, classes, métodos e assim por diante.
    - Encontre conflitos entre seu código e seu design criando **diagramas de dependência** para validar o código.
    - Veja a estrutura de classe e os membros de um projeto específico [Criando diagramas de classe do código](../ide/class-designer/designing-and-viewing-classes-and-types.md).
    - [Gere texto usando modelos T4](../modeling/code-generation-and-t4-text-templates.md) com blocos de texto e lógica de controle dentro de modelos para gerar arquivos baseados em texto. 
    
1. Instrua sua equipe na necessidade de respeitar as dependências de arquitetura.

1. Crie modelos em diferentes níveis de detalhes ao longo do ciclo de vida do aplicativo como parte do seu processo de desenvolvimento.

Consulte [cenário: alterar o design usando visualização e modelagem](../modeling/scenario-change-your-design-using-visualization-and-modeling.md).

## <a name="code-maps"></a>Mapas de código

Os mapas de código são um tipo de modelo que ajuda você a ver a organização e as relações em seu código.

Use mapas para examinar o código do programa para que você possa entender melhor sua estrutura e suas dependências, como atualizá-lo e estimar o custo das alterações propostas.

Saiba mais:
- [Instalar ferramentas de código de arquitetura](install-architecture-tools.md)
- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)

## <a name="dependency-diagrams"></a>Diagramas de dependência

Os diagramas de dependência permitem que você defina a estrutura de um aplicativo como um conjunto de camadas ou blocos com dependências explícitas. A validação dinâmica mostra conflitos entre dependências no código e as dependências descritas em um diagrama de dependência.

Use diagramas de dependência para: 
- Estabilizar a estrutura do aplicativo por meio de várias alterações ao longo de sua vida.
- Descubra conflitos de dependências não intencionais antes de fazer check-in de alterações no código.

Saiba mais:
- [Instalar ferramentas de código de arquitetura](install-architecture-tools.md)
- [Criar diagramas de dependência do código](../modeling/create-layer-diagrams-from-your-code.md)
- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)
- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)

## <a name="domain-specific-language-dsl-models"></a>Modelos de DSL (linguagem específica do domínio)

Uma DSL é uma notação que você cria para uma finalidade específica. No Visual Studio, geralmente é gráfico.

Use a linguagem específica do domínio para: 
- Gerar ou configurar partes do aplicativo. O trabalho é necessário para desenvolver a notação e as ferramentas. O resultado pode ser uma melhor opção para seu domínio do que uma personalização de UML.
- Para projetos grandes ou em linhas de produtos em que o investimento no desenvolvimento da DSL e suas ferramentas são retornadas por seu uso em mais de um projeto.

Saiba mais:
- [SDK de Modelagem para Visual Studio - linguagens específicas ao domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)


## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />Suporte de edição para ferramentas de arquitetura e modelagem

O Visual Studio está disponível em várias edições. Nem todos eles oferecem suporte para as ferramentas de arquitetura e modelagem. A tabela a seguir mostra a disponibilidade de cada ferramenta.

|**Recurso**|**Enterprise Edition**|**Professional Edition**|**Community Edition**|
|-|-|-|-|
|**Mapas de código**|Sim|Dá suporte apenas à leitura de mapas de código, filtragem de mapas de código, adição de novos nós genéricos e criação de um novo grafo direcionado a partir de uma seleção.|-|
|**Diagramas de dependência**|Sim|Dá suporte apenas à leitura de diagramas de dependência.|Dá suporte apenas à leitura de diagramas de dependência.|
|**Grafos direcionados** (diagramas dgml)|Sim|Sim|Sim|
|**Clone de código**|Sim|-|-|
