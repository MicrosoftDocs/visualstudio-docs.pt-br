---
title: Obter uma porta | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 25b703eafccb412c33640a9e73e72afa09c0c277
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56695980"
---
# <a name="get-a-port"></a>Obter uma porta
Uma porta representa uma conexão a uma máquina que processos estão em execução. Esse computador pode ser o computador local ou em um computador remoto (que possivelmente poderia estar executando um sistema de operacional não são baseados no Windows, consulte [portas](../../extensibility/debugger/ports.md) para obter mais informações).

Uma porta é representada pela [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) interface. Ele é usado para obter informações sobre processos em execução no computador em que a porta está conectada a.

Um mecanismo de depuração precisa acessar uma porta para registrar os nós de programa com a porta e para atender a solicitações de informações do processo. Por exemplo, se o mecanismo de depuração implementa o [IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md) interface, a implementação para o [GetProviderProcessData](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) método pode pedir a porta para o processo necessário informações a serem retornadas.

Visual Studio fornece a porta necessária para o mecanismo de depuração, e ele obtém essa porta de um fornecedor de porta. Se um programa estiver anexado a (seja de dentro do depurador ou devido a uma exceção foi lançada, que dispara a caixa de diálogo Just-in-Time [JIT]), o usuário terá a opção de transporte (outro nome para um fornecedor de porta) para usar. Caso contrário, se o usuário inicia o programa a partir do depurador, o sistema de projeto Especifica o fornecedor de porta para usar. Em ambos os casos, o Visual Studio cria uma instância do fornecedor de porta, representado por um [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) interface e solicita uma nova porta chamando [adicionar porta](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) com um [ IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) interface. Em seguida, essa porta é passada para o mecanismo de depuração em um formulário ou outro.

## <a name="example"></a>Exemplo
Este fragmento de código mostra como usar a porta fornecida para [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) para registrar um nó de programa na [ResumeProcess](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md). Parâmetros não estão diretamente relacionados a esse conceito foram omitidos por motivos de clareza.

> [!NOTE]
> Este exemplo usa a porta para iniciar e retomar o processo e pressupõe que o [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md) interface é implementada na porta. Isso não é a única maneira de realizar essas tarefas, e é possível que a porta não pode até mesmo ser envolvida diferente do que o programa [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) atribuído a ele.

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
                hr = spPortEx->ResumeProcess(pDebugProcess);
            }
        }
    }
    return(hr);
}
```

## <a name="see-also"></a>Consulte também
- [Registrar o programa](../../extensibility/debugger/registering-the-program.md)
- [Habilitar um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
- [Fornecedores de porta](../../extensibility/debugger/port-suppliers.md)
- [Portas](../../extensibility/debugger/ports.md)
