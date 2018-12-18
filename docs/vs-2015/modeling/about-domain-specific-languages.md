---
title: Sobre linguagens específicas do domínio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language
ms.assetid: 29e5b6f2-ece4-4f3b-ab08-5f957418702f
caps.latest.revision: 28
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 6cddf51705758d046ab66319d6ac6295f3a4b057
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894515"
---
# <a name="about-domain-specific-languages"></a>Sobre linguagens específicas do domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao contrário de uma linguagem de finalidade geral, como c# ou UML, uma linguagem específica de domínio (DSL) foi projetada para expressar declarações em um determinado problema de espaço ou domínio.  
  
 DSLs Well-Known incluem expressões regulares e SQL. Cada DSL é muito melhor do que uma linguagem de finalidade geral para descrever as operações em cadeias de caracteres de texto ou um banco de dados, mas um desempenho pior para descrever as ideias que estão fora do seu próprio escopo. Setores individuais também têm seus próprios DSLs. Por exemplo, na indústria de telecomunicações, chame descrição idiomas são amplamente usados para especificar a sequência dos estados em uma chamada telefônica e a indústria de viagem no ar um padrão de que DSL é usada para descrever as reservas de voo.  
  
 Sua empresa e seu projeto também lidam com conjuntos especiais de conceitos que podem ser descritos com uma DSL. Por exemplo, você pode definir uma DSL para um desses aplicativos:  
  
- Plano de caminhos de navegação em um site da Web.  
  
- Diagramas de fiação de componentes eletrônicos.  
  
- Redes de belts transportadora e equipamentos para um aeroporto de tratamento de bagagem.  
  
  Ao projetar uma DSL, você define uma *classe de domínio* para cada um dos conceitos importantes no domínio, como uma página da Web, lamp ou aeroporto check-in do suporte técnico. Você define *relações de domínio* como hiperlink, transmissão ou uma esteira para vincular os conceitos.  
  
  Criarem usuários de sua DSL *modelos.* Os modelos são *instâncias* da DSL. Por exemplo, elas descrevem um determinado site ou a fiação de um determinado dispositivo ou a sistema em um aeroporto específico de manipulação de bagagem.  
  
  Os usuários podem exibir um modelo como um diagrama ou como um formulário do Windows. Modelos também podem ser exibidos como XML, que é como eles são armazenados. Quando você define uma DSL, você define como as instâncias de cada classe de domínio e a relação aparecer na tela do usuário. Uma DSL típica é exibida como uma coleção de ícones ou retângulos conectados por setas.  
  
  A figura a seguir mostra um modelo pequeno em uma DSL diagramática:  
  
  ![Modelo de árvore genealógica Tudor](../modeling/media/tudor-familytreemodel.png "Tudor_FamilyTreeModel")  
  
## <a name="what-you-can-do-with-dsls"></a>O que você pode fazer com as DSLs  
 Um aplicativo típico de uma DSL é gerar o código do programa ou outros artefatos. Quando você define sua DSL, você pode definir *modelos de texto* que ler um modelo da DSL e gerar arquivos de texto.  
  
 Por exemplo, você poderia escrever modelos que usam um plano do aeroporto e geram a parte do software para manipular, bem como algumas os documentos do usuário que descrevem o plano de coleta de bagagem.  
  
 Quando você tiver definido uma DSL, você pode distribuí-lo para outros usuários que podem instalá-lo em seus próprios computadores. Os usuários de sua DSL podem criar e editar modelos em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 Você também pode definir comandos de menu e outras ferramentas que ajudam os usuários a editar a DSL, restrições de validação para ajudar a garantir que a DSL é usada corretamente e modelos de item que ajudam os usuários a criam novas instâncias. Você pode encapsular um ou mais DSLs com suas ferramentas e outros [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões como um pacote integrado.  
  
 Normalmente, uma linguagem específica de domínio é criada quando uma equipe de desenvolvimento deve escrever um código semelhante para vários produtos. Por exemplo, uma empresa especializada em sistemas de manuseio de bagagem pode definir uma DSL de faixa de bagagem do qual eles podem gerar algum código para cada instalação. Os benefícios da DSL são o que ele pode ser compreendido por seus clientes, que o código gerado a partir dele é confiável e que o sistema pode ser atualizado rapidamente se alterarem às necessidades dos clientes.  
  
 [!INCLUDE[dsl](../includes/dsl-md.md)] permite criar uma linguagem específica de domínio que tem seu próprio designer gráfico e seu próprio notação do diagrama e, em seguida, usar a linguagem para gerar o código-fonte apropriado para cada projeto.  
  
## <a name="domain-specific-development"></a>Desenvolvimento de domínio específico  
 Desenvolvimento específica de domínio é o processo de identificar as partes de seus aplicativos que podem ser modelados usando uma linguagem específica de domínio e, em seguida, construindo a linguagem e implantá-lo para desenvolvedores de aplicativos. Os desenvolvedores usam a linguagem específica de domínio para construir modelos que são específicos para seus aplicativos, usar os modelos para gerar código-fonte e, em seguida, usar o código-fonte para desenvolver os aplicativos.  
  
## <a name="aspects-of-graphical-domain-specific-development"></a>Aspectos do desenvolvimento de gráfico específica de domínio  
 Uma linguagem específica de domínio gráfica deve incluir os seguintes recursos:  
  
-   Notation  
  
-   Modelo de domínio  
  
-   Geração de artefato  
  
-   Serialização  
  
-   Integração com o Visual Studio  
  
### <a name="notation"></a>Notation  
 Uma linguagem específica de domínio deve ter um conjunto razoavelmente pequeno de elementos que podem ser facilmente definidos e estendida para representar construções específicas do domínio. Uma notação consiste em formas, que representam os elementos, e conectores, que representam as relações entre os elementos em uma superfície de Diagrama gráfico. No [!INCLUDE[dsl](../includes/dsl-md.md)], as formas podem ser estendidas e refinadas para representar os elementos da sua linguagem específica do domínio.  
  
### <a name="domain-model"></a>Modelo de domínio  
 Uma linguagem específica de domínio deve combinar o conjunto de elementos e as relações entre eles em uma gramática coerente. Ele também deve definir se as combinações de elementos e relações são válidas. Por exemplo, linguagens de programação geralmente impedem a herança circular, em que uma classe é derivada de uma segunda classe e a segunda classe é derivada da classe primeiro. Restrições também podem ser usadas para expressar a lógica de negócios, por exemplo, uma pessoa não pode ser um dependente de si próprio. [!INCLUDE[dsl](../includes/dsl-md.md)] usa as restrições para expressar os tipos de restrições que exigem mais a linguagens específicas de domínio.  
  
### <a name="artifact-generation"></a>Geração de artefato  
 Um dos principais objetivos de uma linguagem específica de domínio é gerar um artefato, por exemplo, código-fonte, um arquivo XML ou outros dados utilizáveis. Normalmente, uma alteração no modelo significa que uma alteração no artefato. Você pode usar [!INCLUDE[dsl](../includes/dsl-md.md)] para gerar artefatos e regenerá-las quando você altera o modelo.  
  
### <a name="serialization"></a>Serialização  
 Uma linguagem específica de domínio deve ser persistida em alguma forma que pode ser editada, salvo, fechada e recarregada. [!INCLUDE[dsl](../includes/dsl-md.md)] usa um formato XML que permite definir e personalizar como sua linguagem específica do domínio é serializada ou persistente.  
  
### <a name="integration-with-visual-studio"></a>Integração com o Visual Studio  
 Porque [!INCLUDE[dsl](../includes/dsl-md.md)] é hospedado no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], ela se estende para muitos [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janelas e controles. Ele também permite personalizar o comportamento dos comandos de menu, itens de caixa de ferramentas e outros elementos da interface do usuário.  
  
 Você também pode criar um adaptador de barramento do modelo para sua linguagem específica do domínio. Esse adaptador permite que um modelo de referência e elementos dentro de um modelo e permite que você escreve o código que pode acessar e atualizar uma instância da DSL. Ao usar o mecanismo poderoso do Model Bus, você pode escrever [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões que funcionam com vários modelos. Você também pode escrever aplicativos autônomos que trabalhem com modelos. Para obter mais informações, consulte [integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md).  
  
## <a name="benefits-of-domain-specific-development"></a>Benefícios de desenvolvimento específicas do domínio  
 Uma linguagem específica de domínio pode fornecer os seguintes benefícios:  
  
-   Contém as construções que se ajuste exatamente o problema de espaço.  
  
     Ao contrário de linguagens de finalidade geral, uma linguagem específica de domínio consiste em elementos e relações que representam diretamente a lógica do problema. Por exemplo, um aplicativo da apólice de seguro deve incluir elementos de políticas e declarações. Uma linguagem específica de domínio torna mais fácil de criar o aplicativo e localizar e corrigir os erros de lógica.  
  
-   Permite que as pessoas que não conhecem o domínio de entender o design geral e não-desenvolvedores.  
  
     Usando uma linguagem específica de domínio gráfica, você pode criar uma representação visual do domínio para que não-desenvolvedores podem facilmente entender o design do aplicativo.  
  
-   Torna mais fácil criar um protótipo do aplicativo final.  
  
     Os desenvolvedores podem usar o código que gera de seu modelo para criar um aplicativo de protótipo que eles podem mostrar aos clientes.  
  
## <a name="the-process-of-domain-specific-development"></a>O processo de desenvolvimento específicas do domínio  
 A maioria das equipes de desenvolvimento de software que usam linguagens específicas de domínio siga estas etapas para criar e usar seus modelos:  
  
-   A equipe distingue as partes variáveis do domínio a partir das partes que nunca alterar.  
  
-   Os desenvolvedores escrever código para as partes fixas e deixar os pontos de extensão para as partes variáveis.  
  
-   O gerente de desenvolvimento de software ou o arquiteto cria uma linguagem específica de domínio que incorpora os padrões de design das partes do domínio e os pontos de extensão para as partes variáveis fixas.  
  
-   O gerente de desenvolvimento de software ou o arquiteto implanta a linguagem específica de domínio para os desenvolvedores dos vários aplicativos que produz a equipe.  
  
-   Todo desenvolvedor cria um modelo que se aplica ao aplicativo específico.



