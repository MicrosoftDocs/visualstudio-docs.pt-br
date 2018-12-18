---
title: BoundsRules restringem o local e o tamanho de uma forma
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 104a74a38099286675a742ce9eea367d9eeabe84
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31944382"
---
# <a name="boundsrules-constrain-shape-location-and-size"></a>BoundsRules restringem o local e o tamanho de uma forma

Um *limites regra* é uma classe que define limites sobre o tamanho e o local de uma forma. Ele fornece um método que é chamado repetidamente enquanto um usuário está arrastando uma forma ou cantos ou lados de uma forma.

O exemplo a seguir restringe uma forma retangular para ser uma barra de tamanho fixo, horizontal ou vertical. Quando o usuário arrasta cantos ou lados, a estrutura de tópicos inverte entre as duas configurações permitidas de altura e largura.

Os limites de regra é uma classe derivada de <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules>. Uma instância da regra é criada na forma:

```csharp
using Microsoft.VisualStudio.Modeling.Diagrams; ...

public partial class BarShape
{
  /// <summary>
  /// Rule invoked when the user is resizing a shape.
  /// </summary>
  public override BoundsRules BoundsRules
  { get { return new BarBoundsRule(); } }
}

/// <summary>
/// Rule invoked when the user is changing a shape's outline.
/// Provides real-time mouse rubber-band feedback, so must work fast.
/// </summary>
public class BarBoundsRule: BoundsRules
{
  public override RectangleD GetCompliantBounds
     (ShapeElement shape, RectangleD proposedBounds)
  {
    double thickness = 0.1;
    if (proposedBounds.Height > proposedBounds.Width)
    {
      // There is a minimum width for a shape; the width
      // will actually be set to the lesser of
      // thickness and that minimum.
      return new RectangleD(proposedBounds.Location,
            new SizeD(thickness, proposedBounds.Height));
    }
    else
    {
      // There is a minimum height for a shape; the
      // height will actually be set to the lesser of
      // thickness and that minimum.
      return new RectangleD(proposedBounds.Location,
         new SizeD(proposedBounds.Width, thickness));
} } }
```

Observe que o local e o tamanho podem ser restringidas se desejar.

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules>
- [Responder e propagar alterações](../modeling/responding-to-and-propagating-changes.md)