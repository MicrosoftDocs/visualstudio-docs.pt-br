---
title: Gerar e configurar o aplicativo por meio de modelos
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 78dc0907fa717f61b6cf883994a3ac2fd6072ba1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872792"
---
# <a name="generate-and-configure-your-app-from-models"></a>Gerar e configurar o aplicativo por meio de modelos
Você pode gerar ou configurar as partes do seu aplicativo de um modelo.

 O modelo representa os requisitos mais diretamente o código. Ao derivar o comportamento do aplicativo diretamente do modelo, você pode responder a requisitos alterados atualização muito mais rápida e confiável que o código. Embora algum trabalho inicial é necessária para configurar a derivação, esse investimento é retornado se você espera que as alterações nos requisitos, ou se você planeja fazer diversas variantes do produto.

## <a name="generating-the-code-of-your-application-from-a-model"></a>Gerando o código do seu aplicativo de um modelo
 É a maneira mais fácil para gerar o código usando modelos de texto. Você pode gerar o código na mesma solução do Visual Studio em que você mantenha o modelo. Para obter mais informações, consulte:

- [Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)

- [Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)

  Esse método é mais fácil aplicar incrementalmente. Iniciar com um aplicativo que funciona apenas para um caso específico e escolha algumas partes dele que você deseja variar do modelo. Renomeie os arquivos de código-fonte dessas partes para que se tornem arquivos de modelo (. TT) de texto. Neste ponto, os arquivos de origem. cs automaticamente serão gerados de arquivos de modelo, portanto, o aplicativo funcionará como antes.

  Em seguida, você pode levar a uma parte do código e substituí-la por uma expressão de modelo de texto, que lê o modelo e gera essa parte do arquivo de origem. Pelo menos um valor do modelo deve gerar o código-fonte original para que, novamente, você pode executar o aplicativo e ele funcionará como antes. Depois de testar valores diferentes de modelos, você pode passar para inserir expressões de modelo em outra parte do código.

  Esse método incremental significa que a geração de código geralmente é uma abordagem de baixo risco. Os aplicativos resultantes geralmente executam quase, bem como uma versão manuscrita.

  No entanto, se você iniciar com um aplicativo existente, você pode achar que um lote de refatoração é necessária para separar os diferentes comportamentos que são governados pelo modelo para que eles podem ser variados independentemente. É recomendável que você avalie esse aspecto do aplicativo ao estimar o custo do seu projeto.

## <a name="configuring-your-application-from-a-model"></a>Configurar seu aplicativo de um modelo
 Se você deseja variar o comportamento do aplicativo em tempo de execução, você não pode usar a geração de código, o que gera o código-fonte antes do aplicativo é compilado. Em vez disso, você pode projetar seu aplicativo para ler o modelo e variam de seu comportamento de acordo. Para obter mais informações, consulte:

- [Como abrir um modelo partindo de um arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md)

  Esse método também pode ser aplicado incrementalmente, mas há mais trabalho no início. Você precisa escrever o código que leia o modelo e configurar uma estrutura que permite que seus valores fique acessível para as partes variáveis. Tornar as partes variáveis genéricos é mais caro do que a geração de código.

  Um aplicativo genérico executa normalmente menos bem que suas contrapartes específicos. Se o desempenho é fundamental, seu plano de projeto deve incluir uma avaliação desse risco.

## <a name="developing-a-derived-application"></a>Desenvolvendo um aplicativo derivado
 Você pode achar úteis as seguintes diretrizes gerais.

-   **Iniciar específico, em seguida, generalize.** Escreva uma versão específica do seu aplicativo pela primeira vez. Esta versão deverá funcionar em um conjunto de condições. Quando estiver satisfeito que ele está funcionando corretamente, você pode fazer parte dela derivam de um modelo. Estenda as partes derivadas gradualmente.

     Por exemplo, criação de um site que tem um conjunto específico de páginas da web antes de criar um aplicativo web que apresenta as páginas que são definidas em um modelo.

-   **Os aspectos de variante do modelo.** Identifique os aspectos que irá variar, entre cada implantação de um e outro, ou ao longo do tempo como requisitos de alterar. Estes são os aspectos que devem ser derivados de um modelo.

     Por exemplo, se o conjunto de web de páginas e os links entre eles muda, mas o estilo e o formato das páginas é sempre o mesmo, em seguida, o modelo deve descrever os links, mas não tem que descrevem o formato das páginas.

-   **Preocupações separadas.** Se a variável aspectos podem ser divididos em áreas independentes, use modelos separados para cada área. Usando ModelBus, é possível definir as operações que afetam os modelos e as restrições entre eles.

     Por exemplo, use um modelo para definir a navegação entre as páginas da web e um modelo diferente para definir o layout das páginas.

-   **O requisito, e não na solução de modelo.** Crie o modelo para que ele descreve os requisitos do usuário. Por outro lado, não crie a notação de acordo com as variável aspectos da implementação.

     Por exemplo, o modelo de navegação da web deve representar páginas da web e hiperlinks entre eles. O modelo de navegação da web não deve representar fragmentos de HTML ou classes em seu aplicativo.

-   **Gerar ou interpretar?** Se os requisitos para uma determinada implantação raramente serão alterado, gere código de programa do modelo. Se os requisitos podem mudar com frequência, ou podem coexistir em mais de uma variante na mesma implantação, escreva o aplicativo para que ele pode ler e interpretar um modelo.

     Por exemplo, se você usar o modelo de site para desenvolver uma série de sites diferentes e instalado separadamente, você deve gerar o código do site do modelo. Mas você usa seu modelo para controlar um site que são alterados diariamente, em seguida, é melhor escrever um servidor web que lê o modelo e apresenta o site adequadamente.

-   **UML ou DSL?** Considere a criação de seu notação de modelagem usando estereótipos para estender UML. Defina uma DSL se não houver nenhum diagrama UML que se adapta ao objetivo. Mas, evitar a interrupção a semântica padrão de UML.

     Por exemplo, um diagrama de classe UML é uma coleção de caixas e setas; com essa notação você pode teoricamente definir nada. Mas não recomendamos que você use o diagrama de classe, exceto onde você é na verdade que descreve um conjunto de tipos. Por exemplo, você pode adaptar os diagramas de classe para descrever diferentes tipos de páginas da web.

## <a name="see-also"></a>Consulte também

- [Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)
- [Como abrir um modelo partindo de um arquivo no código do programa](../modeling/how-to-open-a-model-from-file-in-program-code.md)
- [Geração de código no tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md)