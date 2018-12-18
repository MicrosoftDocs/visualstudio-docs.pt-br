---
title: 'CA2115: chamar GC.KeepAlive durante o uso de recursos nativos'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CallGCKeepAliveWhenUsingNativeResources
- CA2115
helpviewer_keywords:
- CA2115
- CallGCKeepAliveWhenUsingNativeResources
ms.assetid: f00a59a7-2c6a-4bbe-a1b3-7bf77d366f34
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 21777b19e488e60e68c11ccceaad779dcf4e94a3
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546987"
---
# <a name="ca2115-call-gckeepalive-when-using-native-resources"></a>CA2115: chamar GC.KeepAlive durante o uso de recursos nativos

|||
|-|-|
|NomeDoTipo|CallGCKeepAliveWhenUsingNativeResources|
|CheckId|CA2115|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um método declarado em um tipo com um finalizador faz referência a um <xref:System.IntPtr?displayProperty=fullName> ou <xref:System.UIntPtr?displayProperty=fullName> campo, mas não chama <xref:System.GC.KeepAlive%2A?displayProperty=fullName>.

## <a name="rule-description"></a>Descrição da regra

Coleta de lixo Finaliza um objeto, se não houver nenhuma referência mais para ele no código gerenciado. Não gerenciadas referências a objetos não impedem que a coleta de lixo. Esta regra detecta erros que podem ocorrer porque um recurso não gerenciado está sendo finalizado, enquanto ainda está sendo usado em código não gerenciado.

Esta regra pressupõe que <xref:System.IntPtr> e <xref:System.UIntPtr> campos armazenam ponteiros para recursos não gerenciados. Como a finalidade de um finalizador é liberar recursos não gerenciados, a regra pressupõe que o finalizador irá liberar o recurso não gerenciado, apontado para os campos de ponteiro. Essa regra também pressupõe que o método está referenciando o campo de ponteiro para passar o recurso não gerenciado para código não gerenciado.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, adicione uma chamada para <xref:System.GC.KeepAlive%2A> para o método, passando a instância atual (`this` em c# e C++) como o argumento. Posicione a chamada após a última linha de código em que o objeto deve ser protegido de coleta de lixo. Imediatamente após a chamada para <xref:System.GC.KeepAlive%2A>, o objeto é considerado novamente pronto para a coleta de lixo supondo que nenhuma referência gerenciada para ele.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Essa regra faz algumas suposições que podem resultar em falsos positivos. Com segurança, você pode suprimir um aviso nessa regra se:

- O finalizador não libera o conteúdo a <xref:System.IntPtr> ou <xref:System.UIntPtr> campo referenciado pelo método.

- O método não passa o <xref:System.IntPtr> ou <xref:System.UIntPtr> campo para código não gerenciado.

Examine cuidadosamente as outras mensagens antes de excluí-las. Essa regra detecta erros que são difíceis de reproduzir e depurar.

## <a name="example"></a>Exemplo

No exemplo a seguir `BadMethod` não inclui uma chamada para `GC.KeepAlive` e, portanto, viola a regra. `GoodMethod` contém o código corrigido.

> [!NOTE]
> Este exemplo é o pseudocódigo. Embora o código é compilado e é executado, o aviso não é acionado porque um recurso não gerenciado não é criado ou liberado.

[!code-csharp[FxCop.Security.IntptrAndFinalize#1](../code-quality/codesnippet/CSharp/ca2115-call-gc-keepalive-when-using-native-resources_1.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.GC.KeepAlive%2A?displayProperty=fullName>
- <xref:System.IntPtr?displayProperty=fullName>
- <xref:System.Object.Finalize%2A?displayProperty=fullName>
- <xref:System.UIntPtr?displayProperty=fullName>
- [Padrão de descarte](/dotnet/standard/design-guidelines/dispose-pattern)