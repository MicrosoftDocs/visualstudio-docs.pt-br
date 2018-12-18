---
title: 'CA1405: Tipos de base de tipo visível COM devem ser visíveis em COM | Microsoft Docs'
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
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
helpviewer_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
ms.assetid: a762ea2f-5285-4f73-bfb9-9eb10aea4290
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ee4c7a501a7c48118285ff37844af856cf7b4395
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49840500"
---
# <a name="ca1405-com-visible-type-base-types-should-be-com-visible"></a>CA1405: os tipos base de tipo visível em COM devem ser visíveis em COM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ComVisibleTypeBaseTypesShouldBeComVisible|
|CheckId|CA1405|
|Categoria|Microsoft.Interoperability|
|Alteração Significativa|DependsOnFix|

## <a name="cause"></a>Causa
 Um tipo visível do modelo de objeto de componente (COM) deriva de um tipo que não é visível do COM.

## <a name="rule-description"></a>Descrição da Regra
 Quando um tipo visível do COM adiciona membros em uma nova versão, ele deve obedecer as diretrizes rígidas para evitar a interrupção de clientes COM associados para a versão atual. Um tipo que é invisível para COM supõe que ele não precisa seguir estas regras de controle de versão de COM quando ele adiciona novos membros. No entanto, se um visíveis em COM tipo deriva de tipo invisível COM e expõe uma interface de classe de <xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName> ou <xref:System.Runtime.InteropServices.ClassInterfaceType> (padrão), todos os membros públicos do tipo base (a menos que eles são especificamente marcados COM como invisíveis, qual seria redundante) são exposto COM. Se o tipo base adiciona novos membros em uma versão posterior, podem interromper todos os clientes COM associados à interface de classe do tipo derivado. Tipos visíveis no COM devem derivar somente de tipos visíveis no COM para reduzir a chance de interromper os clientes COM.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, verifique os tipos base visíveis no COM ou o tipo derivado COM invisível.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Interoperability.ComBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/cs/FxCop.Interoperability.ComBaseTypes.cs#1)]
 [!code-vb[FxCop.Interoperability.ComBaseTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/vb/FxCop.Interoperability.ComBaseTypes.vb#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute?displayProperty=fullName> [Introdução à Interface de classe](http://msdn.microsoft.com/en-us/733c0dd2-12e5-46e6-8de1-39d5b25df024) [interoperação com código não gerenciado](http://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)



