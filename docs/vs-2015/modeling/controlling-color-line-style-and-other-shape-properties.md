---
title: Controlando cor, estilo de linha e outras propriedades de forma | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c06d0066-24aa-4c65-b91c-c2089b81ec8d
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: b5694e81721bcc16b13c1857a07072fcaef00a08
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49285474"
---
# <a name="controlling-color-line-style-and-other-shape-properties"></a>Controlando cor, estilo de linha e outras propriedades de formas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Algumas propriedades de forma, como cor pode ser 'exposta' – ou seja, vinculada a uma propriedade de domínio da forma. Outros têm a ser controlada diretamente.  
  
## <a name="exposing-a-property"></a>Expor uma propriedade  
 Algumas propriedades da forma como a cor podem ser vinculadas ao valor de uma propriedade de domínio.  
  
 Na definição de DSL, selecione uma forma, conector ou classe de diagrama. No menu de contexto, escolha **adicionar exposto**e, em seguida, escolha a propriedade desejada, como cor de preenchimento.  
  
 A forma agora tem uma propriedade de domínio que você pode definir no código do programa ou como um usuário.  
  
## <a name="dynamically-updating-an-exposed-property"></a>Atualização dinâmica de uma propriedade exposta  
 Normalmente você deseja tornar a propriedade exposta dependente de outra propriedade. Por exemplo, convém uma forma para ativar vermelho sempre que uma propriedade de domínio específico é menor que zero. Para tornar essa dependência, crie uma [regra](../modeling/rules-propagate-changes-within-the-model.md). Por exemplo:  
  
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



