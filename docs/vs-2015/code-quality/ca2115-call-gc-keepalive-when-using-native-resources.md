---
title: 'CA2115: chamar GC. KeepAlive ao usar recursos nativos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CallGCKeepAliveWhenUsingNativeResources
- CA2115
helpviewer_keywords:
- CA2115
- CallGCKeepAliveWhenUsingNativeResources
ms.assetid: f00a59a7-2c6a-4bbe-a1b3-7bf77d366f34
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c668172ca318000068fb4e90f4848e456c32208d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543618"
---
# <a name="ca2115-call-gckeepalive-when-using-native-resources"></a>CA2115: Chamar GC.KeepAlive ao usar recursos nativos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|CallGCKeepAliveWhenUsingNativeResources|
|CheckId|CA2115|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método declarado em um tipo com um finalizador faz referência a um <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName> campo ou, mas não chama <xref:System.GC.KeepAlive%2A?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 A coleta de lixo Finaliza um objeto se não houver mais referências a ele no código gerenciado. Referências não gerenciadas a objetos não impedem a coleta de lixo. Esta regra detecta erros que podem ocorrer porque um recurso não gerenciado está sendo finalizado, enquanto ainda está sendo usado em código não gerenciado.

 Essa regra pressupõe que <xref:System.IntPtr> e <xref:System.UIntPtr> campos armazenem ponteiros para recursos não gerenciados. Como a finalidade de um finalizador é liberar recursos não gerenciados, a regra pressupõe que o finalizador liberará o recurso não gerenciado apontado pelos campos de ponteiro. Essa regra também pressupõe que o método está referenciando o campo ponteiro para passar o recurso não gerenciado para código não gerenciado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione uma chamada para <xref:System.GC.KeepAlive%2A> ao método, passando a instância atual ( `this` em C# e C++) como o argumento. Posicione a chamada após a última linha de código em que o objeto deve ser protegido da coleta de lixo. Imediatamente após a chamada para <xref:System.GC.KeepAlive%2A> , o objeto é considerado novamente pronto para coleta de lixo, supondo que não haja nenhuma referência gerenciada a ele.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Essa regra faz algumas suposições que podem levar a falsos positivos. Você pode suprimir com segurança um aviso dessa regra se:

- O finalizador não libera o conteúdo do <xref:System.IntPtr> <xref:System.UIntPtr> campo ou referenciado pelo método.

- O método não passa o <xref:System.IntPtr> campo ou <xref:System.UIntPtr> para o código não gerenciado.

  Revise cuidadosamente outras mensagens antes de exclui-las. Essa regra detecta erros que são difíceis de reproduzir e depurar.

## <a name="example"></a>Exemplo
 No exemplo a seguir, não `BadMethod` inclui uma chamada para `GC.KeepAlive` e, portanto, viola a regra. `GoodMethod`contém o código corrigido.

> [!NOTE]
> Este exemplo é pseudo-código, embora o código seja compilado e executado, o aviso não é acionado porque um recurso não gerenciado não é criado ou liberado.

 [!code-csharp[FxCop.Security.IntptrAndFinalize#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.IntptrAndFinalize/cs/FxCop.Security.IntptrAndFinalize.cs#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.GC.KeepAlive%2A?displayProperty=fullName> <xref:System.IntPtr?displayProperty=fullName>
 <xref:System.Object.Finalize%2A?displayProperty=fullName>
 <xref:System.UIntPtr?displayProperty=fullName>
 [Padrão de descarte](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
