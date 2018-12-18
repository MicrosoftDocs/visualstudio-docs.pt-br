---
title: 'CA2214: não chamar métodos substituíveis em construtores'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotCallOverridableMethodsInConstructors
- CA2214
helpviewer_keywords:
- CA2214
- DoNotCallOverridableMethodsInConstructors
ms.assetid: 335b57ca-a6e8-41b4-a20e-57ee172c97c3
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: ddc827e77b37de6490cb4bee081748f317865b57
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45549554"
---
# <a name="ca2214-do-not-call-overridable-methods-in-constructors"></a>CA2214: não chamar métodos substituíveis em construtores

|||
|-|-|
|NomeDoTipo|DoNotCallOverridableMethodsInConstructors|
|CheckId|CA2214|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

O construtor de um tipo sem lacre chama um método virtual definido na sua classe.

## <a name="rule-description"></a>Descrição da regra

Quando um método virtual é chamado, o tipo real que executa o método não está selecionado até o tempo de execução. Quando um construtor chama um método virtual, é possível que o construtor para a instância que invoca o método não executado.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, não chame métodos virtuais de um tipo de dentro de construtores do tipo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima um aviso nessa regra. O construtor deve ser reformulado para eliminar a chamada para o método virtual.

## <a name="example"></a>Exemplo

O exemplo a seguir demonstra o efeito de violação dessa regra. O aplicativo de teste cria uma instância de `DerivedType`, que faz com que sua classe base (`BadlyConstructedType`) construtor ser executado. `BadlyConstructedType`do construtor incorretamente chama o método virtual `DoSomething`. Como mostra a saída, `DerivedType.DoSomething()` executa e faz, portanto, antes de `DerivedType`do construtor é executado.

[!code-csharp[FxCop.Usage.CtorVirtual#1](../code-quality/codesnippet/CSharp/ca2214-do-not-call-overridable-methods-in-constructors_1.cs)]
[!code-vb[FxCop.Usage.CtorVirtual#1](../code-quality/codesnippet/VisualBasic/ca2214-do-not-call-overridable-methods-in-constructors_1.vb)]

Este exemplo gera a seguinte saída:

```txt
Calling base ctor.
Derived DoSomething is called - initialized ? No
Calling derived ctor.
```