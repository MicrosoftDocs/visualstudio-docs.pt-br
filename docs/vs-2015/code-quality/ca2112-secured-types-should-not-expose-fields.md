---
title: 'CA2112: Tipos seguros não devem expor campos | Microsoft Docs'
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
- CA2112
- SecuredTypesShouldNotExposeFields
helpviewer_keywords:
- SecuredTypesShouldNotExposeFields
- CA2112
ms.assetid: 9eb13a78-3487-49f2-81d1-3c3866db132f
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a09093d05758d58828b9d7ca73223243252cb23c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49871453"
---
# <a name="ca2112-secured-types-should-not-expose-fields"></a>CA2112: os tipos seguros não devem expor campos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SecuredTypesShouldNotExposeFields|
|CheckId|CA2112|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido contém campos públicos e é protegido por um [demandas de Link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d).

## <a name="rule-description"></a>Descrição da Regra
 Se tiver acesso a uma instância de um tipo protegido por uma exigência de vínculo, o código não precisará atender à exigência de vínculo para acessar os campos do tipo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, tornar os campos não públicos e adicione propriedades públicas nem os métodos que retornam os dados do campo. Verificações de segurança de LinkDemand em tipos de protegem o acesso a métodos e propriedades do tipo. No entanto, a segurança de acesso do código não se aplica aos campos.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para problemas de segurança e para um bom design, você deve corrigir violações fazendo não públicos campos públicos. Você pode suprimir um aviso nessa regra, se o campo não mantém informações que devem permanecer protegidas, e você não confiar no conteúdo do campo.

## <a name="example"></a>Exemplo
 O exemplo a seguir é composto de um tipo de biblioteca (`SecuredTypeWithFields`) com os campos não seguros, um tipo (`Distributor`) que pode criar instâncias do tipo biblioteca incorreta passa instâncias de tipos não tem permissão para criá-los e código de aplicativo pode ler os campos de uma instância mesmo que ele não tem a permissão que protege o tipo.

 O seguinte código de biblioteca viola a regra.

 [!code-csharp[FxCop.Security.LinkDemandOnField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LinkDemandOnField/cs/FxCop.Security.LinkDemandOnField.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo não é possível criar uma instância devido à exigência de vínculo que protege o tipo seguro. A classe a seguir permite que o aplicativo para obter uma instância do tipo seguro.

 [!code-csharp[FxCop.Security.LDOnFieldsDistributor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.LDOnFieldsDistributor/cs/FxCop.Security.LDOnFieldsDistributor.cs#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir ilustra como fazer isso, sem a permissão para acessar os métodos do tipo seguro, o código pode acessar seus campos.

 [!code-csharp[FxCop.Security.TestLinkDemandOnFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestLinkDemandOnFields/cs/FxCop.Security.TestLinkDemandOnFields.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **Criando uma instância de SecuredTypeWithFields. ** 
 **Campos de tipo segura: 22, 33**
**alterando o campo do tipo seguro... ** 
 **Campos de objeto armazenado em cache: 99, 33**
## <a name="related-rules"></a>Regras relacionadas
 [CA1051: não declarar campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>Consulte também
 [Demandas de link](http://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) [dados e modelagem](http://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)



