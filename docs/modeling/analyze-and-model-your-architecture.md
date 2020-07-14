---
title: Analisar e modelar a sua arquitetura
ms.date: 11/04/2016
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
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1db28867ea47752aa74b7898c44e797c0704594
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544216"
---
# <a name="analyze-and-model-your-architecture"></a>Analisar e modelar a sua arquitetura

Verifique se seu aplicativo atende aos requisitos de arquitetura usando ferramentas de arquitetura e modelagem do Visual Studio para criar e modelar seu aplicativo.

* Entenda o código do programa existente mais facilmente usando o Visual Studio para visualizar a estrutura, o comportamento e as relações do código.

* Instrua sua equipe na necessidade de respeitar as dependências de arquitetura.

* Crie modelos em diferentes níveis de detalhes ao longo do ciclo de vida do aplicativo como parte do seu processo de desenvolvimento.

Consulte [cenário: alterar o design usando visualização e modelagem](../modeling/scenario-change-your-design-using-visualization-and-modeling.md).

## <a name="article-reference"></a>Referência do artigo

|Cenário|Artigos|
|-|-|
|**Visualizar código**:<br /><br />-Consulte a organização do código e as relações Criando mapas de código. Visualize dependências entre assemblies, namespaces, classes, métodos e assim por diante.<br />-Consulte a estrutura de classe e os membros de um projeto específico Criando diagramas de classe do código.<br />-Encontre conflitos entre seu código e seu design criando diagramas de dependência para validar o código.|- [Visualizar código](../modeling/visualize-code.md)<br />- [Trabalhando com classes e outros tipos (Designer de Classe)](../ide/class-designer/designing-and-viewing-classes-and-types.md)<br />- [Vídeo: entenda o design do código com os mapas de código do Visual Studio 2015](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)<br />- [Vídeo: valide suas dependências de arquitetura em tempo real](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)|
|**Defina a arquitetura**:<br /><br />-Definir e impor restrições em dependências entre os componentes do seu código Criando diagramas de dependência.|- [Vídeo: validar dependências de arquitetura com o Visual Studio (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**Valide seu sistema com os requisitos e o design pretendido:**<br /><br />– Valide dependências de código com diagramas de dependência que descrevem a arquitetura desejada e evite alterações que possam entrar em conflito com o design.|- [Vídeo: validar dependências de arquitetura com o Visual Studio (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**Personalizar modelos e diagramas**:<br /><br />-Crie suas próprias linguagens específicas de domínio.|- [SDK de modelagem para Visual Studio-linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**Gerar texto usando modelos T4**:<br /><br />-Use blocos de texto e lógica de controle dentro de modelos para gerar arquivos baseados em texto.<br /> -Compilação de modelo T4 com MSBuild incluído no Visual Studio|- [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)|
|**Compartilhe modelos, diagramas e mapas de código usando o controle de versão do Team Foundation**:<br /><br />-Coloque mapas de código, projetos e diagramas de dependência sob o controle de versão do Team Foundation para que você possa compartilhá-los.| |

Para ver quais edições do Visual Studio oferecem suporte a cada recurso, consulte [suporte de edição para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="types-of-models-and-typical-uses"></a>Tipos de modelos e usos típicos

### <a name="code-maps"></a>Mapas de código

Os mapas de código ajudam você a ver a organização e as relações em seu código.

**Usos típicos:**

- Examine o código do programa para que você possa entender melhor sua estrutura e suas dependências, como atualizá-la e estimar o custo das alterações propostas.

**Esse**

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)

### <a name="dependency-diagrams"></a>Diagramas de dependência

Os diagramas de dependência permitem que você defina a estrutura de um aplicativo como um conjunto de camadas ou blocos com dependências explícitas. A validação dinâmica mostra conflitos entre dependências no código e as dependências descritas em um diagrama de dependência.

**Usos típicos:**

- Estabilizar a estrutura do aplicativo por meio de várias alterações ao longo de sua vida.
- Descubra conflitos de dependências não intencionais antes de fazer check-in de alterações no código.

**Esse**

- [Criar diagramas de dependência do código](../modeling/create-layer-diagrams-from-your-code.md)
- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)
- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)

### <a name="domain-specific-language-dsl"></a>DSL (linguagem específica de domínio)

Uma DSL é uma notação que você cria para uma finalidade específica. No Visual Studio, geralmente é gráfico.

**Usos típicos:**

- Gerar ou configurar partes do aplicativo. O trabalho é necessário para desenvolver a notação e as ferramentas. O resultado pode ser uma melhor opção para seu domínio do que uma personalização de UML.
- Para projetos grandes ou em linhas de produtos em que o investimento no desenvolvimento da DSL e suas ferramentas são retornadas por seu uso em mais de um projeto.

**Esse**

- [SDK de Modelagem para Visual Studio - linguagens específicas ao domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

## <a name="see-also"></a>Consulte também

- [O que há de novo para modelagem no Visual Studio 2017](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps e gerenciamento de ciclo de vida do aplicativo](/azure/devops/user-guide/devops-alm-overview)
