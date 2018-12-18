---
title: Modelar seu aplicativo&#39;arquitetura s | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML, modeling architecture
ms.assetid: aedce746-9df5-49e1-9662-67eb1b83d313
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 770f93c0ede93201ee873820d6701356837f4ea9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803845"
---
# <a name="model-your-app39s-architecture"></a>Modelar seu aplicativo&#39;arquitetura s
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para ajudar a garantir que seu aplicativo ou sistema de software atenda aos seus usuários precisa, você pode criar modelos no Visual Studio como parte de sua descrição da estrutura geral e o comportamento do seu aplicativo ou sistema de software. Usando modelos, você também pode descrever padrões que são usados em todo o design. Esses modelos de ajudarão-lo a entender a arquitetura existente, discutir as mudanças e comunique suas intenções claramente.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 A finalidade de um modelo é reduzir as ambiguidades que ocorrem nas descrições de linguagem natural e para ajudar você e seus colegas para visualizar o design e para discutir designs alternativos. Um modelo deve ser usado junto com outros documentos ou discussões. Por si só, um modelo não representa uma especificação completa da arquitetura.  
  
> [!NOTE]
>  Ao longo deste tópico, "system" significa que o software que você está desenvolvendo. Pode ser uma grande coleção de muitos componentes de hardware e software, ou um único aplicativo ou uma parte de um aplicativo.  
  
 A arquitetura de um sistema pode ser dividida em duas áreas:  
  
-   [Design de alto nível](#Structure). Descreve os principais componentes e como eles interagem entre si para atender a cada requisito. Se o sistema for grande, cada componente pode ter seu próprio design de alto nível que mostra como ele é composto de componentes menores.  
  
-   [Padrões de design](#Patterns) e as convenções usadas nos designs de componentes. Um padrão descreve uma abordagem específica para alcançar uma meta de programação. Usando os mesmos padrões em todo um design, sua equipe pode reduzir o custo de fazer alterações e desenvolvimento de software novo.  
  
##  <a name="Structure"></a> Design de alto nível  
 Um design de alto nível descreve os principais componentes do seu sistema e como eles interagem entre si para atingir as metas do design. As atividades na lista a seguir são envolvidas no desenvolvimento do design de alto nível, embora não necessariamente em uma sequência específica.  
  
 Se você estiver atualizando o código existente, você pode começar descrevendo os principais componentes. Verifique se você compreender todas as alterações para os requisitos de usuário e, em seguida, adicionar ou modificar as interações entre os componentes. Se você estiver desenvolvendo um novo sistema, comece Noções básicas sobre os principais recursos das necessidades dos usuários. Você pode, em seguida, explore as sequências de interações para os casos de uso principal e, em seguida, consolidar as sequências em um design do componente.  
  
 Em todos os casos, ele é útil para desenvolver as atividades diferentes em paralelo e desenvolver código e testes em um estágio inicial. Evite tentar concluir um dos seguintes aspectos antes de começar outra. Normalmente, os requisitos e seu conhecimento sobre a melhor maneira de projetar o sistema serão alterado enquanto você está gravando e testando o código. Portanto, você deve começar Entendendo e os principais recursos do seu design e os requisitos de codificação. Preencha os detalhes em iterações posteriores do projeto.  
  
-   [Noções básicas sobre os requisitos de](#Requirements). O ponto de partida de qualquer design é uma compreensão clara de necessidades dos usuários.  
  
-   [Padrões de arquitetura](#BigDecisions). As escolhas feitas sobre as principais tecnologias e os elementos de arquitetura do sistema.  
  
-   [Componentes e suas Interfaces](#Components). Você pode desenhar diagramas de componente para mostrar as partes principais do sistema e mostrar as interfaces por meio do qual eles interagem entre si. As interfaces de cada componente incluem todas as mensagens que você identificou nos diagramas de sequência.  
  
-   [As interações entre componentes](#Interactions). Para cada caso de uso, evento ou mensagem de entrada, você pode desenhar um diagrama de sequência que mostra como os principais componentes do sistema interagem para obter a resposta necessária.  
  
-   [Modelo de dados dos componentes e Interfaces](#Data). Você pode desenhar diagramas de classe para descrever as informações que são passadas entre componentes e armazenadas dentro dos componentes.  
  
##  <a name="Requirements"></a> Noções básicas sobre os requisitos  
 O design de alto nível de um aplicativo completo com mais eficiência é desenvolvido em conjunto com um modelo de requisitos ou outra descrição das necessidades dos usuários. Para obter mais informações sobre modelos de requisitos, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).  
  
 Se o sistema que você está desenvolvendo um componente em um sistema maior, parte ou todos os seus requisitos podem ser incorporados em interfaces programáticas.  
  
 O modelo de requisitos fornece essas duas informações essenciais:  
  
- Interfaces fornecidas. Uma interface fornecida lista os serviços ou as operações do sistema ou componente deve fornecer a seus usuários, independentemente de estarem usuários humanos ou outros componentes de software.  
  
- Interfaces necessárias. Uma interface necessária lista os serviços ou operações que pode usar o sistema ou componente. Em alguns casos, você será capaz de criar todos esses serviços como parte do seu próprio sistema. Em outros casos, especialmente se você estiver criando um componente que pode ser combinado com outros componentes em muitas configurações, a interface necessária será definida por considerações externas.  
  
- Qualidade de requisitos de serviço. O desempenho, segurança, robustez e outros objetivos e restrições que o sistema deve atender.  
  
  O modelo de requisitos é escrito do ponto de vista dos usuários do seu sistema, independentemente de estarem pessoas ou outros componentes de software. Eles sabem nada sobre o funcionamento interno do sistema. Por outro lado, sua meta em um modelo de arquitetura é que descrevem o funcionamento interno e mostrar como eles atendem aos usuários necessidades.  
  
  Manter os requisitos e modelos arquitetônicos separados é útil, pois ele torna mais fáceis de discutir os requisitos com os usuários. Ele também ajuda você refatorar o design e considere arquiteturas alternativas enquanto manter os requisitos inalterado.  
  
  Você pode separar os requisitos e os modelos de arquitetura de duas maneiras alternativas:  
  
- Mantê-los na mesma solução mas projetos diferentes. Eles serão exibidos como modelos separados no Gerenciador de modelos UML. Diferentes membros da equipe podem trabalhar em paralelo nos modelos. Limitado de tipos de rastreamento podem ser criados entre os modelos.  
  
- Colocá-los no mesmo modelo de UML, mas em pacotes diferentes. Isso torna mais fácil rastrear dependências entre os modelos, mas impede que mais de uma pessoa por vez de trabalhar com o modelo. Além disso, um modelo muito grande levará mais tempo para carregar no Visual Studio. Portanto, essa abordagem é menos adequada para projetos grandes.  
  
  A quantidade de detalhes que devem ser colocadas em um requisitos ou um modelo de arquitetura depende a escala do projeto e o tamanho e a distribuição da equipe. Uma pequena equipe em um projeto de curto pode ir não mais do que fazer um rascunho de um diagrama de classe de conceitos de negócios e alguns padrões de design; um projeto grande distribuído em mais de uma região precisariam significativamente mais detalhadamente.  
  
##  <a name="BigDecisions"></a> Padrões de arquitetura  
 No início do desenvolvimento de um, você precisa escolher as principais tecnologias e os elementos do qual depende o design. As áreas em que essas opções devem ser feitas incluem o seguinte:  
  
- Opções de tecnologia, como a escolha entre um banco de dados e um sistema de arquivos e a escolha entre um aplicativo de rede e um cliente da Web, de base e assim por diante.  
  
- Opções de estruturas, como uma escolha entre o Windows Workflow Foundation ou o ADO.NET Entity Framework.  
  
- Opções de método de integração, por exemplo, entre um barramento de serviço corporativo ou de um canal de ponto a ponto.  
  
  Essas opções com frequência são determinadas pela qualidade de requisitos de serviço, como a flexibilidade e escala e podem ser feitas antes que os requisitos detalhados são conhecidos. Em um sistema grande, a configuração de hardware e software são altamente inter-relacionadas.  
  
  As seleções feitas afetam como usar e interpretar o modelo de arquitetura. Por exemplo, em um sistema que usa um banco de dados, associações em um diagrama de classe podem representar relações ou chaves estrangeiras no banco de dados, enquanto em um sistema baseado em arquivos XML, associações podem indicar referências cruzadas que usam XPath. Em um sistema distribuído, mensagens em um diagrama de sequência podem representar as mensagens durante uma transmissão; em um aplicativo autocontido, eles podem representar chamadas de função.  
  
##  <a name="Components"></a> Componentes e suas Interfaces  
 As principais recomendações desta seção são da seguinte maneira:  
  
- Crie diagramas de componente para mostrar as principais partes do seu sistema.  
  
- Desenhe as dependências entre os componentes ou suas interfaces para mostrar a estrutura do sistema.  
  
- Use interfaces nos componentes para mostrar os serviços que cada componente fornece ou requer.  
  
- Em um projeto grande, você pode desenhar diagramas separados para decompor cada componente em partes menores.  
  
  Esses pontos são elaborados no restante desta seção.  
  
### <a name="components"></a>Componentes  
 Os modos de exibição centrais de um modelo de arquitetura são os diagramas de componente que mostram as partes principais do sistema e como eles dependem uma da outra. Para obter mais informações sobre diagramas de componente, consulte [diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md).  
  
 ![Diagrama de componente UML mostrando partes](../modeling/media/uml-barecomponent.png "UML_BareComponent")  
  
 Um diagrama de componente típico para um sistema grande pode incluir componentes como estes:  
  
-   Apresentação. O componente que fornece acesso ao usuário, normalmente em execução em um navegador da Web.  
  
-   Componentes do serviço Web. Fornece a conexão entre clientes e servidores.  
  
-   Use controladores de casos. Conduza o usuário pelas etapas de cada cenário.  
  
-   Núcleo de negócios. Contém classes que são baseadas em classes no modelo de requisitos, implementa as operações de chave e impõe restrições de negócios.  
  
-   banco de dados. Armazena os objetos de negócios.  
  
-   Registro em log e componentes de tratamento de erros.  
  
### <a name="dependencies-between-components"></a>Dependências entre componentes  
 Além dos próprios componentes, você pode mostrar as dependências entre eles. Uma seta de dependência entre dois componentes mostra que as alterações no design de um pode afetar o design dos outros. Isso geralmente ocorre porque um componente usa os serviços ou funções que são fornecidas pelo outro componente, direta ou indiretamente.  
  
 Uma arquitetura bem estruturada tem uma disposição clara das dependências, na qual essas condições forem verdadeiras:  
  
- Não há loops em um mapa de código.  
  
- Os componentes podem ser organizados em camadas em que cada dependência vai de um componente em uma camada a um componente na próxima. Acesse todas as dependências entre duas camadas na mesma direção.  
  
  Você pode mostrar as dependências diretamente entre os componentes, ou você pode mostrar as dependências entre necessárias e interfaces que estão anexados aos componentes fornecidas. Usando interfaces, você pode definir as operações que são usadas em cada dependência. Normalmente, as dependências são mostradas entre os componentes quando os diagramas são desenhados primeiro e, em seguida, substituídos por dependências entre as interfaces conforme são adicionadas mais informações. Ambas as versões são descrições corretas do software, mas a versão com interfaces fornece mais detalhes do que a versão anterior.  
  
  Gerenciamento de dependências é mais importante para a produção de software fácil de manter. Os diagramas de componente devem refletir todas as dependências em seu código. Se o código já existir, certifique-se de que todas as dependências são mostradas nos diagramas. Se o código está sendo desenvolvido, certifique-se de que ele não inclui as dependências que não sejam planejadas no diagrama de componente. Para ajudá-lo a descobrir dependências no código, é possível gerar diagramas de camada. Para ajudar a garantir que suas restrições de dependência planejadas sejam atendidas, você pode validar o código em diagramas de camada. Para obter mais informações, consulte [diagramas de camada: referência](../modeling/layer-diagrams-reference.md).  
  
### <a name="interfaces"></a>Interfaces  
 Colocando as interfaces em seus componentes, você pode separar e nomear os principais grupos de operações que são fornecidos por cada componente. Por exemplo, os componentes em um sistema de vendas baseado na web podem ter uma interface por meio do qual os clientes compram produtos, uma interface por meio dos quais fornecedores seus catálogos de atualização e uma terceira interface por meio do qual o sistema é gerenciado.  
  
 Um componente pode ter qualquer número de interfaces fornecidas e obrigatórias. Interfaces fornecidas serviços mostrar que o componente fornece para outros componentes usem. Interfaces necessárias mostram que o componente usa serviços em outros componentes.  
  
 Se você definir ambos fornecidos e interfaces obrigatórias, isso ajuda você a separar o componente corretamente do restante do design, para que você pode usar essas técnicas:  
  
- Coloque o componente em um equipamento de teste no qual os componentes adjacentes são simulados pelo equipamento de teste.  
  
- Desenvolva seu componente independentemente de outros componentes.  
  
- Reutilize o componente em outros contextos aliando suas interfaces para componentes diferentes.  
  
  Quando você deseja definir a lista de operações em uma interface, você pode criar outro modo de exibição da interface em um diagrama de classe UML. Para fazer isso, localize a interface no Gerenciador de modelos UML e arraste-o para um diagrama de classe. Em seguida, você pode adicionar operações à interface.  
  
  Uma operação em uma interface UML pode representar qualquer forma em que um comportamento de um componente pode ser invocado. Ele pode representar uma solicitação de serviço da Web, um sinal ou interação de algum outro tipo, ou uma chamada de função do programa comum.  
  
  Para determinar quais operações para adicionar, crie diagramas de sequência para mostrar como os componentes interagem uns com os outros. Ver [interações entre componentes](#Interactions). Cada um desses diagramas de sequência mostra as interações que ocorrem em um caso de uso diferentes. Dessa forma, você gradualmente pode adicionar à lista de operações na interface de cada componente, conforme você explora os casos de uso.  
  
### <a name="decomposing-a-component-into-parts"></a>Decomposição de um componente em partes  
 Você pode aplicar o procedimento descrito nas seções anteriores para cada componente.  
  
 Dentro de cada componente, você pode mostrar seus subcomponentes como partes. Uma parte é efetivamente um atributo do componente pai, que é um tipo de classe. Cada parte tem seu próprio tipo, que pode ser um componente. Você pode colocar esse componente em um diagrama e mostrar suas partes. Para obter mais informações, consulte [diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md).  
  
 É útil aplicar essa técnica para todo o sistema. Desenhá-lo como um único componente e mostrar seus principais componentes como partes. Isso ajuda você a identificar claramente as interfaces do seu sistema com o mundo externo.  
  
 Quando seu design para um componente usa outro componente, você frequentemente têm uma opção sobre se deve representá-lo como uma parte ou como um componente separado que você acessa por meio de uma Interface exige.  
  
 Use partes nas seguintes situações:  
  
- O design do componente pai sempre deve usar o tipo de componente da parte. Portanto, o design da parte é integral para o design do componente pai.  
  
- O componente pai tem não existência concreta. Por exemplo, você poderia ter um componente conceitual chamado de camada de apresentação que representa uma coleção de componentes reais que lidam com exibições e interações do usuário.  
  
  Use componentes separados, acessados por meio de interfaces necessárias nessas situações:  
  
- O componente que exigem pode ser combinado através das interfaces para diferentes fornece componentes em tempo de execução.  
  
- O design é, de modo que seria fácil substituir um provedor com outra.  
  
  O uso de interfaces necessárias geralmente é preferível o uso de partes. Embora o design pode levar mais tempo, o sistema resultante é mais flexível. Também é mais fácil de testar os componentes separadamente. Isso permite que o menor acoplamento em seus planos de desenvolvimento.  
  
##  <a name="Interactions"></a> Interações entre componentes  
 As principais recomendações desta seção são da seguinte maneira:  
  
- Identifique os casos de uso do seu sistema.  
  
- Para cada caso de uso, desenhe um ou mais diagramas para mostrar como os componentes do seu sistema de obter o resultado esperado pela colaboração entre si e com os usuários. Normalmente, esses são os diagramas de sequência ou diagramas de atividade.  
  
- Use Interfaces para especificar as mensagens recebidas por cada componente.  
  
- Descreva os efeitos das operações nas Interfaces.  
  
- Repita o procedimento para cada componente, mostrando como suas partes interagem.  
  
  Por exemplo, em um sistema de vendas baseado na web, o modelo de requisitos pode definir uma compra do cliente como um caso de uso. Você pode criar um diagrama de sequência para mostrar as interações que o cliente tem com os componentes na camada de apresentação e mostrar as interações que eles têm com o depósito e os componentes de contabilidade.  
  
### <a name="identifying-the-initiating-events"></a>Identificando os eventos de início  
 O trabalho realizado pela maioria dos sistemas de software pode ser dividido convenientemente pelas respostas que ele oferece a eventos ou entradas diferentes. O evento inicial pode ser um dos seguintes eventos:  
  
-   A primeira ação em um caso de uso. Ele pode aparecer no modelo de requisitos como uma etapa em um caso de uso, ou uma ação em um diagrama de atividade. Para obter mais informações, [diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md) e [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).  
  
-   Uma mensagem na interface de programação. Se o sistema que você está desenvolvendo um componente em um sistema maior, devem ser descrito como uma operação em uma das interfaces do componente. Ver [componentes e suas Interfaces](#Components).  
  
-   Uma condição específica que é monitorada pelo seu sistema ou um evento regular, como uma hora do dia.  
  
### <a name="describe-the-computations"></a>Descrever os cálculos  
 Desenhe diagramas de sequência para mostrar como os componentes de respondem ao evento inicial.  
  
 Desenhe uma linha da vida para cada instância do componente que faz parte de uma sequência típica. Em alguns casos, pode haver mais de uma instância de cada tipo. Se você descreveu seu sistema inteiro como um único componente, deverá haver uma linha da vida para cada parte que ele contém.  
  
 Para obter mais informações, consulte [diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md).  
  
 Diagramas de atividade também são úteis em alguns casos. Por exemplo, se seus componentes têm um fluxo contínuo de dados, descrevê-lo como um fluxo do objeto. Se o componente tem um algoritmo complexo, podem descrevê-lo como um fluxo de controle. Certifique-se de que você deixar claro qual componente executa cada ação, por exemplo, usando comentários. Para obter mais informações, consulte [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).  
  
### <a name="specify-the-operations"></a>Especificar as operações  
 Os diagramas mostram as operações executadas por cada componente, representados como mensagens em um diagrama de sequência ou ações em um diagrama de atividade.  
  
 Colete essas operações juntas para cada componente. Criar Interfaces fornecidas no componente e adicionar as operações às interfaces. Normalmente, uma interface separada é usada para cada tipo de cliente. As operações são adicionadas mais facilmente para as interfaces **Gerenciador de modelos UML**. Da mesma maneira, colete as operações que cada componente usa dos outros componentes e colocá-los em Interfaces necessárias anexadas ao componente.  
  
 É útil adicionar comentários a diagramas de atividade ou sequência, observar o que foi obtido após cada operação. Você também pode escrever o efeito de cada operação em seu **pós-condição Local** propriedade.  
  
###  <a name="Data"></a> Modelo de dados dos componentes e Interfaces  
 Defina os parâmetros e retornar valores de cada operação de interfaces de componentes. Em que as operações representam invocações, tais como solicitações de serviço da Web, os parâmetros são as partes de informações que são enviadas como parte da solicitação. Quando vários valores são retornados de uma operação, você pode usar parâmetros com o **direção** propriedade definida como **Out**.  
  
 Cada parâmetro e o valor retornado tem um tipo. Você pode definir esses tipos usando diagramas de classe UML. Não é necessário que representar o detalhe de implementação nesses diagramas. Por exemplo, se descrevendo dados que são transmitidos como XML, você pode usar uma associação para representar qualquer tipo de referência cruzada entre os nós do XML e usar classes para representar nós.  
  
 Use comentários para descrever as restrições de negócios sobre os atributos e associações. Por exemplo, se todos os itens em um pedido de cliente devem vir do mesmo fornecedor, você pode descrever isso por referência para as associações entre os itens da ordem e os itens no catálogo de produtos e entre o item de catálogo e seus fornecedores.  
  
##  <a name="Patterns"></a> Padrões de design  
 Um padrão de design é uma estrutura de tópicos de como criar um aspecto específico do software, especialmente para um que se repete em diferentes partes do sistema. Ao adotar uma abordagem uniforme em todo o projeto, reduzir o custo de design, garantir a consistência na interface do usuário e reduzir o custo da compreensão e alterar o código.  
  
 Alguns padrões de design geral como observador são bem conhecidos e amplamente aplicável. Além disso, há padrões que são aplicáveis apenas para seu projeto. Por exemplo, em um sistema de vendas da Web, haverá várias operações no código onde as alterações são feitas para um pedido de cliente. Para garantir que o estado do pedido seja exibido corretamente em cada estágio, todas essas operações devem seguir um protocolo específico para atualizar o banco de dados.  
  
 Parte do trabalho de arquitetura de software é determinar quais padrões devem ser adotado em design. Isso geralmente é uma tarefa em andamento, porque novos padrões e melhorias para os padrões existentes serão descobertas conforme o andamento do projeto. É útil organizar o plano de desenvolvimento para que você exercita cada um dos seus padrões de design principal em um estágio inicial.  
  
 A maioria dos padrões de design podem ser incorporados em parte no código do framework. Parte do padrão pode ser reduzido para exigir do desenvolvedor usar classes específicas ou componentes, como uma camada de acesso de banco de dados que garante que o banco de dados é tratado corretamente.  
  
 Um padrão de design é descrito em um documento e geralmente inclui estas partes:  
  
-   Nome.  
  
-   Descrição do contexto no qual ele é aplicável. Que critérios devem fazer com que um desenvolvedor considere aplicar esse padrão?  
  
-   Breve explicação sobre o problema que ele resolve.  
  
-   Modelo de partes mais importantes e suas relações. Eles podem ser classes ou componentes e interfaces, com associações e dependências entre eles. Os elementos normalmente se encaixam em duas categorias:  
  
    -   Elementos que o desenvolvedor deve ser replicada em todas as partes do código em que o padrão é usado. Você pode usar tipos de modelo para descrevê-los. Para obter mais informações, consulte [diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md).  
  
    -   Elementos que descrevem as classes do framework que o desenvolvedor deve usar.  
  
-   Modelo de interações entre as partes, usando diagramas de sequência ou atividade.  
  
-   Convenções de nomenclatura.  
  
-   Descrição de como o padrão resolve o problema.  
  
-   Descrição das variações que os desenvolvedores podem ser capazes de adotar.  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Visualizar código](../modeling/visualize-code.md)   
 [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)   
 [Desenvolver testes de um modelo](../modeling/develop-tests-from-a-model.md)   
 [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)



