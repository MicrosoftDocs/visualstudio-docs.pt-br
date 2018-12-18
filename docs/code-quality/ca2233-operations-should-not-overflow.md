---
title: 'CA2233: as operações não devem estourar'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperationsShouldNotOverflow
- CA2233
helpviewer_keywords:
- OperationsShouldNotOverflow
- CA2233
ms.assetid: 3a2b06ba-6d1b-4666-9eaf-e053ef47ffaa
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 73c0e616eb527a2213c77cdae00c42635d49b130
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49938897"
---
# <a name="ca2233-operations-should-not-overflow"></a>CA2233: as operações não devem estourar

|||
|-|-|
|NomeDoTipo|OperationsShouldNotOverflow|
|CheckId|CA2233|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um método executa uma operação aritmética e não valida os operandos com antecedência para evitar estouro.

## <a name="rule-description"></a>Descrição da regra

Não execute operações aritméticas sem primeiro validar os operandos para certificar-se de que o resultado da operação não está fora do intervalo de valores possíveis para os tipos de dados envolvidos. Dependendo do contexto de execução e os tipos de dados envolvidos, o estouro aritmético pode resultar em qualquer um uma <xref:System.OverflowException?displayProperty=fullName> ou os bits mais significativos do resultado é descartada.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, valide os operandos antes de executar a operação.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra, se os valores possíveis dos operandos nunca fará com que a operação aritmética estourar.

## <a name="example-of-a-violation"></a>Exemplo de uma violação

Um método no exemplo a seguir manipula um inteiro que viola essa regra. [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] requer o **remover** opção de estouro de inteiro a ser desabilitado para que isso seja acionado.

[!code-vb[FxCop.Usage.OperationOverflow#1](../code-quality/codesnippet/VisualBasic/ca2233-operations-should-not-overflow_1.vb)]
[!code-csharp[FxCop.Usage.OperationOverflow#1](../code-quality/codesnippet/CSharp/ca2233-operations-should-not-overflow_1.cs)]

Se o método neste exemplo é passado <xref:System.Int32.MinValue?displayProperty=fullName>, a operação seria estouro negativo. Isso faz com que o bit mais significativo do resultado seja descartada. O código a seguir mostra como isso ocorre.

```csharp
public static void Main()
{
    int value = int.MinValue;    // int.MinValue is -2147483648
    value = Calculator.Decrement(value);
    Console.WriteLine(value);
}
```

```vb
Public Shared Sub Main()
    Dim value = Integer.MinValue    ' Integer.MinValue is -2147483648
    value = Calculator.Decrement(value)
    Console.WriteLine(value)
End Sub
```

Saída:

```text
2147483647
```

## <a name="fix-with-input-parameter-validation"></a>Corrigir com validação de parâmetro de entrada

O exemplo a seguir corrige a violação anterior ao validar o valor da entrada.

[!code-csharp[FxCop.Usage.OperationOverflowFixed#1](../code-quality/codesnippet/CSharp/ca2233-operations-should-not-overflow_2.cs)]
[!code-vb[FxCop.Usage.OperationOverflowFixed#1](../code-quality/codesnippet/VisualBasic/ca2233-operations-should-not-overflow_2.vb)]

## <a name="fix-with-a-checked-block"></a>Corrigir com um bloco marcado

O exemplo a seguir corrige a violação anterior ao encapsular a operação em um bloco marcado. Se a operação causa um estouro, um <xref:System.OverflowException?displayProperty=fullName> será lançada.

Não há suporte para blocos marcados no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)].

[!code-csharp[FxCop.Usage.OperationOverflowChecked#1](../code-quality/codesnippet/CSharp/ca2233-operations-should-not-overflow_3.cs)]

## <a name="turn-on-checked-arithmetic-overflowunderflow"></a>Ativar verificado estouro/estouro negativo aritmético

Se você ativar verificado estouro/estouro negativo aritmético em c#, equivale a disposição de cada operação de inteiro em um bloco verificado.

Para ativar verificado estouro/estouro negativo aritmético em c#:

1.  Na **Gerenciador de soluções**, clique em seu projeto e escolha **propriedades**.

2.  Selecione a guia **Compilar** e clique em **Avançado**.

3.  Selecione **verificar estouro/estouro negativo aritmético** e clique em **Okey**.

## <a name="see-also"></a>Consulte também

- <xref:System.OverflowException?displayProperty=fullName>
- [Operadores do C#](/dotnet/csharp/language-reference/operators/index)
- [Checked e Unchecked](/dotnet/csharp/language-reference/keywords/checked-and-unchecked)