---
title: 'Como: usar marcadores de texto | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - using text markers
ms.assetid: 76eed51c-eecb-4579-823e-13df2f0526b9
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1a3b766e4eacc04bbf4d4a8e4c022484d452954f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49820870"
---
# <a name="how-to-use-text-markers"></a>Como: usar marcadores de texto
Marcadores de texto podem ser aplicadas para editar um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer> objeto.  
  
## <a name="procedures"></a>Procedimentos  
  
### <a name="to-apply-text-markers"></a>Para aplicar os marcadores de texto  
  
1.  Obtenha uma instância do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> classe.  
  
    > [!NOTE]
    >  O editor de núcleo aplica automaticamente os marcadores de texto padrão para qualquer documento que ela está editando, e não deve ser necessário aplicar marcadores de texto padrão explicitamente.  
  
2.  Obter uma ID de tipo de marcador do marcador que você está interessado, chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager.GetRegisteredMarkerTypeID%2A> método com o `GUID` do marcador de texto que você deseja trabalhar com.  
  
    > [!NOTE]
    >  Não use o `GUID` do VSPackage ou do serviço que fornece o marcador de texto.  
  
3.  Use a ID de tipo de marcador é obtida chamando o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager.GetRegisteredMarkerTypeID%2A> método como um parâmetro ao chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> método ou o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> método para aplicar um marcador de texto para uma determinada região do texto.  
  
### <a name="to-add-features-to-text-markers"></a>Para adicionar recursos a marcadores de texto  
  
1. Ele pode ser desejável para adicionar recursos adicionais a um marcador de texto, como dicas de ferramenta, um menu de contexto especial ou manipulador para circunstâncias especiais. Para fazer isso:  
  
2. Criar um objeto que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface.  
  
3. Se a funcionalidade adicional for desejada, implemente a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx>e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced> interfaces no mesmo objeto que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface.  
  
4. Passe o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface que você cria, para a chamada para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> método ou o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> método usado para aplicar o marcador de texto para uma determinada região do texto.  
  
5. Ao adicionar o suporte do menu de contexto a uma região de marcador de texto é necessário criar o menu.  
  
    Para obter mais informações sobre como criar um contexto menu, consulte [menus de contexto](../extensibility/context-menus.md).  
  
6. O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ambiente chama os métodos das interfaces fornecidas, tais como o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.GetTipText%2A> método, ou o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.ExecMarkerCommand%2A> método conforme necessário.  
  
## <a name="see-also"></a>Consulte também  
 [Usar marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [Como: adicionar marcadores de texto padrão](../extensibility/how-to-add-standard-text-markers.md)   
 [Como: criar marcadores de texto personalizado](../extensibility/how-to-create-custom-text-markers.md)   
 [Como: implementar o marcador de erros](../extensibility/how-to-implement-error-markers.md)