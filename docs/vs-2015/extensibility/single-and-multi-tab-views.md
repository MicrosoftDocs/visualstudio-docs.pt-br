---
title: Modos de exibição únicos e com várias guias | Microsoft Docs
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
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
caps.latest.revision: 23
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8231581761199be4df9c368494fb27bdc7926c51
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51748989"
---
# <a name="single-and-multi-tab-views"></a>Exibição de guia única e multiguias
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um editor pode criar diferentes tipos de modos de exibição. Um exemplo é uma janela do editor de código, outra é um designer de formulários.  
  
 Uma exibição com várias guias é uma exibição que tem várias guias. Por exemplo, o editor de HTML possui duas guias na parte inferior: **Design** e **origem**, cada uma exibição lógica. O modo de design exibe uma página da web processada, enquanto o outro exibe o HTML que inclui a página da web.  
  
## <a name="accessing-physical-views"></a>Acessando exibições físicas  
 Modos de exibição físicos hospedam objetos de exibição de documento, cada um representando uma exibição dos dados no buffer, como o código ou um formulário. Da mesma forma, cada objeto de exibição de documento tem uma exibição física (identificado por algo conhecido como uma cadeia de caracteres de exibição física) e, em geral, uma única visualização lógica.  
  
 Em alguns casos, no entanto, um modo de exibição físico pode ter dois ou mais modos de exibição lógicos. Alguns exemplos são um editor que tem uma janela dividida com modos de exibição lado a lado, ou um designer de formulários que tem um modo de exibição de design/GUI e um modo de exibição de código behind-o formulário.  
  
 Para habilitar seu editor acessar todas as exibições de físicas disponíveis, você deve criar uma cadeia de caracteres de exibição física exclusivo para cada tipo de objeto de exibição de documento que pode criar a sua fábrica de editor. Por exemplo, o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] fábrica de editor pode criar documento objetos de exibição para uma janela de código e uma janela de designer de formulários.  
  
## <a name="creating-multi-tabbed-views"></a>Criando modos de exibição com várias guias  
 Embora um objeto de exibição de documento deve ser associado uma exibição física por meio de uma cadeia de caracteres de exibição física exclusivo, você pode colocar várias guias dentro da exibição física para ativar a visualização de dados de maneiras diferentes. Nessa configuração com várias guias, todas as guias estão associadas com a mesma cadeia de caracteres de exibição física, mas cada guia é fornecido uma GUID de exibição lógica diferente.  
  
 Para criar uma exibição com várias guias para um editor, implemente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView> da interface e, em seguida, associar uma exibição lógica diferente GUID (<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID>) com cada guia que você cria.  
  
 O editor de HTML do Visual Studio é um exemplo de um editor com um modo de exibição com várias guia. Ele tem **Design** e **origem** guias. Para habilitar isso, uma exibição lógica diferente está associada com cada guia `LOGICALVIEWID_TextView` para o **Design** guia e `LOGICALVIEWID_Code` para o **origem** guia.  
  
 Ao especificar o modo de exibição lógico apropriado, um VSPackage pode acessar o modo de exibição que corresponde a uma finalidade específica, como criação de um formulário, edição de código ou depurar o código. No entanto, uma das janelas deve ser identificada pela cadeia de caracteres nula, e isso deve corresponder da exibição lógica primária (`LOGVIEWID_Primary`).  
  
 A tabela a seguir lista os valores de exibição lógico disponível e seu uso.  
  
|GUID DE LOGVIEWID|Uso recomendado|  
|--------------------|---------------------|  
|`LOGVIEWID_Primary`|Modo de exibição padrão/primário da fábrica de editor.<br /><br /> Todas as fábricas de editor devem dar suporte a esse valor. Este modo de exibição deve usar a cadeia de caracteres nula como sua cadeia de caracteres de exibição física. Pelo menos uma exibição lógica deve ser definida para esse valor.|  
|`LOGVIEWID_Debugging`|Depuração de modo de exibição. Normalmente, `LOGVIEWID_Debugging` mapeia para a mesma exibição da `LOGVIEWID_Code`.|  
|`LOGVIEWID_Code`|Modo iniciado pelos **Exibir código** comando.|  
|`LOGVIEWID_Designer`|Modo iniciado pelos **Exibir formulário** comando.|  
|`LOGVIEWID_TextView`|Exibição do editor de texto. Esta é a exibição que retorna <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>, na qual você pode acessar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.|  
|`LOGVIEWID_UserChooseView`|Solicita que o usuário escolha qual modo de exibição para usar.|  
|`LOGVIEWID_ProjectSpecificEditor`|Passado pela **abrir com** caixa de diálogo<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> Quando o usuário escolhe a entrada "(editor padrão do projeto)".|  
  
 Embora o modo de exibição lógico GUIDs são extensíveis, você pode usar apenas os GUIDs de modo de exibição lógico definidos no seu VSPackage.  
  
 Durante o desligamento, o Visual Studio mantém o GUID da fábrica de editor e as cadeias de caracteres de exibição física associadas com a janela do documento para que possa ser usado para abrir novamente as janelas do documento quando a solução for aberta novamente. Apenas as janelas que estão abertas quando uma solução é fechada são persistidas no arquivo de solução (. suo). Esses valores correspondem do `VSFPROPID_guidEditorType` e `VSFPROPID_pszPhysicalView` valores passados no `propid` parâmetro no <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método.  
  
## <a name="example"></a>Exemplo  
 Este trecho de código ilustra como o <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView> objeto é usado para acessar uma exibição que implementa `IVsCodeWindow`. Nesse caso, o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> service é usado para chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> e a solicitação `LOGVIEWID_TextView`, que obtém um ponteiro para um quadro de janela. Um ponteiro para o objeto de exibição de documento é obtido chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> e especificando um valor de `VSFPROPID_DocView`. Do objeto de visualização de documento `QueryInterface` é chamado para `IVsCodeWindow`. A expectativa nesse caso é que um editor de texto é retornado, e então o objeto de exibição de documento retornado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método é uma janela de código.  
  
```cpp#  
HRESULT CFindTool::GotoFileLocation(const WCHAR * szFile, long iLine, long iStart, long iLen)  
{  
  HRESULT hr;  
  if (NULL == szFile || !*szFile)  
    return E_INVALIDARG;  
  
  if (iLine == -1L)  
    return S_FALSE;  
  
  VSITEMID                  itemid;  
  VARIANT                   var;  
  RECT                      rc;  
  IVsUIShellOpenDocument *  pOpenDoc    = NULL;  
  IVsCodeWindow *           pCodeWin    = NULL;  
  IVsTextView *             pTextView   = NULL;  
  IVsUIHierarchy *          pHierarchy  = NULL;  
  IVsWindowFrame *          pFrame      = NULL;  
  IUnknown *                pUnk        = NULL;  
  IVsHighlight *            pHighlight  = NULL;  
  
  IfFailGo(CGlobalServiceProvider::HrQueryService(SID_SVsUIShellOpenDocument, IID_IVsUIShellOpenDocument, (void **)&pOpenDoc));  
  IfFailGo(pOpenDoc->OpenDocumentViaProject(szFile, LOGVIEWID_TextView, NULL, &pHierarchy, &itemid, &pFrame));  
  pFrame->Show();  
  VariantInit(&var);  
  IfFailGo(pFrame->GetProperty(VSFPROPID_DocView, &var));  
  if (VT_UNKNOWN != var.vt) { hr = E_FAIL; goto Error; }  
  pUnk = V_UNKNOWN(&var);  
  if (NULL != pUnk)  
  {  
    IfFailGo(pUnk->QueryInterface(IID_IVsCodeWindow, (void **)&pCodeWin));  
    if (SUCCEEDED(hr = pCodeWin->GetLastActiveView(&pTextView)) ||  
        SUCCEEDED(hr = pCodeWin->GetPrimaryView(&pTextView)) )  
    {  
      pTextView->SetSelection(iLine, iStart, iLine, iStart + iLen);  
      // uncover selection  
      IfFailGo(pTextView->QueryInterface(IID_IVsHighlight, (void**)&pHighlight));  
      IfFailGo(SUCCEEDED(pHighlight->GetHighlightRect(&rc)));  
      UncoverSelectionRect(&rc);  
    }  
  }  
  
Error:  
  CLEARINTERFACE(pHighlight);  
  CLEARINTERFACE(pTextView);  
  CLEARINTERFACE(pCodeWin);  
  CLEARINTERFACE(pUnk);  
  CLEARINTERFACE(pFrame);  
  CLEARINTERFACE(pOpenDoc);  
  CLEARINTERFACE(pHierarchy);  
  RedrawWindow(m_hwndResults, NULL, NULL, RDW_ERASE|RDW_FRAME|RDW_INVALIDATE|RDW_ALLCHILDREN);  
  return hr;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a vários modos de exibição de documento](../extensibility/supporting-multiple-document-views.md)   
 [Como: anexar exibições para dados de documentos](../extensibility/how-to-attach-views-to-document-data.md)   
 [Criar designers e editores personalizados](../extensibility/creating-custom-editors-and-designers.md)

