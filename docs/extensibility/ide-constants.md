---
title: Constantes do IDE | Microsoft Docs
description: A classe VSConstants fornece constantes específicas para o IDE e que foram definidas anteriormente somente em arquivos de cabeçalho.
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- IDE, errors
- logical views
- errors [Visual Studio], IDE
- UI context constants
- constants, Visual Studio IDE
- IDE, constants
- physical views
ms.assetid: 5030e70a-241d-474a-ba8c-e3b1cf947ff0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 66daa52bc5769a9f8b599a52953a6bc898d2cf20
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069862"
---
# <a name="ide-constants"></a>Constantes do IDE

A <xref:Microsoft.VisualStudio.VSConstants> classe fornece constantes específicas para o ambiente de desenvolvimento integrado (IDE) e que foram definidas anteriormente somente em arquivos de cabeçalho.

## <a name="logical-and-physical-views"></a>Exibições lógica e física

|Valor|Descrição|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>os `cmdidOpenWith` manipuladores devem passar esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter a caixa de diálogo **abrir com** , nesse caso, em possíveis exibições de código.|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>os `cmdidOpenWith` manipuladores passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter a caixa de diálogo **abrir com** , neste caso, preenchida com possíveis <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid> exibições de depuração que são mapeadas para a mesma exibição que <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid> .|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Designer_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>os `cmdidOpenWith` manipuladores passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter a caixa de diálogo **abrir com** , nesse caso, para exibir exibições do designer de **formulário** .|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Primary_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>os `cmdidOpenWith` manipuladores passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter a caixa de diálogo **abrir com** , nesse caso, a exibição padrão/primária da fábrica do editor.|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.TextView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>os `cmdidOpenWith` manipuladores passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método para obter a caixa de diálogo **abrir com** , neste documento ou exibição do editor de texto de dados.|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.UserChooseView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>os `cmdidOpenWith` manipuladores passam esse valor para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método que solicita que o usuário escolha qual exibição definida pelo usuário usar.|

## <a name="editor-factory-flags"></a>Sinalizadores de fábrica do editor

|Valor|Descrição|
|-----------|-----------------|
|[CEF. Clonefile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)|Um sinalizador obsoleto combinou o bit a bit como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método.|
|[CEF. OpenAsNew](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenAsNew>)|Conjunto de bits combinado como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método, isso indica que a fábrica do editor deve executar as correções necessárias.|
|[CEF. OpenFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenFile>)|Conjunto de bits combinado como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método, esse sinalizador é mutuamente exclusivo de [CEF. Clonefile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>).|
|[CEF. Mudo](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_Silent>)|Combinação de bits bit como o primeiro parâmetro do <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método, isso indica que a fábrica do editor deve criar o editor sem exibir uma interface do usuário.|

## <a name="visual-studio-errors"></a>Erros do Visual Studio

|Valor|Descrição|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|Uma constante retornada por interfaces para comportamento assíncrono quando o objeto em questão já estiver ocupado|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|Um erro HRESULT que é específico do Visual Studio para "dados de documento incompatíveis".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|Um erro HRESULT que é específico do Visual Studio e que indica "pacote não carregado".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|Um erro HRESULT que é específico do Visual Studio e que indica que o "projeto já existe".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|Um erro HRESULT que é específico do Visual Studio e que indica "falha na configuração do projeto".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|Um erro HRESULT que é específico do Visual Studio e que indica "projeto não carregado".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|Um erro HRESULT que é específico do Visual Studio e que indica "solução já aberta".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|Um erro HRESULT que é específico do Visual Studio e que indica "solução não aberta".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|Retornado por interfaces de compilação que têm parâmetros para especificar uma matriz da <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput> interface, mas a implementação só pode aplicar o método a todas as saídas.|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|O <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> método retornará esse valor se o documento tiver um formato que não pode ser aberto no editor.|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|Um valor HRESULT que indica que o usuário atingiu o botão voltar em um assistente do Visual Studio.|

## <a name="visual-studio-constants"></a>Constantes do Visual Studio

|Valor|Descrição|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|Um erro HRESULT que é específico do Visual Studio e que indica "projeto encaminhado".|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|Uma constante que é específica para o Visual Studio para um "marcador de caixa de ferramentas".|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|Uma constante que é específica para o Visual Studio para transmitir uma mensagem de notificação por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> método que indica o início da modalidade.|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|Uma constante que é específica para o Visual Studio para transmitir uma mensagem de notificação por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> método que indica o fim da modalidade.|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|Uma constante que é específica ao Visual Studio para transmitir uma mensagem de notificação por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> método que indica que as métricas da barra de comandos foram alteradas.|
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|Uma constante que é específica para o Visual Studio que indica que um cookie não foi definido.|
|[VSITEMID. Apostar](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|Um identificador de item do Visual Studio que representa a ausência de um item de projeto. Esse valor é usado quando não há seleção atual.|
|[VSITEMID. Básica](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|Um identificador de item do Visual Studio que representa a raiz de uma hierarquia de projeto e é usado para identificar toda a hierarquia, em oposição a um único item.|
|[VSITEMID. Selecionado](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|Um identificador de item do Visual Studio que representa o item ou itens selecionados no momento, que podem incluir a raiz da hierarquia.|

## <a name="ivsselectionevents"></a>IVsSelectionEvents
 Descreve qual componente do IDE acabou de ser selecionado, em uma <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> chamada, por exemplo.

|Constante|Valor|
|--------------|-----------|
|[SelectionElement.DocumentFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[Selectionelement. PropertyBrowserSID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[Selectionelement. StartupProject](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[Selectionattribute. UndoManager](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[Selectionelement. UserContext](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0x5|
|[Selectionelement. WindowFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1|

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

## <a name="component-selector-dialog-constants"></a>Constantes da caixa de diálogo Seletor de componentes

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

## <a name="see-also"></a>Confira também

- [Comandos definidos pelo IDE para estender sistemas de projeto](../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
