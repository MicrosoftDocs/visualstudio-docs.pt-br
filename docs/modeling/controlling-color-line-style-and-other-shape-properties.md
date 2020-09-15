---
title: Controlar cor, estilo de linha e outras propriedades de forma
description: Fornece informações sobre como controlar as propriedades de forma, como cor e estilo da linha.
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 759c7def23cf8ac0df33a75d25eb5bcbcf44b209
ms.sourcegitcommit: a18c7e9b367c2f92f6e54c3eaef442775d457667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90100421"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>Controlando cor, estilo de linha e outras propriedades de formas

Algumas propriedades de forma, como Color, podem ser ' expostas '. Ou seja, as propriedades podem ser vinculadas a uma propriedade de domínio da forma. Outras pessoas precisam ser controladas diretamente.

## <a name="exposing-a-property"></a>Expondo uma propriedade
 Algumas propriedades de forma, como Color, podem ser vinculadas ao valor de uma propriedade de domínio.

 Na definição de DSL, selecione uma forma, um conector ou uma classe de diagrama. No menu do clique com o botão direito do mouse, escolha **Adicionar exposto**e escolha a propriedade desejada, como cor de preenchimento.

 A forma agora tem uma propriedade Domain que pode ser definida no código do programa ou como um usuário.

## <a name="dynamically-updating-an-exposed-property"></a>Atualizando dinamicamente uma propriedade exposta
 Normalmente, você deseja tornar a propriedade exposta dependente de outra propriedade. Por exemplo, talvez você queira que uma forma fique vermelha sempre que uma propriedade de domínio específica for menor que zero. Para fazer essa dependência, crie uma [regra](../modeling/rules-propagate-changes-within-the-model.md). Por exemplo:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
namespace ExampleNamespace
{
 // Attribute associates the rule with class:
 [RuleOn(typeof(CarShape), FireTime = TimeToFire.TopLevelCommit)]
 // The rule is a class derived from one of the abstract rules:
 class CarShapeAddRule : AddRule
 {
 // Override the abstract method:
 public override void ElementAdded(ElementAddedEventArgs e)
 {
 base.ElementAdded(e);
 CarShape shape = e.ModelElement as CarShape;
 Store store = shape.Store;
 // Ignore this call if we're currently loading a model:
 if (store.TransactionManager.CurrentTransaction.IsSerializing)
  return;
 Car car = shape.ModelElement as Car;
 // Code here propagates change as required - for example:
 shape.FillColor = car.Somebool ? System.Drawing.Color.Red : System.Drawing.Color.Green;
 }
}
 // The rule must be registered:
 public partial class ExampleDomainModel
 {
 protected override Type[] GetCustomDomainModelTypes()
 {
  List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());
  types.Add(typeof(CarShapeAddRule));
  // If you add more rules, list them here.
  return types.ToArray();
 }
 }
}
```