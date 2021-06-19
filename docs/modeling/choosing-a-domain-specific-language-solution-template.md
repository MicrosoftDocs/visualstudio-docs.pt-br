---
title: Escolhendo um modelo de solução de linguagem específica do domínio
description: Saiba como criar uma solução de linguagem específica ao domínio escolhendo um dos modelos de solução que estão disponíveis no Assistente Domain-Specific Designer de Linguagem.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, solution templates
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c1c638c5a45427fd474f085ff58c9d38682ee054
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385429"
---
# <a name="choosing-a-domain-specific-language-solution-template"></a>Escolhendo um modelo de solução de linguagem específica do domínio
Para criar uma solução de linguagem específica ao domínio, escolha um dos modelos de solução que estão disponíveis no Assistente Domain-Specific Designer de Linguagem. Ao escolher o modelo mais parecido com o idioma que você deseja criar, você pode minimizar as modificações que você precisa fazer na solução inicial.

 Os modelos de solução a seguir estão disponíveis no Assistente Domain-Specific Designer de Linguagem.

|Modelo|Recursos|Descrição|
|-|-|-|
|Diagramas de classe|– Formas de compartimento<br />– Herança de classe<br />– Herança de relação<br />– Herança de forma<br />- Propriedades de relação|Use esse modelo de solução se o idioma específico do domínio incluir entidades e relações que têm propriedades. Esse modelo cria uma linguagem específica do domínio que se assemelha a diagramas de classe UML. As entidades principais são classes e interfaces, juntamente com relações de associação, generalização e implementação. Uma classe ou interface aparece como uma caixa que contém uma lista de atributos.|
|Diagramas de componente|- Portas|Use esse modelo de solução se sua linguagem específica do domínio incluir componentes, ou seja, partes de um sistema de software. Esse modelo cria uma linguagem específica do domínio que se assemelha a diagramas de componente UML. As principais entidades são componentes e portas, que aparecem como formas pequenas fora dos componentes.|
|Diagramas de fluxo de tarefas|– Formas de imagem e geometria<br />-   *Raias*|Use esse modelo de solução se a linguagem específica do domínio incluir fluxos de trabalho, estados ou sequências. Esse modelo cria uma linguagem específica do domínio que se assemelha a diagramas de atividade UML. A entidade principal é uma atividade e a relação principal é uma transição entre atividades. O modelo inclui vários outros elementos, como estado inicial, estado final e uma barra de sincronização.|
|Linguagem mínima|- Uma classe e forma<br />– Uma relação e um conector|Use esse modelo de solução se o idioma específico do domínio não for semelhante aos outros modelos. Esse modelo cria uma linguagem específica do domínio que tem duas  classes e uma relação, que são representadas na Caixa de Ferramentas **como Box** e **Line.** A classe e a relação têm uma propriedade de cadeia de caracteres de exemplo.|
|Designer WinForm mínimo|– Um modelo pequeno.<br />- Um Windows Form que exibe o modelo.|Use esse modelo se você quiser criar um aplicativo no qual uma DSL está vinculada a um Windows Form, em vez de um designer gráfico.<br /><br /> O formulário que atua como a interface do usuário para o idioma está na pasta Dsl\UI.<br /><br /> Você deve criar o projeto antes de abrir o designer de formulário.<br /><br /> Para obter mais informações, consulte [Criando uma linguagem Forms-Based Domain-Specific Windows](../modeling/creating-a-windows-forms-based-domain-specific-language.md).|
|Designer mínimo do WPF|– Um modelo pequeno<br />- Uma Windows Presentation Foundation de usuário que exibe o modelo|Use esse modelo se você quiser criar um aplicativo no qual uma DSL está vinculada a uma interface do usuário do WPF, em vez de um designer gráfico.<br /><br /> O designer para a interface do usuário está na pasta Dsl\UI.<br /><br /> Você deve criar o projeto antes de abrir o designer de interface do usuário.<br /><br /> Para obter mais informações, consulte [Criando uma linguagem WPF-Based Domain-Specific .](../modeling/creating-a-wpf-based-domain-specific-language.md)|
|Biblioteca de DSL|- Uma biblioteca mínima|Use esse modelo se você quiser criar uma definição de DSL parcial que possa ser importada para outras definições de DSL.|

## <a name="see-also"></a>Confira também

- [Visão geral das Ferramentas de Linguagem Específica do Domínio](../modeling/overview-of-domain-specific-language-tools.md)
