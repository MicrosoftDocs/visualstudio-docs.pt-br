---
title: Registrar o programa | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- programs, registration
- debugging [Debugging SDK], program registration
ms.assetid: d726a161-7db3-4ef4-b258-9f6a5be68418
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e12e0ed9abf90911e9d22de60d8dc11363f67adb
ms.sourcegitcommit: 20d1b9a5bf041bb28453501eb63bc0537a8e4f54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51645062"
---
# <a name="register-the-program"></a>Registrar o programa
Depois que o mecanismo de depuração tiver adquirido uma porta, representado por um [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) interface, a próxima etapa na habilitação de programa a ser depurado é registrá-lo com a porta. Depois de registrado, o programa está disponível para depuração por um dos seguintes meios:  
  
-   O processo de anexação, que permite que o depurador obtenha controle total de depuração de um aplicativo em execução.  
  
-   Just-in-time (JIT) depuração, que permite depurar os após o fato de um programa que é executado independentemente de um depurador. Quando a arquitetura de tempo de execução captura uma falha, o depurador é notificado antes do sistema operacional ou o ambiente de tempo de execução libera a memória e os recursos do programa com falha.  
  
## <a name="registering-procedure"></a>Registrar o procedimento  
  
### <a name="to-register-your-program"></a>Para registrar o seu programa  
  
1.  Chame o [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) método implementado pela porta.  
  
     `IDebugPortNotify2::AddProgramNode` requer um ponteiro para um [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) interface.  
  
     Normalmente, quando o sistema operacional ou o ambiente de tempo de execução carrega um programa, ele cria o nó do programa. Se o mecanismo de depuração (DES) é solicitado carregar o programa, o DE cria e registra o nó do programa.  
  
     O exemplo a seguir mostra o mecanismo de depuração iniciar o programa e registrá-lo com uma porta.  
  
    > [!NOTE]
    >  Este exemplo de código não é a única maneira de iniciar e reiniciar um processo; Esse código é principalmente um exemplo de registro de um programa com uma porta.  
  
    ```cpp  
    // This is an IDebugEngineLaunch2 method.  
    HRESULT CDebugEngine::LaunchSuspended(/* omitted parameters */,  
                                          IDebugPort2 *pPort,  
                                          /* omitted parameters */,  
                                          IDebugProcess2**ppDebugProcess)  
    {  
        // do stuff here to set up for a launch (such as handling the other parameters)  
        ...  
  
        // Now get the IPortNotify2 interface so we can register a program node  
        // in CDebugEngine::ResumeProcess.  
        CComPtr<IDebugDefaultPort2> spDefaultPort;  
        HRESULT hr = pPort->QueryInterface(&spDefaultPort);  
        if (SUCCEEDED(hr))  
        {  
            CComPtr<IDebugPortNotify2> spPortNotify;  
            hr = spDefaultPort->GetPortNotify(&spPortNotify);  
            if (SUCCEEDED(hr))  
            {  
                // Remember the port notify so we can use it in ResumeProcess.  
                m_spPortNotify = spPortNotify;  
  
                // Now launch the process in a suspended state and return the  
                // IDebugProcess2 interface  
                CComPtr<IDebugPortEx2> spPortEx;  
                hr = pPort->QueryInterface(&spPortEx);  
                if (SUCCEEDED(hr))  
                {  
                    // pass on the parameters we were given (omitted here)  
                    hr = spPortEx->LaunchSuspended(/* omitted parameters */,ppDebugProcess)  
                }  
            }  
        }  
        return(hr);  
    }  
  
    HRESULT CDebugEngine::ResumeProcess(IDebugProcess2 *pDebugProcess)  
    {  
        // Make a program node for this process  
        HRESULT hr;  
        CComPtr<IDebugProgramNode2> spProgramNode;  
        hr = this->GetProgramNodeForProcess(pProcess, &spProgramNode);  
        if (SUCCEEDED(hr))  
        {  
            hr = m_spPortNotify->AddProgramNode(spProgramNode);  
            if (SUCCEEDED(hr))  
            {  
                // resume execution of the process using the port given to us earlier.  
               // (Querying for the IDebugPortEx2 interface is valid here since  
               // that's how we got the IDebugPortNotify2 interface in the first place.)  
                CComPtr<IDebugPortEx2> spPortEx;  
                hr = m_spPortNotify->QueryInterface(&spPortEx);  
                if (SUCCEEDED(hr))  
                {  
                    hr  = spPortEx->ResumeProcess(pDebugProcess);  
                }  
            }  
        }  
        return(hr);  
    }  
  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Obter uma porta](../../extensibility/debugger/getting-a-port.md)   
 [Habilitar um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)