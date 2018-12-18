---
title: 'CA2233: As operações não devem estourar | Microsoft Docs'
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
- OperationsShouldNotOverflow
- CA2233
helpviewer_keywords:
- OperationsShouldNotOverflow
- CA2233
ms.assetid: 3a2b06ba-6d1b-4666-9eaf-e053ef47ffaa
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5f6690f6577d936757ae3bbe8b725b4434b6bee1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836652"
---
# <a name="ca2233-operations-should-not-overflow"></a>CA2233: as operações não devem estourar
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|OperationsShouldNotOverflow|
|CheckId|CA2233|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um método executa uma operação aritmética e não valida os operandos com antecedência para evitar estouro.

## <a name="rule-description"></a>Descrição da Regra
 Operações aritméticas não devem ser executadas sem primeiro validar os operandos para certificar-se de que o resultado da operação não está fora do intervalo de valores possíveis para os tipos de dados envolvidos. Dependendo do contexto de execução e os tipos de dados envolvidos, o estouro aritmético pode resultar em qualquer um uma <xref:System.OverflowException?displayProperty=fullName> ou os bits mais significativos do resultado é descartada.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, valide os operandos antes de executar a operação.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se os valores possíveis dos operandos nunca fará com que a operação aritmética estourar.

## <a name="example-of-a-violation"></a>Exemplo de uma violação

### <a name="description"></a>Descrição
 Um método no exemplo a seguir manipula um inteiro que viola essa regra. [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] requer o **remover** opção de estouro de inteiro a ser desabilitado para que isso seja acionado.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.OperationOverflow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/cs/FxCop.Usage.OperationOverflow.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/vb/FxCop.Usage.OperationOverflow.vb#1)]

### <a name="comments"></a>Comentários
 Se o método neste exemplo é passado <xref:System.Int32.MinValue?displayProperty=fullName>, a operação seria estouro negativo. Isso faz com que o bit mais significativo do resultado seja descartada. O código a seguir mostra como isso ocorre.

 [C#]

```
public static void Main()
{
    int value = int.MinValue;    // int.MinValue is -2147483648
    value = Calculator.Decrement(value);
    Console.WriteLine(value);
}
```

 [VB]

```
Public Shared Sub Main()
    Dim value = Integer.MinValue    ' Integer.MinValue is -2147483648
    value = Calculator.Decrement(value)
    Console.WriteLine(value)
End Sub
```

### <a name="output"></a>Saída

```
2147483647
```

## <a name="fix-with-input-parameter-validation"></a>Corrigir com validação de parâmetro de entrada

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação anterior ao validar o valor da entrada.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.OperationOverflowFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/cs/FxCop.Usage.OperationOverflowFixed.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflowFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/vb/FxCop.Usage.OperationOverflowFixed.vb#1)]

## <a name="fix-with-a-checked-block"></a>Corrigir com um bloco marcado

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação anterior ao encapsular a operação em um bloco marcado. Se a operação causa um estouro, um <xref:System.OverflowException?displayProperty=fullName> será lançada.

 Observe que não há suporte para blocos marcados no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)].

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.OperationOverflowChecked#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowChecked/cs/FxCop.Usage.OperationOverflowChecked.cs#1)]

## <a name="turn-on-checked-arithmetic-overflowunderflow"></a>Ativar verificado estouro/estouro negativo aritmético
 Se você ativar verificado estouro/estouro negativo aritmético em c#, equivale a disposição de cada operação de inteiro em um bloco verificado.

 **Para ativar o verificado estouro/estouro negativo aritmético em c#**

1.  Na **Gerenciador de soluções**, clique em seu projeto e escolha **propriedades**.

2.  Selecione a guia **Compilar** e clique em **Avançado**.

3.  Selecione **verificar estouro/estouro negativo aritmético** e clique em **Okey**.

## <a name="see-also"></a>Consulte também
 <xref:System.OverflowException?displayProperty=fullName> [Operadores do c#](http://msdn.microsoft.com/library/0301e31f-22ad-49af-ac3c-d5eae7f0ac43) [Checked e Unchecked](http://msdn.microsoft.com/library/a84bc877-2c7f-4396-8735-1ce97c42f35e)



