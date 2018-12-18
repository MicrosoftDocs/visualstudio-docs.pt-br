---
title: 'CA2000: Descartar objetos antes de perder escopo | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA2000
- Dispose objects before losing scope
- DisposeObjectsBeforeLosingScope
helpviewer_keywords:
- CA2000
- DisposeObjectsBeforeLosingScope
ms.assetid: 0c3d7d8d-b94d-46e8-aa4c-38df632c1463
caps.latest.revision: 32
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ce258af87dc9a7732200b410113ee778e0bfbccb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857855"
---
# <a name="ca2000-dispose-objects-before-losing-scope"></a>CA2000: descartar objetos antes de perder o escopo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||  
|-|-|  
|NomeDoTipo|DisposeObjectsBeforeLosingScope|  
|CheckId|CA2000|  
|Categoria|Microsoft.Reliability|  
|Alteração Significativa|Não são significativas|  
  
## <a name="cause"></a>Causa  
 Um objeto de local de um <xref:System.IDisposable> tipo é criado, mas o objeto não for descartado antes de todas as referências ao objeto estão fora do escopo.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Se um objeto descartável não for explicitamente descartado antes de todas as referências a ele estejam fora do escopo, o objeto será descartado em algum momento indeterminado quando o coletor de lixo execute o finalizador do objeto. Como pode ocorrer um evento excepcional que impedirá que o finalizador do objeto seja executado, o objeto deve ser explicitamente descartado.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação dessa regra, chame <xref:System.IDisposable.Dispose%2A> no objeto antes de todas as referências a ele estejam fora do escopo.  
  
 Observe que você pode usar o `using` instrução (`Using` na [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) para encapsular os objetos que implementam `IDisposable`. Objetos que são encapsulados em dessa maneira automaticamente serão descartados no fechamento do `using` bloco.  
  
 A seguir estão algumas situações em que o usando a instrução não é suficiente para proteger os objetos de IDisposable e pode causar CA2000 ocorra.  
  
-   Retornar um objeto descartável requer que o objeto é construído em um bloco try/finally de fora do uso de um bloco.  
  
-   Inicializando membros de um objeto descartável não deve ser feito no construtor do uso de uma instrução.  
  
-   Construtores protegidos somente pelo manipulador de exceção de aninhamento. Por exemplo,  
  
    ```  
    using (StreamReader sr = new StreamReader(new FileStream("C:\myfile.txt", FileMode.Create)))  
    { ... }  
    ```  
  
     faz com que CA2000 ocorrer porque uma falha na construção do objeto StreamReader pode resultar no objeto FileStream nunca seja fechado.  
  
-   Objetos dinâmicos devem usar um objeto de sombra para implementar o padrão de descarte de objetos de IDisposable.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprimir um aviso nessa regra, a menos que você chamou um método em seu objeto que chama `Dispose`, tais como <xref:System.IO.Stream.Close%2A>, ou se o método que gerou o aviso retornará um objeto IDisposable encapsula seu objeto.  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA2213: os campos descartáveis devem ser descartados](../code-quality/ca2213-disposable-fields-should-be-disposed.md)  
  
 [CA2202: não descartar objetos várias vezes](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)  
  
## <a name="example"></a>Exemplo  
 Se você estiver implementando um método que retorna um objeto descartável, use um bloco try/finally sem um bloco catch para certificar-se de que o objeto é descartado. Ao usar um bloco try/finally, você pode permitir que exceções a ser gerado no ponto de falha e certifique-se de que o objeto é descartado.  
  
 No método OpenPort1, a chamada para abrir o objeto ISerializable SerialPort ou a chamada ao SomeMethod pode falhar. Um aviso CA2000 é gerado dessa implementação.  
  
 No método OpenPort2, dois objetos de SerialPort são declarado e está definida como null:  
  
- `tempPort`, que é usado para testar as operações do método tenha êxito.  
  
- `port`, que é usado para o valor retornado do método.  
  
  O `tempPort` é criado e aberto em um `try` bloco e qualquer outro necessários o trabalho é executado no mesmo `try` bloco. No final do `try` bloco, a porta aberta é atribuído para o `port` objeto que será retornado e o `tempPort` objeto é definido como `null`.  
  
  O `finally` bloco verifica o valor de `tempPort`. Se não for nulo, uma operação no método tiver falhado, e `tempPort` está fechado para certificar-se de que todos os recursos são liberados. O objeto de porta retornada conterá o objeto de SerialPort aberto se as operações do método foi bem-sucedida, ou ele será nulo se uma operação falhou.  
  
  [!code-csharp[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/cs/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.cs#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vb#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vboverflow.vb#1)]  
  
## <a name="example"></a>Exemplo  
 Por padrão, o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] compilador tem operadores aritméticos todos os de verificação de estouro. Portanto, qualquer operação aritmética de Visual Basic pode lançar uma <xref:System.OverflowException>. Isso pode levar a inesperado violações de regras como CA2000. Por exemplo, a seguinte função CreateReader1 produzirá uma violação de CA2000, porque o compilador do Visual Basic está emitindo um instrução para a adição que poderia lançar uma exceção que faria com que o StreamReader para não ser descartado de verificação de estouro.  
  
 Para corrigir isso, você pode desabilitar a emissão de verificações de estouro pelo compilador do Visual Basic em seu projeto ou você pode modificar seu código como a seguinte função CreateReader2.  
  
 Para desabilitar a emissão de verificações de estouro, o nome do projeto no Gerenciador de soluções com o botão direito e, em seguida, clique em **propriedades**. Clique em **Compile**, clique em **opções avançadas de compilação**e, em seguida, marque **remover verificações de estouro de inteiro**.  
  
<!-- TODO: review snippet reference  [!CODE [FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1](FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1)]  -->  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.IDisposable>   
 [Padrão de descarte](http://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)