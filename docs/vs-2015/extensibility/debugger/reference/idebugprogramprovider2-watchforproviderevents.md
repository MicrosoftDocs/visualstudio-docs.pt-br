---
title: IDebugProgramProvider2::WatchForProviderEvents | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugProgramProvider2::WatchForProviderEvents
helpviewer_keywords:
- IDebugProgramProvider2::WatchForProviderEvents
ms.assetid: 2eb93653-b5fb-45b6-b136-56008c5d25ef
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6034898ad8c10583a8fa982a978fa05aa884d25a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787686"
---
# <a name="idebugprogramprovider2watchforproviderevents"></a>IDebugProgramProvider2::WatchForProviderEvents
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Permite que o processo ser notificado de eventos de porta.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT WatchForProviderEvents(  
   PROVIDER_FLAGS       Flags,  
   IDebugDefaultPort2*  pPort,  
   AD_PROCESS_ID        processId,  
   CONST_GUID_ARRAY     EngineFilter,  
   REFGUID              guidLaunchingEngine,  
   IDebugPortNotify2*   pEventCallback  
);  
```  
  
```csharp  
int WatchForProviderEvents(  
   enum_PROVIDER_FLAGS   Flags,  
   IDebugDefaultPort2    pPort,  
   AD_PROCESS_ID         ProcessId,  
   CONST_GUID_ARRAY      EngineFilter,  
   ref Guid              guidLaunchingEngine,  
   IDebugPortNotify2     pEventCallback  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `Flags`  
 [in] Uma combinação de sinalizadores do [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) enumeração. Os sinalizadores a seguir são típicos para essa chamada:  
  
|Sinalizador|Descrição|  
|----------|-----------------|  
|`PFLAG_REMOTE_PORT`|Chamador está em execução no computador remoto.|  
|`PFLAG_DEBUGGEE`|Chamador está atualmente em depuração (informações adicionais sobre a realização de marshaling serão retornadas para cada nó).|  
|`PFLAG_ATTACHED_TO_DEBUGGEE`|Chamador foi anexado ao, mas não é iniciado pelo depurador.|  
|`PFLAG_REASON_WATCH`|Chamador deseja observar eventos. Se este sinalizador não for definido. em seguida, o evento de retorno de chamada é removido e o chamador não recebe notificações.|  
  
 `pPort`  
 [in] A porta que o processo de chamada está em execução.  
  
 `processId`  
 [in] Uma [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) estrutura que contém a ID do processo que contém o programa em questão.  
  
 `EngineFilter`  
 [in] Uma matriz de GUIDs de mecanismos de depuração associados com o processo.  
  
 `guidLaunchingEngine`  
 [in] GUID do mecanismo de depuração que iniciou esse processo (se houver).  
  
 `pEventCallback`  
 [in] Uma [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) objeto que recebe as notificações de eventos.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Quando um chamador quiser remover um manipulador de eventos que foi estabelecido com uma chamada anterior a esse método, o chamador passa os mesmos parâmetros, como ele fez na primeira vez, mas deixa desativar o `PFLAG_REASON_WATCH` sinalizador.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como implementar esse método para um **CDebugEngine** objeto que expõe a [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) interface.  
  
```cpp#  
STDMETHODIMP CDebugEngine::WatchForProviderEvents(  
    PROVIDER_FLAGS Flags,   
    IDebugDefaultPort2 *pPort,   
    AD_PROCESS_ID processId,   
    CONST_GUID_ARRAY EngineFilter,   
    REFGUID guidLaunchingEngine,   
    IDebugPortNotify2 *pPortNotify)  
{  
    HRESULT hRes = E_FAIL;  
  
    if (EVAL(pPort != NULL) && EVAL(pPortNotify != NULL))  
    {  
        // We will only watch/send events about the process if the debugger  
        // is actually debugging the process, and only if this is an attach or a LoRIE launch  
        if (IsFlagSet(Flags, PFLAG_DEBUGGEE) &&  
            guidLaunchingEngine == GUID_NULL &&  
            processId.ProcessIdType == AD_PROCESS_ID_SYSTEM)  
        {  
            // We don't support WatchForProviderEvents when in interop mode  
            if (m_fInterop)  
            {  
                ASSERT(!"Shouldn't ever be called in interop mode");  
                hRes = E_FAIL;  
            }  
            else  
            {  
                if (IsFlagSet(Flags, PFLAG_REASON_WATCH))  
                {  
                    // QI to get IDebugEventCallback2 which is required.  
                    CComQIPtr<IDebugEventCallback2> pCallback(pPortNotify);  
  
                    ASSERT(pCallback != NULL);  
                    if ( pCallback != NULL )  
                    {  
                        // Register the callback  
                        hRes = this->InitDebugSession(pCallback);  
  
                        if ( S_OK == hRes )  
                        {  
                            // Get the IDebugProcess2 from the port and call AttachImpl  
                            CComPtr<IDebugProcess2> spProcess;  
  
                            hRes = pPort->GetProcess(processId, &spProcess);  
  
                            if (HREVAL(S_OK, hRes))  
                            {  
                                hRes = AttachImpl(spProcess, NULL, NULL, processId.ProcessId.dwProcessId, ATTACH_REASON_USER, NULL);  
  
                                if ( FAILED(hRes) && (!m_pPidList || 0 == m_pPidList->GetCount()) )  
                                    this->Cleanup();  
                            }  
                        }  
                        else  
                            this->Cleanup();  
                    }  
                    else  
                        hRes = E_FAIL;  
                }  
                else  
                {  
                    // Detach will be done by SDM calling on programs directly if there are managed programs.  
  
                    // This handling is the case where no managed code ever ran.  
                    if ( this->IsProcessBeingDebugged(processId.ProcessId.dwProcessId) )  
                    {  
                        ProgramList *pProgList = this->GetProgramListCopy();  
  
                        if ( EVAL(pProgList) )  
                        {  
                            if ( pProgList->GetCount() == 0)  
                            {  
                                CComPtr<ICorDebugProcess> pCorProcess;  
  
                                hRes = this->GetCorProcess(processId.ProcessId.dwProcessId, &pCorProcess);  
  
                                if (HREVAL(S_OK, hRes) )  
                                {  
                                    hRes = pCorProcess->Stop(INFINITE);  
  
                                    if ( HREVAL(S_OK, hRes) )  
                                        hRes = pCorProcess->Detach();  
                                }  
  
                                // Tell the engine that it should unregister this process from com+  
                                this->UnregisterProcess(processId.ProcessId.dwProcessId);  
  
                                // If there are no more pids left then cleanup everything.  
                                if ( 0 == m_pPidList->GetCount() )  
                                    this->Cleanup();  
                            }  
                            // This is needed for cases where the SDM has not yet recieved program create  
                            // by the time that we need to detach (example: the managed attach succeeds,  
                            // but some other attach step fails).  
                            else  
                            {  
                                PROGNODE *pProgNode = NULL;  
                                while ( pProgNode = pProgList->Next(pProgNode) )  
                                {  
                                    CDebugProgram * pProgram = ((CDebugProgram *)pProgNode->data);  
                                    hRes = pProgram->Detach();  
                                }  
                            }  
  
                            delete pProgList;  
                        }  
                    }  
                    else  
                        hRes = S_OK;  
                }  
            }  
        }  
        else  
        {  
            hRes = S_FALSE;  
        }  
    }  
    else  
    {  
        hRes = E_INVALIDARG;  
    }  
  
    return hRes;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)   
 [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)   
 [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)   
 [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)   
 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)

