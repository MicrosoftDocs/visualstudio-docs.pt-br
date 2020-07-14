---
title: 'CA2212: não marcar componentes atendidos com WebMethod | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
helpviewer_keywords:
- CA2212
- DoNotMarkServicedComponentsWithWebMethod
ms.assetid: 774bc55d-e588-48ee-8f38-c228580feca2
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a3c707fef5562b932b6232300131f6e6e6efef6a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534557"
---
# <a name="ca2212-do-not-mark-serviced-components-with-webmethod"></a>CA2212: Não marcar componentes atendidos com WebMethod
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotMarkServicedComponentsWithWebMethod|
|CheckId|CA2212|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um método em um tipo que herda de <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName> é marcado com <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName> .

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.Web.Services.WebMethodAttribute>aplica-se a métodos em um serviço Web XML que foram criados usando ASP.NET; Ele torna o método que possa ser chamado por clientes Web remotos. O método e a classe devem ser públicos e em execução em um aplicativo Web ASP.NET. <xref:System.EnterpriseServices.ServicedComponent>os tipos são hospedados por aplicativos COM+ e podem usar serviços COM+. <xref:System.Web.Services.WebMethodAttribute>Não é aplicado a <xref:System.EnterpriseServices.ServicedComponent> tipos porque eles não se destinam aos mesmos cenários. Especificamente, a adição do atributo ao <xref:System.EnterpriseServices.ServicedComponent> método não torna o método que possa ser chamado por clientes Web remotos. Como <xref:System.Web.Services.WebMethodAttribute> e um <xref:System.EnterpriseServices.ServicedComponent> método tem comportamentos conflitantes e requisitos de contexto e fluxo de transações, o comportamento do método estará incorreto em alguns cenários.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o atributo do <xref:System.EnterpriseServices.ServicedComponent> método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. Não há cenários em que a combinação desses elementos esteja correta.

## <a name="see-also"></a>Consulte Também
 <xref:System.EnterpriseServices.ServicedComponent?displayProperty=fullName> <xref:System.Web.Services.WebMethodAttribute?displayProperty=fullName>
