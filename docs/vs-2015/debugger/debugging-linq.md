---
title: Depurando LINQ | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, LINQ
- LINQ, viewing results in debugger
- LINQ, debugging
- LINQ, stepping
- LINQ, edit and continue
ms.assetid: dbae26cb-ac5f-4312-b474-b9f29714f4c6
caps.latest.revision: 28
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 081c97bffc062bf2bbc9d24feed13e5e512b8c74
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755608"
---
# <a name="debugging-linq"></a>Depurando LINQ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] oferece suporte à depuração de código de consulta integrado da linguagem (LINQ), com algumas restrições. A maioria dos recursos de depuração funcionam com instruções LINQ, incluindo a depuração, definição de pontos de interrupção e exibição de resultados em janelas de depuração. Este tópico descreve as principais limitações da depuração LINQ.  
  
##  <a name="BKMK_ViewingLINQResults"></a> Exibindo resultados de LINQ  
 É possível exibir o resultado de uma declaração LINQ usando DataTips, a janela de observação, e a caixa de diálogo QuickWatch. Ao usar uma janela de origem, você pode pausar o ponteiro em uma consulta na janela de origem e um DataTip aparecerá. É possível copiar uma variável LINQ e colá-la na janela de observação ou na caixa de diálogo QuickWatch.  
  
 Em LINQ, uma consulta não é avaliada quando é criada ou declarada, mas somente quando a consulta é usada. Portanto, a consulta não terá um valor até ser avaliada. Para obter uma descrição completa da criação de consulta e de avaliação, consulte [Introdução a consultas LINQ (c#)](http://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8) ou [escrever sua primeira consulta de LINQ](http://msdn.microsoft.com/library/4affb732-3e9b-4479-aa31-1f9bd8183cbe).  
  
 Para exibir o resultado de uma consulta, o depurador deverá avaliá-lo. Essa avaliação implícita, que ocorre quando você exibe um resultado de consulta LINQ no depurador, tem alguns efeitos que você deve considerar:  
  
-   Cada avaliação de consulta leva tempo. Expandir o nó de resultados leva tempo. Para algumas consultas, a avaliação repetida pode levar a uma penalidade de desempenho visível.  
  
-   Avaliar uma consulta pode resultar em efeitos colaterais, que são alterações no valor dos dados ou no estado do seu programa. Nem todas as consultas têm efeitos colaterais. Para determinar se uma consulta pode ser avaliada com segurança sem efeitos colaterais, você deverá compreender o código que implementa a consulta.  
  
##  <a name="BKMK_SteppingAndLinq"></a> {1&gt;etapas e LINQ  
 Quando estiver depurando o código LINQ, a depuração terá algumas diferenças de comportamento que você deve saber.  
  
### <a name="linq-to-sql"></a>LINQ to SQL  
 Em consultas LINQ to SQL, o código de predicado está além do controle do depurador. Portanto, você não poderá entrar no código de predicado. Qualquer consulta que compila a uma árvore de expressão gera código que vai além do controle do depurador.  
  
### <a name="stepping-in-visual-basic"></a>Executando etapas no Visual Basic  
 Quando estiver depurando um programa do Visual Basic e o depurador encontrar uma declaração de consulta, ele não irá entrará na declaração, mas realçará a declaração inteira como uma única instrução. Esse comportamento ocorre porque a consulta não é avaliada até ser chamada. Para obter mais informações, consulte [Introdução ao LINQ no Visual Basic](http://msdn.microsoft.com/library/3047d86e-0d49-40e2-928b-dc02e46c7984).  
  
 Caso você passe pelo código de exemplo a seguir, o depurador realça a declaração de consulta, ou a criação de consulta, como uma instrução única.  
  
```  
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
  
```  
Dim items() as integer ={1, 2, 3, 4, 5, 6, 7, 8, 9, 10}  
  
' Get the even numbers  
Dim query = From nextInt in items Where nextInt Mod 2 = 0 Select nextInt  
  
For each item in query  
      Console.WriteLine(item)  
Next  
```  
  
 É possível mover o código de predicado para uma nova função chamada de `IsEven`:  
  
```  
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
 Editar e continuar não suporta alterações em consultas LINQ. Se você adicionar, remover ou alterar uma instrução LINQ durante uma sessão de depuração, uma caixa de diálogo aparece o que indica que a alteração não é suportada por Editar and Continuar. Nesse ponto, você pode desfazer as alterações ou parar a sessão de depuração e reiniciar uma nova sessão com o código editado.  
  
 Além disso, Editar e Continuar não dá suporte à alteração do tipo ou do valor de uma variável usado em uma instrução LINQ. Além disso, você pode desfazer as alterações ou parar e reiniciar a sessão de depuração.  
  
 Em C#, não é possível usar Editar e Continuar em qualquer código em um método que contenha uma consulta LINQ.  
  
 No Visual Basic, você pode usar Editar e Continuar no código de não LINQ, mesmo em um método que contém uma consulta LINQ. É possível adicionar ou remover o código antes da instrução LINQ, mesmo se as alterações afetarem o número da linha de consulta LINQ. Sua experiência de depuração do Visual Basic para código de não LINQ permanecerá a mesma como era antes da introdução do LINQ. No entanto, não é possível modificar, adicionar, ou remover uma consulta LINQ, a menos que você deseje parar a depuração para aplicar as alterações.  
  
## <a name="see-also"></a>Consulte também  
 [Depuração de SQL](http://msdn.microsoft.com/en-us/f27c17e6-1d90-49f2-9fc0-d02e6a27f109)   
 [Efeitos colaterais e expressões](http://msdn.microsoft.com/library/e1f8a6ea-9e19-481d-b6bd-df120ad3bf4e)   
 [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)   
 [Introdução a consultas LINQ (C#)](http://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8)   
 [Introdução ao LINQ no Visual Basic](http://msdn.microsoft.com/library/3047d86e-0d49-40e2-928b-dc02e46c7984)



