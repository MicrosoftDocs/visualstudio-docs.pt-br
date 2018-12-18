---
title: Constantes IDE | Microsoft Docs
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
- IDE, errors
- logical views
- errors [Visual Studio], IDE
- UI context constants
- constants, Visual Studio IDE
- IDE, constants
- physical views
ms.assetid: 5030e70a-241d-474a-ba8c-e3b1cf947ff0
caps.latest.revision: 24
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: aa8fb2e4af74facc0ca00343e6abad36b7fcec50
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51743309"
---
# <a name="ide-constants"></a>Constantes do IDE
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O <xref:Microsoft.VisualStudio.VSConstants> classe fornece constantes que são específicos para o ambiente de desenvolvimento integrado (IDE) e que foram definidos anteriormente apenas em arquivos de cabeçalho.  
  
## <a name="logical-and-physical-views"></a>Modos de exibição lógicos e físicos  
  
|Valor|Descrição|  
|-----------|-----------------|  
|[LOGVIEWID_Code_guid](/dotnet/api/microsoft.visualstudio.vsconstants.logviewid.code_guid?view=visualstudiosdk-2015)|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` manipuladores devem passar esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter o **abrir com** caixa de diálogo, neste caso, em possíveis modos de exibição de código.|  
|[LOGVIEWID_Debugging_guid](/dotnet/api/microsoft.visualstudio.vsconstants.logviewid.debugging_guid?view=visualstudiosdk-2015)|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` manipuladores de passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter o **abrir com** caixa de diálogo, nesse caso, preenchida com possíveis <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid> depuração exibições que são mapeados para a mesma exibição da <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>.|  
|[LOGVIEWID_Designer_guid](/dotnet/api/microsoft.visualstudio.vsconstants.logviewid.designer_guid?view=visualstudiosdk-2015)|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` manipuladores de passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter o **abrir com** caixa de diálogo, neste caso, para **Exibir formulário** as exibições de designer.|  
|[LOGVIEWID_Primary_guid](/dotnet/api/microsoft.visualstudio.vsconstants.logviewid.primary_guid?view=visualstudiosdk-2015)|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` manipuladores de passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter o **abrir com** caixa de diálogo, neste caso, o modo de exibição padrão/primário da fábrica de editor.|  
|[LOGVIEWID_TextView_guid](/dotnet/api/microsoft.visualstudio.vsconstants.logviewid.textview_guid?view=visualstudiosdk-2015)|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` manipuladores de passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter o **abrir com** caixa de diálogo para uma exibição de editor de texto do documento ou de dados.|  
|[LOGVIEWID_UserChooseView_guid](/dotnet/api/microsoft.visualstudio.vsconstants.logviewid.userchooseview_guid?view=visualstudiosdk-2015)|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> `cmdidOpenWith` manipuladores de passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método que solicita que o usuário escolha qual exibição definida pelo usuário para usar.|  
  
## <a name="editor-factory-flags"></a>Sinalizadores de fábrica do Editor  
  
|Valor|Descrição|  
|-----------|-----------------|  
|[CEF.CloneFile](/dotnet/api/microsoft.visualstudio.vsconstants.cef?view=visualstudiosdk-2015)|Um sinalizador obsoleto combinados bit a bit como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método.|  
|[CEF.CloneFile](/dotnet/api/microsoft.visualstudio.vsconstants.cef?view=visualstudiosdk-2015)|Combinado bit a bit como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>, método, isso indica que a fábrica do editor deve executar as correções necessárias.|  
|[CEF.CloneFile](/dotnet/api/microsoft.visualstudio.vsconstants.cef?view=visualstudiosdk-2015)|Combinado bit a bit como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método, esse sinalizador é mutuamente exclusivo de [CEF. CloneFile](/dotnet/api/microsoft.visualstudio.vsconstants.cef?view=visualstudiosdk-2015).|  
|[CEF.CloneFile](/dotnet/api/microsoft.visualstudio.vsconstants.cef?view=visualstudiosdk-2015)|Combinado bit a bit como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método, isso indica que a fábrica do editor deve criar o editor sem exibir uma interface do usuário (IU).|  
  
## <a name="visual-studio-errors"></a>Erros do Visual Studio  
  
|Valor|Descrição|  
|-----------|-----------------|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|Uma constante retornada pelas interfaces ao comportamento assíncrono quando o objeto em questão no já está ocupado|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|Um erro HRESULT que é específico para o Visual Studio "dados de documento incompatível".|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|Um erro HRESULT que é específico para o Visual Studio e que indica "Não carregado o pacote."|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|Um erro HRESULT que é específico para o Visual Studio e que indica que o "Projeto já existe".|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|Um erro HRESULT que é específico para o Visual Studio e que indica "Falha na configuração do projeto".|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|Um erro HRESULT que é específico para o Visual Studio e que indica "O projeto não carregado".|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|Um erro HRESULT que é específico para o Visual Studio e que indica "Solução já aberta".|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|Um erro HRESULT que é específico para o Visual Studio e que indica "Solução não abrir".|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|Retornado por interfaces de compilação que tenham parâmetros para especificar uma matriz do <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput> interface, mas a implementação pode aplicar apenas o método para todas as saídas.|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|O <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método retornará esse valor se o documento tem um formato que não pode ser aberto no editor.|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|Um valor HRESULT que indica que o usuário pressionasse o botão Voltar em um assistente do Visual Studio.|  
  
## <a name="visual-studio-constants"></a>Constantes do Visual Studio  
  
|Valor|Descrição|  
|-----------|-----------------|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|Um erro HRESULT que é específico para o Visual Studio e que indica "Projeto encaminhado".|  
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|Uma constante que é específica para o Visual Studio para um "marcador de caixa de ferramentas".|  
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|Uma constante que é específica para o Visual Studio para transmitir uma mensagem de notificação por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> método que indica o início da modalidade.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|Uma constante que é específica para o Visual Studio para transmitir uma mensagem de notificação por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> método que indica o fim da modalidade.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|Uma constante que é específica para o Visual Studio para transmitir uma mensagem de notificação por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> método indicando que as métricas de barra de comando foram alterados.|  
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|Uma constante que é específica para o Visual Studio que indica que um cookie não foi definido.|  
|[VSITEMID.Nil](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|Um identificador de item do Visual Studio que representa a ausência de um item de projeto. Esse valor é usado quando não houver nenhuma seleção atual.|
|[VSITEMID.Root](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|Um identificador de item do Visual Studio que representa a raiz de uma hierarquia de projeto e é usado para identificar a hierarquia inteira, em vez de um único item.|
|[VSITEMID.Selection](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|Um identificador de item do Visual Studio que representa o item selecionado no momento ou os itens, que podem incluir a raiz da hierarquia.| 
  
## <a name="ivsselectionevents"></a>IVsSelectionEvents  
 Descreve qual componente do IDE apenas foi selecionado, em um <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> chamar, por exemplo.  
  
|Constante|Valor|
|--------------|-----------|
|[SelectionElement.DocumentFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[SelectionElement.PropertyBrowserSID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[SelectionElement.StartupProject](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[SelectionElement.UndoManager](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[SelectionElement.UserContext](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0x5|
|[SelectionElement.WindowFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1| 
  
## <a name="vsselelemid"></a>VSSELELEMID  
 Constantes usadas para indicar um novo estado de seleção.  
  
|Constante|Valor|  
|--------------|-----------|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|2|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|7|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|4|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|6|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|3|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|0|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|5|  
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|1|  
  
## <a name="component-selector-dialog-constants"></a>Constantes de caixa de diálogo do seletor de componente  
  
|Constante|Valor|  
|--------------|-----------|  
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELCHANGED>|WM_USER + 1280|  
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELDBLCLICK>|WM_USER + 1281|  
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_CLEARSELECTION>|WM_USER + 1290|  
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_GETSELECTION>|WM_USER + 1287|  
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZELIST>|WM_USER + 1285|  
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZETAB>|WM_USER + 1288|  
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_QUERYCANSELECT>|WM_USER + 1286|  
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_SETMULTISELECT>|WM_USER + 1289|  
  
## <a name="see-also"></a>Consulte também  
 [Comandos definidos pelo IDE para estender sistemas de projeto](../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

