---
title: BoundsRules restringem o local de forma e tamanho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, events
ms.assetid: 4d08e541-fc67-4e68-bf31-30d346aa2aa0
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: cb9d9c35f5600ee98d53863780d9f54c3eed53f4
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49253715"
---
# <a name="boundsrules-constrain-shape-location-and-size"></a>BoundsRules restringem o local e o tamanho de uma forma
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um *regra* é uma classe que define os limites no tamanho e local de uma forma. Ele fornece um método que é chamado repetidamente, enquanto um usuário está arrastando uma forma ou cantos ou lados de uma forma.  
  
 O exemplo a seguir restringe uma forma retangular para ser uma barra de tamanho fixo, horizontal ou vertical. Quando o usuário arrasta o cantos ou lados, a estrutura de tópicos inverte entre as duas configurações permitidas da altura e largura.  
  
 Os limites de regra é uma classe derivada de <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules>. Uma instância da regra é criada na forma:  
  
```  
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
  
 Observe que o local e o tamanho podem ser restrito se você quiser.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Modeling.Diagrams.BoundsRules>   
 [Respondendo a alterações e propagando-as](../modeling/responding-to-and-propagating-changes.md)



