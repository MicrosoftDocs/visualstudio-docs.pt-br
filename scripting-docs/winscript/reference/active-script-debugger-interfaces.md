---
title: Interfaces do depurador de Script ativo | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Active Script Debugger interfaces
- activdbg.h
ms.assetid: bf4750b1-4e58-442b-ab56-254e640de61d
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f260df5a23ef6b5ef6ef7253726b1fea7bc00269
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49855424"
---
# <a name="active-script-debugger-interfaces"></a>Interfaces do depurador de script ativo
Os arquivos de cabeçalho activdbg.h e activdbg100.h fornecem as interfaces, enumerações e estruturas listadas nesta seção. Eles são para depuração de script.  
  
> [!NOTE]
>  O `IJSDebug*` interfaces e o `IEnumJsStackFrames` interface foram lançados pela primeira vez no Internet Explorer 11 para depurar o código nativo com script. O arquivo de cabeçalho para essas interfaces é jscript9diag.h.  
  
## <a name="in-this-section"></a>Nesta seção  
 As seguintes interfaces permitem a depuração com neutralidade de idioma, neutralidade de host:  
  
- [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)  
  
- [IActiveScriptDebug Interface](../../winscript/reference/iactivescriptdebug-interface.md)  
  
- [IActiveScriptErrorDebug Interface](../../winscript/reference/iactivescripterrordebug-interface.md)  
  
- [IActiveScriptErrorDebug110 Interface](../../winscript/reference/iactivescripterrordebug110-interface.md)  
  
- [IActiveScriptSiteDebug Interface](../../winscript/reference/iactivescriptsitedebug-interface.md)  
  
- [IActiveScriptSiteDebug32 Interface](../../winscript/reference/iactivescriptsitedebug32-interface.md)  
  
- [IActiveScriptSiteDebugEx Interface](../../winscript/reference/iactivescriptsitedebugex-interface.md)  
  
- [IActiveScriptWinRTErrorDebug Interface](../../winscript/reference/iactivescriptwinrterrordebug-interface.md)  
  
- [IApplicationDebugger Interface](../../winscript/reference/iapplicationdebugger-interface.md)  
  
- [IApplicationDebuggerUI Interface](../../winscript/reference/iapplicationdebuggerui-interface.md)  
  
- [IDebugApplication Interface](../../winscript/reference/idebugapplication-interface.md)  
  
- [IDebugApplication110 Interface](../../winscript/reference/idebugapplication110-interface.md)  
  
- [IDebugApplicationNode Interface](../../winscript/reference/idebugapplicationnode-interface.md)  
  
- [IDebugApplicationNode100 Interface](../../winscript/reference/idebugapplicationnode100-interface.md)  
  
- [IDebugApplicationNodeEvents Interface](../../winscript/reference/idebugapplicationnodeevents-interface.md)  
  
- [Interface IDebugApplicationThread](../../winscript/reference/idebugapplicationthread-interface.md)  
  
- [Interface IDebugApplicationThread110](../../winscript/reference/idebugapplicationthread110-interface.md)  
  
- [Interface IDebugApplicationThreadEvents110](../../winscript/reference/idebugapplicationthreadevents110-interface.md)  
  
- [IDebugAsyncOperation Interface](../../winscript/reference/idebugasyncoperation-interface.md)  
  
- [IDebugAsyncOperationCallBack Interface](../../winscript/reference/idebugasyncoperationcallback-interface.md)  
  
- [Interface IDebugCodeContext](../../winscript/reference/idebugcodecontext-interface.md)  
  
- [Interface IDebugCookie](../../winscript/reference/idebugcookie-interface.md)  
  
- [Interface IDebugDocument](../../winscript/reference/idebugdocument-interface.md)  
  
- [Interface IDebugDocumentContext](../../winscript/reference/idebugdocumentcontext-interface.md)  
  
- [IDebugDocumentHelper Interface](../../winscript/reference/idebugdocumenthelper-interface.md)  
  
- [IDebugDocumentHost Interface](../../winscript/reference/idebugdocumenthost-interface.md)  
  
- [Interface IDebugDocumentInfo](../../winscript/reference/idebugdocumentinfo-interface.md)  
  
- [Interface IDebugDocumentProvider](../../winscript/reference/idebugdocumentprovider-interface.md)  
  
- [Interface IDebugDocumentText](../../winscript/reference/idebugdocumenttext-interface.md)  
  
- [Interface IDebugDocumentTextAuthor](../../winscript/reference/idebugdocumenttextauthor-interface.md)  
  
- [Interface IDebugDocumentTextEvents](../../winscript/reference/idebugdocumenttextevents-interface.md)  
  
- [IDebugDocumentTextExternalAuthor Interface](../../winscript/reference/idebugdocumenttextexternalauthor-interface.md)  
  
- [Interface IDebugExpression](../../winscript/reference/idebugexpression-interface.md)  
  
- [IDebugExpressionCallBack Interface](../../winscript/reference/idebugexpressioncallback-interface.md)  
  
- [Interface IDebugExpressionContext](../../winscript/reference/idebugexpressioncontext-interface.md)  
  
- [Interface IDebugFormatter](../../winscript/reference/idebugformatter-interface.md)  
  
- [Interface IDebugHelper](../../winscript/reference/idebughelper-interface.md)  
  
- [Interface IDebugSessionProvider](../../winscript/reference/idebugsessionprovider-interface.md)  
  
- [Interface IDebugSessionProviderEx](../../winscript/reference/idebugsessionproviderex-interface.md)  
  
- [Interface IDebugStackFrame](../../winscript/reference/idebugstackframe-interface.md)  
  
- [Interface IDebugStackFrameSniffer](../../winscript/reference/idebugstackframesniffer-interface.md)  
  
- [Interface IDebugStackFrameSnifferEx](../../winscript/reference/idebugstackframesnifferex-interface.md)  
  
- [Interface IDebugSyncOperation](../../winscript/reference/idebugsyncoperation-interface.md)  
  
- [Interface IDebugThreadCall](../../winscript/reference/idebugthreadcall-interface.md)  
  
- [Interface IEnumDebugApplicationNodes](../../winscript/reference/ienumdebugapplicationnodes-interface.md)  
  
- [Interface IEnumDebugCodeContexts](../../winscript/reference/ienumdebugcodecontexts-interface.md)  
  
- [Interface IEnumDebugExpressionContexts](../../winscript/reference/ienumdebugexpressioncontexts-interface.md)  
  
- [Interface IEnumDebugStackFrames](../../winscript/reference/ienumdebugstackframes-interface.md)  
  
- [Interface IEnumJsStackFrames](../../winscript/reference/ienumjsstackframes-interface.md)  
  
- [Interface IEnumRemoteDebugApplications](../../winscript/reference/ienumremotedebugapplications-interface.md)  
  
- [IEnumRemoteDebugApplicationThreads Interface](../../winscript/reference/ienumremotedebugapplicationthreads-interface.md)  
  
- [Interface IJsDebug](../../winscript/reference/ijsdebug-interface.md)  
  
- [Interface IJsDebugBreakPoint](../../winscript/reference/ijsdebugbreakpoint-interface.md)  
  
- [Interface IJsDebugDataTarget](../../winscript/reference/ijsdebugdatatarget-interface.md)  
  
- [Interface IJsDebugFrame](../../winscript/reference/ijsdebugframe-interface.md)  
  
- [Interface IJsDebugProcess](../../winscript/reference/ijsdebugprocess-interface.md)  
  
- [Interface IJsDebugProperty](../../winscript/reference/ijsdebugproperty-interface.md)  
  
- [Interface IJsDebugStackWalker](../../winscript/reference/ijsdebugstackwalker-interface.md)  
  
- [Interface IJsEnumDebugProperty](../../winscript/reference/ijsenumdebugproperty-interface.md)  
  
- [Interface IMachineDebugManager](../../winscript/reference/imachinedebugmanager-interface.md)  
  
- [Interface IMachineDebugManagerCookie](../../winscript/reference/imachinedebugmanagercookie-interface.md)  
  
- [Interface IMachineDebugManagerEvents](../../winscript/reference/imachinedebugmanagerevents-interface.md)  
  
- [Interface IProcessDebugManager](../../winscript/reference/iprocessdebugmanager-interface.md)  
  
- [IProvideExpressionContexts Interface](../../winscript/reference/iprovideexpressioncontexts-interface.md)  
  
- [IRemoteDebugApplication Interface](../../winscript/reference/iremotedebugapplication-interface.md)  
  
- [Interface IRemoteDebugApplication110](../../winscript/reference/iremotedebugapplication110-interface.md)  
  
- [Interface IRemoteDebugApplicationEx](../../winscript/reference/iremotedebugapplicationex-interface.md)  
  
- [Interface IRemoteDebugApplicationEvents](../../winscript/reference/iremotedebugapplicationevents-interface.md)  
  
- [Interface IRemoteDebugApplicationThread](../../winscript/reference/iremotedebugapplicationthread-interface.md)  
  
- [Interface IRemoteDebugApplicationThreadEx](../../winscript/reference/iremotedebugapplicationthreadex-interface.md)  
  
- [Interface ISetNextStatement](../../winscript/reference/isetnextstatement-interface.md)  
  
- [Interface ISimpleConnectionPoint](../../winscript/reference/isimpleconnectionpoint-interface.md)  
  
- [Interface IWebAppDiagnosticsSetup](../../winscript/reference/iwebappdiagnosticssetup-interface.md)  
  
- [Interface IWebAppDiagnosticsObjectInitialization](../../winscript/reference/iwebappdiagnosticsobjectinitialization-interface.md)  
  
  A seção a seguir lista as constantes, enumerações e estruturas usadas para depuração:  
  
- [Constantes, enumerações e estruturas de depurador do script ativo](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de depuração de script ativo](../../winscript/active-script-debugging-overview.md)