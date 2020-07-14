---
title: 'CA2107: revisar a negação e permitir apenas o uso | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2107
- ReviewDenyAndPermitOnlyUsage
helpviewer_keywords:
- ReviewDenyAndPermitOnlyUsage
- CA2107
ms.assetid: 366f4a56-ae93-4882-81d0-bd0a55ebbc26
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7f273ea5f58babf7a0c04f6b0758732d43aab7db
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547765"
---
# <a name="ca2107-review-deny-and-permit-only-usage"></a>CA2107: Examinar uso de deny e permit only
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ReviewDenyAndPermitOnlyUsage|
|CheckId|CA2107|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método contém uma verificação de segurança que especifica a ação de segurança PermitOnly ou Deny.

## <a name="rule-description"></a>Descrição da Regra
 O [uso do método PermitOnly e das](https://msdn.microsoft.com/8c7bdb7f-882f-45b7-908c-6cbaa1767649) <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName> ações de segurança deve ser usado somente por aqueles que têm um conhecimento avançado de [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] segurança. O código que usa essas ações de segurança deve passar por uma revisão de segurança.

 Deny altera o comportamento padrão da movimentação de pilha que ocorre em resposta a uma demanda de segurança. Ele permite que você especifique permissões que não devem ser concedidas durante o método de negação, independentemente das permissões reais dos chamadores na pilha de chamadas. Se a movimentação da pilha detectar um método protegido por Deny e se a permissão solicitada estiver incluída nas permissões negadas, a movimentação da pilha falhará. PermitOnly também altera o comportamento padrão da movimentação da pilha. Ele permite que o código especifique somente as permissões que podem ser concedidas, independentemente das permissões dos chamadores. Se a movimentação da pilha detectar um método protegido por PermitOnly e se a permissão solicitada não estiver incluída nas permissões especificadas pelo PermitOnly, a movimentação da pilha falhará.

 O código que depende dessas ações deve ser avaliado cuidadosamente quanto às vulnerabilidades de segurança devido à sua utilidade limitada e ao comportamento sutil. Considere o seguinte:

- As [demandas de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) não são afetadas por Deny ou PermitOnly.

- Se o Deny ou PermitOnly ocorrer no mesmo quadro de pilha que a demanda que causa a movimentação da pilha, as ações de segurança não terão nenhum efeito.

- Os valores que são usados para construir permissões baseadas em caminho normalmente podem ser especificados de várias maneiras. Negar acesso a uma forma do caminho não nega o acesso a todos os formulários. Por exemplo, se um compartilhamento de arquivos \\ \Server\Share for mapeado para uma unidade de rede X:, para negar acesso a um arquivo no compartilhamento, você deverá negar \\ \Server\Share\File, X:\File e todos os outros caminhos que acessam o arquivo.

- Um <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> pode encerrar uma movimentação de pilha antes que Deny ou PermitOnly seja atingido.

- Se uma negação tiver algum efeito, ou seja, quando um chamador tiver uma permissão bloqueada pela negação, o chamador poderá acessar o recurso protegido diretamente, ignorando a negação. Da mesma forma, se o chamador não tiver a permissão negada, a movimentação da pilha falhará sem a negação.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Qualquer uso dessas ações de segurança resultará em uma violação. Para corrigir uma violação, não use essas ações de segurança.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Suprimir um aviso desta regra somente depois de concluir uma revisão de segurança.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra algumas limitações de Deny.

 A biblioteca a seguir contém uma classe que tem dois métodos que são idênticos, exceto pelas demandas de segurança que os protegem.

 [!code-csharp[FxCop.Security.PermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PermitAndDeny/cs/FxCop.Security.PermitAndDeny.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir demonstra os efeitos de Deny nos métodos protegidos da biblioteca.

 [!code-csharp[FxCop.Security.TestPermitAndDeny#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestPermitAndDeny/cs/FxCop.Security.TestPermitAndDeny.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Demanda: a negação do chamador não tem nenhum efeito sob demanda com a permissão declarada.** 
 **LinkDemand: Deny do chamador não tem efeito em LinkDemand com a permissão declarada.** 
 **LinkDemand: Deny do chamador não tem efeito com código protegido por LinkDemand.** 
 **LinkDemand: essa negação não tem efeito com código protegido por LinkDemand.**
## <a name="see-also"></a>Consulte Também
 <xref:System.Security.CodeAccessPermission.PermitOnly%2A?displayProperty=fullName> <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
 <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName>
 <xref:System.Security.IStackWalk.PermitOnly%2A?displayProperty=fullName>
 [Diretrizes de codificação seguras](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [substituindo verificações de segurança](https://msdn.microsoft.com/4acdeff5-fc05-41bf-8505-7387cdbfca28) [usando o método PermitOnly](https://msdn.microsoft.com/8c7bdb7f-882f-45b7-908c-6cbaa1767649)
