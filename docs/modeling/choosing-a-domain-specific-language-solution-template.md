---
title: Escolhendo um modelo de solução de linguagem específica do domínio
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, solution templates
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: d2977d546d463a8c21446a3643cff7ef49a01fb1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49908815"
---
# <a name="choosing-a-domain-specific-language-solution-template"></a>Escolhendo um modelo de solução de linguagem específica do domínio
Para criar uma solução de linguagem específica de domínio, escolha um dos modelos de solução que estão disponíveis no Assistente de Designer de linguagem específica do domínio. Escolhendo o modelo que mais se assemelha a linguagem que você deseja criar, você pode minimizar as modificações que você precisa fazer a solução inicial.

 Os seguintes modelos de solução estão disponíveis no Assistente de Designer de linguagem específica do domínio.

|Modelo|Recursos|Descrição|
|-|-|-|
|Diagramas de classe|-Formas do compartimento<br />-Herança de classe<br />-Herança de relacionamento<br />-Herança de forma<br />-Propriedades de relação|Use esse modelo de solução se sua linguagem específica do domínio inclui entidades e relações que têm propriedades. Este modelo cria uma linguagem específica de domínio que se parece com diagramas de classe UML. As principais entidades são classes e interfaces, junto com os relacionamentos de associação, generalização e implementação. Uma classe ou interface é exibido como uma caixa que contém uma lista de atributos.|
|Diagramas de componente|-Portas|Use esse modelo de solução se sua linguagem específica do domínio inclui os componentes, ou seja, partes de um sistema de software. Este modelo cria uma linguagem específica de domínio que se parece com diagramas de componente UML. As principais entidades são componentes e portas, que são exibidos como formas pequenas fora dos componentes.|
|Diagramas de fluxo de tarefa|-Imagens e formas geométricas<br />-   *Raias*|Use esse modelo de solução se sua linguagem específica do domínio inclui fluxos de trabalho, estados ou sequências. Este modelo cria uma linguagem específica de domínio que se parece com diagramas de atividade UML. A entidade principal é uma atividade e a relação principal é uma transição entre atividades. O modelo inclui vários outros elementos, como estado inicial, o estado final e uma barra de sincronização.|
|Linguagem mínima|-Uma classe e forma<br />-Um relacionamento e conector|Use esse modelo de solução se sua linguagem específica do domínio não se assemelha os outros modelos. Este modelo cria uma linguagem específica de domínio que tem duas classes e uma relação, que são representados na **caixa de ferramentas** como **caixa** e **linha**. A classe e a relação tem uma propriedade de cadeia de caracteres de exemplo.|
|WinForm Designer mínimo|-Um modelo pequeno.<br />-Um formulário do Windows que exibe o modelo.|Use este modelo para criar um aplicativo em que uma DSL está associada a um formulário do Windows, em vez de um designer gráfico.<br /><br /> O formulário que atua como a interface do usuário para o idioma está na pasta Dsl\UI.<br /><br /> Você deve compilar o projeto antes de abrir o designer de formulário.<br /><br /> Para obter mais informações, consulte [criando uma linguagem específica de domínio de Windows Forms-Based](../modeling/creating-a-windows-forms-based-domain-specific-language.md).|
|Mínimo de WPF Designer|-Um modelo pequeno<br />-Uma interface de usuário do Windows Presentation Foundation que exibe o modelo|Use este modelo para criar um aplicativo em que uma DSL está associada a uma interface de usuário do WPF, em vez de um designer gráfico.<br /><br /> O designer de interface do usuário está na pasta Dsl\UI.<br /><br /> Você deve compilar o projeto antes de abrir o designer de interface do usuário.<br /><br /> Para obter mais informações, consulte [criando uma linguagem específica de domínio de WPF-Based](../modeling/creating-a-wpf-based-domain-specific-language.md).|
|Biblioteca de DSL|– Uma biblioteca mínima|Use este modelo se quiser compilar uma definição de DSL parcial que pode ser importada para outras definições de DSL.|

## <a name="see-also"></a>Consulte também

- [Visão geral das Ferramentas de Linguagem Específica de Domínio](../modeling/overview-of-domain-specific-language-tools.md)
