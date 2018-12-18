---
title: Desenvolver testes por meio de um modelo
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tests and requirements
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: e1fd3b1cd19efa9032b7b92576a489e3b17373db
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49919320"
---
# <a name="develop-tests-from-a-model"></a>Desenvolver testes por meio de um modelo
Você pode usar os requisitos e modelos de arquitetura para ajudar você a organizar os testes do seu sistema e seus componentes. Essa prática ajuda a garantir que você teste os requisitos que são importantes para os usuários e outros participantes e ajudá-lo a atualizar os testes rapidamente quando os requisitos são alterados. Se você usar [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)], você também pode manter os vínculos entre os modelos e os testes.

 Para ver quais versões do Visual Studio dão suporte a esses recursos, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="system-and-subsystem-testing"></a>Teste de subsistema e sistema
 *Testes de sistema* também conhecido como *testes de aceitação*, significa testando se as necessidades de usuários que estão sendo atendidas. Esses testes estão preocupados com o comportamento visível externamente do sistema em vez do design interno.

 Testes de sistema são muito valiosos ao estender ou reformular um sistema. Eles ajudam a evitar introduzir bugs quando você alterar o código.

 Quando você planejar qualquer alteração ou a extensão a um sistema, é útil começar com um conjunto de testes de sistema que são executados em um sistema existente. Em seguida, você pode estender ou ajustar os testes para testar os novos requisitos, faça as alterações no código e execute novamente o conjunto completo de testes.

 Quando você desenvolve um novo sistema, você pode começar a criar testes, assim que o desenvolvimento começa. Definindo testes antes de desenvolver cada recurso, você pode capturar as discussões de requisitos de uma maneira muito específica.

 Teste de subsistema aplica-se os mesmos princípios para os principais componentes de um sistema. Cada componente é testado separadamente de outros componentes. Subsistema de testes de foco no comportamento visível em interfaces de usuário ou a API do componente.

## <a name="deriving-system-tests-from-a-requirements-model"></a>Derivando de testes do sistema de um modelo de requisitos
 Você pode criar e manter uma relação entre os testes de sistema e um modelo de requisitos. Para estabelecer essa relação, você escreve testes que correspondem aos elementos principais do modelo de requisitos. Visual Studio ajuda você a manter essa relação, permitindo que você criar links entre os testes e as partes do modelo. Para obter mais informações sobre modelos de requisitos, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).

### <a name="write-tests-for-each-use-case"></a>Escrever testes para cada caso de uso
 Se você usar [!INCLUDE[TCMext](../misc/includes/tcmext_md.md)], você pode criar um grupo de testes para cada caso de uso que você definiu no seu modelo de requisitos. Por exemplo, se você tiver um caso de uso ordem uma refeição, que inclui criar pedido e Adicionar Item à ordem, você pode criar testes para ambos os geral e mais detalhada desses casos de uso.

 Essas diretrizes podem ser úteis:

-   Cada caso de uso deve ter vários testes, para caminhos principais e os resultados excepcionais.

-   Quando você descreve um caso de uso no modelo de requisitos, é mais importante definir seu pós-condição, ou seja, a meta é obtida do que para descrever em detalhes os procedimentos que o usuário segue para alcançar a meta. Por exemplo, a pós-condição de ordem de uma refeição pode ser que um restaurante está preparando uma refeição para um cliente e que o cliente paga. A pós-condição é o critério que seus testes devem verificar.

-   Base testes separados em cláusulas de separados de pós-condição. Por exemplo, crie testes separados para notificar o restaurante da ordem e para fazer o pagamento do cliente. Essa separação tem estas vantagens:

    -   Com frequência as alterações em diferentes aspectos dos requisitos ocorrem de forma independente. Separando os testes em diferentes aspectos dessa maneira, você tornar mais fácil atualizar os testes quando requisitos mudam.

    -   Se o plano de desenvolvimento implementa um aspecto do caso de uso antes da outra, você pode habilitar os testes separadamente à medida que progride de desenvolvimento.

-   Quando você cria os testes, separe a escolha de dados de teste do código ou script que determina se a pós-condição foi atingida. Por exemplo, um teste de uma função aritmético simples pode ser: 4 de entrada; Verifique se a saída é 2. Em vez disso, criar o script como: escolha uma entrada; Multiplique o resultado por si só e verifique se o resultado é a entrada original. Esse estilo permite variar as entradas de teste sem alterar o corpo principal do teste.

#### <a name="linking-tests-to-use-cases"></a>Testes de vinculação para casos de uso
 Se você estiver usando [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)] para criar e executar seus testes, você pode organizar seus testes em itens de trabalho de história de usuário, requisito ou em caso de uso. Você pode vincular esses itens de trabalho para casos de uso em seu modelo. Isso permite que você rapidamente rastrear alterações de requisitos para os testes e ajuda a acompanhar o progresso de cada caso de uso.

###### <a name="to-link-tests-to-a-use-case"></a>Para vincular os testes para um caso de uso

1. No [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)], criar um requisito e um conjunto de testes de base nele.

    O requisito de que você cria é um item de trabalho em [!INCLUDE[vstsTfsShort](../modeling/includes/vststfsshort_md.md)]. Pode ser um item de trabalho de história de usuário, requisito ou caso de uso, dependendo do modelo de processo que usa o seu projeto com o Team Foundation. Para obter mais informações, consulte [gerenciamento de projeto de ferramentas sobre Agile e Agile](/azure/devops/boards/backlogs/overview?view=vsts).

2. Vincule o item de trabalho de requisito para um ou mais casos de uso em seu modelo.

    Em um diagrama de caso de uso, um caso de uso com o botão direito e, em seguida, clique em **Link para o Item de trabalho**.

3. Adicione ao conjunto de testes, casos de teste que verificam se os casos de uso.

   Normalmente, cada item de trabalho de história ou requisito de usuário será vinculado a vários casos de uso em seu modelo, e cada caso de uso será vinculado a vários requisitos ou histórias de usuários. Isso ocorre porque cada história de usuário ou requisito aborda um conjunto de tarefas que desenvolver vários casos de uso. Por exemplo, em uma iteração inicial do seu projeto, você pode desenvolver a história de usuário básico no qual um cliente pode escolher itens de um catálogo e que eles sejam entregues. Em uma iteração posterior, o texto pode ser que o usuário paga quando concluir a ordem e o fornecedor recebe o dinheiro depois que ele envia as mercadorias.  Cada história adiciona uma cláusula a pós-condição de caso de uso de bens de ordem.

   Você pode criar links separados de requisitos para as cláusulas de pós-condição escrevendo essas cláusulas em comentários separados no diagrama de caso de uso. Você pode vincular cada comentário a um item de trabalho de requisito e vincular o comentário para o caso de uso no diagrama.

### <a name="base-tests-on-the-requirements-types"></a>Testes de base nos tipos de requisitos
 Os tipos, o que é, as classes, interfaces e enumerações, de um modelo de requisitos descrevem os conceitos e as relações em termos de como os usuários pensam e se comunicar sobre seus negócios. Ele exclui tipos preocupado apenas com o design interno do sistema.

 Os testes em termos desses tipos de requisitos de design. Essa prática ajuda a garantir que, quando as alterações nos requisitos são discutidas, é fácil relacionar as alterações para as alterações necessárias nos testes. Ele possibilita discutir os testes e seus resultados pretendidos diretamente com os usuários finais e outros participantes. Isso significa que os usuários precisam pode ser mantidos fora do processo de desenvolvimento e evita o design acidental dos testes em torno de possíveis falhas no design.

 Para testes manuais, essa prática envolve a aderir ao vocabulário do modelo requisitos nos scripts de teste. Para testes automatizados, essa prática envolve usando os diagramas de classe de requisitos como base para seu código de teste e criar acessador e updater funções para vincular o modelo de requisito no código.

 Por exemplo, requisitos de modelo pode incluir tipos de Item de Menu, Menu, Order e associações entre elas. Esse modelo representa as informações que são armazenadas e tratadas pela refeição sistema de pedidos, mas não representam as complexidades de sua implementação. O sistema de trabalho, pode haver vários realizações diferentes de cada tipo, em bancos de dados, nas interfaces do usuário e as APIs. Em um sistema distribuído, pode haver diversas variantes de cada instância sejam armazenados em diferentes partes do sistema ao mesmo tempo.

 Para testar um caso de uso, como adicionar Item à ordem, um método de teste pode incluir código semelhante a este:

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

 Observe que esse método de teste usa as classes do modelo de requisitos. Associações e os atributos são realizados como propriedades .NET.

 Para fazer isso funcionar, as propriedades das classes devem ser definidas como funções de somente leitura ou acessadores, que acessam o sistema para recuperar informações sobre seu estado atual. Métodos que simulam casos de uso, como AddItemToOrder devem direcionar o sistema por meio de sua API ou por meio de uma camada sob sua interface do usuário. Os construtores de objetos de teste como ordem e MenuItem também devem direcionar o sistema para criar os itens correspondentes dentro do sistema.

 Muitos dos acessadores e atualizadores já estarão disponíveis por meio de API normal do aplicativo. Mas algumas funções adicionais podem ter a ser gravado para habilitar os testes. Esses acessadores adicionais e atualizadores de aplicativos também são conhecidas como 'instrumentação de teste'. Porque eles dependem do design interno do sistema, é responsabilidade dos desenvolvedores do sistema para fornecer a eles, enquanto os testadores escrever o código dos testes em termos do modelo de requisitos.

 Ao escrever testes automatizados, você pode usar testes genéricos para encapsular os acessadores e atualizadores de aplicativos.

### <a name="tests-for-business-rules"></a>Testes para regras de negócio
 Alguns requisitos não estão diretamente relacionados a qualquer um caso de uso. Por exemplo, a empresa DinnerNow permite que os clientes escolham entre muitos Menus, mas requer que em cada ordem, todos os itens deverão ser de um único Menu escolhida. Essa regra de negócio pode ser expresso como uma invariável sobre as associações entre os pedidos, Menus e itens no modelo de classe de requisitos.

 Uma regra invariável desse tipo controla não apenas todos os casos de uso são definidos no momento, mas também qualquer outros casos de uso que serão definidos posteriormente. Portanto, é útil para gravá-lo separadamente de qualquer caso de uso e testá-lo separadamente dos casos de uso.

## <a name="deriving-subsystem-tests-from-models"></a>Derivando de testes do subsistema de modelos
 O design de um sistema grande de alto nível, você pode identificar componentes ou subsistemas. Elas representam as partes que podem ser criadas separadamente, estão localizados em diferentes computadores ou são módulos reutilizáveis que podem ser recombinados de várias maneiras.

 Você pode aplicar a cada componente principal os mesmos princípios que você usa em todo o sistema. Em um projeto grande, cada componente pode ter seu próprio modelo de requisitos. Em projetos menores, um modelo de arquitetura ou design de alto nível pode ser criado para mostrar os principais componentes e suas interações. Para obter mais informações, consulte [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md).

 Em ambos os casos, você pode estabelecer uma relação entre os elementos de modelo e os testes do subsistema da mesma maneira como você faria entre o modelo de requisitos e os testes do sistema.

### <a name="isolate-components-with-provided-and-required-interfaces"></a>Isolar os componentes com Interfaces fornecidas e obrigatórias
 É útil para identificar todas as dependências de um componente tem em outras partes do seu sistema ou serviços externos e para representar esses como Interfaces necessárias. Este exercício geralmente resulta em alguma reformulação que deixa o componente facilmente separáveis e muito mais separado do restante do seu design.

 Uma vantagem essa desassociação é que o componente pode ser executado para testes, substituindo com objetos fictícios, os serviços que normalmente usa. Esses são componentes que são configurados para fins de teste. Um componente fictício fornece a interface que seu componente requer, respondendo a consultas com dados simulados. Os componentes da simulação fazem parte de um equipamento de teste completo que você pode se conectar a todas as interfaces do componente.

 Um benefício dos testes de simulação é que você pode desenvolver seu componente, enquanto os outros componentes cujos, ele usará os serviços ainda estão em desenvolvimento.

## <a name="maintain-the-relationships-between-tests-and-model"></a>Manter as relações entre os testes e modelo
 Em um projeto típico que realiza uma iteração em algumas semanas, uma análise dos requisitos é mantida no início de cada iteração. A reunião aborda os recursos que devem ser entregues na próxima iteração. Um modelo de requisitos pode ser usado para ajudar a discutir os conceitos, cenários e as sequências de ações que serão desenvolvidas. As partes interessadas no negócio definir prioridades, os desenvolvedores a fazer estimativas e os testadores garantir que o comportamento esperado de cada recurso é capturado corretamente.

 Escrevendo testes é a maneira mais eficiente para definir um requisito, e também é uma maneira eficiente para garantir que uma pessoa tenha uma compreensão clara do que é necessário. No entanto, enquanto a escrever testes leva muito tempo para fazer durante um workshop de especificação, criação de modelos pode ser feito muito mais rapidamente.

 Do ponto de vista teste, um modelo de requisitos pode ser visto como uma abreviação para os testes. Portanto, é importante manter a relação entre os testes e o modelo em todo o projeto.

## <a name="Attaching"></a> Anexando a casos de teste para elementos de modelo
 Se seu projeto usa [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)], você pode vincular os testes aos elementos no seu modelo. Isso permite que você localize rapidamente os testes afetados por uma alteração nos requisitos e ajuda você a controlar a extensão para o qual um requisito foi concretizado.

 Você pode vincular os testes para todos os tipos de elemento. Estes são alguns exemplos:

-   Vincule um caso de uso para os testes que exercitam a ele.

-   Gravar as cláusulas de pós-condição de casos de uso ou meta em comentários que estão vinculados ao caso de uso, e, em seguida, vincular testes para cada comentário.

-   Escrever regras de invariáveis nos comentários em diagramas de classe ou diagramas de atividade e vinculá-los aos testes.

-   Vincular testes para um diagrama de atividade, ou para atividades individuais.

-   Vincule a um conjunto de testes para o componente ou o subsistema que ele testa.

#### <a name="to-link-tests-to-a-model-element-or-relationship"></a>Para vincular os testes a um elemento de modelo ou a relação

1. No [!INCLUDE[TCMlong](../modeling/includes/tcmlong_md.md)], criar um requisito e um conjunto de testes de base nele.

    O requisito de que você cria é um item de trabalho em [!INCLUDE[vstsTfsShort](../modeling/includes/vststfsshort_md.md)]. Pode ser um item de trabalho de história de usuário, requisito ou caso de uso, dependendo do modelo de processo que usa o seu projeto com o Team Foundation. Para obter mais informações, consulte [gerenciamento de projeto de ferramentas sobre Agile e Agile](/azure/devops/boards/backlogs/overview?view=vsts).

2. Vincule o item de trabalho de requisito para um ou mais elementos em seu modelo.

    Em um diagrama de modelagem, clique com botão direito um elemento, comentário ou relação e, em seguida, clique em **Link para o Item de trabalho**.

3. Adicione ao conjunto de testes, casos de teste que verificam se o requisito expressado no elemento de modelo.

## <a name="see-also"></a>Consulte também

- [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)
- [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)
- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)
- [Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)
