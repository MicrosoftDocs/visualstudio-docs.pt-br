---
title: 'CA2112: os tipos protegidos não devem expor campos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2112
- SecuredTypesShouldNotExposeFields
helpviewer_keywords:
- SecuredTypesShouldNotExposeFields
- CA2112
ms.assetid: 9eb13a78-3487-49f2-81d1-3c3866db132f
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4267b4f55f78106a4d1e8f3b2f9b296be9ddf618
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546530"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112: Tipos protegidos não devem expor campos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém campos públicos e é protegido por [demandas de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d).

## <a name="rule-description"></a>Descrição da Regra
 Se tiver acesso a uma instância de um tipo protegido por uma exigência de vínculo, o código não precisará atender à exigência de vínculo para acessar os campos do tipo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne os campos não públicos e adicione propriedades públicas ou métodos que retornam os dados do campo. As verificações de segurança de LinkDemand em tipos protegem o acesso às propriedades e aos métodos do tipo. No entanto, a segurança de acesso ao código não se aplica a campos.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para problemas de segurança e para um bom design, você deve corrigir violações tornando os campos públicos não públicos. Você poderá suprimir um aviso dessa regra se o campo não mantiver informações que devem permanecer protegidas e se você não depender do conteúdo do campo.

## <a name="example"></a>Exemplo
 O exemplo a seguir é composto de um tipo de biblioteca ( `SecuredTypeWithFields` ) com campos não seguros, um tipo ( `Distributor` ) que pode criar instâncias do tipo de biblioteca e as instâncias de passes incorretas para os tipos não têm permissão para criá-las e o código do aplicativo que pode ler os campos de uma instância, embora não tenha a permissão que protege o tipo.

 O código de biblioteca a seguir viola a regra.

 [!code-csharp[FxCop.Security.LinkDemandOnField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LinkDemandOnField/cs/FxCop.Security.LinkDemandOnField.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo não pode criar uma instância devido à demanda de link que protege o tipo protegido. A classe a seguir permite que o aplicativo obtenha uma instância do tipo protegido.

 [!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LDOnFieldsDistributor/cs/FxCop.Security.LDOnFieldsDistributor.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir ilustra como, sem permissão para acessar métodos de um tipo protegido, o código pode acessar seus campos.

 [!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestLinkDemandOnFields/cs/FxCop.Security.TestLinkDemandOnFields.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Criando uma instância de SecuredTypeWithFields.** 
 **Campos de tipo protegido: 22, 33** 
 **Alterando campo do tipo protegido...** 
 **Campos de objeto em cache: 99, 33**
## <a name="related-rules"></a>Regras relacionadas
 [CA1051: Não declarar campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>Consulte Também
 [Dados e modelagem de](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) [demandas de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
