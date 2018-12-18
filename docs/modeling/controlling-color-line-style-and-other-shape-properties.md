---
title: Controlando cor, estilo de linha e outras propriedades de formas
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: bfe0cbdda1b3eaa7d1afc936c7dbba75df6da07b
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31947161"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>Controlando cor, estilo de linha e outras propriedades de formas
Algumas propriedades de forma, como cor pode ser 'exposta' - ou seja, vinculada a uma propriedade de domínio da forma. Outras pessoas precisam ser controlada diretamente.

## <a name="exposing-a-property"></a>Expor uma propriedade
 Algumas propriedades de forma como cores podem ser vinculadas ao valor de uma propriedade de domínio.

 Na definição de DSL, selecione uma forma, o conector ou a classe do diagrama. Em seu menu de contexto, escolha **adicionar expostos**e, em seguida, escolha a propriedade desejadas, como cor de preenchimento.

 A forma agora tem uma propriedade de domínio que você pode definir no código do programa, ou como um usuário.

## <a name="dynamically-updating-an-exposed-property"></a>Atualização dinâmica de uma propriedade exposta
 Normalmente você deseja fazer com que a propriedade exposta dependente de outra propriedade. Por exemplo, talvez seja uma forma para ativar vermelho sempre que uma propriedade de domínio específico é menor que zero. Para fazer essa dependência, crie um [regra](../modeling/rules-propagate-changes-within-the-model.md). Por exemplo:

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