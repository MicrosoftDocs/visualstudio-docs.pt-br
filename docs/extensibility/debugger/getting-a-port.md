---
title: Obtendo uma porta | Microsoft Docs
description: Saiba como o Visual Studio fornece uma porta para o mecanismo de depuração para registrar nós de programa com a porta e atender a solicitações de informações de processo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b2d9c58f9a2e58e58fce44cb06827e9039e48c9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054862"
---
# <a name="get-a-port"></a>Obter uma porta
Uma porta representa uma conexão com um computador no qual os processos estão em execução. Esse computador pode ser o computador local ou um computador remoto (que poderia estar executando um sistema operacional não baseado no Windows; consulte [portas](../../extensibility/debugger/ports.md) para obter mais informações).

Uma porta é representada pela interface [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) . Ele é usado para obter informações sobre processos em execução no computador ao qual a porta está conectada.

Um mecanismo de depuração precisa acessar uma porta para registrar nós de programa com a porta e atender a solicitações de informações de processo. Por exemplo, se o mecanismo de depuração implementar a interface [IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md) , a implementação do método [GetProviderProcessData](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) poderá solicitar a porta para que as informações necessárias do processo sejam retornadas.

O Visual Studio fornece a porta necessária para o mecanismo de depuração e obtém essa porta de um fornecedor de porta. Se um programa estiver anexado a (de dentro do depurador ou devido a uma exceção gerada, o que dispara a caixa de diálogo [JIT] just-in-time), o usuário receberá a opção de transporte (outro nome para um fornecedor de porta) a ser usado. Caso contrário, se o usuário iniciar o programa de dentro do depurador, o sistema do projeto especificará o fornecedor da porta a ser usado. Em qualquer evento, o Visual Studio instancia o fornecedor da porta, representado por uma interface [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) , e solicita uma nova porta chamando [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) com uma interface [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) . Essa porta é passada para o mecanismo de depuração de uma forma ou outra.

## <a name="example"></a>Exemplo
Este fragmento de código mostra como usar a porta fornecida para [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) para registrar um nó de programa no [ResumeProcess](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md). Os parâmetros que não estão diretamente relacionados a esse conceito foram omitidos para fins de clareza.

> [!NOTE]
> Este exemplo usa a porta para iniciar e retomar o processo e pressupõe que a interface [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md) está implementada na porta. Isso não significa a única maneira de executar essas tarefas, e é possível que a porta não possa nem mesmo estar envolvida a não ser que o [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) do programa seja fornecido a ele.

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

## <a name="see-also"></a>Confira também
- [Registrando o programa](../../extensibility/debugger/registering-the-program.md)
- [Habilitando um programa a ser depurado](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
- [Fornecedores de porta](../../extensibility/debugger/port-suppliers.md)
- [Portas](../../extensibility/debugger/ports.md)
