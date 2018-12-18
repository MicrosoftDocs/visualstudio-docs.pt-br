---
title: Analisar e modelar a sua arquitetura
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
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
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4b32f5585c71f5767a907d9f3eb9c2dc8329ab97
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51348872"
---
# <a name="analyze-and-model-your-architecture"></a>Analisar e modelar a sua arquitetura

Verifique se que o aplicativo atende aos requisitos de arquitetura usando a arquitetura do Visual Studio e ferramentas para projetar e modelar seu aplicativo de modelagem.

* Entenda o código existente do programa com mais facilidade usando o Visual Studio para visualizar a estrutura do código, o comportamento e relações.

* Treinar sua equipe na necessidade de respeitando as dependências de arquitetura.

* Crie modelos em diferentes níveis de detalhe em todo o ciclo de vida do aplicativo como parte de seu processo de desenvolvimento.

Ver [cenário: alterar o design usando visualização e modelagem](../modeling/scenario-change-your-design-using-visualization-and-modeling.md).

## <a name="to"></a>Para

|||
|-|-|
|**Visualizar código**:<br /><br /> -Consulte a organização e os relacionamentos do código Criando mapas de código. Visualize dependências entre assemblies, namespaces, classes, métodos e assim por diante.<br />-Consulte a estrutura de classes e membros para um projeto específico com a criação de diagramas de classe do código.<br />-Encontre conflitos entre o código e seu design com a criação de diagramas de dependência para validar o código.|-   [Visualizar código](../modeling/visualize-code.md)<br />-   [Trabalhando com Classes e outros tipos (Designer de classe)](../ide/working-with-classes-and-other-types-class-designer.md)<br />-   [Vídeo: Entenda design de código com mapas de código do Visual Studio 2015](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)<br />-   [Vídeo: Validar suas dependências de arquitetura em tempo real](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)|
|**Definir a arquitetura**:<br /><br /> -Definir e impor restrições sobre dependências entre os componentes do seu código com a criação de diagramas de dependência.|-   [Vídeo: Validar dependências de arquitetura com o Visual Studio (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**Validar o sistema com os requisitos e se destina a design:**<br /><br /> -Validar dependências de código com diagramas de dependência que descrevem a arquitetura pretendida e evitar alterações entrarem em conflito com o design.|-   [Vídeo: Validar dependências de arquitetura com o Visual Studio (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**Personalizar modelos e diagramas**:<br /><br /> -Crie seus próprios linguagens específicas de domínio.|-   [SDK de modelagem para Visual Studio - linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**Gerar texto usando modelos T4**:<br /><br /> -Usar blocos de texto e a lógica de controle dentro de modelos para gerar arquivos baseados em texto.<br /> -Compilação de modelo T4 com o MSBuild incluída no Visual Studio|-   [Geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md)|
|**Compartilhar modelos, diagramas e mapas de código usando o controle de versão do Team Foundation**:<br /><br /> -Coloque mapas de código, projetos e diagramas de dependência sob controle de versão do Team Foundation para que você pode compartilhá-los.| |

Para ver quais edições do Visual Studio dão suporte a cada recurso, consulte [suporte de edição para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)

## <a name="types-of-models-and-typical-uses"></a>Tipos de modelos e usos típicos

### <a name="code-maps"></a>Mapas de código
Mapas de código ajudam você a ver a organização e relações em seu código.

**Usos típicos:**

-   Examinar o código de programa para que você possa entender melhor a sua estrutura e suas dependências, como atualizá-lo e estimar o custo de alterações propostas.

**Consulte:**

-   [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
-   [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
-   [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)

### <a name="dependency-diagram"></a>Diagrama de dependência
Diagramas de dependência permitem que você definir a estrutura de um aplicativo como um conjunto de blocos com dependências explícitas ou camadas. Você pode executar a validação para detectar conflitos entre dependências no código e descritos em um diagrama de dependência.

**Usos típicos:**

-   Estabilize a estrutura do aplicativo por meio de várias alterações ao longo do ciclo de vida.
-   Detecte conflitos de dependência não intencional antes de fazer check-in de alterações no código.

**Consulte:**

-   [Criar diagramas de dependência usando seu código](../modeling/create-layer-diagrams-from-your-code.md)
-   [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)
-   [Validar código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)

### <a name="domain-specific-language-dsl"></a>Linguagem específica de domínio (DSL)
Uma DSL é uma notação de design para uma finalidade específica. No Visual Studio, é geralmente gráfica.

**Usos típicos:**

-   Gerar ou configurar as partes do aplicativo. Trabalho é necessário para desenvolver as ferramentas e a notação. O resultado pode ser mais adequado ao seu domínio do que uma personalização de UML.
-   Para projetos grandes ou em linhas de produtos em que o investimento em DSL e suas ferramentas de desenvolvimento é retornado por seu uso em mais de um projeto.

**Consulte:**

-   [SDK de Modelagem para Visual Studio – linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

## <a name="where-can-i-get-more-information"></a>Onde posso obter mais informações?

[Visualização do Visual Studio & Fórum das ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)

## <a name="see-also"></a>Consulte também

- [O que há de novo](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps e gerenciamento de ciclo de vida do aplicativo](/azure/devops/user-guide/devops-alm-overview)
