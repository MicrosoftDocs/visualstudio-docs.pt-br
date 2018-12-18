---
title: 'CA2107: revisar uso de deny e permit only'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2107
- ReviewDenyAndPermitOnlyUsage
helpviewer_keywords:
- ReviewDenyAndPermitOnlyUsage
- CA2107
ms.assetid: 366f4a56-ae93-4882-81d0-bd0a55ebbc26
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 4324805c90c3a0f1b8dbfddcdfe277c5c8a2fd05
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49868034"
---
# <a name="ca2107-review-deny-and-permit-only-usage"></a>CA2107: revisar uso de deny e permit only

|||
|-|-|
|NomeDoTipo|ReviewDenyAndPermitOnlyUsage|
|CheckId|CA2107|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método contém uma verificação de segurança que especifica a ação de segurança PermitOnly ou Deny.

## <a name="rule-description"></a>Descrição da regra
 O <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName> ação de segurança deve ser usada apenas por aqueles que tenham um conhecimento avançado de segurança do .NET Framework. O código que usa essas ações de segurança deve passar por uma revisão de segurança.

 Negar altera o comportamento padrão, a movimentação de pilha ocorre em resposta a uma exigência de segurança. Ele permite que você especifique as permissões que não devem ser concedidas para a duração do método negando, independentemente das permissões reais dos chamadores na pilha de chamadas. Se a movimentação da pilha detecta um método que é protegido por Negar e se a permissão exigida é incluída nas permissões negadas, a movimentação da pilha falha. PermitOnly também altera o comportamento padrão do exame da pilha. Ele permite que o código especificar somente as permissões que podem ser concedidas, independentemente das permissões dos chamadores. Se a movimentação da pilha detecta um método que é protegido pelo PermitOnly, e se a permissão exigida não está incluída nas permissões que são especificadas pela PermitOnly, a movimentação da pilha falha.

 Código que depende dessas ações deve ser avaliado cuidadosamente para vulnerabilidades de segurança devido à sua utilidade limitada e comportamento sutil. Considere o seguinte:

- [Demandas de link](/dotnet/framework/misc/link-demands) não são afetados por Deny ou PermitOnly.

- Se o Deny ou PermitOnly ocorre no quadro de pilha como a demanda que faz com que a movimentação da pilha, as ações de segurança não terão efeito.

- Valores que são usados para construir as permissões com base em caminho geralmente podem ser especificados de várias maneiras. Negar acesso a um formulário do caminho não nega acesso a todas as formas. Por exemplo, se um compartilhamento de arquivos \\\Server\Share é mapeado para uma unidade de rede x, para negar acesso a um arquivo no compartilhamento, você deve negar \\\Server\Share\File, X:\File e todos os caminhos que acessa o arquivo.

- Um <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> podem encerrar uma movimentação de pilha antes de atingir o Deny ou PermitOnly.

- Se um Deny tem qualquer efeito, ou seja, quando um chamador tiver uma permissão que está bloqueada por Deny, o chamador pode acessar o recurso protegido diretamente, ignorando a negar. Da mesma forma, se o chamador não tem a permissão negada, a movimentação da pilha falhará sem a negar.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Qualquer uso das seguintes ações de segurança fará com que uma violação. Para corrigir uma violação, não use essas ações de segurança.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Suprima um aviso nessa regra somente depois de concluir uma revisão de segurança.

## <a name="example-1"></a>Exemplo 1
 O exemplo a seguir demonstra algumas limitações de negar.

 A seguinte biblioteca contém uma classe que tem dois métodos que são idênticos, exceto para as demandas de segurança que protegem-los.

 [!code-csharp[FxCop.Security.PermitAndDeny#1](../code-quality/codesnippet/CSharp/ca2107-review-deny-and-permit-only-usage_1.cs)]

## <a name="example-2"></a>Exemplo 2
 O aplicativo a seguir demonstra os efeitos de negar sobre os métodos protegidos da biblioteca.

 [!code-csharp[FxCop.Security.TestPermitAndDeny#1](../code-quality/codesnippet/CSharp/ca2107-review-deny-and-permit-only-usage_2.cs)]

Este exemplo gera a seguinte saída:

```txt
Demand: Caller's Deny has no effect on Demand with the asserted permission.
LinkDemand: Caller's Deny has no effect on LinkDemand with the asserted permission.
LinkDemand: Caller's Deny has no effect with LinkDemand-protected code.
LinkDemand: This Deny has no effect with LinkDemand-protected code.
```

## <a name="see-also"></a>Consulte também

- <xref:System.Security.CodeAccessPermission.PermitOnly%2A?displayProperty=fullName>
- <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>
- <xref:System.Security.CodeAccessPermission.Deny%2A?displayProperty=fullName>
- <xref:System.Security.IStackWalk.PermitOnly%2A?displayProperty=fullName>
- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines)