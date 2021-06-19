---
title: Definir um relógio em variáveis | Microsoft Docs
description: Enquanto você depura, consulte variáveis e expressões em Watch e QuickWatch. A observação pode exibir várias variáveis, QuickWatch apenas uma e apenas enquanto estiver em pausa.
ms.custom: SEO-VS-2020
ms.date: 10/11/2018
ms.topic: how-to
f1_keywords:
- vs.debug.watch
helpviewer_keywords:
- debugging [Visual Studio], Watch window
- expressions [debugger], evaluating
- variables [debugger], evaluating
- expression evaluation
- registers, evaluating
- debugging [Visual Studio], expression evaluation
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 192a11a028c297dc2c642e65982a978f7b5596a7
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385013"
---
# <a name="watch-variables-with-watch-windows-and-quickwatch"></a>Observar variáveis com Janelas de observação e QuickWatch

Durante a depuração, você pode usar As janelas **Watch** e **QuickWatch** para observar variáveis e expressões. As janelas só estão disponíveis durante uma sessão de depuração.

**As** janelas de relógio podem exibir várias variáveis por vez durante a depuração. A **caixa de diálogo QuickWatch** exibe uma única variável por vez e deve ser fechada antes que a depuração possa continuar.

> [!NOTE]
> Se esta for a primeira vez que você tentou depurar o código, talvez você queira ler Depuração para [iniciantes absolutos](../debugger/debugging-absolute-beginners.md) e técnicas e ferramentas de [depuração](../debugger/write-better-code-with-visual-studio.md) antes de passar por este artigo.

## <a name="observe-variables-with-a-watch-window"></a>Observar variáveis com um janela Inspeção

Você pode abrir mais de uma **janela De** observação e observar mais de uma variável em uma **janela** De observação.

Por exemplo, para definir um relógio nos valores `a` de , e no código a `b` `c` seguir:

```C++
int main()
{
    int a, b, c;
    a = 1;
    b = 2;
    c = 0;

    for (int i = 0; i < 10; i++)
    {
        a++;
        b *= 2;
        c = a + b;
    }

    return 0;
}

```

1. De definir um ponto de interrupção na linha clicando na margem esquerda, selecionando Depurar Alternar Ponto de Interrupção `c = a + b;`   >  ou pressionando **F9**.

1. Inicie a depuração selecionando a seta **verde Iniciar** ou **Depurar**  >  **Iniciar Depuração** ou pressione **F5**. A execução pausa no ponto de interrupção.

1. Abra uma **janela** Observar selecionando **Depurar**  >  **o Windows**  >  **Watch**  >  **Watch 1** ou pressionando **Ctrl** + **Alt** + **W**  >  **1**.

   Você pode abrir janelas **de** relógio adicionais selecionando windows **2,** **3** ou **4.**

1. Na janela **Observar,** selecione uma linha vazia e digite a variável `a` . Faça o mesmo para `b` e `c` .

   ![Observar variáveis](../debugger/media/watchvariables.png "WatchVariables")

1. Continue a depuração selecionando **Depurar**  >  **Entrar** ou pressionando **F11** conforme necessário para avançar. Os valores de variáveis na **janela** De assistir mudam conforme você itera pelo `for` loop.

>[!NOTE]
>Somente para C++,
>- Talvez seja necessário qualificar o contexto de um nome de variável ou uma expressão que usa um nome de variável. O contexto é a função, o arquivo de origem ou o módulo em que uma variável está localizada. Se você tiver que qualificar o contexto, use a sintaxe do operador [de contexto (C++)](../debugger/context-operator-cpp.md) **no Nome** **na** janela Observar.
>
>- Você pode adicionar nomes de registro e nomes de variáveis **$\<register&nbsp;name>** usando ou ao **@\<register&nbsp;name>** **Nome** na **janela** Observar. Para obter mais informações, consulte [Pseudovariáveis.](../debugger/pseudovariables.md)

## <a name="use-expressions-in-a-watch-window"></a>Usar expressões em um janela Inspeção

Você pode observar qualquer expressão válida reconhecida pelo depurador em uma **janela** De observação.

Por exemplo, para o código na seção anterior, você pode obter a média dos três valores inserindo `(a + b + c) / 3` na **janela** Observar:

![Expressão watch](../debugger/media/watchexpression.png "Expressão de inspeção")

As regras para avaliar expressões na **janela** Observar geralmente são as mesmas que as regras para avaliar expressões na linguagem de código. Se uma expressão tiver um erro de sintaxe, espere o mesmo erro do compilador que no editor de códigos. Por exemplo, um erro de digitação na expressão anterior produz esse erro na **janela** Observar:

![Erro de expressão de relógio](../debugger/media/watchexpressionerror.png "Erro de expressão de inspeção")

Um círculo com dois ícones de linhas onduladas pode aparecer na **janela** Observar. Esse ícone significa que o depurador não avalia a expressão devido a uma possível dependência entre threads. A avaliação do código exige que outros threads em seu aplicativo sejam executados temporariamente, mas como você está no modo de quebra, todos os threads em seu aplicativo geralmente são interrompidos. Permitir que outros threads executem temporariamente pode ter efeitos inesperados sobre o estado do seu aplicativo, e o depurador pode ignorar eventos como pontos de interrupção e exceções nesses threads.

::: moniker range=">= vs-2019" 
## <a name="search-in-the-watch-window"></a>Pesquisar no janela Inspeção

Você pode pesquisar palavras-chave nas colunas Nome,  Valor e Tipo da janela Observar usando a barra de pesquisa acima de cada janela. Clique em ENTER ou selecione uma das setas para executar uma pesquisa. Para cancelar uma pesquisa em andamento, selecione o ícone "x" na barra de pesquisa.

Use as setas esquerda e direita (Shift+F3 e F3, respectivamente) para navegar entre as correspondeções encontradas.

![Pesquisar na janela Observar](../debugger/media/ee-search-watch.png "Pesquisar na janela de inspeção")

Para tornar sua pesquisa mais ou menos completa, use o  **menu** suspenso Pesquisar mais profundamente na parte superior da janela Observar para selecionar quantos níveis você deseja pesquisar em objetos aninhados. 

## <a name="pin-properties-in-the-watch-window"></a>Fixar propriedades no janela Inspeção

>[!NOTE]
> Esse recurso tem suporte no .NET Core 3.0 ou superior.

Você pode inspecionar rapidamente objetos por suas propriedades no janela Inspeção com a **ferramenta Propriedades Pinnáveis.**  Para usar essa ferramenta, passe o mouse sobre uma propriedade e selecione o ícone de pino que aparece ou clique com o botão direito do mouse e selecione a opção Fixar **Membro** como Favorito no menu de contexto resultante.  Isso esbulha essa propriedade na parte superior da lista de propriedades do objeto e o nome e o valor da propriedade são exibidos na **coluna** Valor.  Para desempinar uma propriedade, selecione o ícone de pino novamente ou selecione a opção **Unpin Member as Favorite** no menu de contexto.

![Fixar propriedades no janela Inspeção](../debugger/media/basic-pin-watch.gif "Propriedades de PIN no janela Inspeção")

Você também pode alternar nomes de propriedade e filtrar propriedades não fixadas ao exibir a lista de propriedades do objeto no janela Inspeção.  Você pode acessar as duas opções selecionando os botões na barra de ferramentas acima da janela de relógio.

::: moniker-end

### <a name="refresh-watch-values"></a><a name="bkmk_refreshWatch"></a> Atualizar valores de relógio

Um ícone de atualização (seta circular) pode aparecer **na** janela Observar quando uma expressão é avaliada. O ícone de atualização indica um erro ou um valor que está des date.

Para atualizar o valor, selecione o ícone de atualização ou pressione a barra de espaços. O depurador tenta reavaliar a expressão. No entanto, talvez você não queira ou possa reavaliar a expressão, dependendo do motivo pelo qual o valor não foi avaliado.

Passe o mouse sobre o ícone de atualização ou veja **a coluna** Valor pelo motivo pelo qual a expressão não foi avaliada. Os motivos incluem:

- Ocorreu um erro quando a expressão estava sendo avaliada, como no exemplo anterior. Um tempoout pode ocorrer ou uma variável pode estar fora do escopo.

- A expressão tem uma chamada de função que pode disparar um efeito colateral no aplicativo. Consulte [Efeitos colaterais da expressão](#bkmk_sideEffects).

- A avaliação automática de propriedades e chamadas de função implícitas está desabilitada.

Se o ícone de atualização aparecer porque a avaliação automática de  propriedades e chamadas de função implícitas está desabilitada, você poderá habilita-lo selecionando Habilitar avaliação de propriedade e outras chamadas de função implícitas em Opções de Ferramentas  >    >  **Depuração**  >  **Geral.**

Para demonstrar o uso do ícone de atualização:

1. Em **Opções de**  >  **Ferramentas**  >  **Depurando**  >  **Geral**, des marque a caixa de seleção **Habilitar avaliação** de propriedade e outras chamadas de função implícitas.

1. Insira o código a seguir e, **na** janela Observar, de definir um relógio na `list.Count` propriedade .

   ```csharp
   static void Main(string[] args)
   {
       List<string> list = new List<string>();
       list.Add("hello");
       list.Add("goodbye");
   }
   ```

1. Inicie a depuração. A **janela** Observar mostra algo parecido com a seguinte mensagem:

   ![Atualizar Relógio](../debugger/media/refreshwatch.png "Atualizar inspeção")

1. Para atualizar o valor, selecione o ícone de atualização ou pressione a barra de espaços. O depurador reavalia a expressão.

### <a name="expression-side-effects"></a><a name="bkmk_sideEffects"></a> Efeitos colaterais da expressão

Avaliar algumas expressões pode alterar o valor de uma variável ou afetar o estado do aplicativo. Por exemplo, avaliar a expressão a seguir altera o valor de `var1`:

```csharp
var1 = var2
```

Esse código pode causar um [efeito colateral](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)). Os efeitos colaterais podem dificultar a depuração alterando a maneira como seu aplicativo opera.

Uma expressão com efeitos colaterais é avaliada apenas uma vez, quando você a ins insinte pela primeira vez. Depois disso, a expressão aparece es cinza na **janela** Observar e avaliações posteriores são desabilitadas. A dica de ferramenta ou **a coluna Valor** explica que a expressão causa um efeito colateral. Você pode forçar a reavaliação selecionando o ícone de atualização que aparece ao lado do valor.

Uma maneira de evitar a designação de efeitos colaterais é desativar a avaliação automática da função. Em **Opções de**  >  **Ferramentas**  >  **Depurando**  >  **Geral**, desmarque Habilitar avaliação de propriedade e outras chamadas de função **implícitas**.

Somente para C#, quando a avaliação de propriedades ou chamadas de função implícitas é desligada, você pode forçar a avaliação adicionando o modificador de formato **ac** a uma variável **Nome** na **janela** Relógio. Consulte [Especificadores de formato em C#.](../debugger/format-specifiers-in-csharp.md)

## <a name="use-object-ids-in-the-watch-window-c-and-visual-basic"></a><a name="bkmk_objectIds"></a> Usar IDs de objeto no janela Inspeção (C# e Visual Basic)

Às vezes, você deseja observar o comportamento de um objeto específico. Por exemplo, talvez você queira acompanhar um objeto referenciado por uma variável local depois que essa variável sair do escopo. No C# e no Visual Basic, você pode criar IDs de objeto para instâncias específicas de tipos de referência e usá-las na janela Observar e em condições de ponto de interrupção.  A ID do Objeto é gerada pelos serviços de depuração do CLR (Common Language Runtime) e associada ao objeto .

> [!NOTE]
> As IDs de objeto criam referências fracas que não impedem que o objeto seja coletado como lixo. Eles são válidos apenas para a sessão de depuração atual.

No código a seguir, o `MakePerson()` método cria um usando uma `Person` variável local:

```csharp
class Person
{
    public Person(string name)
    {
        Name = name;
    }
    public string Name { get; set; }
}

public class Program
{
    static List<Person> _people = new List<Person>();
    public static void Main(string[] args)
    {
        MakePerson();
        DoSomething();
    }

    private static void MakePerson()
    {
        var p = new Person("Bob");
        _people.Add(p);
    }

    private static void DoSomething()
    {
        // more processing
         Console.WriteLine("done");
    }
}
```

Para descobrir o nome do no método , você pode adicionar uma referência à `Person` `DoSomething()` `Person` ID do Objeto na **janela** De assistir.

1. Defina um ponto de interrupção no código depois que o `Person` objeto tiver sido criado.

1. Inicie a depuração.

1. Quando a execução pausa no ponto de interrupção, abra a janela **locais** escolhendo **depurar**  >    >  **locais** do Windows.

1. Na janela **locais** , clique com o botão direito do mouse na `Person` variável e selecione **criar ID de objeto**.

   Você deve ver um sinal de cifrão ( **$** ) mais um número na janela **locais** , que é a ID do objeto.

1. Adicione a ID de objeto à janela de **inspeção** clicando com o botão direito do mouse na ID do objeto e selecionando **Adicionar inspeção**.

1. Defina outro ponto de interrupção no `DoSomething()` método.

1. Continue a depuração. Quando a execução pausa no `DoSomething()` método, a janela de **Observação** exibe o `Person` objeto.

   > [!NOTE]
   > Se você quiser ver as propriedades do objeto, como `Person.Name` , você deve habilitar a avaliação de propriedade selecionando **ferramentas**  >  **Opções**  >  **depuração**  >  **geral**  >  **habilitar avaliação de propriedade e outras chamadas de função implícitas**.

## <a name="dynamic-view-and-the-watch-window"></a>Exibição dinâmica e o janela Inspeção

Algumas linguagens de script (por exemplo, JavaScript ou Python) usam digitação dinâmica ou [pato](https://en.wikipedia.org/wiki/Duck_typing) , e o .net versão 4,0 e posterior dá suporte a objetos que são difíceis de observar nas janelas de depuração normais.

A janela **Watch** exibe esses objetos como objetos dinâmicos, que são criados a partir de tipos que implementam a <xref:System.Dynamic.IDynamicMetaObjectProvider> interface. Nós de objetos dinâmicos mostram os membros dinâmicos dos objetos dinâmicos, mas não permitem a edição dos valores de membro.

Para atualizar os valores de **exibição dinâmica** , selecione o [ícone de atualização](#bkmk_refreshWatch) ao lado do nó de objeto dinâmico.

Para exibir apenas a **exibição dinâmica** de um objeto, adicione um especificador de formato **dinâmico** após o nome do objeto dinâmico na janela **Watch** :

- Para C#: `ObjectName, dynamic`
- Para o Visual Basic: `$dynamic, ObjectName`

>[!NOTE]
>- O depurador C# não reavalia automaticamente os valores na **exibição dinâmica** quando você passar para a próxima linha de código.
>- O depurador de Visual Basic atualiza automaticamente as expressões adicionadas por meio da **exibição dinâmica**.
>- A avaliação dos membros de um **Modo de Exibição Dinâmico** pode ter [efeitos colaterais](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)).

**Para inserir uma nova variável Watch que converte um objeto em um objeto dinâmico:**

1. Clique com o botão direito do mouse em qualquer filho de uma **exibição dinâmica**.
1. Escolha **Adicionar inspeção**. O `object.name` se torna `((dynamic) object).name` e aparece em uma nova janela **Watch** .

O depurador também adiciona um nó filho da **exibição dinâmica** do objeto à janela de **automóveis** . Para abrir a janela **automáticos** durante a depuração, selecione **depurar**  >    >  **automáticos** do Windows.

A **exibição dinâmica** também aprimora a depuração de objetos com. Quando o depurador chega a um objeto COM encapsulado em **System.__ComObject**, ele adiciona um nó de **exibição dinâmica** para o objeto.

## <a name="observe-a-single-variable-or-expression-with-quickwatch"></a>Observar uma única variável ou expressão com QuickWatch

Você pode usar **QuickWatch** para observar uma única variável.

Por exemplo, para o código a seguir:

```csharp
static void Main(string[] args)
{
    int a, b;
    a = 1;
    b = 2;
    for (int i = 0; i < 10; i++)
    {
        a = a + b;
    }
}
```

Para observar a `a` variável,

1. Defina um ponto de interrupção na linha `a = a + b;`.

1. Inicie a depuração. A execução pausa no ponto de interrupção.

1. Selecione a variável `a` no código.

1. Selecione **depurar**  >  **QuickWatch**, pressione **Shift** + **F9** ou clique com o botão direito do mouse e selecione **QuickWatch**.

   A caixa de diálogo **QuickWatch** é exibida. A `a` variável está na caixa de **expressão** com um **valor** de **1**.

   ![Variável QuickWatch](../debugger/media/quickwatchvariable.png "Variável QuickWatch")

1. Para avaliar uma expressão usando a variável, digite uma expressão como `a + b` na caixa **expressão** e selecione **reavaliar**.

   ![Expressão QuickWatch](../debugger/media/quickwatchexpression.png "Expressão QuickWatch")

1. Para adicionar a variável ou expressão do **QuickWatch** à janela de **inspeção** , selecione **Adicionar inspeção**.

1. Selecione **fechar** para fechar a janela **QuickWatch** . (**QuickWatch** é uma caixa de diálogo modal, portanto, você não pode continuar a depuração enquanto estiver aberta.)

1. Continue a depuração. Você pode observar a variável na janela **Watch** .

## <a name="see-also"></a>Confira também
- [O que é depuração?](../debugger/what-is-debugging.md)
- [Técnicas e ferramentas de depuração](../debugger/write-better-code-with-visual-studio.md)
- [Primeira olhada na depuração](../debugger/debugger-feature-tour.md)
- [Janelas do depurador](../debugger/debugger-windows.md)
