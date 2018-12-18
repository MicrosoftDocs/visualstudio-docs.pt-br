---
title: Inspeção e QuickWatch Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.watch
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], Watch window
- expressions [debugger], evaluating
- variables [debugger], evaluating
- expression evaluation
- registers, evaluating
- debugging [Visual Studio], expression evaluation
ms.assetid: d5c18377-2a0e-4819-a645-407e24ccc58c
caps.latest.revision: 50
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b171352475b6c0b3bc916d27ab4ba351e84be42b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791664"
---
# <a name="watch-and-quickwatch-windows"></a>Inspeção e QuickWatch Windows
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o **Watch** (**depurar / Windows / Assista / assistir (1, 2, 3 e 4)**) e **QuickWatch** (com o botão direito na variável / **depurar / QuickWatch**) windows para inspecionar variáveis e expressões durante uma sessão de depuração.  A diferença é que o **Watch** janela pode exibir diversas variáveis, enquanto o **QuickWatch** janela exibe uma única variável por vez.  
  
## <a name="observing-a-single-variable-with-quickwatch"></a>Observar uma única variável com QuickWatch  
 Você pode usar o **QuickWatch** janela para observar uma única variável. Por exemplo, se você tiver o seguinte código:  
  
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
  
 Você pode observar a uma variável na janela QuickWatch da seguinte maneira:  
  
1.  Defina um ponto de interrupção a `a = a + b;` linha.  
  
2.  Inicie a depuração. Interrompe a execução no ponto de interrupção.  
  
3.  Abrir o **QuickWatch** janela (com o botão direito em a, em seguida, escolha **depurar / QuickWatch**, ou **SHIFT + F9**). Você pode abrir a janela e adicionar a uma variável para o **expressão** janela, em seguida, clique em **reavaliar**. Você deve ver a uma variável na **valores** janela, com um valor de 2.  
  
4.  O **QuickWatch** janela é uma janela de caixa de diálogo modal, portanto, você não pode continuar a depuração, desde que ele está aberto. Você pode adicionar a variável para o **Watch** janela clicando **Adicionar inspeção**.  
  
5.  Fechar o **QuickWatch** janela. Agora você pode continuar a depuração enquanto você observar o valor de **inspeção** janela  
  
## <a name="observing-variables-with-the-watch-window"></a>Observando as variáveis com a janela Inspeção  
 Você pode observar diversas variáveis com o **inspeção** janela. Por exemplo, se você tiver o seguinte código:  
  
```csharp  
static void Main(string[] args)  
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
}  
  
```  
  
 Adicione os valores das três variáveis à janela Inspeção, da seguinte maneira:  
  
1. Defina um ponto de interrupção a `c = a + b;` linha.  
  
2. Iniciar a depuração (**F5**). Interrompe a execução no ponto de interrupção.  
  
3. Abra a janela Watch (**depurar / Windows / Assista / Assista 1**, ou **CTRL + ALT + W, 1**).  
  
4. Adicione a `a` variável para a primeira linha, o `b` variável à segunda linha e o `c` variável para a terceira linha.  
  
5. Continue a depuração.  
  
   Você deve ver os valores das variáveis e alterado conforme você itera através de `for` loop.  
  
   Se você estiver programando em código nativo, às vezes talvez seja necessário qualificar o contexto de um nome de variável ou de uma expressão que contenham um nome de variável. O contexto é a função, o arquivo de origem e o módulo onde se encontra uma variável. Se você precisar fazer isso, poderá usar a sintaxe de operador de contexto. Para obter mais informações, consulte expressões em C++.  
  
## <a name="observing-expressions-with-the-watch-window"></a>Observando as expressões com a janela Inspeção  
 Agora vamos tentar usar uma expressão em vez disso. Você pode adicionar qualquer expressão válida reconhecida pelo depurador.  
  
 Por exemplo, se você tiver o código listado na seção anterior, você pode obter a média dos três valores como esta:  
  
 ![WatchExpression](../debugger/media/watchexpression.png "WatchExpression")  
  
 Em geral, as regras para avaliar expressões na **inspeção** janela são as mesmas regras para avaliar expressões na linguagem de codificação. Se a expressão possui um erro de sintaxe, você pode esperar o mesmo erro de compilador que você veria no editor de códigos. Aqui está um exemplo:  
  
 ![WatchExpressionError](../debugger/media/watchexpressionerror.png "WatchExpressionError")  
  
##  <a name="bkmk_refreshWatch"></a> Atualizando valores de inspeção estão desatualizados  
 Em determinadas circunstâncias, você poderá ver um ícone de atualização (um círculo com duas setas, ou um círculo com duas linhas onduladas) quando uma expressão é avaliada na **inspeção** janela.  Por exemplo, se você tiver desativada de avaliação da propriedade (**Ferramentas / opções / depuração / habilitar a avaliação de propriedade e outras chamadas de função implícitas**), e você tem o código a seguir:  
  
```csharp  
static void Main(string[] args)  
{  
    List<string> list = new List<string>();  
    list.Add("hello");  
    list.Add("goodbye");  
}  
  
```  
  
 Se você definir uma inspeção no `Count` propriedade da lista, você deverá ver algo semelhante ao seguinte:  
  
 ![RefreshWatch](../debugger/media/refreshwatch.png "RefreshWatch")  
  
 Isso indica um erro ou um valor que está desatualizado. Geralmente, você pode atualizar o valor clicando no ícone, mas em alguns casos, você talvez prefira não para atualizá-la. Primeiro, você precisa saber por que o valor não foi avaliado.  
  
 Se você apontar para o ícone, uma dica de ferramenta fornecerá informações sobre como a expressão não foi avaliada.  Se as setas de circundamento aparecerem, isso significará que a expressão não foi avaliada para um dos seguintes motivos:  
  
- • Um erro ocorreu como a expressão estava sendo avaliada. Por exemplo, um tempo limite pode ter ocorrido, ou uma variável pode ter ficado fora do escopo.  
  
- • A expressão contém uma chamada de função que pode disparar um efeito colateral no aplicativo (consulte [efeitos colaterais e expressões](#bkmk_sideEffects)).  
  
- A avaliação automática de propriedades e chamadas de função implícitas pelo depurador está desativada (**Ferramentas / opções / depuração / habilitar a avaliação de propriedade e outras chamadas de função implícitas**), e, em seguida, a expressão não pode ser avaliado automaticamente.  
  
  Para atualizar o valor, clique no ícone de atualização ou pressione a barra de espaços. O depurador tenta reavaliar a expressão. Se o ícone de atualização apareceu porque a avaliação automática de propriedades e efeitos colaterais implícitos foi desativada, a expressão pode ser avaliada.  
  
  Se você vir um ícone que é um círculo com duas linhas onduladas cordas, a expressão não foi avaliada devido à dependência potencial entre threads. Em outras palavras, a avaliar o código requer outros threads em seu aplicativo sejam executados temporariamente. Quando você está no modo de interrupção, todos os threads em seu aplicativo normalmente estão parados. Permitir que outros threads sejam executados temporariamente pode ter inesperado de efeitos sobre o estado do seu programa e faz com que o depurador ignorar eventos como pontos de interrupção e as exceções geradas nesses threads.  
  
##  <a name="bkmk_sideEffects"></a> Efeitos colaterais e expressões  
 Avaliar algumas expressões pode alterar o valor de uma variável ou, de outra forma, afetar o estado do programa. Por exemplo, avaliar a expressão a seguir altera o valor de `var1`:  
  
```  
var1 = var2  
```  
  
 Isso é chamado de um [efeito colateral](https://en.wikipedia.org/wiki/Side_effect_\(computer_science\)). Efeitos colaterais podem dificultar a depuração mais alterando o modo de que operação do seu programa.  
  
 Uma expressão que é conhecida por ter efeitos colaterais é avaliada apenas uma vez, quando você primeiro inseri-la. As avaliações subsequentes serão desativadas. Manualmente, você pode substituir esse comportamento, clicando no ícone de atualização que aparece ao lado do valor.  
  
 Uma maneira de evitar todos os efeitos colaterais é desativar a avaliação automática de função (**Ferramentas / opções / depuração / habilitar a avaliação de propriedade e outras chamadas de função implícitas**).  
  
 Quando a avaliação de propriedades ou chamadas de função implícitas é desativada, você pode forçar a avaliação usando o **ac** modificador de formato (apenas para c#). Ver [especificadores em c# de formato](../debugger/format-specifiers-in-csharp.md).  
  
## <a name="using-object-ids-in-the-watch-window-c-and-visual-basic"></a>Usando IDs de objeto na janela de inspeção (c# e Visual Basic)  
 Há vezes quando você deseja observar o comportamento de um objeto específico; Por exemplo, você talvez queira controlar um objeto referenciado por uma variável local depois que essa variável tiver saído do escopo. Em c# e Visual Basic, você pode criar IDs para instâncias específicas de tipos de referência de objeto e usá-los na janela de inspeção e em condições de ponto de interrupção. A ID de objeto é gerada pelo common language runtime (CLR) serviços de depuração e associada ao objeto.  
  
> [!NOTE]
>  IDs de objeto criem referências fracas e não impedem que o objeto que está sendo coletado como lixo. Eles só são válidos para a sessão de depuração atual.  
  
 No código a seguir cria um método de um `Person` usando uma variável local, mas você deseja descobrir o que o `Person`do nome está em um método diferente:  
  
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
    List<Person> _people = new List<Person>();  
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
  
 Você pode adicionar uma referência a esse `Person` do objeto na **inspeção** janela da seguinte maneira:  
  
1.  Defina um ponto de interrupção no código de algum tempo depois que o objeto foi criado.  
  
2.  Iniciar a depuração e quando a execução é interrompida no ponto de interrupção, localize a variável na **Locals** , clique duas vezes e selecione **criar ID de objeto**.  
  
3.  Você deve ver uma **$** além de um número no **locais** janela. Isso é a ID de objeto.  
  
4.  Adicione a ID de objeto para a janela de observação.  
  
5.  Defina um ponto de interrupção em que você deseja observar o comportamento do objeto.  No código acima, que seria no `DoSomething()` método.  
  
6.  Continuar a depuração, e quando a execução é interrompida na `DoSomething()` método, o **inspeção** janela exibe o `Person` objeto.  
  
> [!NOTE]
>  Se você deseja ver as propriedades do objeto, como `Person.Name` no exemplo acima, você deve habilitar avaliação de propriedade.  
  
## <a name="using-registers-in-the-watch-window-c-only"></a>Usando os registros na janela Watch (apenas C++)  
 Se você estiver depurando código nativo, você pode adicionar nomes de registro, como também os nomes de variáveis usando  **$ \<registrar nome >** ou  **@ \<registrar nome >**.  Para obter mais informações, consulte [pseudovariáveis](../debugger/pseudovariables.md).  
  
## <a name="dynamicview-and-the-watch-window"></a>DynamicView e a janela Inspeção  
 Algumas linguagens de script (por exemplo, Python ou JavaScript) usam dinâmico ou [digitação pato](https://en.wikipedia.org/wiki/Duck_typing), e os objetos que são difíceis de observar usando janelas de depuração normais, pois eles podem ter suportam a linguagens .NET (na versão 4.0 e posterior) Propriedades de tempo de execução e métodos que não podem ser exibidos.  
  
 Quando a janela de observação exibe um ou um objeto criado a partir de um tipo que implementa o <xref:System.Dynamic.IDynamicMetaObjectProvider>, o depurador adiciona um especial **modo de exibição dinâmico** nó para o **Autos** exibir. Esse nó mostra os membros dinâmicos do objeto dinâmico, mas não permite editar os valores dos membros.  
  
 Se o botão direito do mouse qualquer filho de um **modo de exibição dinâmico** e escolha **Adicionar inspeção**, o depurador vai inserir uma nova variável de inspeção que converte um objeto em um objeto dinâmico. Em outras palavras, **nome do objeto** torna-se (**objeto (dinâmico)). Nome**.  
  
 Avaliar os membros de um **modo de exibição dinâmico** pode ter efeitos colaterais. Para obter uma explicação dos quais são os efeitos colaterais, consulte [efeitos colaterais e expressões](#bkmk_sideEffects). Para c#, o depurador não reavalia automaticamente os valores mostrados na **modo de exibição dinâmico** quando você depura em uma nova linha de código. Para o Visual Basic, as expressões adicionadas por meio de **modo de exibição dinâmico** são atualizados automaticamente.  
  
 Para obter instruções sobre como atualizar os valores do modo de exibição dinâmico, consulte [valores de inspeção de atualização que estão desatualizados](#bkmk_refreshWatch).  
  
 Se você quiser exibir apenas os **modo de exibição dinâmico** para um objeto, você pode usar o **dinâmico** especificador de formato:  
  
- C#: **ObjectName, dinâmico**  
  
- Visual Basic:: **$dynamic, ObjectName**  
  
  O **modo de exibição dinâmico** também melhora a experiência de depuração para objetos COM. Quando o depurador encontra um objeto COM envolvido na **ComObject**, ele adiciona um **modo de exibição dinâmico** nó do objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Janelas do depurador](../debugger/debugger-windows.md)





