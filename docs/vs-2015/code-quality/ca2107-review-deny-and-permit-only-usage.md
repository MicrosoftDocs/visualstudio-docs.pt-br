---
title: 'CA2107: Revisar deny e permit o uso apenas | Microsoft Docs'
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
- CA2107
- ReviewDenyAndPermitOnlyUsage
helpviewer_keywords:
- ReviewDenyAndPermitOnlyUsage
- CA2107
ms.assetid: 366f4a56-ae93-4882-81d0-bd0a55ebbc26
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f7a82e6b1acdb8eee1d97dcf6f264ebf66343b58
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49851095"
---
# <a name="ca2107-review-deny-and-permit-only-usage"></a>CA2107: revisar uso de deny e permit only
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ReviewDenyAndPermitOnlyUsage|
|CheckId|CA2107|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método contém uma verificação de segurança que especifica a ação de segurança PermitOnly ou Deny.

## <a name="rule-description"></a>Descrição da Regra
 O [usando o método PermitOnly](http://msdn.microsoft.com/en-us/8c7bdb7f-882f-45b7-908c-6cbaa1767649) e <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName> ações de segurança devem ser usadas apenas por aqueles que tenham um conhecimento avançado de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] segurança. O código que usa essas ações de segurança deve passar por uma revisão de segurança.

 Negar altera o comportamento padrão, a movimentação de pilha ocorre em resposta a uma exigência de segurança. Ele permite que você especifique as permissões que não devem ser concedidas para a duração do método negando, independentemente das permissões reais dos chamadores na pilha de chamadas. Se a movimentação da pilha detecta um método que é protegido por Negar e se a permissão exigida é incluída nas permissões negadas, a movimentação da pilha falha. PermitOnly também altera o comportamento padrão do exame da pilha. Ele permite que o código especificar somente as permissões que podem ser concedidas, independentemente das permissões dos chamadores. Se a movimentação da pilha detecta um método que é protegido pelo PermitOnly, e se a permissão exigida não está incluída nas permissões que são especificadas pela PermitOnly, a movimentação da pilha falha.

 Código que depende dessas ações deve ser avaliado cuidadosamente para vulnerabilidades de segurança devido à sua utilidade limitada e comportamento sutil. Considere o seguinte:

-   [Demandas de link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) não são afetados por Deny ou PermitOnly.

-   Se o Deny ou PermitOnly ocorre no quadro de pilha como a demanda que faz com que a movimentação da pilha, as ações de segurança não terão efeito.

-   Valores que são usados para construir as permissões com base em caminho geralmente podem ser especificados de várias maneiras. Negar acesso a um formulário do caminho não nega acesso a todas as formas. Por exemplo, se um compartilhamento de arquivos \\\Server\Share é mapeado para uma unidade de rede x, para negar acesso a um arquivo no compartilhamento, você deve negar \\\Server\Share\File, X:\File e todos os caminhos que acessa o arquivo.

-   Um <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> podem encerrar uma movimentação de pilha antes de atingir o Deny ou PermitOnly.

-   Se um Deny tem qualquer efeito, ou seja, quando um chamador tiver uma permissão que está bloqueada por Deny, o chamador pode acessar o recurso protegido diretamente, ignorando a negar. Da mesma forma, se o chamador não tem a permissão negada, a movimentação da pilha falhará sem a negar.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Qualquer uso das seguintes ações de segurança fará com que uma violação. Para corrigir uma violação, não use essas ações de segurança.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprima um aviso nessa regra somente depois de concluir uma revisão de segurança.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra algumas limitações de negar.

 A seguinte biblioteca contém uma classe que tem dois métodos que são idênticos, exceto para as demandas de segurança que protegem-los.

 [!code-csharp[FxCop.Security.PermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PermitAndDeny/cs/FxCop.Security.PermitAndDeny.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir demonstra os efeitos de negar sobre os métodos protegidos da biblioteca.

 [!code-csharp[FxCop.Security.TestPermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestPermitAndDeny/cs/FxCop.Security.TestPermitAndDeny.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Por demanda: Deny do chamador não tem nenhum efeito sob demanda com a permissão declarada. ** 
 **LinkDemand: Deny do chamador não tem nenhum efeito em LinkDemand com a permissão declarada.** 
 **LinkDemand: Deny do chamador não tem nenhum efeito com o código protegido por LinkDemand.** 
 **LinkDemand: negar esta não tem nenhum efeito com o código protegido por LinkDemand.**
## <a name="see-also"></a>Consulte também
 <xref:System.Security.CodeAccessPermission.PermitOnly%2A?displayProperty=fullName> <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
 <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName>
 <xref:System.Security.IStackWalk.PermitOnly%2A?displayProperty=fullName>
 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [substituindo verificações de segurança](http://msdn.microsoft.com/en-us/4acdeff5-fc05-41bf-8505-7387cdbfca28) [usando o método PermitOnly](http://msdn.microsoft.com/en-us/8c7bdb7f-882f-45b7-908c-6cbaa1767649)



