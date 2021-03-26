---
title: Exibições únicas e de várias guias | Microsoft Docs
description: Saiba como implementar exibições de várias guias em editores, como uma janela do editor de código e um designer de formulários.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c23693b5ae622912695c139714c7e818ed0e868
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056318"
---
# <a name="single-and-multi-tab-views"></a>Exibição de guia única e multiguias
Um editor pode criar diferentes tipos de exibições. Um exemplo é uma janela do editor de código, outra é um designer de formulários.

 Uma exibição com várias guias é uma exibição com várias guias. Por exemplo, o editor de HTML tem duas guias na parte inferior: **design** e **origem**, cada uma das exibições lógicas. A exibição Design exibe uma página da Web renderizada, enquanto a outra exibe o HTML que compõe a página da Web.

## <a name="accessing-physical-views"></a>Acessando exibições físicas
 As exibições físicas hospedam objetos de exibição de documento, cada um representando uma exibição dos dados no buffer, como um código ou um formulário. De acordo, cada objeto de exibição de documento tem uma exibição física (identificada por algo conhecido como uma cadeia de caracteres de exibição física) e, geralmente, uma única exibição lógica.

 No entanto, em alguns casos, uma exibição física pode ter duas ou mais exibições lógicas. Alguns exemplos são um editor que tem uma janela dividida com exibições lado a lado ou um designer de formulários que tem um modo de exibição de GUI/design e uma exibição de código por trás do formulário.

 Para permitir que o editor acesse todas as exibições físicas disponíveis, você deve criar uma cadeia de caracteres de exibição física exclusiva para cada tipo de objeto de exibição de documento que sua fábrica de editor pode criar. Por exemplo, a [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] fábrica do editor pode criar objetos de exibição de documento para uma janela de código e uma janela do designer de formulários.

## <a name="creating-multi-tabbed-views"></a>Criando exibições com várias guias
 Embora um objeto de exibição de documento deva ser associado a uma exibição física por meio de uma cadeia de caracteres de exibição física exclusiva, você pode inserir várias guias na exibição física para habilitar a exibição de dados de diferentes maneiras. Nessa configuração com várias guias, todas as guias são associadas à mesma cadeia de caracteres de exibição física, mas cada guia recebe um GUID de exibição lógica diferente.

 Para criar uma exibição com várias guias para um editor, implemente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView> interface e associe um GUID de exibição lógica diferente ( <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID> ) a cada guia que você criar.

 O editor de HTML do Visual Studio é um exemplo de um editor com uma exibição de várias guias. Ele tem guias de **design** e **origem** . Para habilitar isso, uma exibição lógica diferente é associada a cada guia, `LOGICALVIEWID_TextView` para a guia **design** e `LOGICALVIEWID_Code` para a guia **origem** .

 Ao especificar a exibição lógica apropriada, um VSPackage pode acessar a exibição que corresponde a uma finalidade específica, como a criação de um formulário, edição de código ou depuração de código. No entanto, uma das janelas deve ser identificada pela cadeia de caracteres nula e deve corresponder à exibição lógica primária ( `LOGVIEWID_Primary` ).

 A tabela a seguir lista os valores de exibição lógica disponíveis e seu uso.

|GUID DE LOGVIEWID|Uso recomendado|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|Exibição padrão/primária da fábrica do editor.<br /><br /> Todas as fábricas de editor devem dar suporte a esse valor. Esta exibição deve usar a cadeia de caracteres nula como sua cadeia de caracteres de exibição física. Pelo menos uma exibição lógica deve ser definida para esse valor.|
|`LOGVIEWID_Debugging`|Modo de depuração. Normalmente, `LOGVIEWID_Debugging` o mapeia para a mesma exibição que `LOGVIEWID_Code` .|
|`LOGVIEWID_Code`|Exibição iniciada pelo comando **View Code** .|
|`LOGVIEWID_Designer`|Exibição iniciada pelo comando **Exibir formulário** .|
|`LOGVIEWID_TextView`|Exibição do editor de texto. Essa é a exibição que retorna <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> , da qual você pode acessar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> .|
|`LOGVIEWID_UserChooseView`|Solicita que o usuário escolha qual exibição deve ser usada.|
|`LOGVIEWID_ProjectSpecificEditor`|Passado pela caixa de diálogo **abrir com** para<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> Quando o usuário escolhe a entrada "(editor padrão do projeto)".|

 Embora os GUIDs de exibição lógica sejam extensíveis, você pode usar apenas os GUIDs de exibição lógica definidos em seu VSPackage.

 Durante o desligamento, o Visual Studio retém o GUID da fábrica do editor e as cadeias de caracteres de exibição física associadas à janela do documento para que ela possa ser usada para reabrir janelas de documentos quando a solução é aberta novamente. Somente as janelas abertas quando uma solução é fechada são mantidas no arquivo da solução (. suo). Esses valores correspondem aos `VSFPROPID_guidEditorType` valores e `VSFPROPID_pszPhysicalView` passados no `propid` parâmetro no <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método.

## <a name="example"></a>Exemplo
 Este trecho de código ilustra como o <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView> objeto é usado para acessar uma exibição que implementa `IVsCodeWindow` . Nesse caso, o <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> serviço é usado para chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> e solicitar `LOGVIEWID_TextView` , que obtém um ponteiro para um quadro de janela. Um ponteiro para o objeto de exibição de documento é obtido chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> e especificando um valor de `VSFPROPID_DocView` . No objeto de exibição de documento, `QueryInterface` é chamado para `IVsCodeWindow` . Nesse caso, a expectativa é que um editor de texto seja retornado e, portanto, o objeto de exibição de documento retornado no <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> método é uma janela de código.

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

## <a name="see-also"></a>Confira também
- [Suporte a várias exibições de documento](../extensibility/supporting-multiple-document-views.md)
- [Como anexar exibições para dados de documentos](../extensibility/how-to-attach-views-to-document-data.md)
- [Criar designers e editores personalizados](../extensibility/creating-custom-editors-and-designers.md)
