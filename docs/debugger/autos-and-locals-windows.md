---
title: Inspecionar variáveis – Janelas automáticas e locais Microsoft Docs
ms.custom: seodec18
ms.date: 10/18/2018
ms.topic: how-to
f1_keywords:
- vs.debug.autos
- vs.debug.locals
helpviewer_keywords:
- debugger, variable windows
- debugging [Visual Studio], variable windows
ms.assetid: bb6291e1-596d-4af0-9f22-5fd713d6b84b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3ae67fadf5d9710f2088f47617b74eeeb8212826
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350739"
---
# <a name="inspect-variables-in-the-autos-and-locals-windows"></a>Inspecionar variáveis nas janelas automáticas e locais

O **Autos** e **Locals** windows mostram valores de variáveis durante a depuração. As janelas só estão disponíveis durante uma sessão de depuração. O **Autos** janela mostra as variáveis usadas em torno do ponto de interrupção atual. A janela **Locals** mostra as variáveis definidas no escopo local, que geralmente é o método ou a função atual. Se esta for a primeira vez que você tentou depurar o código, talvez você queira ler [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) e [ferramentas e técnicas de depuração antes de](../debugger/write-better-code-with-visual-studio.md) passar por este artigo.

 O **Autos** janela está disponível para C#, código do Visual Basic, C++ e Python, mas não para JavaScript ou F#.

Para abrir o **Autos** janela, durante a depuração, selecione **Debug** > **Windows** > **Autos**, ou pressione **Ctrl**+**Alt**+**V** > **um**.

Para abrir a janela **Locals**, durante a depuração, selecione **Debug** > **Windows** > **Locals**, ou pressione **Alt**+**4**.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para Visual Studio para Mac, consulte [visualizações de dados no Visual Studio para Mac](/visualstudio/mac/data-visualizations).

## <a name="use-the-autos-and-locals-windows"></a>Usar as janelas automáticas e locais

Matrizes e objetos mostram na **Autos** e **locais** windows como controles de árvore. Selecione a seta à esquerda de um nome de variável para expandir a exibição para mostrar campos e propriedades. Aqui está um exemplo de uma <xref:System.IO.FileStream?displayProperty=fullName> do objeto na janela **Locals**:

![Locais-FileStream](../debugger/media/locals-filestream.png "Locais-FileStream")

Um valor de vermelho na janela **Locals** ou **Autos** significa que o valor foi alterado desde a última avaliação. A alteração pode ser de uma sessão de depuração anterior ou porque você alterou o valor na janela.

O formato numérico padrão nas janelas do depurador é Decimal. Para alterá-la em hexadecimal, clique com botão direito na janela **Locals** ou **Autos** e selecione **exibição Hexadecimal**. Essa alteração afeta todas as janelas do depurador.

## <a name="edit-variable-values-in-the-autos-or-locals-window"></a>Editar valores de variáveis na janela automáticos ou locais

Para editar os valores da maioria das variáveis na **Autos** ou **Locals** windows, clique duas vezes o valor e digite o novo valor.

Você pode inserir uma expressão para um valor, por exemplo `a + b` . O depurador aceita mais expressões de linguagem válidas.

No código C++ nativo, talvez você precise qualificar o contexto de um nome de variável. Para obter mais informações, consulte [Context Operator (C++)](../debugger/context-operator-cpp.md).

>[!CAUTION]
>Certifique-se de entender as consequências antes de alterar valores e expressões. Alguns dos possíveis problemas são:
>
>- Avaliar algumas expressões pode alterar o valor de uma variável ou, de outra forma, afetar o estado do programa. Por exemplo, avaliar `var1 = ++var2` altera o valor de `var1` e `var2` . Essas expressões são consideradas como [efeitos colaterais](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)). Os efeitos colaterais podem causar resultados inesperados se você não estiver ciente deles.
>
>- Editar valores de ponto flutuante pode resultar em imprecisões secundárias devido à conversão decimal-binária de componentes fracionários. Até mesmo uma edição aparentemente inofensiva pode resultar em alterações em alguns dos bits na variável de ponto flutuante.

::: moniker range=">= vs-2019" 
## <a name="search-in-the-autos-or-locals-window"></a>Pesquisar na janela automáticos ou locais

Você pode pesquisar palavras-chave nas colunas nome, valor e tipo da janela **automáticos** ou **locais** usando a barra de pesquisa acima de cada janela. Pressione ENTER ou selecione uma das setas para executar uma pesquisa. Para cancelar uma pesquisa em andamento, selecione o ícone "x" na barra de pesquisa.

Use as setas para a esquerda e para a direita (Shift + F3 e F3, respectivamente) para navegar entre as correspondências encontradas.

![Pesquisar na janela locais](../debugger/media/ee-search-locals.png "Pesquisar na janela locais")

Para tornar sua pesquisa mais ou menos completa, use a lista suspensa de **pesquisa mais profunda** na parte superior da janela **automáticos** ou **locais** para selecionar quantos níveis de profundidade você deseja pesquisar em objetos aninhados. 

## <a name="pin-properties-in-the-autos-or-locals-window"></a>Propriedades de PIN na janela automáticos ou locais

> [!NOTE]
> Esse recurso tem suporte para o .NET Core 3,0 ou superior.

Você pode inspecionar rapidamente os objetos por suas propriedades nas janelas automáticos e locais com a ferramenta de **Propriedades fixas** .  Para usar essa ferramenta, focalize uma propriedade e selecione o ícone de pino que aparece ou clique com o botão direito do mouse e selecione a opção **fixar membro como favorito** no menu de contexto resultante.  Isso faz com que essa propriedade apareça na parte superior da lista de propriedades do objeto e o nome e o valor da propriedade são exibidos na coluna **valor** .  Para Desafixar uma propriedade, selecione o ícone de fixação novamente ou selecione a opção **Desafixar membro como favorito** no menu de contexto.

![Propriedades de PIN na janela locais](../debugger/media/basic-pin.gif "Propriedades de PIN na janela locais")

Você também pode alternar os nomes de propriedade e filtrar as propriedades não fixadas ao exibir a lista de propriedades do objeto nas janelas automáticas ou locais.  Você pode acessar cada opção selecionando os botões na barra de ferramentas acima das janelas automáticas ou locais.

![Filtrar propriedades favoritas](../debugger/media/filter-pinned-properties-locals.png "Filtrar propriedades favoritas") 
 ![Alternar nomes de propriedade](../debugger/media/toggle-property-names.gif "Alternar nomes de propriedade")

::: moniker-end

## <a name="change-the-context-for-the-autos-or-locals-window"></a>Alterar o contexto para a janela automáticos ou locais

Você pode usar a barra de ferramentas **Local de Depuração** para selecionar uma função desejada, thread ou processo, que altera o contexto para as janelas **Autos** e **Locals**.

Para habilitar a barra de ferramentas **local de depuração**, clique em uma parte vazia da área da barra de ferramentas e selecione **local de depuração** da lista suspensa ou selecione **exibição** > **Barras de ferramentas** > **local de depuração**.

Definir um ponto de interrupção e iniciar a depuração. Quando o ponto de interrupção é atingido, a execução para e você pode ver o local na barra de ferramentas **local de depuração**.

![Barra de ferramentas do local de depuração](../debugger/media/debuglocationtoolbar.png "Depurar barra de ferramentas de local")

## <a name="variables-in-the-autos-window-c-c-visual-basic-python"></a><a name="bkmk_whatvariables"></a>Variáveis na janela Autos (C#, C++, Visual Basic, Python)

Linguagens de código diferentes exibem variáveis diferentes nos **Autos** janela.

- No C# e Visual Basic, a janela **Autos** exibirá qualquer variável usada na linha atual ou anterior. Por exemplo, em C# ou Visual Basic código, declare as quatro variáveis a seguir:

   ```csharp
       public static void Main()
       {
          int a, b, c, d;
          a = 1;
          b = 2;
          c = 3;
          d = 4;
       }
   ```

   Defina um ponto de interrupção na linha `c = 3;` e inicie o depurador. Quando a execução pausa, o **Autos** janela será exibida:

   ![Auto-CSharp](../debugger/media/autos-csharp.png "Auto-CSharp")

   O valor de `c` é 0, porque a linha `c = 3` ainda não foi executada.

- No C++, o **Autos** janela exibe as variáveis usadas em pelo menos três linhas antes da linha atual em que a execução está em pausa. Por exemplo, no código C++, declare seis variáveis:

   ```C++
       void main() {
           int a, b, c, d, e, f;
           a = 1;
           b = 2;
           c = 3;
           d = 4;
           e = 5;
           f = 6;
       }
   ```

    Defina um ponto de interrupção na linha `e = 5;` e execute o depurador. Quando a execução for interrompida, o **Autos** janela será exibida:

    ![Auto-C + +](../debugger/media/autos-cplus.png "Auto-C + +")

    A variável `e` não foi inicializada, pois a linha `e = 5` ainda não foi executada.

## <a name="view-return-values-of-method-calls"></a><a name="bkmk_returnValue"></a>Exibir valores de retorno de chamadas de método
 No código .NET e C++, você pode examinar os valores de retorno na **Autos** janela ao passar sobre ou fora de uma chamada de método. Pode ser útil exibir valores de retornor de chamadas de método quando eles não são armazenados em variáveis locais. Um método pode ser usado como um parâmetro ou como o valor retornado de outro método.

 Por exemplo, o seguinte código C# adiciona os valores de retorno de duas funções:

```csharp
static void Main(string[] args)
{
    int a, b, c, d;
    a = 1;
    b = 2;
    c = 3;
    d = 4;
    int x = sumVars(a, b) + subtractVars(c, d);
}

private static int sumVars(int i, int j)
{
    return i + j;
}

private static int subtractVars(int i, int j)
{
    return j - i;
}
```

Para ver os valores de retorno das `sumVars()` `subtractVars()` chamadas de método e na janela de automóveis:

1. Defina um ponto de interrupção na linha `int x = sumVars(a, b) + subtractVars(c, d);`.

1. Inicie a depuração e, quando a execução parar no ponto de interrupção, selecione **Step Over** ou pressione **F10**. Você deve ver os seguintes valores de retornados na **Autos** janela:

  ![Valor de retorno automático C #](../debugger/media/autosreturnvaluecsharp2.png "Valor de retorno automático C #")

## <a name="see-also"></a>Veja também

- [O que é depuração?](../debugger/what-is-debugging.md)
- [Técnicas e ferramentas de depuração](../debugger/write-better-code-with-visual-studio.md)
- [Primeira olhada na depuração](../debugger/debugger-feature-tour.md)
- [Janelas do depurador](../debugger/debugger-windows.md)
