---
title: Sobre linguagens específicas do domínio
description: Saiba como uma DSL (linguagem específica de domínio) foi projetada para expressar instruções em um determinado espaço de problema ou domínio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ab56292aafda25efc0b3dfeeb14e93d4502a5567
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112384974"
---
# <a name="about-domain-specific-languages"></a>Sobre linguagens específicas do domínio

Diferentemente de uma linguagem de finalidade geral, como C# ou UML, uma DSL (linguagem específica de domínio) foi projetada para expressar instruções em um determinado espaço de problema ou domínio.

As DSLs conhecidas incluem expressões regulares e SQL. Cada DSL é muito melhor do que uma linguagem de finalidade geral para descrever as operações em cadeias de caracteres de texto ou um banco de dados, mas muito pior para descrever ideias que estão fora de seu próprio escopo. Os setores individuais também têm suas próprias DSLs. Por exemplo, no setor de telecomunicações, as linguagens de descrição da chamada são amplamente usadas para especificar a sequência de Estados em uma chamada telefônica e, no setor de viagens aéreas, uma DSL padrão é usada para descrever as reservas de voo.

Seu negócio e seu projeto também lidam com conjuntos especiais de conceitos que poderiam ser descritos com uma DSL. Por exemplo, você pode definir uma DSL para um desses aplicativos:

- Plano de caminhos de navegação em um site.

- Diagramas de fiação para componentes eletrônicos.

- Redes de esteiras de transmissão e equipamento de manuseio de bagagem para um aeroporto.

Ao projetar uma DSL, você define uma *classe de domínio* para cada um dos conceitos importantes no domínio, como uma página da Web, uma lâmpada ou uma central de verificação de aeroportos. Você define *relações de domínio* , como hiperlink, fio ou uma correia de transmissão para vincular os conceitos juntos.

Os usuários de sua DSL criam *modelos.* Os modelos são *instâncias* da DSL. Por exemplo, eles descrevem um site específico, ou a fiação de um dispositivo específico, ou o sistema de manuseio de bagagem em um aeroporto específico.

Os usuários podem exibir um modelo como um diagrama ou um formulário do Windows. Os modelos também podem ser exibidos como XML, que é como eles são armazenados. Ao definir uma DSL, você define como as instâncias de cada classe de domínio e relação aparecem na tela do usuário. Uma DSL típica é exibida como uma coleção de ícones ou retângulos conectados por setas.

A figura a seguir mostra um modelo pequeno em uma DSL diagramáticas:

![Modelo de árvore da família Tudor](../modeling/media/tudor_familytreemodel.png)

## <a name="what-you-can-do-with-dsls"></a>O que você pode fazer com DSLs

Um aplicativo típico de uma DSL é gerar código de programa ou outros artefatos. Ao definir sua DSL, você pode definir *modelos de texto* que lêem um modelo de DSL e geram arquivos de texto.

Por exemplo, você poderia escrever modelos que usam um plano de aeroportos e gerar parte do software para manipulação de bagagem, bem como alguns documentos de usuário que descrevem o plano.

Quando você tiver definido uma DSL, poderá distribuí-la a outros usuários que possam instalá-lo em seus próprios computadores. Os usuários de sua DSL podem criar e editar modelos no Visual Studio.

Você também pode definir comandos de menu e outras ferramentas que ajudam os usuários a editar a DSL, restrições de validação para ajudar a garantir que a DSL seja usada corretamente e os modelos de item que ajudam os usuários a criar novas instâncias. Você pode encapsular uma ou mais DSLs com suas ferramentas e outras extensões do Visual Studio como um pacote integrado.

Normalmente, uma linguagem específica de domínio é criada quando uma equipe de desenvolvimento precisa escrever código semelhante para vários produtos. Por exemplo, uma empresa especializada em sistemas de manuseio de bagagem pode definir uma DSL de bagagem Track da qual eles podem gerar algum código para cada instalação. Os benefícios da DSL são que ele pode ser compreendido por seus clientes, que o código gerado por ele é confiável e que o sistema pode ser atualizado rapidamente se os requisitos dos clientes mudarem.

[!INCLUDE[dsl](../modeling/includes/dsl_md.md)] permite que você crie uma linguagem específica de domínio que tenha seu próprio designer gráfico e sua própria notação de diagrama e, em seguida, use a linguagem para gerar o código-fonte apropriado para cada projeto.

## <a name="domain-specific-development"></a>Desenvolvimento de Domain-Specific

O desenvolvimento específico de domínio é o processo de identificar as partes de seus aplicativos que podem ser modelados usando uma linguagem específica de domínio e, em seguida, construir o idioma e implantá-lo nos desenvolvedores de aplicativos. Os desenvolvedores usam a linguagem específica de domínio para construir modelos que são específicos para seus aplicativos, usam os modelos para gerar código-fonte e, em seguida, usam o código-fonte para desenvolver os aplicativos.

## <a name="aspects-of-graphical-domain-specific-development"></a>Aspectos do desenvolvimento de Domain-Specific gráfico

Uma linguagem gráfica específica do domínio deve incluir os seguintes recursos:

- Notation

- Modelo de domínio

- Geração de artefatos

- Serialização

- Integração com o Visual Studio

### <a name="notation"></a>Notation

Uma linguagem específica de domínio deve ter um conjunto razoavelmente pequeno de elementos que podem ser facilmente definidos e estendidos para representar construções específicas de domínio. Uma notação consiste em formas, que representam os elementos e conectores, que representam as relações entre os elementos, em uma superfície de diagrama gráfico. No [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] , as formas podem ser estendidas e refinadas para representar os elementos de sua linguagem específica de domínio.

### <a name="domain-model"></a>Modelo de domínio

Uma linguagem específica de domínio deve combinar o conjunto de elementos e as relações entre eles em uma gramática coerente. Ele também deve definir se as combinações de elementos e relações são válidas. Por exemplo, as linguagens de programação normalmente impedem a herança circular, na qual uma classe é derivada de uma segunda classe e a segunda classe é derivada da primeira classe. As restrições também podem ser usadas para expressar a lógica de negócios, por exemplo, uma pessoa não pode ser dependente de si mesma. [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] usa restrições para expressar os tipos de restrições que a maioria das linguagens específicas de domínio exigem.

### <a name="artifact-generation"></a>Geração de artefatos

Uma das principais finalidades de uma linguagem específica de domínio é gerar um artefato, por exemplo, código-fonte, um arquivo XML ou alguns outros dados utilizáveis. Normalmente, uma alteração no modelo significa uma alteração no artefato. Você pode usar [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] para gerar artefatos e gerá-los novamente quando alterar o modelo.

### <a name="serialization"></a>Serialização

Uma linguagem específica de domínio deve ser persistida em alguma forma que possa ser editada, salva, fechada e recarregada. [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] usa um formato XML que permite definir e personalizar como sua linguagem específica de domínio é serializada ou persistente.

### <a name="integration-with-visual-studio"></a>Integração com o Visual Studio

Como o [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] é hospedado no Visual Studio, ele estende muitas janelas e controles do Visual Studio. Ele também permite que você personalize o comportamento de comandos de menu, de itens da caixa de ferramentas e de outros elementos da interface do usuário.

Você também pode criar um adaptador de barramento de modelo para sua linguagem específica de domínio. Esse adaptador permite que você referencie um modelo e elementos dentro de um modelo e permite que você escreva um código que possa acessar e atualizar uma instância do DSL. Usando o poderoso mecanismo de barramento de modelo, você pode escrever extensões do Visual Studio que funcionam com vários modelos. Você também pode escrever aplicativos autônomos que funcionam com modelos. Para obter mais informações, consulte [integrando modelos usando o Visual Studio ModelBus](../modeling/integrating-models-by-using-visual-studio-modelbus.md).

## <a name="benefits-of-domain-specific-development"></a>Benefícios do desenvolvimento de Domain-Specific

Uma linguagem específica de domínio pode fornecer os seguintes benefícios:

- Contém construções que se ajustam exatamente ao espaço do problema.

     Diferentemente das linguagens de finalidade geral, uma linguagem específica de domínio consiste em elementos e relações que representam diretamente a lógica do espaço do problema. Por exemplo, um aplicativo de apólice de seguro deve incluir elementos para políticas e declarações. Uma linguagem específica de domínio torna mais fácil criar o aplicativo, localizar e corrigir erros de lógica.

- Permite que não desenvolvedores e pessoas que não conhecem o domínio compreendam o design geral.

     Usando uma linguagem gráfica específica do domínio, você pode criar uma representação visual do domínio para que os não-desenvolvedores possam entender facilmente o design do aplicativo.

- Torna mais fácil criar um protótipo do aplicativo final.

     Os desenvolvedores podem usar o código que o modelo gera para criar um aplicativo de protótipo que pode ser mostrado aos clientes.

## <a name="the-process-of-domain-specific-development"></a>O processo de desenvolvimento de Domain-Specific

A maioria das equipes de desenvolvimento de software que usam linguagens específicas de domínio segue estas etapas para criar e usar seus modelos:

- A equipe distingue as partes variáveis do domínio das partes que nunca mudam.

- Os desenvolvedores escrevem código para as partes fixas e deixam os pontos de extensão para as partes variáveis.

- O desenvolvedor de software líder ou o arquiteto cria uma linguagem específica de domínio que incorpora os padrões de design das partes fixas do domínio e os pontos de extensão para as partes variáveis.

- O desenvolvedor de software líder ou o arquiteto implanta a linguagem específica do domínio para os desenvolvedores de vários aplicativos que a equipe produz.

- Todo desenvolvedor cria um modelo que se aplica ao aplicativo específico.
