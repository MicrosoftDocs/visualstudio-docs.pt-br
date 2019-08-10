---
title: 'CA1407: Evitar membros estáticos em tipos visíveis no COM'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
helpviewer_keywords:
- CA1407
- AvoidStaticMembersInComVisibleTypes
ms.assetid: bebd0776-ad04-453c-bca8-8c124c2d7840
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 631be1a93318cd24af4251fefbc710294fa52bf7
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922004"
---
# <a name="ca1407-avoid-static-members-in-com-visible-types"></a>CA1407: Evitar membros estáticos em tipos visíveis no COM

|||
|-|-|
|NomeDoTipo|AvoidStaticMembersInComVisibleTypes|
|CheckId|CA1407|
|Categoria|Microsoft. Interoperability|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
Um tipo marcado especificamente como visível para Component Object Model (com) contém um `public``static` método.

## <a name="rule-description"></a>Descrição da regra
COM não oferece suporte `static` a métodos.

Essa regra ignora os acessadores de propriedade e evento, métodos de sobrecarga de operador ou métodos que são marcados usando o <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> atributo ou o <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> atributo.

Por padrão, os itens a seguir são visíveis para COM: assemblies, tipos públicos, membros de instância pública em tipos públicos e todos os membros de tipos de valor público.

Para que essa regra ocorra, um <xref:System.Runtime.InteropServices.ComVisibleAttribute> nível de assembly deve ser `false` definido como e a classe `true`- <xref:System.Runtime.InteropServices.ComVisibleAttribute> deve ser definida como, como mostra o código a seguir.

```csharp
using System;
using System.Runtime.InteropServices;

[assembly: ComVisible(false)]
namespace Samples
{
    [ComVisible(true)]
    public class MyClass
    {
        public static void DoSomething()
        {
        }
    }
}
```

## <a name="how-to-fix-violations"></a>Como corrigir violações
Para corrigir uma violação dessa regra, altere o design para usar um método de instância que forneça a mesma funcionalidade que o `static` método.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
É seguro suprimir um aviso dessa regra se um cliente com não precisar de acesso à funcionalidade fornecida pelo `static` método.

## <a name="example-violation"></a>Violação de exemplo

### <a name="description"></a>Descrição
O exemplo a seguir mostra `static` um método que viola essa regra.

### <a name="code"></a>Código
[!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersViolation#1](../code-quality/codesnippet/CSharp/ca1407-avoid-static-members-in-com-visible-types_1.cs)]

### <a name="comments"></a>Comentários
Neste exemplo, o método **book. FromPages** não pode ser chamado de com.

## <a name="example-fix"></a>Correção de exemplo

### <a name="description"></a>Descrição
Para corrigir a violação no exemplo anterior, você pode alterar o método para um método de instância, mas isso não faz sentido nessa instância. Uma solução melhor é aplicar `ComVisible(false)` explicitamente ao método para deixá-lo claro para outros desenvolvedores que o método não pode ser visto do com.

O exemplo a seguir <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> aplica-se ao método.

### <a name="code"></a>Código
[!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersFixed#1](../code-quality/codesnippet/CSharp/ca1407-avoid-static-members-in-com-visible-types_2.cs)]

## <a name="related-rules"></a>Regras relacionadas
[CA1017: Marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

[CA1406: Evite argumentos Int64 para clientes Visual Basic 6](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)

[CA1413: Evitar campos não públicos em tipos de valores visíveis COM](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

## <a name="see-also"></a>Consulte também
[Interoperação com código não gerenciado](/dotnet/framework/interop/index)