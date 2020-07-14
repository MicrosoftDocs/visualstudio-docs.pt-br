---
title: 'CA2214: não chamar métodos substituíveis em construtores | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotCallOverridableMethodsInConstructors
- CA2214
helpviewer_keywords:
- CA2214
- DoNotCallOverridableMethodsInConstructors
ms.assetid: 335b57ca-a6e8-41b4-a20e-57ee172c97c3
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ad467e880b3281a75db2627108af0e0b2f90ea99
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534453"
---
# <a name="ca2214-do-not-call-overridable-methods-in-constructors"></a>CA2214: Não chamar métodos substituíveis em construtores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotCallOverridableMethodsInConstructors|
|CheckId|CA2214|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 O construtor de um tipo sem lacre chama um método virtual definido em sua classe.

## <a name="rule-description"></a>Descrição da Regra
 Quando um método virtual é chamado, o tipo real que executa o método não é selecionado até o tempo de execução. Quando um construtor chama um método virtual, é possível que o construtor da instância que invoca o método não tenha sido executado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, não chame os métodos virtuais de um tipo de dentro dos construtores do tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra. O construtor deve ser reprojetado para eliminar a chamada para o método virtual.

## <a name="example"></a>Exemplo
 O exemplo a seguir demonstra o efeito de violar essa regra. O aplicativo de teste cria uma instância do `DerivedType` , que faz com que seu construtor de classe base ( `BadlyConstructedType` ) seja executado. `BadlyConstructedType`o construtor do chama incorretamente o método virtual `DoSomething` . Como a saída mostra, `DerivedType.DoSomething()` executa e faz isso antes `DerivedType` da execução do construtor.

 [!code-csharp[FxCop.Usage.CtorVirtual#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CtorVirtual/cs/FxCop.Usage.CtorVirtual.cs#1)]
 [!code-vb[FxCop.Usage.CtorVirtual#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CtorVirtual/vb/FxCop.Usage.CtorVirtual.vb#1)]

 Este exemplo gerencia a seguinte saída.

 **Chamando o construtor base.** 
 **Doitem derivado é chamado-Initialized? Nenhum** 
 **Construtor derivado de chamada.**
