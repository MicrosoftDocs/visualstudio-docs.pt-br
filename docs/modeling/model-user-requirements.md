---
title: Requisitos de usuário do modelo
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- requirements
- stories
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 4791566d3c37517c3c93e62e371bf4cbc9fc6604
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966551"
---
# <a name="model-user-requirements"></a>Requisitos de usuário do modelo

Visual Studio ajuda a entender, discuta e comunicar-se suas necessidades de usuários ao desenhar diagramas sobre suas atividades e a parte seu sistema é reproduzido ajudá-los a atingir suas metas. Um modelo de requisitos é um conjunto desses diagramas, cada um deles enfoca um aspecto das necessidades dos usuários. Para uma demonstração em vídeo, consulte: [modelagem do domínio de negócios](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-3-modeling-the-business-domain).

Para ver quais versões do Visual Studio dão suporte a cada tipo de modelo, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

Um modelo de requisitos ajuda você a:

- Focalizar o comportamento do sistema externo, separadamente do seu design interno.

- Descrever dos usuários e das partes interessadas precisa com muito menos ambiguidade que no idioma natural.

- Defina um glossário consistente de termos que podem ser usados por usuários, desenvolvedores e testadores.

- Reduza as lacunas e inconsistências nos requisitos.

- Reduza o trabalho necessário para responder a alterações de requisitos.

- Planeje a ordem na qual os recursos serão desenvolvidos.

- Use os modelos como base para testes de sistema, fazendo uma relação clara entre os testes e os requisitos. Quando os requisitos mudam, essa relação ajuda você a atualizar os testes corretamente. Isso garante que o sistema atende aos novos requisitos.

Um modelo de requisitos fornece o maior benefício se você usá-lo para discussões de foco com os usuários ou seus representantes e visite-a no início de cada iteração. Não é necessário para concluí-lo detalhadamente antes de escrever código. Um aplicativo de trabalho parcialmente, mesmo se muito simplificado, geralmente constitui a base mais interessantes para discussão sobre os requisitos de usuários. O modelo é uma maneira eficaz de resumir os resultados dessas discussões. Para obter mais informações, consulte [usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md).

> [!NOTE]
> Ao longo desses tópicos, "system" significa que o sistema ou o aplicativo que você está desenvolvendo. Pode ser uma grande coleção de muitos componentes de hardware e software; ou um único aplicativo; ou um componente de software dentro de um sistema maior. Em todos os casos, o modelo de requisitos descreve o comportamento que é visível fora do seu sistema, seja por meio de uma interface do usuário ou a API.

## <a name="common-tasks"></a>Tarefas comuns

Você pode criar várias exibições diferentes dos requisitos dos usuários.  Cada modo de exibição fornece um tipo específico de informações.  Quando você cria esses modos de exibição, é melhor mudam frequentemente uns aos outros. Você pode iniciar a partir de qualquer modo de exibição.

|Diagrama ou documento|Ele descreve em um modelo de requisitos|Seção|
|-|-|-|
|Diagrama de classe conceitual|Glossário de tipos que são usados para descrever os requisitos; os tipos visíveis na interface do sistema.||
|Documentos adicionais ou itens de trabalho|Critérios de desempenho, segurança, usabilidade e confiabilidade.|[Que descreve a qualidade dos requisitos de serviço](#QoSRequirements)|
|Documentos adicionais ou itens de trabalho|Restrições e regras não específicas a um determinado caso de uso|[Mostrando as regras de negócio](#BusinessRules)|

Observe que a maioria dos tipos de diagrama pode ser usada para outras finalidades. Para obter uma visão geral dos tipos de diagrama, consulte [criar modelos para o aplicativo](../modeling/create-models-for-your-app.md).

##  <a name="BusinessRules"></a> Mostrando as regras de negócio

Uma regra de negócios é um requisito que não está associado um caso de uso específico e deve ser observado em todo o sistema.

Muitas regras de negócios são restrições nas relações entre as classes conceituais. Você pode escrever esses *regras de negócio estático* como comentários associados com as classes relevantes em um diagrama de classe conceitual. Por exemplo:

![Regra em comentário anexado à classe Order.](../modeling/media/uml_reqmcd2.png)

*Regras de negócio dinâmico* restringir as permitidas sequências de eventos. Por exemplo, você deve usar um diagrama de sequência ou atividade para mostrar que um usuário deve fazer logon antes de executar outras operações em seu sistema.

No entanto, muitas regras dinâmicas podem ser com mais eficiência e genericamente declaradas substituindo-os por regras estáticas. Por exemplo, você poderia adicionar um atributo booliano 'Registrado em' a uma classe no modelo conceitual de classe. Você seria adicionar conectado como a pós-condição do log em caso de uso e adicioná-lo como uma pré-condição para a maioria dos casos de uso. Essa abordagem permite que você evite definir todas as combinações possíveis de sequências de eventos. Também é mais flexível quando você precisa adicionar novos casos de uso para o modelo.

Observe que a escolha aqui é sobre como definir os requisitos e que isso é independente de como implementar os requisitos no código do programa.

Os tópicos a seguir fornecem mais informações:

|Para saber mais sobre|Ler|
|-|-|
|Como desenvolver um código que obedeça às regras de negócio|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|

##  <a name="QoSRequirements"></a> Que descreve a qualidade dos requisitos de serviço

Há várias categorias de qualidade de requisito de serviço. Elas incluem o seguinte:

-   Desempenho

-   Segurança

-   Usabilidade

-   Confiabilidade

-   Robustez

Você pode incluir alguns desses requisitos nas descrições de casos de uso específico. Outros requisitos não são específicos para casos de uso e com mais eficiência são gravados em um documento separado. Quando possível, é útil cumprir o vocabulário definido pelo modelo de requisitos. No exemplo a seguir, observe-se de que as palavras principais usadas requisitos de estão os títulos das classes nas ilustrações anteriores, casos de uso e atores:

Se um restaurante exclui um Item de Menu, enquanto que um cliente é ordenar uma refeição, qualquer Item do pedido que se refere a esse Item de Menu será exibido em vermelho.

Ver [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md) para aprender a desenvolver código que obedeça a qualidade dos requisitos de serviço.

## <a name="see-also"></a>Consulte também

- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)
