---
title: 'CA2000: descartar objetos antes de perder o escopo | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2000
- Dispose objects before losing scope
- DisposeObjectsBeforeLosingScope
helpviewer_keywords:
- CA2000
- DisposeObjectsBeforeLosingScope
ms.assetid: 0c3d7d8d-b94d-46e8-aa4c-38df632c1463
caps.latest.revision: 32
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e3de3246980ead0b20d471321a9696451aed81ac
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534765"
---
# <a name="ca2000-dispose-objects-before-losing-scope"></a>CA2000: Descartar objetos antes de perder o escopo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DisposeObjectsBeforeLosingScope|
|CheckId|CA2000|
|Categoria|Microsoft. confiabilidade|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um objeto local de um <xref:System.IDisposable> tipo é criado, mas o objeto não é descartado antes que todas as referências ao objeto estejam fora do escopo.

## <a name="rule-description"></a>Descrição da Regra
 Se um objeto descartável não for explicitamente descartado antes que todas as referências a ele estejam fora do escopo, o objeto será descartado em algum momento indeterminado quando o coletor de lixo executar o finalizador do objeto. Como pode ocorrer um evento excepcional que impedirá que o finalizador do objeto seja executado, o objeto deve ser explicitamente descartado em vez disso.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame <xref:System.IDisposable.Dispose%2A> no objeto antes que todas as referências a ele estejam fora do escopo.

 Observe que você pode usar a `using` instrução ( `Using` in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ) para encapsular objetos que implementam `IDisposable` . Os objetos que são encapsulados dessa maneira serão automaticamente descartados no fechamento do `using` bloco.

 A seguir estão algumas situações em que a instrução using não é suficiente para proteger objetos IDisposable e pode fazer com que o CA2000 ocorra.

- Retornar um objeto descartável requer que o objeto seja construído em um bloco try/finally fora de um bloco Using.

- A inicialização de membros de um objeto descartável não deve ser feita no construtor de uma instrução using.

- Aninhando construtores que são protegidos somente por um manipulador de exceção. Por exemplo,

    ```
    using (StreamReader sr = new StreamReader(new FileStream("C:\myfile.txt", FileMode.Create)))
    { ... }
    ```

     faz com que CA2000 ocorra porque uma falha na construção do objeto StreamReader pode fazer com que o objeto FileStream nunca seja fechado.

- Objetos dinâmicos devem usar um objeto Shadow para implementar o padrão Dispose de objetos IDisposable.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso dessa regra, a menos que você tenha chamado um método em seu objeto que chame `Dispose` , como <xref:System.IO.Stream.Close%2A> , ou se o método que gerou o aviso retornar um objeto IDisposable encapsular o objeto.

## <a name="related-rules"></a>Regras relacionadas
 [CA2213: Campos descartáveis devem ser descartados](../code-quality/ca2213-disposable-fields-should-be-disposed.md)

 [CA2202: Não descartar objetos várias vezes](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)

## <a name="example"></a>Exemplo
 Se você estiver implementando um método que retorna um objeto descartável, use um bloco try/finally sem um bloco catch para certificar-se de que o objeto foi Descartado. Usando um bloco try/finally, você permite que exceções sejam geradas no ponto de falha e certifique-se de que o objeto seja Descartado.

 No método OpenPort1, a chamada para abrir o objeto ISerializable SerialPort ou a chamada para SomeMethod pode falhar. Um aviso CA2000 é gerado nessa implementação.

 No método OpenPort2, dois objetos SerialPort são declarados e definidos como NULL:

- `tempPort`, que é usado para testar se as operações do método são bem-sucedidos.

- `port`, que é usado para o valor de retorno do método.

  O `tempPort` é construído e aberto em um `try` bloco, e qualquer outro trabalho necessário é executado no mesmo `try` bloco. No final do `try` bloco, a porta aberta é atribuída ao `port` objeto que será retornado e o `tempPort` objeto será definido como `null` .

  O `finally` bloco verifica o valor de `tempPort` . Se não for NULL, uma operação no método terá falhado e `tempPort` será fechada para garantir que todos os recursos sejam liberados. O objeto de porta retornado conterá o objeto SerialPort aberto se as operações do método tiverem êxito ou serão nulas se uma operação falhar.

  [!code-csharp[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/cs/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.cs#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vb#1)]
  [!code-vb[FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope/vb/fxcop.reliability.ca2000.disposeobjectsbeforelosingscope.vboverflow.vb#1)]

## <a name="example"></a>Exemplo
 Por padrão, o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] compilador tem todos os operadores aritméticos verificam o estouro. Portanto, qualquer Visual Basic operação aritmética pode gerar um <xref:System.OverflowException> . Isso pode levar a violações inesperadas em regras como CA2000. Por exemplo, a seguinte função CreateReader1 produzirá uma violação de CA2000, pois o compilador de Visual Basic está emitindo uma instrução de verificação de estouro para a adição que poderia gerar uma exceção que faria com que StreamReader não fosse descartado.

 Para corrigir isso, você pode desabilitar a emissão de verificações de estouro pelo compilador Visual Basic em seu projeto ou pode modificar seu código como na seguinte função CreateReader2.

 Para desabilitar a emissão de verificações de estouro, clique com o botão direito do mouse no nome do projeto em Gerenciador de Soluções e clique em **Propriedades**. Clique em **Compilar**, clique em **Opções de compilação avançadas**e marque **Remover verificações de estouro de inteiro**.

<!-- TODO: review snippet reference  [!CODE [FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1](FxCop.Reliability.CA2000.DisposeObjectsBeforeLosingScope.VBOverflow#1)]  -->

## <a name="see-also"></a>Consulte Também
 <xref:System.IDisposable>[Descartar padrão](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)