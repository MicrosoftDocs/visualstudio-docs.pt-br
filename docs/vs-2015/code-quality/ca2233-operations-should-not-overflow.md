---
title: 'CA2233: as operações não devem exceder | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperationsShouldNotOverflow
- CA2233
helpviewer_keywords:
- OperationsShouldNotOverflow
- CA2233
ms.assetid: 3a2b06ba-6d1b-4666-9eaf-e053ef47ffaa
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: eff09fb8f4423560c4681c94507d909f5864c69e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545230"
---
# <a name="ca2233-operations-should-not-overflow"></a>CA2233: As operações não devem estourar
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|OperationsShouldNotOverflow|
|CheckId|CA2233|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método executa uma operação aritmética e não valida os operandos com antecedência para evitar o estouro.

## <a name="rule-description"></a>Descrição da Regra
 As operações aritméticas não devem ser executadas sem primeiro validar os operandos para garantir que o resultado da operação não esteja fora do intervalo de valores possíveis para os tipos de dados envolvidos. Dependendo do contexto de execução e dos tipos de dados envolvidos, o estouro aritmético pode resultar em um <xref:System.OverflowException?displayProperty=fullName> ou nos bits mais significativos do resultado descartados.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, valide os operandos antes de executar a operação.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se os valores possíveis dos operandos nunca causarem o estouro da operação aritmética.

## <a name="example-of-a-violation"></a>Exemplo de uma violação

### <a name="description"></a>Descrição
 Um método no exemplo a seguir manipula um inteiro que viola essa regra. [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]requer que a opção **remover** estouro de inteiro seja desabilitada para que isso seja acionado.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.OperationOverflow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/cs/FxCop.Usage.OperationOverflow.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/vb/FxCop.Usage.OperationOverflow.vb#1)]

### <a name="comments"></a>Comentários
 Se o método neste exemplo for passado <xref:System.Int32.MinValue?displayProperty=fullName> , a operação fluirá. Isso faz com que o bit mais significativo do resultado seja Descartado. O código a seguir mostra como isso ocorre.

 [C#]

```
public static void Main()
{
    int value = int.MinValue;    // int.MinValue is -2147483648
    value = Calculator.Decrement(value);
    Console.WriteLine(value);
}
```

 VB

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
 O exemplo a seguir corrige a violação anterior, validando o valor da entrada.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.OperationOverflowFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/cs/FxCop.Usage.OperationOverflowFixed.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflowFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/vb/FxCop.Usage.OperationOverflowFixed.vb#1)]

## <a name="fix-with-a-checked-block"></a>Corrigir com um bloco marcado

### <a name="description"></a>Descrição
 O exemplo a seguir corrige a violação anterior, encapsulando a operação em um bloco marcado. Se a operação causar um estouro, um <xref:System.OverflowException?displayProperty=fullName> será gerado.

 Observe que os blocos verificados não têm suporte no [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .

### <a name="code"></a>Código
 [!code-csharp[FxCop.Usage.OperationOverflowChecked#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowChecked/cs/FxCop.Usage.OperationOverflowChecked.cs#1)]

## <a name="turn-on-checked-arithmetic-overflowunderflow"></a>Ativar estouro aritmético/negativo selecionado
 Se você ativar o estouro aritmético/negativo marcado em C#, será equivalente a encapsular cada operação de inteiro em um bloco marcado.

 **Para ativar o estouro aritmético/negativo marcado em C #**

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto e escolha **Propriedades**.

2. Selecione a guia **Compilar** e clique em **Avançado**.

3. Selecione **verificar estouro aritmético/Subfluxo** e clique em **OK**.

## <a name="see-also"></a>Consulte Também
 <xref:System.OverflowException?displayProperty=fullName>[Operadores C#](https://msdn.microsoft.com/library/0301e31f-22ad-49af-ac3c-d5eae7f0ac43) [marcados e desmarcados](https://msdn.microsoft.com/library/a84bc877-2c7f-4396-8735-1ce97c42f35e)
