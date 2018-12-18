---
title: Definir uma inspeção nas variáveis | Microsoft Docs
ms.custom: seodec18
ms.date: 10/11/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 898c79f3985e24f52620f12dc25ad6044d05ac64
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53059477"
---
# <a name="watch-variables-with-watch-windows-and-quickwatch"></a>Assista a variáveis com janelas de inspeção e QuickWatch 

Enquanto você estiver depurando, você pode usar **Watch** windows e **QuickWatch** para inspecionar variáveis e expressões. Os windows estão disponíveis somente durante uma sessão de depuração.

**Assista** windows podem exibir diversas variáveis de cada vez durante a depuração. O **QuickWatch** caixa de diálogo exibe uma única variável por vez e deve ser fechada antes de depuração de continuar.

Se essa for a primeira vez que você tentou depurar o código, você talvez queira ler [corrigir bugs, escrevendo melhor C# código](../debugger/write-better-code-with-visual-studio.md) e [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) antes de prosseguir com este artigo.

## <a name="observe-variables-with-a-watch-window"></a>Observe as variáveis com uma janela Inspeção

Você pode abrir mais de um **Watch** janela e observar mais de uma variável em uma **inspeção** janela. 

Por exemplo, para definir os valores de um observador `a`, `b`, e `c` no código a seguir:

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

1. Defina um ponto de interrupção a `c = a + b;` linha clicando na margem esquerda, selecionando **Debug** > **alternar ponto de interrupção**, ou pressionando **F9**.
   
1. Iniciar a depuração, selecionando o verde **inicie** seta ou **Debug** > **iniciar depuração**, ou pressione **F5**. A execução pausa no ponto de interrupção.
   
1. Abra uma **Watch** janela selecionando **depurar** > **Windows** > **inspeção**  >   **Assista a 1**, ou pressionando **Ctrl**+**Alt**+**W** > **1**.
   
   Você pode abrir adicionais **Watch** windows selecionando windows **2**, **3**, ou **4**.
   
1. No **Watch** janela, selecione uma linha vazia e variável de tipo `a`. Faça o mesmo para `b` e `c`.
   
   ![Assista a variáveis](../debugger/media/watchvariables.png "WatchVariables")
   
1. Continuar a depuração, selecionando **Debug** > **intervir** ou pressionando **F11** conforme necessário para Avançar. Os valores da variável na **Watch** janela alterar como você itera através de `for` loop.
   
>[!NOTE]
>Para C++ 
>- Talvez você precise qualificar o contexto de um nome de variável ou uma expressão que usa um nome de variável. O contexto é a função, arquivo de origem ou módulo onde se encontra uma variável. Se você tiver qualificar o contexto, use o [operador de contexto (C++)](../debugger/context-operator-cpp.md) sintaxe na **nome** no **Assista** janela. 
>  
>- Você pode adicionar nomes de registro e nomes de variáveis usando  **$ \<registrar&nbsp;nome >** ou  **@ \<registrar&nbsp;nome >** para o **nome** no **inspeção** janela. Para obter mais informações, consulte [pseudovariáveis](../debugger/pseudovariables.md).

## <a name="use-expressions-in-a-watch-window"></a>Usar expressões em uma janela Inspeção

Você pode observar qualquer expressão válida reconhecida pelo depurador em um **inspeção** janela.

Por exemplo, para o código na seção anterior, você pode obter a média dos três valores, digitando `(a + b + c) / 3` no **inspeção** janela:

![Expressão de inspeção](../debugger/media/watchexpression.png "expressão de inspeção")

As regras para avaliar expressões na **inspeção** janela geralmente são as mesmas regras de avaliação de expressões na linguagem de código. Se a expressão não tem um erro de sintaxe, esperar que o erro do compilador mesmo como no editor de códigos. Por exemplo, um erro de digitação na expressão anterior gera esse erro no **inspeção** janela:

![Assista a erro de expressão](../debugger/media/watchexpressionerror.png "assistir o erro de expressão")

Um círculo com ícone de duas linhas onduladas pode aparecer na **inspeção** janela. Este ícone significa que o depurador não avalia a expressão devido à dependência potencial entre threads. Avaliar o código requer outros threads no seu aplicativo seja executado temporariamente, mas como você está no modo de interrupção, todos os threads em seu aplicativo geralmente são interrompidos. Permitir que outros threads sejam executados temporariamente pode ter efeitos inesperados no estado do seu aplicativo e o depurador podem ignorar eventos como pontos de interrupção e exceções nesses threads.

### <a name="bkmk_refreshWatch"></a> Atualizar valores de inspeção

Um ícone de atualização (seta circular) pode aparecer na **inspeção** janela quando uma expressão é avaliada. O ícone de atualização indica um erro ou um valor que está desatualizado. 

Para atualizar o valor, selecione o ícone de atualização, ou pressione a barra de espaços. O depurador tenta reavaliar a expressão. No entanto, não pode desejar ou conseguir reavaliar a expressão, dependendo por que o valor não foi avaliado. 

Passe o mouse sobre o ícone de atualização ou consulte os **valor** coluna para o motivo pelo qual a expressão não foi avaliada. Os motivos incluem:

- Ocorreu um erro como a expressão estava sendo avaliada, como no exemplo anterior. Um tempo limite pode ocorrer ou uma variável pode estar fora do escopo.
  
- A expressão tem uma chamada de função que pode disparar um efeito colateral no aplicativo. Ver [efeitos colaterais de expressão](#bkmk_sideEffects).
  
- A avaliação automática de propriedades e chamadas de função implícitas é desativada. 
  
Se o ícone de atualização é exibida porque a avaliação automática de propriedades e chamadas de função implícitas é desativada, você pode habilitá-la selecionando **habilitar a avaliação de propriedade e outras chamadas de função implícitas** em **ferramentas**   >  **Opções** > **depuração** > **geral**.

Para demonstrar o uso o ícone de atualização:

1. Na **ferramentas** > **opções** > **depuração** > **geral**, desmarque o **Habilitar a avaliação de propriedade e outras chamadas de função implícitas** caixa de seleção. 
   
1. Insira o código a seguir e, na **Watch** janela, definir uma inspeção no `list.Count` propriedade. 
   
   ```csharp
   static void Main(string[] args)
   {
       List<string> list = new List<string>();
       list.Add("hello");
       list.Add("goodbye");
   }
   ```
   
1. Inicie a depuração. O **inspeção** janela mostra algo parecido com a seguinte mensagem:
   
   ![Atualizar Watch](../debugger/media/refreshwatch.png "atualizar Watch")
   
1. Para atualizar o valor, selecione o ícone de atualização, ou pressione a barra de espaços. O depurador reavalia a expressão. 

### <a name="bkmk_sideEffects"></a> Efeitos colaterais de expressão 

Avaliar algumas expressões pode alterar o valor de uma variável ou afetar o estado do seu aplicativo. Por exemplo, avaliar a expressão a seguir altera o valor de `var1`:

```csharp
var1 = var2
```

Esse código pode causar uma [efeito colateral](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)). Efeitos colaterais podem dificultar a depuração mais alterando a maneira como o aplicativo funciona.

Uma expressão com efeitos colaterais é avaliada apenas uma vez, quando você primeiro inseri-la. Depois disso, a expressão será exibido em cinza na **inspeção** janela e ainda mais as avaliações são desabilitados. A dica de ferramenta ou **valor** coluna explica que a expressão causa um efeito colateral. Você pode forçar a reavaliação selecionando o ícone de atualização que aparece ao lado do valor.

Uma maneira de impedir a designação de efeitos colaterais é desativar a avaliação automática de funções. Na **ferramentas** > **opções** > **depuração** > **geral**, cancele a seleção de **Habilitar a avaliação de propriedade e outras chamadas de função implícitas**.

Para C# apenas, quando a avaliação de propriedades ou chamadas de função implícitas é desativada, você pode forçar a avaliação, adicionando o **CA** modificador de formato para uma variável **nome** no **Watch**  janela. Ver [Formatar especificadores em C# ](../debugger/format-specifiers-in-csharp.md).

## <a name="bkmk_objectIds"></a> Usar IDs de objeto na janela de inspeção (C# e Visual Basic)

Às vezes você deseja observar o comportamento de um objeto específico. Por exemplo, você talvez queira controlar um objeto referenciado por uma variável local depois que essa variável tiver saído do escopo. No C# e Visual Basic, você pode criar IDs de objeto para instâncias específicas de tipos de referência e usá-los na **inspeção** janela e, em condições de ponto de interrupção. A ID de objeto é gerada pelo common language runtime (CLR) serviços de depuração e associada ao objeto.

> [!NOTE]
> IDs de objeto criar referências fracas que não impedem que o objeto que está sendo coletado como lixo. Eles só são válidos para a sessão de depuração atual.

No código a seguir, o `MakePerson()` método cria um `Person` usando uma variável local: 

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

Para descobrir o nome da `Person` no `DoSomething()` método, você pode adicionar uma referência para o `Person` ID de objeto no **inspeção** janela.

1. Defina um ponto de interrupção no código após o `Person` objeto foi criado.
   
1. Inicie a depuração.
   
1. Quando a execução pausa no ponto de interrupção, abra o **Locals** janela escolhendo **Debug** > **Windows** > **locais**.
   
1. No **Locals** janela, com o botão direito do `Person` variável e selecione **criar ID de objeto**.
   
   Você verá um sinal de cifrão (**$**) e a um número no **locais** janela, que é a ID de objeto.
   
1. Adicione a ID de objeto para o **Watch** janela clicando duas vezes a ID de objeto e selecionando **Adicionar inspeção**.
   
1. Definir outro ponto de interrupção no `DoSomething()` método.
   
1. Continue a depuração. Quando a execução pausa na `DoSomething()` método, o **inspeção** janela exibe o `Person` objeto.
   
   > [!NOTE]
   > Se você deseja ver as propriedades do objeto, como `Person.Name`, você deve habilitar a avaliação da propriedade, selecionando **ferramentas** > **opções**  >   **Depurando** > **gerais** > **habilitar avaliação de propriedade e outras chamadas de função implícitas**.

## <a name="dynamic-view-and-the-watch-window"></a>Modo de exibição dinâmico e a janela Inspeção

Algumas linguagens de script (por exemplo, Python ou JavaScript) usam dinâmico ou [pato](https://en.wikipedia.org/wiki/Duck_typing) digitando e .NET versão 4.0 e posterior dá suporte a objetos que são difíceis de observar em janelas de depuração normais.

O **Watch** janela exibe esses objetos como objetos dinâmicos, que são criados a partir de tipos que implementam o <xref:System.Dynamic.IDynamicMetaObjectProvider> interface. Nós de objeto dinâmico mostram os membros dinâmicos dos objetos dinâmicos, mas não permitem a edição dos valores de membro. 

Para atualizar **modo de exibição dinâmico** valores, selecionadas o [ícone atualizar](#bkmk_refreshWatch) ao lado do nó de objeto dinâmico. 

Para exibir apenas o **modo de exibição dinâmico** para um objeto, adicione uma **dinâmico** especificador de formato após o nome de objeto dinâmico na **Assista** janela:

- Para C#: `ObjectName, dynamic`
- Para o Visual Basic: `$dynamic, ObjectName`

>[!NOTE]
>- O C# depurador não reavalia automaticamente os valores de **modo de exibição dinâmico** quando você entrar para a próxima linha de código. 
>- O depurador do Visual Basic é atualizada automaticamente expressões adicionadas por meio de **modo de exibição dinâmico**.
>- A avaliação dos membros de um **Modo de Exibição Dinâmico** pode ter [efeitos colaterais](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)). 

**Para inserir uma nova inspeção variável que converte um objeto em um objeto dinâmico:**
  
1. Clique com botão direito qualquer filho de um **modo de exibição dinâmico**.
1. Escolher **Adicionar inspeção**. O `object.name` se torna `((dynamic) object).name` e é exibido em uma nova **inspeção** janela.

O depurador também adiciona uma **modo de exibição dinâmico** nó filho do objeto para o **Autos** janela. Para abrir o **automóveis** janela, durante a depuração, selecione **Debug** > **Windows** > **Autos**. 

**Modo de exibição dinâmico** também melhora a depuração para objetos COM. Quando o depurador chega a um objeto COM encapsulado em **ComObject**, ele adiciona um **modo de exibição dinâmico** nó do objeto.

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

Para observar o `a` variável, 
   
1. Defina um ponto de interrupção a `a = a + b;` linha.
   
1. Inicie a depuração. A execução pausa no ponto de interrupção.
   
1. Selecione a variável `a` no código.
   
1. Selecione **Debug** > **QuickWatch**, pressione **Shift**+**F9**, ou clique com botão direito e selecione **QuickWatch**. 
   
   O **QuickWatch** caixa de diálogo é exibida. O `a` variável está no **expressão** caixa com um **valor** de **1**.
   
   ![Variável QuickWatch](../debugger/media/quickwatchvariable.png "variável QuickWatch")
   
1. Para avaliar uma expressão usando a variável, digite uma expressão como `a + b` no **expressão** caixa e selecione **reavaliar**.
   
   ![Expressão QuickWatch](../debugger/media/quickwatchexpression.png "expressão QuickWatch")
   
1. Para adicionar a variável ou expressão de **QuickWatch** para o **inspeção** janela, selecione **Adicionar inspeção**.
   
1. Selecione **feche** para fechar o **QuickWatch** janela. (**QuickWatch** é uma caixa de diálogo modal, portanto, você não pode continuar a depuração, desde que ele está aberto.)
   
1. Continue a depuração. Você pode observar a variável na **inspeção** janela.

## <a name="see-also"></a>Consulte também
 [O que é depuração?](../debugger/what-is-debugging.md)  
 [Corrigir bugs escrevendo um melhor código C#](../debugger/write-better-code-with-visual-studio.md)  
 [Introdução à depuração](../debugger/debugger-feature-tour.md) [janelas do depurador](../debugger/debugger-windows.md)
