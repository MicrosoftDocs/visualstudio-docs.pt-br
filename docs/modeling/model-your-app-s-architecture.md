---
title: Modelar seu aplicativo&#39;arquitetura s
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UML, modeling architecture
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 7322738fe1bd17944bc5d1883bc9c16e56cc59e6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49855062"
---
# <a name="model-your-app39s-architecture"></a>Modelar seu aplicativo&#39;arquitetura s
Para ajudar a garantir que seu aplicativo ou sistema de software atenda aos seus usuários precisa, você pode criar modelos no Visual Studio como parte de sua descrição da estrutura geral e o comportamento do seu aplicativo ou sistema de software. Usando modelos, você também pode descrever padrões que são usados em todo o design. Esses modelos de ajudarão-lo a entender a arquitetura existente, discutir as mudanças e comunique suas intenções claramente.

 Para ver quais edições do Visual Studio dão suporte a esse recurso, consulte [suporte de edição para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

 A finalidade de um modelo é reduzir as ambiguidades que ocorrem nas descrições de linguagem natural e para ajudar você e seus colegas para visualizar o design e para discutir designs alternativos. Um modelo deve ser usado junto com outros documentos ou discussões. Por si só, um modelo não representa uma especificação completa da arquitetura.

> [!NOTE]
>  Ao longo deste tópico, "system" significa que o software que você está desenvolvendo. Pode ser uma grande coleção de muitos componentes de hardware e software, ou um único aplicativo ou uma parte de um aplicativo.

 A arquitetura de um sistema pode ser dividida em duas áreas:

-   [Design de alto nível](#Structure). Descreve os principais componentes e como eles interagem entre si para atender a cada requisito. Se o sistema for grande, cada componente pode ter seu próprio design de alto nível que mostra como ele é composto de componentes menores.

-   [Padrões de design](#Patterns) e as convenções usadas nos designs de componentes. Um padrão descreve uma abordagem específica para alcançar uma meta de programação. Usando os mesmos padrões em todo um design, sua equipe pode reduzir o custo de fazer alterações e desenvolvimento de software novo.

## <a name="Structure"></a> Design de alto nível
 Um design de alto nível descreve os principais componentes do seu sistema e como eles interagem entre si para atingir as metas do design. As atividades na lista a seguir são envolvidas no desenvolvimento do design de alto nível, embora não necessariamente em uma sequência específica.

 Se você estiver atualizando o código existente, você pode começar descrevendo os principais componentes. Verifique se você compreender todas as alterações para os requisitos de usuário e, em seguida, adicionar ou modificar as interações entre os componentes. Se você estiver desenvolvendo um novo sistema, comece Noções básicas sobre os principais recursos das necessidades dos usuários. Você pode, em seguida, explore as sequências de interações para os casos de uso principal e, em seguida, consolidar as sequências em um design do componente.

 Em todos os casos, ele é útil para desenvolver as atividades diferentes em paralelo e desenvolver código e testes em um estágio inicial. Evite tentar concluir um dos seguintes aspectos antes de começar outra. Normalmente, os requisitos e seu conhecimento sobre a melhor maneira de projetar o sistema serão alterado enquanto você está gravando e testando o código. Portanto, você deve começar Entendendo e os principais recursos do seu design e os requisitos de codificação. Preencha os detalhes em iterações posteriores do projeto.

-   [Noções básicas sobre os requisitos de](#Requirements). O ponto de partida de qualquer design é uma compreensão clara de necessidades dos usuários.

-   [Padrões de arquitetura](#BigDecisions). As escolhas feitas sobre as principais tecnologias e os elementos de arquitetura do sistema.

-   Modelo de dados dos componentes e Interfaces. Você pode desenhar diagramas de classe para descrever as informações que são passadas entre componentes e armazenadas dentro dos componentes.

## <a name="Requirements"></a> Noções básicas sobre os requisitos
 O design de alto nível de um aplicativo completo com mais eficiência é desenvolvido em conjunto com um modelo de requisitos ou outra descrição das necessidades dos usuários. Para obter mais informações sobre modelos de requisitos, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).

 Se o sistema que você está desenvolvendo um componente em um sistema maior, parte ou todos os seus requisitos podem ser incorporados em interfaces programáticas.

 O modelo de requisitos fornece essas duas informações essenciais:

- Interfaces fornecidas. Uma interface fornecida lista os serviços ou as operações do sistema ou componente deve fornecer a seus usuários, independentemente de estarem usuários humanos ou outros componentes de software.

- Interfaces necessárias. Uma interface necessária lista os serviços ou operações que pode usar o sistema ou componente. Em alguns casos, você será capaz de criar todos esses serviços como parte do seu próprio sistema. Em outros casos, especialmente se você estiver criando um componente que pode ser combinado com outros componentes em muitas configurações, a interface necessária será definida por considerações externas.

- Qualidade de requisitos de serviço. O desempenho, segurança, robustez e outros objetivos e restrições que o sistema deve atender.

  O modelo de requisitos é escrito do ponto de vista dos usuários do seu sistema, independentemente de estarem pessoas ou outros componentes de software. Eles sabem nada sobre o funcionamento interno do sistema. Por outro lado, sua meta em um modelo de arquitetura é que descrevem o funcionamento interno e mostrar como eles atendem aos usuários necessidades.

  Manter os requisitos e modelos arquitetônicos separados é útil, pois ele torna mais fáceis de discutir os requisitos com os usuários. Ele também ajuda você refatorar o design e considere arquiteturas alternativas enquanto manter os requisitos inalterado.

  A quantidade de detalhes que devem ser colocadas em um requisitos ou um modelo de arquitetura depende a escala do projeto e o tamanho e a distribuição da equipe. Uma pequena equipe em um projeto de curto pode ir não mais do que fazer um rascunho de um diagrama de classe de conceitos de negócios e alguns padrões de design; um projeto grande distribuído em mais de uma região precisariam significativamente mais detalhadamente.

## <a name="BigDecisions"></a> Padrões de arquitetura
 No início do desenvolvimento de um, você precisa escolher as principais tecnologias e os elementos do qual depende o design. As áreas em que essas opções devem ser feitas incluem o seguinte:

- Opções de tecnologia, como a escolha entre um banco de dados e um sistema de arquivos e a escolha entre um aplicativo de rede e um cliente da web, de base e assim por diante.

- Opções de estruturas, como uma escolha entre o Windows Workflow Foundation ou o ADO.NET Entity Framework.

- Opções de método de integração, por exemplo, entre um barramento de serviço corporativo ou de um canal de ponto a ponto.

  Essas opções com frequência são determinadas pela qualidade de requisitos de serviço, como a flexibilidade e escala e podem ser feitas antes que os requisitos detalhados são conhecidos. Em um sistema grande, a configuração de hardware e software são altamente inter-relacionadas.

  As seleções feitas afetam como usar e interpretar o modelo de arquitetura. Por exemplo, em um sistema que usa um banco de dados, associações em um diagrama de classe podem representar relações ou chaves estrangeiras no banco de dados, enquanto em um sistema baseado em arquivos XML, associações podem indicar referências cruzadas que usam XPath. Em um sistema distribuído, mensagens em um diagrama de sequência podem representar as mensagens durante uma transmissão; em um aplicativo autocontido, eles podem representar chamadas de função.

## <a name="Patterns"></a> Padrões de design
 Um padrão de design é uma estrutura de tópicos de como criar um aspecto específico do software, especialmente para um que se repete em diferentes partes do sistema. Ao adotar uma abordagem uniforme em todo o projeto, reduzir o custo de design, garantir a consistência na interface do usuário e reduzir o custo da compreensão e alterar o código.

 Alguns padrões de design geral como observador são bem conhecidos e amplamente aplicável. Além disso, há padrões que são aplicáveis apenas para seu projeto. Por exemplo, em um sistema de vendas da web, haverá várias operações no código onde as alterações são feitas para um pedido de cliente. Para garantir que o estado do pedido seja exibido corretamente em cada estágio, todas essas operações devem seguir um protocolo específico para atualizar o banco de dados.

 Parte do trabalho de arquitetura de software é determinar quais padrões devem ser adotado em design. Isso geralmente é uma tarefa em andamento, porque novos padrões e melhorias para os padrões existentes serão descobertas conforme o andamento do projeto. É útil organizar o plano de desenvolvimento para que você exercita cada um dos seus padrões de design principal em um estágio inicial.

 A maioria dos padrões de design podem ser incorporados em parte no código do framework. Parte do padrão pode ser reduzido para exigir do desenvolvedor usar classes específicas ou componentes, como uma camada de acesso de banco de dados que garante que o banco de dados é tratado corretamente.

 Um padrão de design é descrito em um documento e geralmente inclui estas partes:

-   Nome.

-   Descrição do contexto no qual ele é aplicável. Que critérios devem fazer com que um desenvolvedor considere aplicar esse padrão?

-   Breve explicação sobre o problema que ele resolve.

-   Modelo de partes mais importantes e suas relações. Eles podem ser classes ou componentes e interfaces, com associações e dependências entre eles. Os elementos normalmente se encaixam em duas categorias:

-   Convenções de nomenclatura.

-   Descrição de como o padrão resolve o problema.

-   Descrição das variações que os desenvolvedores podem ser capazes de adotar.

## <a name="see-also"></a>Consulte também

- [Visualizar código](../modeling/visualize-code.md)
- [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)
- [Desenvolver testes por meio de um modelo](../modeling/develop-tests-from-a-model.md)
- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)