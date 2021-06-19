---
title: Desenvolver testes por meio de um modelo
description: Saiba como você pode usar requisitos e modelos de arquitetura para ajudar a organizar os testes do sistema e seus componentes.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tests and requirements
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dadffd0a2950d55145b24d3172564eb572f98d70
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389144"
---
# <a name="develop-tests-from-a-model"></a>Desenvolver testes por meio de um modelo
Você pode usar requisitos e modelos de arquitetura para ajudá-lo a organizar os testes do sistema e seus componentes. Essa prática ajuda a garantir que você teste os requisitos que são importantes para os usuários e outros stakeholders e ajuda você a atualizar os testes rapidamente quando os requisitos mudarem. Se você usar [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] , também poderá manter links entre os modelos e os testes.

 Para ver quais versões do Visual Studio dar suporte a esses recursos, consulte [Suporte de versão para ferramentas de arquitetura e modelagem](../modeling/analyze-and-model-your-architecture.md#VersionSupport).

## <a name="system-and-subsystem-testing"></a>Teste de sistema e subsistema
 *O teste do sistema,* também conhecido como *teste de aceitação,* significa testar se as necessidades dos usuários estão sendo atendidas. Esses testes estão preocupados com o comportamento visível externamente do sistema em vez do design interno.

 Os testes de sistema são muito valiosos ao estender ou recriar um sistema. Eles ajudam a evitar a introdução de bugs quando você altera o código.

 Quando você planeja qualquer alteração ou extensão para um sistema, é útil começar com um conjunto de testes do sistema que são executados no sistema existente. Em seguida, você pode estender ou ajustar os testes para testar os novos requisitos, fazer as alterações no código e realizar o conjunto completo de testes.

 Ao desenvolver um novo sistema, você pode começar a criar testes assim que o desenvolvimento começar. Ao definir testes antes de desenvolver cada recurso, você pode capturar as discussões de requisitos de uma maneira muito específica.

 O teste de subsistema aplica os mesmos princípios aos principais componentes de um sistema. Cada componente é testado separadamente de outros componentes. Os testes de subsistema se concentram no comportamento visível nas interfaces do usuário ou na API do componente.

## <a name="deriving-system-tests-from-a-requirements-model"></a>Derivando testes de sistema de um modelo de requisitos
 Você pode criar e manter uma relação entre testes de sistema e um modelo de requisitos. Para estabelecer essa relação, você escreve testes que correspondem aos principais elementos do modelo de requisitos. Visual Studio ajuda você a manter essa relação, deixando que você crie links entre os testes e partes do modelo. Para obter mais informações sobre modelos de requisitos, consulte [Requisitos do usuário do modelo.](../modeling/model-user-requirements.md)

### <a name="write-tests-for-each-use-case"></a>Gravar testes para cada caso de uso
 Se você usar , poderá criar um grupo de testes para cada [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)] caso de uso que você definiu em seu modelo de requisitos. Por exemplo, se você tiver um caso de uso Solicitar uma Refeição, que inclui Criar Pedido e Adicionar Item à Ordem, poderá criar testes para o geral e o mais detalhado desses casos de uso.

 Essas diretrizes podem ser úteis:

- Cada caso de uso deve ter vários testes, para caminhos principais e resultados excepcionais.

- Quando você descreve um caso de uso no modelo de requisitos, é mais importante definir sua pós-condição, ou seja, a meta que é atingida, do que descrever detalhadamente os procedimentos que o usuário segue para atingir a meta. Por exemplo, a pós-condição de Pedir uma Refeição pode ser que um Restaurante está preparando uma refeição para um Cliente e que o Cliente tenha pago. A pós-condição é o critério que seus testes devem verificar.

- Basear testes separados nas cláusulas separadas da pós-condição. Por exemplo, crie testes separados para notificar o restaurante do pedido e para receber o pagamento do cliente. Essa separação tem estas vantagens:

  - Alterações em diferentes aspectos dos requisitos ocorrem frequentemente de forma independente. Ao separar os testes em diferentes aspectos dessa maneira, você facilita a atualização dos testes quando os requisitos mudam.

  - Se o plano de desenvolvimento implementar um aspecto do caso de uso antes de outro, você poderá habilitar os testes separadamente à medida que o desenvolvimento progride.

- Ao projetar os testes, separe a escolha de dados de teste do código ou script que determina se a pós-condição foi atingida. Por exemplo, um teste de uma função aritmética simples pode ser: Entrada 4; verifique se a saída é 2. Em vez disso, projete o script como: Escolha uma entrada; multiplique a saída por si só e verifique se o resultado é a entrada original. Esse estilo permite que você varie as entradas de teste sem alterar o corpo principal do teste.

#### <a name="linking-tests-to-use-cases"></a>Vinculando testes para casos de uso
 Se você estiver usando para projetar e executar seus testes, poderá organizar seus testes sob requisitos, casos de uso ou itens de trabalho [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)] de história do usuário. Você pode vincular esses itens de trabalho para casos de uso em seu modelo. Isso permite que você rastreia rapidamente as alterações de requisitos nos testes e ajuda você a acompanhar o progresso de cada caso de uso.

###### <a name="to-link-tests-to-a-use-case"></a>Para vincular testes a um caso de uso

1. No [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)] , crie um requisito e basee um conjunto de testes nele.

    O requisito que você cria é um item de trabalho no [!INCLUDE[vstsTfsShort](../modeling/includes/vststfsshort_md.md)] . Pode ser um item de trabalho História do Usuário, Requisito ou Caso de Uso, dependendo do modelo de processo que seu projeto usa com o Team Foundation. Para obter mais informações, consulte [Sobre ferramentas Agile e Gerenciamento de projetos Agile](/azure/devops/boards/backlogs/backlogs-overview?view=vsts&preserve-view=true).

2. Vincule o item de trabalho de requisito a um ou mais casos de uso em seu modelo.

    Em um diagrama de caso de uso, clique com o botão direito do mouse em um caso de uso e clique **em Vincular ao Item de Trabalho**.

3. Adicione ao conjunto de testes, casos de teste que verificam os casos de uso.

   Normalmente, cada item de trabalho de requisito ou história do usuário será link para vários casos de uso em seu modelo, e cada caso de uso será link para várias histórias ou requisitos do usuário. Isso porque cada história ou requisito do usuário abrange um conjunto de tarefas que desenvolvem vários casos de uso. Por exemplo, em uma iteração inicial do seu projeto, você pode desenvolver a história básica do usuário na qual um cliente pode escolher itens de um catálogo e fazer com que eles os entreguem. Em uma iteração posterior, a história pode ser que o usuário paga ao concluir o pedido e o fornecedor recebe o dinheiro depois de enviar a mercadorias.  Cada história adiciona uma cláusula à pós-condição do caso de uso de Bens de Pedido.

   Você pode criar links separados de requisitos para as cláusulas da pós-condição escrevendo essas cláusulas em comentários separados no diagrama de caso de uso. Você pode vincular cada comentário a um item de trabalho de requisito e vincular o comentário ao caso de uso no diagrama.

### <a name="base-tests-on-the-requirements-types"></a>Testes de base nos tipos de requisitos
 Os tipos, ou seja, as classes, interfaces e enumerações de um modelo de requisitos descrevem os conceitos e relações em termos de como os usuários pensam e se comunicam sobre seus negócios. Ela exclui tipos que se preocupam apenas com o design interno do sistema.

 Projete seus testes em termos desses tipos de requisitos. Essa prática ajuda você a garantir que, quando as alterações nos requisitos são discutidas, é fácil relacionar as alterações às alterações necessárias nos testes. Isso possibilita discutir os testes e seus resultados pretendido diretamente com os usuários finais e outros stakeholders. Isso significa que as necessidades dos usuários podem ser mantidas fora do processo de desenvolvimento e evita o design inadvertido dos testes em torno de possíveis falhas no design.

 Para testes manuais, essa prática envolve a aderindo ao vocabulário do modelo de requisitos nos scripts de teste. Para testes automatizados, essa prática envolve o uso dos diagramas de classe de requisitos como base para seu código de teste e a criação de funções de acessador e atualizador para vincular o modelo de requisito ao código.

 Por exemplo, um modelo de requisitos pode incluir tipos Menu, Item de Menu, Pedido e associações entre eles. Esse modelo representa as informações armazenadas e tratadas pelo sistema de pedidos de alimentos, mas não representa as complexidades de sua implementação. No sistema de trabalho, pode haver várias realizaçãos diferentes de cada tipo, em bancos de dados, em interfaces do usuário e em APIs. Em um sistema distribuído, pode haver várias variantes de cada instância armazenadas em diferentes partes do sistema ao mesmo tempo.

 Para testar um caso de uso, como Adicionar Item à Ordem, um método de teste pode incluir código semelhante a este:

```
Order order = ... ; // set up an order
// Store prior state:
int countBefore = order.MenuItems.Count;
// Perform use case:
MenuItem chosenItem = ...; // choose an item
AddItemToOrder (chosenItem, order);
// Verify part of postcondition:
int countAfter = order.MenuItems.Count;
Assert (countAfter == countBefore = 1);
```

 Observe que esse método de teste usa as classes do modelo de requisitos. Associações e atributos são realizados como propriedades do .NET.

 Para fazer isso funcionar, as propriedades das classes devem ser definidas como funções ou acessadores somente leitura, que acessam o sistema para recuperar informações sobre seu estado atual. Métodos que simulam casos de uso, como AddItemToOrder, devem conduzir o sistema por meio de sua API ou por meio de uma camada sob sua interface do usuário. Os construtores de objetos de teste, como Order e MenuItem, também devem conduzir o sistema para criar itens correspondentes dentro do sistema.

 Muitos acessadores e atualizadores já estarão disponíveis por meio da API normal do aplicativo. Mas algumas funções adicionais podem precisar ser escritas para habilitar os testes. Esses acessadores e atualizadores adicionais às vezes são conhecidos como "instrumentação de teste". Como eles dependem do design interno do sistema, é responsabilidade dos desenvolvedores do sistema fornecer a eles, enquanto os testadores escrevem o código dos testes em termos do modelo de requisitos.

 Ao escrever testes automatizados, você pode usar Testes Genéricos para envolver os acessadores e os atualizadores.

### <a name="tests-for-business-rules"></a>Testes para Business Rules
 Alguns requisitos não estão diretamente relacionados a nenhum caso de uso. Por exemplo, a empresa DinnerNow permite que os clientes escolham entre muitos Menus, mas exige que, em cada Pedido, todos os Itens escolhidos sejam de um único Menu. Essa regra de negócio pode ser expressa como uma invariável sobre as associações entre Pedidos, Menus e Itens no modelo de classe requirements.

 Uma regra invariável desse tipo rege não apenas todos os casos de uso que estão definidos no momento, mas também todos os outros casos de uso que serão definidos posteriormente. Portanto, é útil escrevê-lo separadamente de qualquer caso de uso e testá-lo separadamente dos casos de uso.

## <a name="deriving-subsystem-tests-from-models"></a>Derivando testes de subsistema de modelos
 No design de alto nível de um sistema grande, você pode identificar componentes ou subsistemas. Eles representam partes que podem ser projetadas separadamente ou estão localizadas em computadores diferentes ou são módulos reutilizáveis que podem ser recombinados de várias maneiras.

 Você pode aplicar a cada componente principal os mesmos princípios que usa para o sistema completo. Em um projeto grande, cada componente pode ter seu próprio modelo de requisitos. Em projetos menores, um modelo de arquitetura ou design de alto nível pode ser criado para mostrar os principais componentes e suas interações. Para obter mais informações, [consulte Modelar a arquitetura do aplicativo.](../modeling/model-your-app-s-architecture.md)

 Em ambos os casos, você pode estabelecer uma relação entre os elementos de modelo e os testes de subsistema da mesma maneira que faria entre o modelo de requisitos e os testes do sistema.

### <a name="isolate-components-with-provided-and-required-interfaces"></a>Isolar componentes com interfaces fornecidas e necessárias
 É útil identificar todas as dependências que um componente tem em outras partes do sistema ou serviços externos e representá-los como Interfaces Necessárias. Este exercício geralmente leva a alguma reformulação que deixa o componente muito mais desacompanhado e facilmente comparável do restante do seu design.

 Uma vantagem desse desacouplamento é que o componente pode ser executado para teste substituindo por objetos simulados os serviços que ele geralmente usa. Esses são componentes que são definidos para fins de teste. Um componente simulado fornece a interface que seu componente requer, respondendo a consultas com dados simulados. Os componentes de simulação fazem parte de um harness de teste completo que você pode conectar a todas as interfaces do componente.

 Um benefício do teste de simulação é que você pode desenvolver seu componente enquanto os outros componentes cujos serviços ele usará ainda estão em desenvolvimento.

## <a name="maintain-the-relationships-between-tests-and-model"></a>Manter as relações entre testes e modelo
 Em um projeto típico que executa uma iteração a cada algumas semanas, uma revisão de requisitos é mantida perto do início de cada iteração. A reunião discute os recursos que devem ser entregues na próxima iteração. Um modelo de requisitos pode ser usado para ajudar a discutir os conceitos, cenários e sequências de ações que serão desenvolvidas. Os stakeholders de negócios estabelecem prioridades, os desenvolvedores fazem estimativas e os testadores garantem que o comportamento esperado de cada recurso seja capturado corretamente.

 Escrever testes é a maneira mais eficaz de definir um requisito e também é uma maneira eficaz de garantir que uma pessoa tenha uma compreensão clara do que é necessário. No entanto, enquanto a escrita de testes leva muito tempo para ser feita durante um workshop de especificação, a criação de modelos pode ser feita muito mais rapidamente.

 Do ponto de vista de teste, um modelo de requisitos pode ser visto como um atalho para os testes. Portanto, é importante manter a relação entre testes e modelo em todo o projeto.

## <a name="attaching-test-cases-to-model-elements"></a><a name="Attaching"></a> Anexando casos de teste a elementos de modelo
 Se o projeto usar [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)] , você poderá vincular testes aos elementos em seu modelo. Isso permite localizar rapidamente os testes afetados por uma alteração nos requisitos e ajuda você a acompanhar a extensão até a qual um requisito foi realizado.

 Você pode vincular testes a todos os tipos de elemento. Estes são alguns exemplos:

- Vincule um caso de uso aos testes que o exerçam.

- Escreva as cláusulas de uma pós-condição de caso de uso ou meta em comentários vinculados ao caso de uso e, em seguida, vincule testes a cada comentário.

- Escreva regras invariantes em comentários em diagramas de classe ou diagramas de atividade e vincule-as a testes.

- Vincular testes a um diagrama de atividade ou a atividades individuais.

- Vincule um conjunto de testes ao componente ou subsistema que ele testa.

#### <a name="to-link-tests-to-a-model-element-or-relationship"></a>Para vincular testes a um elemento ou relação de modelo

1. No [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)] , crie um requisito e basee um conjunto de testes nele.

    O requisito que você cria é um item de trabalho no [!INCLUDE[vstsTfsShort](../modeling/includes/vststfsshort_md.md)] . Pode ser um item de trabalho História do Usuário, Requisito ou Caso de Uso, dependendo do modelo de processo que seu projeto usa com o Team Foundation. Para obter mais informações, consulte [Sobre ferramentas Agile e Gerenciamento de projetos Agile](/azure/devops/boards/backlogs/backlogs-overview?view=vsts&preserve-view=true).

2. Vincule o item de trabalho de requisito a um ou mais elementos em seu modelo.

    Em um diagrama de modelagem, clique com o botão direito do mouse em um elemento, comentário ou relação e clique **em Vincular ao Item de Trabalho**.

3. Adicione ao conjunto de testes, casos de teste que verificam o requisito expresso no elemento de modelo.

## <a name="see-also"></a>Confira também

- [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)
- [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)
- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)
- [Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)
