---
title: Requisitos de usuário do modelo
description: Saiba como Visual Studio ajuda você a entender, discutir e comunicar as necessidades dos usuários desenhando diagramas sobre suas atividades.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- requirements
- stories
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 381395eb0b9dabde0e94c479cb43033bc8443c8f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390145"
---
# <a name="model-user-requirements"></a>Requisitos de usuário do modelo

Visual Studio ajuda você a entender, discutir e comunicar as necessidades dos usuários desenhando diagramas sobre suas atividades e a parte que seu sistema desempenha ao ajudá-los a atingir suas metas. Um modelo de requisitos é um conjunto desses diagramas, cada um deles se concentra em um aspecto diferente das necessidades dos usuários. Para ver uma demonstração em vídeo, confira: [Modelando o domínio de negócios.](https://channel9.msdn.com/blogs/clinted/uml-with-vs-2010-part-3-modeling-the-business-domain)

Para ver quais versões do Visual Studio dar suporte a cada tipo de modelo, consulte [Suporte de versão para ferramentas de arquitetura e modelagem](../modeling/analyze-and-model-your-architecture.md#VersionSupport).

Um modelo de requisitos ajuda você a:

- Concentre-se no comportamento externo do sistema, separadamente de seu design interno.

- Descreva as necessidades dos usuários e dos stakeholders com muito menos ambiguidade do que você pode em linguagem natural.

- Defina um glossário consistente de termos que podem ser usados por usuários, desenvolvedores e testadores.

- Reduzir lacunas e inconsistências nos requisitos.

- Reduza o trabalho necessário para responder às alterações de requisitos.

- Planeje a ordem na qual os recursos serão desenvolvidos.

- Use os modelos como base para testes do sistema, tornando uma relação clara entre os testes e os requisitos. Quando os requisitos mudam, essa relação ajuda você a atualizar os testes corretamente. Isso garante que o sistema atenda aos novos requisitos.

Um modelo de requisitos oferece o maior benefício se você usá-lo para concentrar discussões com os usuários ou seus representantes e revisitá-lo no início de cada iteração. Você não precisa conclu-lo em detalhes antes de escrever código. Um aplicativo parcialmente funcionando, mesmo que muito simplificado, geralmente forma a base mais interessante para discussão dos requisitos com os usuários. O modelo é uma maneira eficaz de resumir os resultados dessas discussões. Para obter mais informações, [consulte Usar modelos em seu processo de desenvolvimento](../modeling/use-models-in-your-development-process.md).

> [!NOTE]
> Ao longo desses tópicos, "system" significa o sistema ou o aplicativo que você está desenvolvendo. Pode ser uma grande coleção de muitos componentes de software e hardware; ou um único aplicativo; ou um componente de software dentro de um sistema maior. Em todos os casos, o modelo de requisitos descreve o comportamento visível de fora do sistema, seja por meio de uma interface do usuário ou API.

## <a name="common-tasks"></a>Tarefas comuns

Você pode criar várias exibições diferentes dos requisitos dos usuários.  Cada exibição fornece um tipo específico de informações.  Quando você cria essas exibições, é melhor mover com frequência de uma para outra. Você pode iniciar em qualquer exibição.

|Diagrama ou documento|O que ele descreve em um modelo de requisitos|Seção|
|-|-|-|
|Diagrama de classe conceitual|Glossário de tipos que são usados para descrever os requisitos; os tipos visíveis na interface do sistema.||
|Documentos adicionais ou itens de trabalho|Critérios de desempenho, segurança, usabilidade e confiabilidade.|[Descrevendo a qualidade dos requisitos de serviço](#QoSRequirements)|
|Documentos adicionais ou itens de trabalho|Restrições e regras não específicas para um caso de uso específico|[Mostrando regras de negócio](#BusinessRules)|

Observe que a maioria dos tipos de diagrama pode ser usada para outras finalidades. Para uma visão geral dos tipos de diagrama, [consulte Criar modelos para seu aplicativo.](../modeling/create-models-for-your-app.md)

## <a name="showing-business-rules"></a><a name="BusinessRules"></a> Mostrando Business Rules

Uma regra de negócio é um requisito que não está associado a um caso de uso específico e deve ser observado em todo o sistema.

Muitas regras de negócio são restrições nas relações entre as classes conceituais. Você pode escrever essas *regras de negócio estáticas* como comentários associados às classes relevantes em um diagrama de classe conceitual. Por exemplo:

![Regra em Comentário anexado à classe Order.](../modeling/media/uml_reqmcd2.png)

*As regras de negócio* dinâmicas restringem as sequências de eventos que permitem. Por exemplo, você usa um diagrama de sequência ou atividade para mostrar que um usuário deve fazer logoff antes de executar outras operações em seu sistema.

No entanto, muitas regras dinâmicas podem ser afirmadas de forma mais eficaz e genérica substituindo-as por regras estáticas. Por exemplo, você pode adicionar um atributo booliana 'Conectado' a uma classe no modelo de classe conceitual. Você adicionaria Conectado como a pós-condição do log no caso de uso e o adicionaria como uma pré-condição da maioria dos outros casos de uso. Essa abordagem permite evitar definir todas as combinações possíveis de sequências de eventos. Também é mais flexível quando você precisa adicionar novos casos de uso ao modelo.

Observe que a opção aqui é sobre como você define os requisitos e que isso é independente de como você implementa os requisitos no código do programa.

Os tópicos a seguir fornecem mais informações:

|Para saber mais|Ler|
|-|-|
|Como desenvolver código que adere às regras de negócio|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|

## <a name="describing-quality-of-service-requirements"></a><a name="QoSRequirements"></a> Descrevendo requisitos de qualidade de serviço

Há várias categorias de requisito de qualidade de serviço. Eles incluem o seguinte:

- Desempenho

- Segurança

- Usabilidade

- Confiabilidade

- Robustez

Você pode incluir alguns desses requisitos nas descrições de casos de uso específicos. Outros requisitos não são específicos para casos de uso e são escritos com mais eficiência em um documento separado. Quando você pode, é útil aderir ao vocabulário definido pelo modelo de requisitos. No exemplo a seguir, observe que as palavras principais usadas no requisito são os títulos de atores, casos de uso e classes nas ilustrações anteriores:

Se um Restaurante excluir um item de menu enquanto um cliente está ordenando uma refeição, qualquer item de pedido que se refere a esse Item de Menu será exibido em vermelho.

Confira [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md) para saber como desenvolver código que adere aos requisitos de qualidade de serviço.

## <a name="see-also"></a>Confira também

- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)
