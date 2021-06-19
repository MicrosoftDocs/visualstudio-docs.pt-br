---
title: Gerar e configurar o aplicativo por meio de modelos
description: Saiba o que um modelo representa e como você pode gerar ou configurar partes do seu aplicativo de um modelo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 68339159ed9926490f22a82cd30ce69f45ab6a30
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388861"
---
# <a name="generate-and-configure-your-app-from-models"></a>Gerar e configurar o aplicativo por meio de modelos
Você pode gerar ou configurar partes do seu aplicativo de um modelo.

 O modelo representa os requisitos mais diretamente do que o código. Ao derivar o comportamento do aplicativo diretamente do modelo, você pode responder aos requisitos alterados muito mais rapidamente e de forma confiável do que atualizando o código. Embora seja necessário algum trabalho inicial para configurar a derivação, esse investimento será retornado se você esperar alterações nos requisitos ou se você planeja fazer várias variantes do produto.

## <a name="generating-the-code-of-your-application-from-a-model"></a>Gerando o código do aplicativo de um modelo
 A maneira mais fácil de gerar código é usando modelos de texto. Você pode gerar código na mesma Visual Studio na qual você mantém o modelo. Para obter mais informações, consulte:

- [Geração de código na hora de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)

- [Gerando código a partir de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md)

  Esse método é fácil de aplicar incrementalmente. Comece com um aplicativo que funciona apenas para um caso específico e escolha algumas partes dele que você deseja variar do modelo. Renomeie os arquivos de origem dessas partes para que eles se tornem arquivos de modelo de texto (.tt). Neste ponto, os arquivos .cs de origem serão gerados automaticamente dos arquivos de modelo, portanto, o aplicativo funcionará como antes.

  Em seguida, você pode pegar uma parte do código e substituí-la por uma expressão de modelo de texto, que lê o modelo e gera essa parte do arquivo de origem. Pelo menos um valor do modelo deve gerar a origem original para que você possa executar novamente o aplicativo e ele funcionará como antes. Depois de testar valores de modelo diferentes, você pode passar para inserir expressões de modelo em outra parte do código.

  Esse método incremental significa que a geração de código geralmente é uma abordagem de baixo risco. Os aplicativos resultantes geralmente executam quase tão bem quanto uma versão escrita manualmente.

  No entanto, se você começar com um aplicativo existente, poderá achar que é necessário muita refação para separar os diferentes comportamentos que são regidos pelo modelo para que eles possam ser variados independentemente. Recomendamos que você avalie esse aspecto do aplicativo ao estimar o custo do seu projeto.

## <a name="configuring-your-application-from-a-model"></a>Configurando seu aplicativo de um modelo
 Se você quiser variar o comportamento do aplicativo em tempo de executar, não poderá usar a geração de código, que gera o código-fonte antes que o aplicativo seja compilado. Em vez disso, você pode projetar seu aplicativo para ler o modelo e variar seu comportamento de acordo. Para obter mais informações, consulte:

- [Como abrir um modelo a partir de um arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md)

  Esse método também pode ser aplicado incrementalmente, mas há mais trabalho no início. Você precisa escrever o código que lerá o modelo e configurar uma estrutura que permita que seus valores sejam acessíveis às partes variáveis. Tornar as partes variáveis genéricas é mais cara do que a geração de código.

  Um aplicativo genérico geralmente tem um desempenho menor do que seus equivalentes específicos. Se o desempenho for crucial, seu plano de projeto deverá incluir uma avaliação desse risco.

## <a name="developing-a-derived-application"></a>Desenvolvendo um aplicativo derivado
 Você pode achar as diretrizes gerais a seguir úteis.

- **Inicie específico e generalize.** Primeiro, escreva uma versão específica do aplicativo. Essa versão deve funcionar em um conjunto de condições. Quando estiver satisfeito de que ele está funcionando corretamente, você poderá fazer parte dele derivar de um modelo. Estenda as partes derivadas gradualmente.

     Por exemplo, projete um site que tenha um conjunto específico de páginas da Web antes de criar um aplicativo Web que apresenta páginas definidas em um modelo.

- **Modele os aspectos variantes.** Identifique os aspectos que variam, entre uma implantação e outra ou ao longo do tempo, conforme os requisitos mudam. Esses são os aspectos que devem ser derivados de um modelo.

     Por exemplo, se o conjunto de páginas da Web e links entre elas mudar, mas o estilo e o formato das páginas for sempre o mesmo, o modelo deverá descrever os links, mas não precisa descrever o formato das páginas.

- **Preocupações separadas.** Se os aspectos da variável puderem ser divididos em áreas independentes, use modelos separados para cada área. Usando ModelBus, você pode definir operações que afetam os modelos e as restrições entre eles.

     Por exemplo, use um modelo para definir a navegação entre as páginas da Web e um modelo diferente para definir o layout das páginas.

- **Modele o requisito, não a solução.** Projete o modelo para que ele descreva os requisitos do usuário. Por outro lado, não projete a notação de acordo com os aspectos variáveis da implementação.

     Por exemplo, o modelo de navegação na Web deve representar páginas da Web e hiperlinks entre elas. O modelo de navegação na Web não deve representar fragmentos de HTML ou classes em seu aplicativo.

- **Gerar ou interpretar?** Se os requisitos de uma implantação específica raramente mudarem, gere o código do programa do modelo. Se os requisitos podem mudar com frequência ou podem existir em mais de uma variante na mesma implantação, escreva o aplicativo para que ele possa ler e interpretar um modelo.

     Por exemplo, se você usar seu modelo de site para desenvolver uma série de sites instalados separadamente e diferentes, deverá gerar o código do site do modelo. Mas se você usar seu modelo para controlar um site que muda todos os dias, é melhor escrever um servidor Web que leia o modelo e apresente o site de acordo.

- **UML ou DSL?** Considere criar sua notação de modelagem usando os preconceitos para estender um UML. Defina uma DSL se não houver nenhum diagrama UML que se ajuste à finalidade. Mas evite quebrar a semântica padrão de UML.

     Por exemplo, um diagrama de classe UML é uma coleção de caixas e setas; com essa notação, você pode, em teoria, definir qualquer coisa. Mas não recomendamos que você use o diagrama de classe, exceto quando, na verdade, você está descrevendo um conjunto de tipos. Por exemplo, você pode adaptar diagramas de classe para descrever diferentes tipos de páginas da Web.

## <a name="see-also"></a>Confira também

- [Gerando código a partir de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md)
- [Como abrir um modelo a partir de um arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md)
- [Geração de código na hora de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)
