---
title: 'Etapa 2: Adicionar um objeto aleatório e uma lista de ícones'
ms.custom: ''
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
ms.assetid: 95faea28-eddc-4cfa-95fb-3b34b5a976d7
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 84c9c837fdb812b18f72e768b8ee528118b28777
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34746826"
---
# <a name="step-2-add-a-random-object-and-a-list-of-icons"></a>Etapa 2: Adicionar um objeto aleatório e uma lista de ícones
Nesta etapa, você cria um conjunto de símbolos correspondentes para o jogo. Cada símbolo é adicionado a duas células aleatórias no TableLayoutPanel do formulário. Para isso, use duas instruções `new` para criar dois objetos. A primeira é um objeto <xref:System.Random>, como o usado no jogo de enigmas de matemática. Ele é usado nesse código para escolher aleatoriamente células no TableLayoutPanel. O segundo objeto, que pode ser novo para você, é um objeto <xref:System.Collections.Generic.List%601>, que é usado para armazenar os símbolos escolhidos aleatoriamente.

## <a name="to-add-a-random-object-and-a-list-of-icons"></a>Para adicionar um objeto aleatório e uma lista de ícones

1.  No **Gerenciador de Soluções**, escolha *Form1.cs* se você estiver usando o Visual C# ou o *Form1.vb* se você estiver usando o Visual Basic e, em seguida, na barra de menus, escolha **Exibir** > **Código**. Como uma alternativa, é possível pressionar a tecla **F7** ou clicar duas vezes em **Form1** no **Gerenciador de Soluções**.

     Isso exibe o módulo de código por trás de Form1.

2.  No código existente, adicione o código a seguir.

     [!code-csharp[VbExpressTutorial4Step2_3_4#1](../ide/codesnippet/CSharp/step-2-add-a-random-object-and-a-list-of-icons_1.cs)]
     [!code-vb[VbExpressTutorial4Step2_3_4#1](../ide/codesnippet/VisualBasic/step-2-add-a-random-object-and-a-list-of-icons_1.vb)]

     Se você estiver usando o Visual C#, certifique-se de colocar o código após a chave da abertura e logo após a declaração de classe (`public partial class Form1 : Form`). Se estiver usando o Visual Basic, coloque o código logo depois da declaração de classe (`Public Class Form1`).

3.  Ao adicionar o objeto de lista, observe a janela do **IntelliSense** que é aberta. Veja a seguir um exemplo do Visual C#, mas texto semelhante aparece quando você adiciona uma lista no Visual Basic.

     ![Janela Propriedades mostrando o evento de clique](../ide/media/express_listintellisense.png) Janela do IntelliSense

    > [!NOTE]
    >  A janela do IntelliSense aparece apenas quando você insere código manualmente. Se você copiar e colar o código, ela não aparecerá.

     Se você observar o código (e fizer observações) em pequenas seções, será mais fácil entender. Seus programas podem usar objetos de lista para acompanhar muitos tipos de item diferentes. Uma lista pode manter números, valores verdadeiro/falso, texto ou outros objetos. Você pode ter até mesmo um objeto de lista que mantém outros objetos de lista. Os itens em uma lista são chamados de elementos e cada lista mantém apenas um tipo de elemento. Desse modo, uma lista de números pode manter apenas números; não é possível adicionar texto a essa lista. Da mesma forma, não é possível adicionar número a uma lista de valores verdadeiro/falso.

     Quando você cria um objeto `List` usando uma declaração `new`, é preciso especificar o tipo de dados que deseja armazenar nele. É por esse motivo que a dica de ferramenta na parte superior da janela do **IntelliSense** mostra os tipos de elementos na lista. Além disso, isso é o que `List<string>` (no Visual C#) e `List(Of String)` (no Visual Basic) significam: é um objeto `List` que mantém elementos do tipo de dados `string`. Uma cadeia de caracteres é o que seu programa usa para armazenar texto, que é o que a dica de ferramenta à direita da janela do **IntelliSense** está informando a você.

4.  Considere por que, no Visual Basic, uma matriz temporária deve ser criada primeiro, mas, no Visual C#, a lista pode ser criada com uma declaração. Isso ocorre porque a linguagem do Visual C# tem *inicializadores de coleção*, que preparam a lista para aceitar valores. No Visual Basic, você pode usar um inicializador de coleção. No entanto, para compatibilidade com a versão anterior do Visual Basic, é recomendável usar o código anterior.

     Quando você usa um inicializador de coleção com uma instrução `new`, depois que o novo objeto de lista é criado, o programa o preenche com os dados fornecidos entre chaves. Nesse caso, você obtém uma lista de cadeias de caracteres denominadas ícones e essa lista será inicializada para que contenha dezesseis cadeias de caracteres. Cada uma dessas cadeias de caracteres é uma única letra e elas correspondem aos ícones que estarão nos rótulos. Desse modo, o jogo terá um par de pontos de exclamação, um par de letras N maiúsculas, um par de vírgulas, e assim por diante. (Quando esses caracteres são definidos para a fonte Webdings, eles aparecerão como símbolos, como um ônibus, uma bicicleta, uma aranha, e assim por diante.) Seu objeto de lista terá dezesseis cadeias de caracteres ao todo, uma para cada célula no painel TableLayoutPanel.

    > [!NOTE]
    >  No Visual Basic, você obtém o mesmo resultado, mas primeiro as cadeias de caracteres são colocadas em uma matriz temporária, que é então convertida em um objeto de lista. Uma matriz é semelhante a uma lista, exceto, por exemplo, as matrizes que são criadas com um tamanho fixo. As listas podem ser reduzidas e aumentadas, conforme a necessidade, que é importante nesse programa.

## <a name="to-continue-or-review"></a>Para continuar ou revisar

-   Para acessar a próxima etapa do tutorial, confira [Etapa 3: Atribuir um ícone aleatório a cada rótulo](../ide/step-3-assign-a-random-icon-to-each-label.md).

-   Para retornar à etapa anterior do tutorial, confira [Etapa 1: Criar um projeto e adicionar uma tabela ao formulário](../ide/step-1-create-a-project-and-add-a-table-to-your-form.md).
