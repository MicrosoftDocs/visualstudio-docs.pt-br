---
title: 'CA2133: Delegados devem associar a métodos com transparência consistente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2133
ms.assetid: a09672e2-63cb-4abd-9e8f-dff515e101ce
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a8a19a84336cc6452f663eb65429326b52268728
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386949"
---
# <a name="ca2133-delegates-must-bind-to-methods-with-consistent-transparency"></a>CA2133: Representantes devem ser associados a métodos com transparência consistente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DelegatesMustBindWithConsistentTransparency|
|CheckId|CA2133|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

> [!NOTE]
> Esse aviso só será aplicado ao código que está executando o CoreCLR (a versão do CLR que é específico para aplicativos Web do Silverlight).

## <a name="cause"></a>Causa
 Esse aviso é acionado em um método que associa um representante que é marcado com o <xref:System.Security.SecurityCriticalAttribute> para um método transparente ou marcado com o <xref:System.Security.SecuritySafeCriticalAttribute>. O aviso também é acionado em um método que associa um representante transparente ou de segurança crítica a um método crítico.

## <a name="rule-description"></a>Descrição da Regra
 Tipos de delegado e os métodos que elas se associam a devem ter uma transparência consistente. Delegados transparentes e crítico de segurança só podem ser associado a outros métodos transparentes ou de segurança crítica. Da mesma forma, delegados críticos só podem ser associado a métodos críticos. Essas regras de associação garantem que o único código que pode invocar um método por meio de um delegado pode ter também chamado o mesmo método diretamente. Por exemplo, regras de associação de impedir que o código transparente chamando código crítico diretamente por meio de um representante transparente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação esse aviso, altere a transparência do delegado ou do método que associa para que a transparência dos dois são equivalentes.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

### <a name="code"></a>Código
 [!code-csharp[FxCop.Security.CA2133.DelegatesMustBindWithConsistentTransparency#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2133.delegatesmustbindwithconsistenttransparency/cs/ca2133 - delegatesmustbindwithconsistenttransparency.cs#1)]
