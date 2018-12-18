---
title: Acessando as camadas de texto usando a API herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text layers
ms.assetid: 2258fcdd-38d1-479d-b8f8-1d4e6525f72c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1506c035fca0cdaf4916d93daad8ced7550bfe6e
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39078661"
---
# <a name="access-text-layers-by-using-the-legacy-api"></a>Camadas de texto de acesso usando a API herdada
Uma camada de texto normalmente encapsula algum aspecto do layout de texto. Por exemplo, uma camada de "uma função no tempo" oculta o texto antes e depois de uma função que contém o cursor (ponto de inserção de texto).  
  
 Uma camada de texto reside entre um buffer e uma exibição, e ele modifica a maneira como o modo de exibição vê o conteúdo do buffer.  
  
## <a name="text-layer-information"></a>Informações de camada de texto  
 A lista a seguir descreve como as camadas de texto funcionam no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]:  
  
-   O texto em uma camada de texto pode ser adornado com marcadores e coloração de sintaxe.  
  
-   No momento, você não pode implementar suas próprias camadas.  
  
-   Uma camada expõe <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer>, que é derivado de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>. O buffer de texto em si também é implementado como uma camada, que permite que um modo de exibição lidar polimorficamente com camadas subjacentes.  
  
-   Qualquer número de camadas pode estar entre o modo de exibição e o buffer. Cada camada lida apenas com a camada abaixo dela, e o modo de exibição lida principalmente com a camada superior. (O modo de exibição tem algumas informações sobre o buffer.)  
  
-   Uma camada pode afetar somente camadas que estão abaixo dela. Ele não pode afetar as camadas acima dele, além da origem de eventos padrão.  
  
-   No editor de texto oculto, texto sintético e quebra automática de linha são implementados como camadas. Você pode implementar texto oculto e sintético sem interagir diretamente com as camadas. Para obter mais informações, consulte [estrutura de tópicos em um serviço de linguagem herdado](../extensibility/internals/outlining-in-a-legacy-language-service.md) e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSyntheticTextSession>.  
  
-   Cada camada de texto tem seu próprio sistema de coordenadas de local que é exposto por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer> interface. A camada de quebra automática de linha, por exemplo, pode conter duas linhas enquanto o buffer de texto subjacente pode conter apenas uma linha.  
  
-   O modo de exibição se comunica com camadas por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView> interface. Use esta interface para reconciliar as coordenadas de exibição com as coordenadas de buffer.  
  
-   Qualquer camada, como a camada de texto sintéticos que se origina o texto deve fornecer uma implementação local do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CreateTrackingPoint%2A>.  
  
-   Além disso <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer>, uma camada de texto deve implementar <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> e acionar os eventos no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLinesEvents> interface.  
  
## <a name="see-also"></a>Consulte também  
 [Coloração de sintaxe em editores personalizados](../extensibility/syntax-coloring-in-custom-editors.md)   
 [Usar marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [Personalizar menus e controles de editor usando a API herdada](../extensibility/customizing-editor-controls-and-menus-by-using-the-legacy-api.md)