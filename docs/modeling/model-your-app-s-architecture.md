---
title: Modelar a arquitetura &apos; do aplicativo
description: Saiba como você pode criar modelos no Visual Studio como parte de sua descrição da estrutura geral e do comportamento do seu aplicativo ou sistema de software.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- UML, modeling architecture
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fa2be8f4da963c21d9f7f68939421dd7d2d72d0b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390106"
---
# <a name="model-your-app39s-architecture"></a>Modelar a arquitetura&#39;aplicativo
Para ajudar a garantir que seu sistema de software ou aplicativo atenda às necessidades dos usuários, você pode criar modelos no Visual Studio como parte de sua descrição da estrutura geral e do comportamento do seu aplicativo ou sistema de software. Usando modelos, você também pode descrever padrões que são usados em todo o design. Esses modelos ajudam você a entender a arquitetura existente, discutir alterações e comunicar suas intenções claramente.

 Para ver quais edições do Visual Studio suporte a esse recurso, confira [Suporte à edição para ferramentas de arquitetura e modelagem](../modeling/analyze-and-model-your-architecture.md#VersionSupport).

 A finalidade de um modelo é reduzir as ambiguidades que ocorrem em descrições de linguagem natural e ajudar você e seus colegas a visualizar o design e discutir designs alternativos. Um modelo deve ser usado junto com outros documentos ou discussões. Por si só, um modelo não representa uma especificação completa da arquitetura.

> [!NOTE]
> Ao longo deste tópico, "system" significa o software que você está desenvolvendo. Pode ser uma grande coleção de muitos componentes de software e hardware, um único aplicativo ou uma parte de um aplicativo.

 A arquitetura de um sistema pode ser dividida em duas áreas:

- [Design de alto nível.](#Structure) Isso descreve os principais componentes e como eles interagem entre si para atender a cada requisito. Se o sistema for grande, cada componente poderá ter seu próprio design de alto nível que mostra como ele é composto por componentes menores.

- [Design Padrões e](#Patterns) convenções usados em todos os designs dos componentes. Um padrão descreve uma abordagem específica para atingir uma meta de programação. Usando os mesmos padrões em um design, sua equipe pode reduzir o custo de fazer alterações e desenvolver novos softwares.

## <a name="high-level-design"></a><a name="Structure"></a> Design de alto nível
 Um design de alto nível descreve os principais componentes do sistema e como eles interagem entre si para atingir as metas do design. As atividades na lista a seguir estão envolvidas no desenvolvimento do design de alto nível, embora não necessariamente em uma sequência específica.

 Se você estiver atualizando o código existente, poderá começar descrevendo os principais componentes. Certifique-se de entender as alterações nos requisitos do usuário e, em seguida, adicionar ou modificar interações entre os componentes. Se você estiver desenvolvendo um novo sistema, comece compreendendo os principais recursos das necessidades dos usuários. Em seguida, você pode explorar sequências de interações para os principais casos de uso e, em seguida, consolidar as sequências em um design de componente.

 Em todos os casos, é útil desenvolver as diferentes atividades em paralelo e desenvolver código e testes em um estágio inicial. Evite tentar concluir um desses aspectos antes de iniciar outro. Normalmente, os requisitos e sua compreensão da melhor maneira de projetar o sistema mudarão enquanto você estiver escrevendo e testando o código. Portanto, você deve começar compreendendo e codificando os principais recursos dos requisitos e seu design. Preencha os detalhes em ierções posteriores do projeto.

- [Noções básicas sobre os requisitos.](#Requirements) O ponto de partida de qualquer design é uma compreensão clara das necessidades dos usuários.

- [Padrões de arquitetura](#BigDecisions). As escolhas feitas sobre as principais tecnologias e elementos de arquitetura do sistema.

- Modelo de dados dos componentes e interfaces. Você pode desenhar diagramas de classe para descrever as informações passadas entre componentes e armazenadas dentro dos componentes.

## <a name="understanding-the-requirements"></a><a name="Requirements"></a> Noções básicas sobre os requisitos
 O design de alto nível de um aplicativo completo é desenvolvido com mais eficiência junto com um modelo de requisitos ou outra descrição das necessidades dos usuários. Para obter mais informações sobre modelos de requisitos, consulte [Requisitos do usuário do modelo.](../modeling/model-user-requirements.md)

 Se o sistema que você está desenvolvendo for um componente em um sistema maior, parte ou todos os seus requisitos poderão ser embodiados em interfaces programáticas.

 O modelo de requisitos fornece essas informações essenciais:

- Interfaces fornecidas. Uma interface fornecida lista os serviços ou operações que o sistema ou o componente deve fornecer aos usuários, sejam eles usuários humanos ou outros componentes de software.

- Interfaces necessárias. Uma interface necessária lista os serviços ou operações que o sistema ou componente pode usar. Em alguns casos, você poderá projetar todos esses serviços como parte de seu próprio sistema. Em outros casos, especialmente se você estiver projetando um componente que pode ser combinado com outros componentes em muitas configurações, a interface necessária será definida por considerações externas.

- Requisitos de qualidade de serviço. O desempenho, a segurança, a robustez e outras metas e restrições que o sistema deve atender.

  O modelo de requisitos é escrito do ponto de vista dos usuários do sistema, sejam eles pessoas ou outros componentes de software. Eles não sabem nada sobre o funcionamento interno do sistema. Por outro lado, sua meta em um modelo de arquitetura é descrever o funcionamento interno e mostrar como eles atendem às necessidades dos usuários.

  Manter os requisitos e os modelos de arquitetura separados é útil porque facilita a discussão dos requisitos com os usuários. Ele também ajuda você a refactor o design e a considerar arquiteturas alternativas, mantendo os requisitos inalterados.

  A quantidade de detalhes que você deve colocar em um requisito ou um modelo de arquitetura depende da escala do projeto e do tamanho e da distribuição da equipe. Uma pequena equipe em um projeto curto pode não ir além de esboçar um diagrama de classe dos conceitos de negócios e alguns padrões de design; um projeto grande distribuído em mais de uma região precisaria de significativamente mais detalhes.

## <a name="architectural-patterns"></a><a name="BigDecisions"></a> Padrões de arquitetura
 No início de um desenvolvimento, você precisa escolher as principais tecnologias e elementos dos quais o design depende. As áreas nas quais essas opções devem ser feitas incluem o seguinte:

- Opções de tecnologia base, como a escolha entre um banco de dados e um sistema de arquivos e a escolha entre um aplicativo em rede e um cliente Web e assim por diante.

- Opções de estruturas, como uma escolha entre Windows Workflow Foundation ou ADO.NET Entity Framework.

- Opções de método de integração, por exemplo, entre um barramento de serviço corporativo ou um canal ponto a ponto.

  Essas opções são frequentemente determinadas pela qualidade dos requisitos de serviço, como escala e flexibilidade, e podem ser feitas antes que os requisitos detalhados sejam conhecidos. Em um sistema grande, a configuração de hardware e software é fortemente inter-relacionada.

  As seleções que você faz afetam o uso e a interpretação do modelo de arquitetura. Por exemplo, em um sistema que usa um banco de dados, as associações em um diagrama de classe podem representar relações ou chaves estrangeiras no banco de dados, enquanto em um sistema baseado em arquivos XML, as associações podem indicar referências cruzadas que usam XPath. Em um sistema distribuído, as mensagens em um diagrama de sequência podem representar mensagens em uma transmissão; em um aplicativo autossuvente, eles podem representar chamadas de função.

## <a name="design-patterns"></a><a name="Patterns"></a> Padrões de design
 Um padrão de design é um contorno de como criar um aspecto específico do software, especialmente um que se recorre em diferentes partes do sistema. Ao adotar uma abordagem uniforme em todo o projeto, você pode reduzir o custo de design, garantir a consistência na interface do usuário e reduzir o custo de compreensão e alteração do código.

 Alguns padrões de design gerais, como Observador, são conhecidos e amplamente aplicáveis. Além disso, há padrões aplicáveis apenas ao seu projeto. Por exemplo, em um sistema de vendas na Web, haverá várias operações no código em que as alterações são feitas no pedido de um cliente. Para garantir que o estado da ordem seja exibido com precisão em cada estágio, todas essas operações devem seguir um protocolo específico para atualizar o banco de dados.

 Parte do trabalho da arquitetura de software é determinar quais padrões devem ser adotados em todo o design. Essa geralmente é uma tarefa contínua, porque novos padrões e melhorias nos padrões existentes serão descobertos à medida que o projeto progride. É útil organizar o plano de desenvolvimento para que você exerça cada um dos seus principais padrões de design em um estágio inicial.

 A maioria dos padrões de design pode ser parcialmente embodiado no código de estrutura. Parte do padrão pode ser reduzida para exigir que o desenvolvedor use classes ou componentes específicos, como uma camada de acesso ao banco de dados que garante que o banco de dados seja tratado corretamente.

 Um padrão de design é descrito em um documento e normalmente inclui estas partes:

- Nome.

- Descrição do contexto no qual ele é aplicável. Quais critérios devem fazer com que um desenvolvedor considere aplicar esse padrão?

- Breve explicação do problema que ele resolve.

- Modelo das partes principais e suas relações. Elas podem ser classes ou componentes e interfaces, com associações e dependências entre elas. Os elementos geralmente se enquadram em duas categorias:

- Convenções de nomenclatura.

- Descrição de como o padrão resolve o problema.

- Descrição das variações que os desenvolvedores podem adotar.

## <a name="see-also"></a>Confira também

- [Visualizar código](../modeling/visualize-code.md)
- [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)
- [Desenvolver testes por meio de um modelo](../modeling/develop-tests-from-a-model.md)
- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
