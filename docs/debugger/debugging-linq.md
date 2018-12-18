---
title: Depurando LINQ | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, LINQ
- LINQ, viewing results in debugger
- LINQ, debugging
- LINQ, stepping
- LINQ, edit and continue
ms.assetid: dbae26cb-ac5f-4312-b474-b9f29714f4c6
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8511c3ac9efd79b712680bfe3f9d5611f3c5aa9c
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349420"
---
# <a name="debugging-linq"></a>Depurando LINQ
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] oferece suporte à depuração de código de consulta integrado da linguagem (LINQ), com algumas restrições. A maioria dos recursos de depuração funcionam com instruções LINQ, incluindo a depuração, definição de pontos de interrupção e exibição de resultados em janelas de depuração. Este tópico descreve as principais limitações da depuração LINQ.  
  
##  <a name="BKMK_ViewingLINQResults"></a> Exibindo resultados de LINQ  
 É possível exibir o resultado de uma declaração LINQ usando DataTips, a janela de observação, e a caixa de diálogo QuickWatch. Ao usar uma janela de origem, você pode pausar o ponteiro em uma consulta na janela de origem e um DataTip aparecerá. É possível copiar uma variável LINQ e colá-la na janela de observação ou na caixa de diálogo QuickWatch.  
  
 Em LINQ, uma consulta não é avaliada quando é criada ou declarada, mas somente quando a consulta é usada. Portanto, a consulta não terá um valor até ser avaliada. Para obter uma descrição completa da criação de consulta e de avaliação, consulte [Introdução a consultas LINQ (c#)](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries) ou [escrever sua primeira consulta de LINQ](/dotnet/visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query).  
  
 Para exibir o resultado de uma consulta, o depurador deverá avaliá-lo. Essa avaliação implícita, que ocorre quando você exibe um resultado de consulta LINQ no depurador, tem alguns efeitos que você deve considerar:  
  
-   Cada avaliação de consulta leva tempo. Expandir o nó de resultados leva tempo. Para algumas consultas, a avaliação repetida pode levar a uma penalidade de desempenho visível.  
  
-   Avaliar uma consulta pode resultar em efeitos colaterais, que são alterações no valor dos dados ou no estado do seu programa. Nem todas as consultas têm efeitos colaterais. Para determinar se uma consulta pode ser avaliada com segurança sem efeitos colaterais, você deverá compreender o código que implementa a consulta.  
  
##  <a name="BKMK_SteppingAndLinq"></a> {1&gt;etapas e LINQ  
 Quando estiver depurando o código LINQ, a depuração terá algumas diferenças de comportamento que você deve saber.  
  
### <a name="linq-to-sql"></a>LINQ to SQL  
 Em consultas LINQ to SQL, o código de predicado está além do controle do depurador. Portanto, você não poderá entrar no código de predicado. Qualquer consulta que compila a uma árvore de expressão gera código que vai além do controle do depurador.  
  
### <a name="stepping-in-visual-basic"></a>Executando etapas no Visual Basic  
 Quando estiver depurando um programa do Visual Basic e o depurador encontrar uma declaração de consulta, ele não irá entrará na declaração, mas realçará a declaração inteira como uma única instrução. Esse comportamento ocorre porque a consulta não é avaliada até ser chamada. Para obter mais informações, consulte [Introdução ao LINQ no Visual Basic](/dotnet/visual-basic/programming-guide/language-features/linq/introduction-to-linq).  
  
 Caso você passe pelo código de exemplo a seguir, o depurador realça a declaração de consulta, ou a criação de consulta, como uma instrução única.  
  
```vb
Function MyFunction(ByVal x As Char)  
    Return True  
End Function  
  
Sub Main()  
    'Query creation  
    Dim x = From it In "faoaoeua" _  
            Where MyFunction(it) _  
            Select New With {.a = it}  
  
    ' Query execution  
    For Each cur In x  
        Console.WriteLine(cur.ToString())  
    Next  
End Sub  
```  
  
 Ao passar novamente pelo código, o depurador realça `For Each cur In x`. Na próxima etapa, entra na função `MyFunction`. Depois de avançar até `MyFunction`, volte para `Console.WriteLine(cur.ToSting())`. Em nenhum ponto ele percorre o código de predicado na declaração de consulta, embora o depurador avalia aquele código.  
  
### <a name="replacing-a-predicate-with-a-function-to-enable-stepping-visual-basic"></a>Substituindo um predicado por uma função para habilitar a depuração (Visual Basic)  
 Se precisar passar pelo código de predicado para fins de depuração, você poderá substituir o predicado por uma chamada para uma função que contenha o código de predicado original. Por exemplo, suponha que você tenha este código:  
  
```vb
Dim items() as integer ={1, 2, 3, 4, 5, 6, 7, 8, 9, 10}  
  
' Get the even numbers  
Dim query = From nextInt in items Where nextInt Mod 2 = 0 Select nextInt  
  
For each item in query  
      Console.WriteLine(item)  
Next  
```  
  
 É possível mover o código de predicado para uma nova função chamada de `IsEven`:  
  
```vb
Dim items () as integer ={1, 2, 3, 4, 5, 6, 7, 8, 9, 10}  
  
' Get the even numbers  
Dim query = From nextInt in items Where IsEven(nextInt) Select nextInt  
  
For each item in query  
      Console.WriteLine(item)  
Next  
...   
Function IsEven(item As =Integer) as Boolean  
      Return item Mod 2 = 0  
End Function  
```  
  
 A consulta revisada chama a função `IsEven` em cada passo por meio de `items`. É possível usar as janelas de depuração para ver se cada item está de acordo com a condição especificada, e você pode percorrer o código em `IsEven`. O predicado neste exemplo é bastante simples. No entanto, se você tem um predicado mais difícil que precisa depurar, essa técnica pode ser muito útil.  
  
##  <a name="BKMK_EditandContinueNotSupportedforLINQ"></a> Editar e continuar não suportada para LINQ  
 Editar e continuar dá suporte a alterações em consultas LINQ com limitações. Para obter detalhes, consulte [alterações de suporte EnC](https://github.com/dotnet/roslyn/wiki/EnC-Supported-Edits))
  
## <a name="see-also"></a>Consulte também

- [Depuração de SQL](/previous-versions/visualstudio/visual-studio-2010/zefbf0t6\(v\=vs.100\))
- [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)
- [Introdução a consultas LINQ (C#)](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries)
- [Introdução ao LINQ no Visual Basic](/dotnet/visual-basic/programming-guide/language-features/linq/introduction-to-linq)
