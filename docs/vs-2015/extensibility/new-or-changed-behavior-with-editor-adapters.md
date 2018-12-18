---
title: Comportamento de novo ou alterado com adaptadores de Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - adapter behavior
ms.assetid: 5555b116-cfdb-4773-ba62-af80fda64abd
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: cac26a6aeca6985546bcd21aec6cf45d72164e8a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817393"
---
# <a name="new-or-changed-behavior-with-editor-adapters"></a>Comportamento de novo ou alterado com adaptadores de Editor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você estiver atualizando o código escrito em relação a versões anteriores do editor de núcleo do Visual Studio, e você planeja usar o editor adaptadores (ou correções) em vez de usar a nova API, você deve estar ciente das seguintes diferenças no comportamento dos adaptadores de editor em relação ao editor principal do anterior.  
  
## <a name="features"></a>Recursos  
  
#### <a name="using-setsite"></a>Usando SetSite()  
 Você deve chamar <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite.SetSite%2A> quando você criar buffers de texto, modos de exibição de texto e janelas de código antes de executar outras operações neles. No entanto, isso não é necessário se você usar o <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> criá-los, porque a chamada de métodos de Create () deste serviço propriamente ditos <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.SetSite%2A>.  
  
#### <a name="hosting-ivscodewindow-and-ivstextview-in-your-own-content"></a>Hospedagem IVsCodeWindow e IVsTextView em seu próprio conteúdo  
 Você pode hospedar os <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> em seu próprio conteúdo usando o modo de Win32 ou modo do WPF. No entanto, você deve ter em mente que há algumas diferenças nos dois modos.  
  
##### <a name="using-win32-and-wpf-versions-of-ivscodewindow"></a>Usando versões de IVsCodeWindow Win32 e WPF  
 Janela do editor de código é derivada de <xref:Microsoft.VisualStudio.Shell.WindowPane>, que implementa o Win32 mais antigas <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface, bem como o WPF novo <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane> interface. Você pode usar o <xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsWindowPane%23CreatePaneWindow%2A> método para criar um ambiente de hospedagem com base em HWND, ou o <xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsUIElementPane%23CreateUIElementPane%2A> método para criar um ambiente de hospedagem do WPF. O editor subjacente sempre usa o WPF, mas você pode criar o tipo de painel de janela que atenda aos seus requisitos de hospedagem, se você estiver inserindo este painel de janela diretamente no seu próprio conteúdo.  
  
##### <a name="using-win32-and-wpf-versions-of-ivstextview"></a>Usando versões de IVsTextView Win32 e WPF  
 Você pode definir um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> aos modos de Win32 ou WPF.  
  
 Quando uma fábrica de editor cria uma exibição de texto, por padrão, ele é hospedado dentro de um HWND e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A> retorna um HWND. Você não deve usar esse modo para inserir o editor dentro de um controle WPF.  
  
 Para definir uma exibição de texto para o modo do WPF, você deve chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.Initialize%2A> e passe <xref:Microsoft.VisualStudio.TextManager.Interop.TextViewInitFlags3> como um da inicialização sinalizadores no `InitView` parâmetro. Você pode obter o <xref:System.Windows.FrameworkElement> chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane.CreateUIElementPane%2A>.  
  
 Modo do WPF é diferente do modo do Win32 de duas maneiras. Em primeiro lugar, a exibição de texto pode ser hospedada em um contexto WPF. Você pode acessar o painel do WPF ao converter o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> à <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane> e chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElement.GetUIObject%2A>. Segundo, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A> ainda retorna um HWND, mas esse HWND que pode ser usado apenas para verificar sua posição e definir o foco. Você não deve usar esse HWND para responder a uma mensagem WM_PAINT, porque ele não afeta como o editor pinta a janela. Neste HWND está presente apenas para facilitar a transição para o novo editor de código por meio dos adaptadores. É altamente recomendável que você não deve usar `VIF_NO_HWND_SUPPORT` se seu componente requer um HWND para o trabalho, devido a limitações no HWND retornado de `GetWindowHandle` enquanto nesse modo.  
  
#### <a name="passing-arrays-as-parameters-in-native-code"></a>Passando matrizes como parâmetros em código nativo  
 Há muitos métodos no editor API herdado que têm parâmetros que incluem uma matriz e sua contagem. Os exemplos são:  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.AppendViewOnlyMarkerTypes%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.RemoveViewOnlyMarkerTypes%2A>  
  
 Se você estiver chamando esses métodos no código nativo, você deve passar apenas um elemento de cada vez. Se você passar em mais de um elemento, a chamada será rejeitada, devido a problemas com a implementação de interoperabilidade primário.  
  
 O problema é mais complexo com métodos como <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.SetIgnoreMarkerTypes%2A>. Sempre que esse método é chamado, limpa a lista anterior de tipos de marcador ignorados, portanto, não é possível simplesmente chamar esse método três vezes com três tipos de marcador diferente. A única solução é chamar esse método apenas em código gerenciado.  
  
#### <a name="threading"></a>Threading  
 Você sempre deve chamar o adaptador de buffer do thread de interface do usuário. O adaptador de buffer é um objeto gerenciado, o que significa que a chamada para ele no código gerenciado ignorarão marshaling COM e sua chamada não serão automaticamente controlada para o thread de interface do usuário.  Se você estiver chamando o adaptador de buffer de um thread em segundo plano, você deve usar <xref:System.Windows.Threading.Dispatcher.Invoke%2A> ou um método semelhante.  
  
#### <a name="lockbuffer-methods"></a>Métodos de LockBuffer  
 Todos os métodos de LockBuffer() foram preteridos. Os exemplos são:  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.LockBuffer%2A>  
  
#### <a name="commit-events"></a>Confirmação de eventos  
 Confirmar eventos não são suportados. Chamar um método que avisa que esses eventos faz com que o método retorne um código de falha.  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUndoRedoClusterWithCommitEvents>  
  
#### <a name="texteditorevents"></a>TextEditorEvents  
 O <xref:EnvDTE.TextEditorEvents> não são acionados em Commit (). Em vez disso, disparam em cada alteração de texto.  
  
#### <a name="text-markers"></a>Marcadores de texto  
 Você deve chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker.Invalidate%2A> em <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker> objetos quando você removê-los. Nas versões anteriores, é necessário apenas para os marcadores de versão.  
  
#### <a name="line-numbers"></a>Os números de linha  
 Para uma variedade de métodos em <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx>, números de linha correspondem aos números de linha de buffer subjacente, não números de linha que o fator na estrutura de tópicos e quebra automática, como no Visual Studio 2008.  
  
 Os métodos afetados incluem o seguinte (a lista não é exaustiva):  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.CenterLines%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetCaretPos%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetLineAndColumn%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetNearestPosition%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetPointOfLineColumn%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetTextStream%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWordExtent%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.PositionCaretForEditing%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.ReplaceTextOnLine%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetCaretPos%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetSelection%2A>  
  
-   <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetTopLine%2A>  
  
#### <a name="outlining"></a>Estrutura de tópicos  
 Os clientes do <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> verá somente essas regiões de estrutura de tópicos que foram adicionados usando <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>ou <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSessionEx.AddHiddenRegionsEx%2A>. Eles não verão regiões ad-hoc, porque eles não são adicionados por meio dos adaptadores do editor. Da mesma forma, esses clientes não verão adicionados por linguagens (incluindo c# e C++) que estão usando o novo editor de código em vez dos adaptadores de editor de regiões de estrutura de tópicos.  
  
#### <a name="line-heights"></a>Alturas de linha  
 No novo editor, linhas de texto podem ter alturas diferentes, dependendo do tamanho da fonte e transformações de linha possíveis que podem mover a linha em relação a outras linhas. A altura da linha retornada por métodos como <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetLineHeight%2A> é a altura de uma linha usando o tamanho da fonte padrão com nenhum transformações de linha aplicadas. Essa altura pode, ou pode não refletir a altura real de uma linha no modo de exibição.  
  
#### <a name="eventing-and-undo"></a>Eventos e desfazer  
 No novo editor, o modo de exibição continua a executar operações como renderização e acionando eventos continuamente, mesmo quando um cluster de desfazer está aberto. Esse comportamento é diferente das exibições herdadas que não realizar essas operações até após o fechamento do cluster de desfazer.  
  
#### <a name="intellisense"></a>IntelliSense  
  
-   O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.UpdateTipWindow%2A> método irá falhar se você passar em uma classe que não implementa <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextTipWindow2> ou <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow3>. Win32 personalizado pop-ups desenhado pelo proprietário não têm mais suporte.  
  
#### <a name="smarttags"></a>Marcas inteligentes  
 Não há suporte do adaptador de marcas inteligentes, criado com, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagData>, <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow>, e <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow2> interfaces.  
  
#### <a name="dte"></a>DTE  
 <xref:EnvDTE80.IncrementalSearch> Não foi implementado.  
  
## <a name="unimplemented-methods"></a>Métodos não implementados  
 Alguns métodos não foram implementados no adaptador de buffer de texto, adaptador de exibição de texto e adaptador de camada de texto.  
  
|Interface|Não implementado|  
|---------------|---------------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|`Reload(false)` Não foi implementado.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.EnumSpans%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetBufferMappingModes%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetSpanMappings%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.GetMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.ReleaseMarkerData%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CanReplaceLines%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CopyLineText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CreateTrackingPoint%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.EnumLayerMarkers%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetBaseBuffer%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLengthOfLine%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLineCount%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLineText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.LockBufferEx%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.MapLocalSpansToTextOriginatingLayer%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReleaseMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReplaceLines%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReplaceLinesEx%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.UnlockBufferEx%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView.GetSelectedAtom%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetSelectionDataObject%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.PositionCaretForEditing%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RestrictViewRange%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateViewFrameCaption%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.GetSmartTagRect%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.InvokeInsertionUI%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.SetHoverWaitTimer%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow.SetViewClassID%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.AfterCompletorCommit%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.BeforeCompletorCommit%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetContextLocation%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetServiceProvider%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSmartTagRect%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectCaretPos%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectSelection%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.ReplaceSubjectTextSpan%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.SetSubjectCaretPos%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.SetSubjectSelection%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.UpdateSmartTagWindow%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost.SetSubjectFromPrimaryBuffer%2A> é implementado nos adaptadores, mas ignorados pela estrutura de tópicos interface do usuário.|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx.GetBannerAttr%2A> é implementado nos adaptadores, mas ignorados pela estrutura de tópicos interface do usuário.|

