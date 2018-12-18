---
title: Modos de exibição único e multi-guia | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 23feeaee14e6a149ad385c9f5e4a0c4b41be1e86
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31142966"
---
# <a name="single-and-multi-tab-views"></a>Modos de exibição único e multi-guia
Um editor pode criar diferentes tipos de modos de exibição. Um exemplo é uma janela do editor de código, o outro é um designer de formulários.  
  
 Uma exibição de várias guias é uma exibição que tem várias guias. Por exemplo, o editor de HTML tem duas guias na parte inferior: **Design** e **fonte**, cada uma exibição lógica. O modo de exibição de design exibe uma página da web processada, enquanto o outro exibe o HTML que compõem a página da web.  
  
## <a name="accessing-physical-views"></a>Acessar modos de exibição físicos  
 Modos de exibição físicos hospedam objetos de exibição de documento, cada uma representando uma exibição de dados no buffer, como código ou um formulário. Da mesma forma, cada objeto de exibição do documento tem um modo de exibição físico (identificadas por alguma coisa conhecida como uma cadeia de caracteres de exibição físico) e, em geral, uma única exibição lógica.  
  
 Em alguns casos, porém, um modo de exibição físico pode ter dois ou mais modos de exibição lógicos. Alguns exemplos são um editor que tem uma janela separadora com modos de exibição lado a lado, ou um designer de formulários que tem um modo de exibição de design/interface gráfica do usuário e uma exibição de código por trás-o formulário.  
  
 Para habilitar o editor acessar todos os modos de exibição físicos disponíveis, você deve criar uma cadeia de caracteres de exibição físico exclusivo para cada tipo de objeto de exibição de documento que pode criar a fábrica do editor. Por exemplo, o [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] fábrica do editor pode criar documento objetos de exibição para uma janela de código e uma janela de designer de formulários.  
  
## <a name="creating-multi-tabbed-views"></a>Criando modos de exibição de várias guias  
 Embora um objeto de exibição de documento deve ser associado uma exibição física por meio de uma cadeia de caracteres de exibição físico exclusivo, você pode colocar várias guias no modo de exibição físico para habilitar a exibição de dados de maneiras diferentes. Nessa configuração de várias guias, todas as guias estão associadas com a mesma cadeia de caracteres de exibição físico, mas cada guia é fornecido uma GUID de exibição lógica diferente.  
  
 Para criar um modo de exibição de várias guias para um editor, implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView> de interface e, em seguida, associar uma exibição lógica diferente GUID (<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID>) com cada guia que você criar.  
  
 O editor de HTML do Visual Studio é um exemplo de um editor com um modo de exibição de multi-guia. Ele tem **Design** e **fonte** guias. Para habilitar isso, outro modo de exibição lógico é associado com cada guia, `LOGICALVIEWID_TextView` para o **Design** guia e `LOGICALVIEWID_Code` para o **fonte** guia.  
  
 Especificando o modo de exibição lógico apropriado, um VSPackage pode acessar o modo de exibição que corresponde a uma finalidade específica, como criação de um formulário, a edição do código ou depurar o código. No entanto, uma do windows deve ser identificada pela cadeia de caracteres nula, e isso deve corresponder ao modo de exibição lógico primário (`LOGVIEWID_Primary`).  
  
 A tabela a seguir lista os valores do modo de exibição lógico disponível e seu uso.  
  
|GUID DE LOGVIEWID|Uso recomendado|  
|--------------------|---------------------|  
|`LOGVIEWID_Primary`|Exibição padrão/primário a fábrica do editor.<br /><br /> Todas as fábricas de editor devem oferecer suporte a esse valor. Este modo de exibição deve usar a cadeia de caracteres nula como sua cadeia de caracteres de exibição físico. Pelo menos um modo de exibição lógico deve ser definido para esse valor.|  
|`LOGVIEWID_Debugging`|Modo de depuração. Normalmente, `LOGVIEWID_Debugging` mapeia para a mesma exibição da `LOGVIEWID_Code`.|  
|`LOGVIEWID_Code`|Exibição iniciou o **Exibir código** comando.|  
|`LOGVIEWID_Designer`|Exibição iniciou o **Exibir formulário** comando.|  
|`LOGVIEWID_TextView`|Exibição do editor de texto. Esta é a exibição retorna <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>, da qual você pode acessar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>.|  
|`LOGVIEWID_UserChooseView`|Solicita que o usuário escolha qual exibição a ser usado.|  
|`LOGVIEWID_ProjectSpecificEditor`|Passados pelo **abrir com** caixa de diálogo<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> Quando o usuário escolhe a entrada "(editor padrão do projeto)".|  
  
 Embora o modo de exibição lógico GUIDs são extensíveis, você pode usar somente os GUIDs de modo de exibição lógico definidos no seu VSPackage.  
  
 Durante o desligamento, o Visual Studio mantém o GUID da fábrica de editor e as cadeias de caracteres de exibição físico associadas à janela de documento para que ele pode ser usado para reabrir janelas de documentos quando a solução for aberta novamente. Somente windows que estão abertos quando uma solução for fechada são persistidos no arquivo de solução (. suo). Esses valores correspondem ao `VSFPROPID_guidEditorType` e `VSFPROPID_pszPhysicalView` valores passados a `propid` parâmetro o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método.  
  
## <a name="example"></a>Exemplo  
 Este trecho de código ilustra como o <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView> objeto é usado para acessar uma exibição que implementa `IVsCodeWindow`. Nesse caso, o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> serviço é usado para chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> e solicitação `LOGVIEWID_TextView`, que obtém um ponteiro para um quadro de janela. Um ponteiro para o objeto de exibição do documento é obtido chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> e especificando um valor de `VSFPROPID_DocView`. Do objeto de visualização de documento, `QueryInterface` é chamado para `IVsCodeWindow`. A expectativa nesse caso é que um editor de texto é retornado, e portanto o objeto de exibição de documento retornado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método é uma janela de código.  
  
```cpp  
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
 [Dando suporte a várias exibições de documento](../extensibility/supporting-multiple-document-views.md)   
 [Como: anexar modos de exibição para dados de documento](../extensibility/how-to-attach-views-to-document-data.md)   
 [Criar designers e editores personalizados](../extensibility/creating-custom-editors-and-designers.md)