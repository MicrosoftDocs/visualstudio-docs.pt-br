---
title: Requisitos de usuário do modelo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- requirements
- stories
- UML, modeling requirements
ms.assetid: 359900f8-6d69-493d-bfdf-2c9069c74a26
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: ab92a08aa7359aa4393b3356384a4ccc352afb27
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51776480"
---
# <a name="model-user-requirements"></a>Requisitos de usuário do modelo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio ajuda a entender, discuta e comunicar-se suas necessidades de usuários ao desenhar diagramas sobre suas atividades e a parte seu sistema é reproduzido ajudá-los a atingir suas metas. Um modelo de requisitos é um conjunto desses diagramas, cada um deles enfoca um aspecto das necessidades dos usuários. Para uma demonstração em vídeo, consulte: [modelagem do domínio de negócios](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-3-Modeling-the-Business-Domain/).  
  
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
>  Ao longo desses tópicos, "system" significa que o sistema ou o aplicativo que você está desenvolvendo. Pode ser uma grande coleção de muitos componentes de hardware e software; ou um único aplicativo; ou um componente de software dentro de um sistema maior. Em todos os casos, o modelo de requisitos descreve o comportamento que é visível fora do seu sistema, seja por meio de uma interface do usuário ou a API.  
  
## <a name="common-tasks"></a>Tarefas comuns  
 Você pode criar várias exibições diferentes dos requisitos dos usuários.  Cada modo de exibição fornece um tipo específico de informações.  Quando você cria esses modos de exibição, é melhor mudam frequentemente uns aos outros. Você pode iniciar a partir de qualquer modo de exibição.  
  
|Diagrama ou documento|Ele descreve em um modelo de requisitos|Seção|  
|-------------------------|-----------------------------------------------|-------------|  
|Diagrama de caso de uso|Quem usa o sistema e o que fazer com ele.|[Descrevendo como seu sistema é usado](#UseCases)|  
|Diagrama de classe conceitual|Glossário de tipos que são usados para descrever os requisitos; os tipos visíveis na interface do sistema.|[Definição de termos usados para descrever os requisitos](#RequirementsClasses)|  
|Diagrama de atividade|Fluxo de trabalho e as informações entre as atividades executadas pelo sistema ou usuários e suas partes.|[Mostrando o fluxo de trabalho entre usuários e seu sistema](#Workflow)|  
|Diagrama de sequência|Sequência de interações entre usuários e de sistema ou de suas partes. Uma exibição alternativa para o diagrama de atividade.|[Mostrando as interações entre usuários e seu sistema](#Sequences)|  
|Documentos adicionais ou itens de trabalho|Critérios de desempenho, segurança, usabilidade e confiabilidade.|[Que descreve a qualidade dos requisitos de serviço](#QoSRequirements)|  
|Documentos adicionais ou itens de trabalho|Restrições e regras não específicas a um determinado caso de uso|[Mostrando as regras de negócio](#BusinessRules)|  
  
 Observe que a maioria dos tipos de diagrama pode ser usada para outras finalidades. Para obter uma visão geral dos tipos de diagrama, consulte [criar modelos para o aplicativo](../modeling/create-models-for-your-app.md). Para obter informações básicas sobre diagramas de desenho, consulte [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
##  <a name="UseCases"></a> Descrevendo como seu sistema é usado  
 Crie diagramas de caso de uso para descrever o que usa o sistema e o que ele usá-lo para. Um caso de uso representa uma meta de um usuário do sistema e o procedimento que eles executam para atingir a meta.  
  
 Por exemplo, uma refeição online vendendo o sistema deve permitir que os clientes escolham itens de um menu e deve permitir que os restaurantes fornecendo atualizar no menu. Você pode resumir isso em um diagrama de caso de uso:  
  
 ![Casos de uso do cliente e restaurante](../modeling/media/uml-reqmuc1.png "UML_ReqmUC1")  
  
 Você também pode mostrar como um caso de uso é composto de casos menores. Por exemplo, ordenar uma refeição é parte do comprando uma refeição, que também inclui o pagamento e entrega:  
  
 ![Sistema participa de pagamento, mas não entrega. ](../modeling/media/uml-reqmuc2.png "UML_ReqmUC2")  
  
 Você também pode mostrar quais casos de uso são incluídos no escopo do sistema que você está desenvolvendo. Por exemplo, o sistema na ilustração não fazer parte em caso de uso a refeição entregar. Isso ajuda a definir o contexto para o trabalho de desenvolvimento. (Em um diagrama de caso de uso, os contêineres de subsistema podem ser usados para representar o sistema ou seus componentes.)  
  
 Ele também ajuda sua equipe discutir o que será incluído em versões sucessivas. Por exemplo, você pode discutir se, na versão inicial do sistema, pagamento para refeição é organizada diretamente entre o restaurante e o cliente, em vez de passar por meio do sistema. Nesse caso, você pode mover pague refeição fora do retângulo de sistema do Dinner Now na versão inicial.  
  
 Um diagrama de caso de uso fornece apenas um resumo dos casos de uso. Para fornecer descrições mais detalhadas, você pode vincular casos de uso no diagrama para separar os documentos e com outros diagramas. Para saber como fazer isso, consulte [vincular um caso de uso a documentos e diagramas](../modeling/link-a-use-case-to-documents-and-diagrams.md).  
  
 Desenhar um diagrama de caso de uso ajuda sua equipe:  
  
- Se concentrar no que os usuários esperam fazer com o sistema, sem se distrair com detalhes da implementação.  
  
- Discuta o escopo do sistema ou versões específicas do sistema.  
  
  Os tópicos a seguir fornecem mais informações:  
  
|Para saber mais sobre|Ler|  
|--------------------|----------|  
|Informações mais detalhadas sobre como criar casos de uso|[Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)|  
|Elementos em um diagrama de caso de uso|[Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)|  
|Como desenvolver o código de casos de uso|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|  
  
##  <a name="RequirementsClasses"></a> Definição de termos usados para descrever os requisitos  
 Você pode usar diagramas de classe UML para ajudar você a desenvolver um vocabulário consistentes com os conceitos de negócios usados para as seguintes finalidades:  
  
- Pelos próprios usuários para discutir os negócios em que o sistema funciona.  
  
- Descrever as necessidades de usuários, por exemplo, nas descrições de casos de uso, as regras de negócio e histórias de usuários.  
  
- Os tipos de informações trocadas na API do sistema ou por meio da interface do usuário.  
  
- Descrições dos testes de aceitação ou de sistema.  
  
  Quando eles são usados para essa finalidade, o conteúdo de um diagrama de classe UML é chamado de um diagrama de classe conceitual. (Ele também é conhecido como um *modelo de domínio* ou *modelo de análise de classe*.)  
  
  Em um diagrama de classe conceitual, é possível mostrar apenas essas classes necessárias nas descrições dos requisitos, sem mostrar qualquer um dos detalhes do design de interno do sistema. O diagrama não mostra os detalhes de design de interno do sistema. Você não geralmente mostraria operações ou interfaces nas classes conceituais.  
  
  Por exemplo, você pode desenhar essas classes conceituais para o sistema Dinner Now:  
  
  ![Menu de classes, a ordem de Item de Menu, Item do pedido. ](../modeling/media/uml-reqmcd1.png "UML_ReqMCD1")  
  
  Um diagrama de classe conceitual fornece o vocabulário de termos que você usa em todo o modelo de requisitos. Por exemplo, na descrição detalhada do uso caso ordenar uma refeição, você pode escrever:  
  
  O cliente escolhe um *menus* do qual construir um *ordem*e, em seguida, cria *itens do pedido* no *ordem* selecionando  *Itens de menu* do *Menu*.  
  
  Observe como os termos usados na descrição do que são os nomes das classes no modelo. O diagrama remove ambiguidades de relações entre essas classes. Por exemplo, mostra claramente que cada pedido está associado a apenas um Menu.  
  
  Com frequência podem ser rastreados mal-entendidos sobre os requisitos dos usuários mal-entendidos sobre os significados detalhados de palavras. Por exemplo, a maioria dos restaurantes terá uma compreensão geral dos termos de Menu e ordem, mas a diferença entre um item em uma ordem e um item em um Menu é menos clara. Quando os requisitos de estão sendo discutidos com participantes de negócios, é importante para expor essas diferenças. O diagrama de classe é uma ferramenta útil para ajudar a esclarecer os termos e suas relações.  
  
  O modelo de classe conceitual pode formar o vocabulário básico pelo qual a lógica de negócios do seu sistema pode ser descrita. Mas as classes no software geralmente será muito mais complexas do que o modelo conceitual, porque sua implementação deve considerar os problemas, como desempenho, distribuição, flexibilidade e outros fatores. Várias implementações diferentes de uma classe conceitual frequentemente são encontradas em um sistema.  
  
  Por exemplo, pedidos poderia ser representados em XML, SQL, HTML e c# em diferentes partes do sistema e em interfaces diferentes entre as partes. A associação entre um pedido e um Menu poderia ser representada de várias maneiras diferentes, como referências no código do c#, as relações em um banco de dados, ou a referência cruzada IDs em XML. Mas, apesar dessas variações, o modelo conceitual fornece informações importantes que se aplica a todas as partes do software. O diagrama de classe no exemplo nos informa que cada implementação, haverá apenas um que menu associado com cada pedido.  
  
  Desenhando um diagrama de classe requisitos ajuda sua equipe:  
  
- Definir e padronizar os termos básicos usados em discussões de necessidades dos usuários.  
  
- Esclareça as relações entre esses termos.  
  
  Os tópicos a seguir fornecem mais informações:  
  
|Para saber mais sobre|Ler|  
|--------------------|----------|  
|Informações mais detalhadas sobre a localização de classes de requisitos|[Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|  
|Elementos em um diagrama de classe conceitual|[Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)|  
|Como desenvolver o código de classes conceituais|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|  
  
 Em um diagrama de classe conceitual, normalmente não é útil colocar as setas nas associações para representar navegabilidade. Isso ocorre porque o diagrama não representa uma implementação. As associações representam relações entre objetos do mundo real. O seguinte [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão tornar setas de não-direcional padrão: [exemplo: recursos de modelagem de domínio UML](http://go.microsoft.com/fwlink/?LinkId=213849).  
  
##  <a name="BusinessRules"></a> Mostrando as regras de negócio  
 Uma regra de negócios é um requisito que não está associado um caso de uso específico e deve ser observado em todo o sistema.  
  
 Muitas regras de negócios são restrições nas relações entre as classes conceituais. Você pode escrever esses *regras de negócio estático* como comentários associados com as classes relevantes em um diagrama de classe conceitual. Por exemplo:  
  
 ![Regra em comentário anexado à classe Order. ](../modeling/media/uml-reqmcd2.png "UML_ReqmCD2")  
  
 *Regras de negócio dinâmico* restringir as permitidas sequências de eventos. Por exemplo, você deve usar um diagrama de sequência ou atividade para mostrar que um usuário deve fazer logon antes de executar outras operações em seu sistema.  
  
 No entanto, muitas regras dinâmicas podem ser com mais eficiência e genericamente declaradas substituindo-os por regras estáticas. Por exemplo, você poderia adicionar um atributo booliano 'Registrado em' a uma classe no modelo conceitual de classe. Você seria adicionar conectado como a pós-condição do log em caso de uso e adicioná-lo como uma pré-condição para a maioria dos casos de uso. Essa abordagem permite que você evite definir todas as combinações possíveis de sequências de eventos. Também é mais flexível quando você precisa adicionar novos casos de uso para o modelo.  
  
 Observe que a escolha aqui é sobre como definir os requisitos e que isso é independente de como implementar os requisitos no código do programa.  
  
 Os tópicos a seguir fornecem mais informações:  
  
|Para saber mais sobre|Ler|  
|--------------------|----------|  
|Informações mais detalhadas sobre a localização e a gravação de regras de negócio estático|[Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|  
|Elementos em um diagrama de classe conceitual|[Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)|  
|Como desenvolver um código que obedeça às regras de negócio|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|  
  
##  <a name="QoSRequirements"></a> Que descreve a qualidade dos requisitos de serviço  
 Há várias categorias de qualidade de requisito de serviço. Elas incluem o seguinte:  
  
- Desempenho  
  
- Segurança  
  
- Usabilidade  
  
- Confiabilidade  
  
- Robustez  
  
  Você pode incluir alguns desses requisitos nas descrições de casos de uso específico. Outros requisitos não são específicos para casos de uso e com mais eficiência são gravados em um documento separado. Quando possível, é útil cumprir o vocabulário definido pelo modelo de requisitos. No exemplo a seguir, observe-se de que as palavras principais usadas requisitos de estão os títulos das classes nas ilustrações anteriores, casos de uso e atores:  
  
  Se um restaurante exclui um Item de Menu, enquanto que um cliente é ordenar uma refeição, qualquer Item do pedido que se refere a esse Item de Menu será exibido em vermelho.  
  
  Os tópicos a seguir fornecem mais informações:  
  
|Para saber mais sobre|Ler|  
|--------------------|----------|  
|Informações mais detalhadas sobre a qualidade dos requisitos de serviço da gravação|[Diretrizes para definir a qualidade dos requisitos de serviço](http://msdn.microsoft.com/en-us/9677a437-c2cb-4ac4-8c2d-4e3350005f06)|  
|Anexando documentos adicionais para casos de uso|[Vincular um caso de uso a documentos e diagramas](../modeling/link-a-use-case-to-documents-and-diagrams.md)|  
|Como desenvolver um código que obedeça a qualidade dos requisitos de serviço|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|  
  
##  <a name="Workflow"></a> Mostrando o fluxo de trabalho entre usuários e seu sistema  
 Você pode usar um diagrama de atividade para mostrar o fluxo de trabalho entre diferentes casos de uso. Geralmente é útil começar a um modelo de requisitos desenhando um diagrama de atividade mostrando as principais tarefas que os usuários realizam - com o sistema e fora dele.  
  
 Por exemplo:  
  
 ![Atividade com três ações e um loop. ](../modeling/media/uc-reqmwfact.png "UC_ReqmWFAct")  
  
 Você pode desenhar diagramas de caso de uso e os diagramas de atividade para mostrar exibições diferentes das mesmas informações.  O diagrama de caso de uso é mais eficaz para mostrar o aninhamento das ações menores dentro da atividade maior, mas não mostra o fluxo de trabalho. Por exemplo:  
  
 ![Casos de uso para ações anteriores](../modeling/media/uml-reqmwfuc.png "UML_ReqmWFUC")  
  
 Observe que você também pode usar diagramas de atividade para descrever os algoritmos de dentro de seu software, mas quando você usa os diagramas para o processo de negócios, você se concentre nas ações que são visíveis fora do sistema.  
  
 Os tópicos a seguir fornecem mais informações:  
  
|Para saber mais sobre|Ler|  
|--------------------|----------|  
|Para obter mais informações sobre como definir fluxos de trabalho de negócios|[Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)|  
|Elementos em um diagrama de atividade|[Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)|  
|Como desenvolver o código em diagramas de atividade|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|  
  
##  <a name="Sequences"></a> Mostrando as interações entre usuários e seu sistema  
 Você pode usar um diagrama de sequência para mostrar o intercâmbio de mensagens entre seu sistema e atores externos ou entre as partes do seu sistema. Isso fornece uma exibição das etapas em um caso de uso que mostra claramente a sequência de interações. Diagramas de sequência são especialmente úteis em que há que várias interagir a terceiros em um caso de uso e também em que seu sistema tem uma API.  
  
 Por exemplo:  
  
 ![Diagrama de sequência com sistema e atores. ](../modeling/media/uml-reqmseq.png "UML_ReqmSeq")  
  
 Uma vantagem de diagramas de sequência é que ele é fácil ver quais mensagens entram no sistema que você está construindo. Para o sistema de design, você pode substituir a única linha de vida do sistema com uma linha da vida separada para cada um de seus componentes e, em seguida, mostrar as interações entre eles em resposta a cada mensagem de entrada.  
  
 Os tópicos a seguir fornecem mais informações:  
  
|Para saber mais sobre|Ler|  
|--------------------|----------|  
|Para obter mais informações sobre como definir as interações|[Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)|  
|Elementos em um diagrama de sequência|[Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)|  
|Como desenvolver o código em diagramas de sequência|[Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)|  
  
## <a name="using-a-model-to-reduce-inconsistencies"></a>Usando um modelo para reduzir as inconsistências  
 Criando um modelo geralmente resulta em uma redução significativa em inconsistências e ambiguidades nos requisitos dos usuários. Participantes diferentes frequentemente têm diferentes Noções básicas do mundo dos negócios em que o sistema funciona. Portanto, a primeira tarefa é resolver essas diferenças entre os clientes.  
  
 Você encontrará muitas perguntas sobre o domínio de negócios naturalmente surgem durante a criação de um modelo. Colocando essas perguntas para seus usuários, você reduzirá a necessidade de alterações em um estágio posterior no projeto. Aqui estão algumas perguntas específicas, você pode perguntar primeiro e, em seguida, solicitar as partes interessadas no negócio se a resposta não está clara:  
  
- Para cada classe no modelo de requisitos, perguntar "o que usar caso cria as instâncias dessa classe?" Por exemplo, em um serviço online da ordenação de refeição, você poderia perguntar: "o que caso de uso cria instâncias da classe de Menu do restaurante?" Isso levaria a uma discussão sobre como um novo restaurante está inscrito no serviço e contribui com o menu. Você pode fazer perguntas semelhantes sobre o que cria ou altera os atributos e associações.  
  
- Para cada caso de uso no modelo de requisitos, experimente descrever o resultado ou pós-condição de cada caso de uso em palavras fornecida pelos diagramas de classe. Geralmente é útil mostrar o efeito de um caso de uso, esboçando instâncias das classes antes e após uma ocorrência do caso de uso. Por exemplo, se a pós-condição de casos de uso diz: "um item de menu é adicionado para o pedido do cliente" esboço instâncias das classes de ordem e o Item de Menu. Mostra os efeitos do caso de uso, como um novo link ou um novo objeto, em uma cor diferente ou em um novo desenho. Com frequência, isso resulta em discussões sobre quais informações são necessárias no modelo. Embora as classes de requisitos não estão diretamente relacionadas com a implementação, eles descrevem as informações que o sistema precisará armazenar e transmitir.  
  
- Pergunte sobre as restrições em atributos e associações, especialmente as restrições que envolvem mais de um atributo ou uma associação.  
  
- Pergunte sobre sequências válidas e inválidas de casos de uso, desenhar diagramas de sequência ou atividade para ilustrá-los.  
  
  Examinando as relações entre as exibições que fornecem diagramas diferentes, você pode rapidamente compreender os conceitos principais com os quais os usuários trabalham, e ajudá-lo a entender o que precisam do sistema. Você também pode acessar um melhor entendimento de quais requisitos os participantes são menos certos sobre. Você pode planejar desenvolver esses recursos, uma forma simplificada, pelo menos um estágio inicial do projeto, para permitir que os usuários a fazer experimentos com elas.  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Desenvolver testes de um modelo](../modeling/develop-tests-from-a-model.md)   
 [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)   
 [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)   
 [Extensão do VS de exemplo: Recursos de modelagem de domínio UML](http://go.microsoft.com/fwlink/?LinkId=213849)   
 [Extensão do VS de exemplo: Elementos UML de cor por estereótipo](http://go.microsoft.com/fwlink/?LinkID=213841)   
 [Extensão do VS de amostra: Elementos UML de Link diagramas, arquivos e outros elementos](http://go.microsoft.com/fwlink/?LinkID=213813)   
 [Extensão do VS de exemplo: Alinhar formas em um diagrama UML](http://go.microsoft.com/fwlink/?LinkID=213809)   
 [Vídeo: Modelando o domínio corporativo](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-3-Modeling-the-Business-Domain/)



