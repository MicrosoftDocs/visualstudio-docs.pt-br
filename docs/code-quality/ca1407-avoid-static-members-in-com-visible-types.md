---
title: 'CA1407: evitar membros estáticos em tipos visíveis COM'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ed145c1b3a3ddf6b0308c8862ee0f15e7637c990
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49879084"
---
# <a name="ca1407-avoid-static-members-in-com-visible-types"></a>CA1407: evitar membros estáticos em tipos visíveis COM

|||
|-|-|
|NomeDoTipo|AvoidStaticMembersInComVisibleTypes|
|CheckId|CA1407|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo que é marcado especificamente como visível para COM Component Object Model () contém um `public``static` método.

## <a name="rule-description"></a>Descrição da regra
 COM não oferece suporte `static` métodos.

 Essa regra ignora a propriedade e acessadores de eventos, métodos ou métodos que são marcados usando qualquer um de sobrecarga de operador de <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> atributo ou o <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> atributo.

 Por padrão, a seguir é visível no COM: assemblies, tipos públicos, membros de instância pública em tipos públicos e todos os membros de tipos de valor público.

 Para esta regra para ocorrer, um nível de conjunto <xref:System.Runtime.InteropServices.ComVisibleAttribute> deve ser definida como `false` e a classe - <xref:System.Runtime.InteropServices.ComVisibleAttribute> deve ser definida como `true`, como mostra o código a seguir.

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
 Para corrigir uma violação dessa regra, altere o projeto para usar um método de instância que fornece a mesma funcionalidade que o `static` método.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se um cliente COM não exigir acesso à funcionalidade fornecida pelo `static` método.

## <a name="example-violation"></a>Violação de exemplo

### <a name="description"></a>Descrição
 A exemplo a seguir mostra um `static` método que viola essa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersViolation#1](../code-quality/codesnippet/CSharp/ca1407-avoid-static-members-in-com-visible-types_1.cs)]

### <a name="comments"></a>Comentários
 Neste exemplo, o **Book.FromPages** método não pode ser chamado COM.

## <a name="example-fix"></a>Correção de exemplo

### <a name="description"></a>Descrição
 Para corrigir a violação no exemplo anterior, você pode alterar o método para um método de instância, mas que não faz sentido nesta instância. Uma solução melhor é aplicar explicitamente `ComVisible(false)` para o método para deixar claro para outros desenvolvedores que o método não pode ser visto de COM.

 O exemplo a seguir aplica-se <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> para o método.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Interoperability.ComVisibleStaticMembersFixed#1](../code-quality/codesnippet/CSharp/ca1407-avoid-static-members-in-com-visible-types_2.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1017: marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

 [CA1406: evitar argumentos Int64 para clientes do Visual Basic 6](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)

 [CA1413: evitar campos não públicos em tipos de valor visíveis em COM](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

## <a name="see-also"></a>Consulte também
 [Interoperação com código não gerenciado](/dotnet/framework/interop/index)