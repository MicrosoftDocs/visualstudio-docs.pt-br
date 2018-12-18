---
title: SDK de Modelagem para Visual Studio - linguagens específicas ao domínio
titleSuffix: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools
- Domain-Specific Language
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6de309ca6ff9c1813a2a2a6ebc54ea6baa3a795f
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53060472"
---
# <a name="modeling-sdk-for-visual-studio---domain-specific-languages"></a>SDK de Modelagem para Visual Studio - linguagens específicas ao domínio

Usando o SDK de modelagem para Visual Studio, você pode criar ferramentas de desenvolvimento baseado em modelo avançadas que podem ser integradas ao Visual Studio. Da mesma forma, você pode criar uma ou mais definições de modelo e integrá-las em um conjunto de ferramentas.

No centro do MSDK está a definição de um modelo que você cria para representar conceitos em sua área de negócios. Você pode cercar o modelo com uma variedade de ferramentas, como uma exibição diagramática, a capacidade de gerar o código e outros artefatos, comandos para transformar o modelo e a capacidade de interagir com o código e outros objetos no Visual Studio. À medida que o modelo é desenvolvido, você pode combiná-lo com outros modelos e ferramentas para formar um conjunto de ferramentas avançadas centradas em seu desenvolvimento.

O MSDK permite desenvolver rapidamente um modelo na forma de uma linguagem específica do domínio (DSL). Você começa ao usar um editor especializado para definir um esquema ou sintaxe abstrata junto com uma notação gráfica. Dessa definição, o VMSDK gera:

- Uma implementação de modelo com uma API fortemente tipada executada em um repositório baseado em transação.

- Um gerenciador baseado em árvore.

- Um editor gráfico no qual os usuários podem exibir o modelo ou partes dele que você definir.

- Métodos de serialização que salvam seus modelos em XML legível.

- Recursos para gerar código de programa e outros artefatos usando modelagem de texto.

Você pode personalizar e estender todos esses recursos. Suas extensões são integradas de tal forma que você ainda pode atualizar a definição de DSL e gerar novamente os recursos sem perder suas extensões.

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

[Postagens de blogs relacionadas](https://blogs.msdn.microsoft.com/visualstudioalm/tag/code-index/)

Para obter orientação sobre técnicas avançadas e solução de problemas, visite [Fórum de extensibilidade de ferramentas de modelagem & de DSL do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=186074).

## <a name="in-this-section"></a>Nesta seção
 [Introdução às linguagens específicas de domínio](../modeling/getting-started-with-domain-specific-languages.md)

 [Noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md)

 [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)

 [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md)

 [Validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md)

 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)

 [Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)

 [Noções básicas do código DSL](../modeling/understanding-the-dsl-code.md)

 [Personalizando o armazenamento de arquivos e a serialização XML](../modeling/customizing-file-storage-and-xml-serialization.md)

 [Implantando soluções de linguagem específica de domínio](../modeling/deploying-domain-specific-language-solutions.md)

 [Criando uma linguagem específica de domínio baseada no Windows Forms](../modeling/creating-a-windows-forms-based-domain-specific-language.md)

 [Criando uma linguagem específica de domínio baseada no WPF](../modeling/creating-a-wpf-based-domain-specific-language.md)

 [Como estender o designer de linguagem específica de domínio](../modeling/how-to-extend-the-domain-specific-language-designer.md)

 [Edições do Visual Studio com suporte pelo SDK de Visualização e Modelagem](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)

 [Como migrar uma linguagem específica de domínio para uma nova versão](../modeling/how-to-migrate-a-domain-specific-language-to-a-new-version.md)

 [Referência de API do SDK de Modelagem para Visual Studio](../modeling/api-reference-for-modeling-sdk-for-visual-studio.md)
