---
title: Usar marcadores de texto com a API herdada | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - text markers
ms.assetid: 937a0b19-1216-45d5-a7ad-4fe1d6f73097
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 62b77180858b40bf2620eaed284fa35b9a48288a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49835924"
---
# <a name="using-text-markers-with-the-legacy-api"></a>Usar marcadores de texto com a API herdada
Um marcador de texto é um intervalo de texto em um buffer que pode afetar a exibição de flutuante e o comportamento de uma região de texto. Marcadores incluem pontos de interrupção, indicadores, sublinhados ondulados e regiões de somente leitura. Marcadores de texto são basicamente diferentes das cores de sintaxe. Coloração de sintaxe é uma maneira rápida de se comunicar a sintaxe de linguagem que está associada uma região de texto. Coloração de sintaxe geralmente é solicitada ao Windows redesenha a tela, quando a velocidade é importante. Coloração de sintaxe altera apenas a cor do texto. Marcadores de texto podem alterar muitas outras propriedades de texto. Marcadores de texto podem "flutuar" e aplicar um comportamento especial e colorir.  
  
 Devido à sobrecarga de desempenho associada com marcadores de texto, não crie muitos marcadores para seus buffers de texto. Cada marcador é atualizado toda vez que um usuário edita o conteúdo do buffer.  
  
> [!NOTE]
>  Os usuários podem alterar a cor de um tipo de marcador visíveis, mas não sua forma e estilo. Para obter mais informações, consulte [fontes e cores, ambiente, caixa de diálogo Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
| Título | Descrição |
| - | - |
| [Como adicionar marcadores de texto padrão](../extensibility/how-to-add-standard-text-markers.md) | Descreve como adicionar um tipo de marcador de texto padrão fornecido pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo para uma exibição de texto. |
| [Como implementar o marcador de erros](../extensibility/how-to-implement-error-markers.md) | Descreve como implementar uma instância da [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] marcador que é usado para indicar erros usando ondulados vermelhos. |
| [Como criar marcadores de texto personalizados](../extensibility/how-to-create-custom-text-markers.md) | Descreve como criar e adicionar um tipo de marcador de texto personalizado a uma exibição de texto. |
| [Como usar marcadores de texto](../extensibility/how-to-use-text-markers.md) | Explica como adicionar marcadores de texto. |
| [Dentro do editor principal](../extensibility/inside-the-core-editor.md) | Descreve os recursos do editor de núcleo e fornece detalhes sobre como personalizar o editor de núcleo. |
| [Recursos do Editor](https://msdn.microsoft.com/library/bdac940d-1f14-4019-a01f-fd0bb3dc7198) | Descreve os recursos disponíveis no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo. |
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType>  
 Fornece um mecanismo uniforme para obter informações sobre um tipo de marcador de texto específico, se predefinidos pelo editor ou registrados por um VSPackage.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLineMarker>  
 Fornece acesso a e ajusta a posição de um marcador de texto em um buffer de texto usando as coordenadas bidimensionais.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker>  
 Fornece métodos para gerenciar os marcadores de texto.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>  
 Fornece os retornos de chamada para o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE e outros processos que são usados para ajustar um marcador de texto.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientAdvanced>  
 Estende a funcionalidade que está disponível por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface fornecendo adicionais retornos de chamada.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClientEx>  
 Estende a funcionalidade que está disponível por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> interface fornecendo adicionais retornos de chamada.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerColorSet>  
 Permite que um tipo de marcador determinar se outros tipos de marcador compartilham o mesmo conjunto de cores.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider>  
 Fornece o contexto para os marcadores de texto no editor de núcleo. Para cada tipo de marcador de texto que está no editor de núcleo, o IDE cria um separado <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerContextProvider> objeto.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerGlyphDropHandler>  
 Um manipulador que é fornecido para os marcadores cujos glifos dá suporte à edição de arrastar e soltar. Um glifo é um ícone que indica a posição de um marcador.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerTypeProvider>  
 Retorna um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPackageDefinedTextMarkerType> interface de um serviço que fornece um texto marcadores para outros VSPackages.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStreamMarker>  
 Fornece acesso a e ajusta a posição de um marcador de texto em um buffer de texto, usando coordenadas unidimensionais. Se for possível, não use essa interface.