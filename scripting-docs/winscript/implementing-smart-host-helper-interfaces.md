---
title: Interfaces auxiliares do host inteligente de implementação | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Smart Host Helper Interfaces, implementing
ms.assetid: b9c44246-4d4d-469e-91be-00c8f5796fa5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: deac5827aa38039099f1d0f5e621d473db96743d
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835596"
---
# <a name="implementing-smart-host-helper-interfaces"></a>Interfaces auxiliares do host inteligente de implementação
A [Interface IDebugDocumentHelper](../winscript/reference/idebugdocumenthelper-interface.md) simplifica a tarefa de criação de um host inteligente para depuração ativa, porque ela fornece implementações de várias interfaces necessárias para hospedagem inteligente.  
  
 Para ser um host inteligente usando `IDebugDocumentHelper`, um aplicativo host deve executar apenas três ações:  
  
1. `CoCreate` o gerenciador de depuração do processo e usar a [Interface IProcessDebugManager](../winscript/reference/iprocessdebugmanager-interface.md) para adicionar o aplicativo à lista de aplicativos depuráveis.  
  
2. Criar um auxiliar de documentos de depuração para cada objeto de script, usando o método [IProcessDebugManager::CreateDebugDocumentHelper](../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md). Verifique se o nome do documento, documento pai, texto e blocos de script estão definidos.  
  
3. Implemente a [Interface IActiveScriptSiteDebug](../winscript/reference/iactivescriptsitedebug-interface.md) em seu objeto que implementa a interface [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) (que é necessária para script ativo). O único método não trivial na interface `IActiveScriptSiteDebug` simplesmente delega para o auxiliar.  
  
   Opcionalmente, o host poderá implementar a [Interface IDebugDocumentHost](../winscript/reference/idebugdocumenthost-interface.md) se precisar de mais controle sobre as cores de sintaxe, a criação de contexto do documento e outras funcionalidades estendidas.  
  
   A principal limitação no auxiliar de host inteligente é que ele pode manipular apenas documentos cujo conteúdo é alterado ou reduzido depois de ser adicionado (embora documentos possam expandir). Para muitos hosts inteligentes, no entanto, a funcionalidade que ele fornece é exatamente o que é necessário.  
  
   As seções a seguir explicam cada etapa em mais detalhes.  
  
## <a name="create-an-application-object"></a>Criar um objeto de aplicativo  
 Antes que o auxiliar de host inteligente possa ser usado, é necessário criar um objeto de [Interface IDebugApplication](../winscript/reference/idebugapplication-interface.md) para representar seu aplicativo no depurador.  
  
#### <a name="to-create-an-application-object"></a>Para criar um objeto de aplicativo  
  
1. Criar uma instância do gerenciador de depuração do processo usando o `CoCreateInstance`.  
  
2. Chamar [IProcessDebugManager::CreateApplication](../winscript/reference/iprocessdebugmanager-createapplication.md).  
  
3. Defina o nome do aplicativo usando [IDebugApplication::SetName](../winscript/reference/idebugapplication-setname.md).  
  
4. Adicionar o objeto de aplicativo à lista de aplicativos depuráveis usando [IProcessDebugManager::AddApplication](../winscript/reference/iprocessdebugmanager-addapplication.md).  
  
     O código a seguir descreve o processo, mas ele não inclui a verificação de erros ou outras técnicas de programação robustas.  
  
    ```cpp
    CoCreateInstance(CLSID_ProcessDebugManager, NULL,  
          CLSCTX_INPROC_SERVER | CLSCTX_INPROC_HANDLER  
          | CLSCTX_LOCAL_SERVER,  
    IID_IProcessDebugManager, (void **)&g_ppdm);  
    g_ppdm->CreateApplication(&g_pda);  
    g_pda->SetName(L"My cool application");  
    g_ppdm->AddApplication(g_pda, &g_dwAppCookie);  
    ```  
  
## <a name="using-idebugdocumenthelper"></a>Usando IDebugDocumentHelper  
  
#### <a name="to-use-the-helper-minimal-sequence-of-steps"></a>Para usar o auxiliar (sequência de etapas mínima)  
  
1. Para cada documento de host, crie um auxiliar usando [IProcessDebugManager::CreateDebugDocumentHelper](../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md).  
  
2. Chame [IDebugDocumentHelper::Init](../winscript/reference/idebugdocumenthelper-init.md) no auxiliar, fornecendo o nome, atributos de documento e assim por diante.  
  
3. Chame [IDebugDocumentHelper::Attach](../winscript/reference/idebugdocumenthelper-attach.md) com o auxiliar pai para o documento (ou NULL se o documento é a raiz) para definir a posição do documento na árvore e torná-lo visível para o depurador.  
  
4. Chame [IDebugDocumentHelper::AddDBCSText](../winscript/reference/idebugdocumenthelper-adddbcstext.md) ou [IDebugDocumentHelper::AddUnicodeText](../winscript/reference/idebugdocumenthelper-addunicodetext.md) para definir o texto do documento. (Esses podem ser chamados várias vezes se o documento é baixado de forma incremental, como no caso de um navegador.)  
  
5. Chame [IDebugDocumentHelper::DefineScriptBlock](../winscript/reference/idebugdocumenthelper-definescriptblock.md) para definir os intervalos para cada bloco de script e os mecanismos de script associados.  
  
## <a name="implementing-iactivescriptsitedebug"></a>Implementando IActiveScriptSiteDebug  
 Para implementar [IActiveScriptSiteDebug::GetDocumentContextFromPosition](../winscript/reference/iactivescriptsitedebug-getdocumentcontextfromposition.md), obtenha o auxiliar que corresponde ao site especificado e, em seguida, obtenha o deslocamento inicial do documento para o contexto de origem fornecido, da seguinte maneira:  
  
```cpp
pddh->GetScriptBlockInfo(dwSourceContext, NULL, &ulStartPos, NULL);  
```  
  
 Em seguida, use o auxiliar para criar um novo contexto de documento para o deslocamento de caractere especificado:  
  
```cpp
pddh->CreateDebugDocumentContext(ulStartPos + uCharacterOffset, cChars, &pddcNew);  
```  
  
 Para implementar [IActiveScriptSiteDebug::GetRootApplicationNode](../winscript/reference/iactivescriptsitedebug-getrootapplicationnode.md), simplesmente chame `IDebugApplication::GetRootNode` (herdado de [IRemoteDebugApplication::GetRootNode](../winscript/reference/iremotedebugapplication-getrootnode.md)).  
  
 Para implementar [IDebugDocumentHelper::GetDebugApplicationNode](../winscript/reference/idebugdocumenthelper-getdebugapplicationnode.md), basta retornar o `IDebugApplication` que você criou inicialmente usando o gerenciador de depuração do processo.  
  
## <a name="the-optional-idebugdocumenthost-interface"></a>A interface IDebugDocumentHost opcional  
 O host pode fornecer uma implementação de [IDebugDocumentHost Interface](../winscript/reference/idebugdocumenthost-interface.md) usando [IDebugDocumentHelper::SetDebugDocumentHost](../winscript/reference/idebugdocumenthelper-setdebugdocumenthost.md) para lhe dar mais controle sobre o auxiliar. Aqui estão algumas coisas importantes que a interface de host permite que você faça:  
  
- Adicione texto usando [IDebugDocumentHelper::AddDeferredText](../winscript/reference/idebugdocumenthelper-adddeferredtext.md) para que o host não precise fornecer os caracteres reais imediatamente. Quando os caracteres forem realmente necessários, o auxiliar chamará [IDebugDocumentHost::GetDeferredText](../winscript/reference/idebugdocumenthost-getdeferredtext.md) no host.  
  
- Substitua a colorização de sintaxe padrão fornecida pelo auxiliar. O auxiliar chamará [IDebugDocumentHost::GetScriptTextAttributes](../winscript/reference/idebugdocumenthost-getscripttextattributes.md) para determinar a colorização para um intervalo de caracteres, voltando para sua implementação padrão se o host retornar `E_NOTIMPL`.  
  
- Fornecer um controle desconhecido para contextos de documento criados pelo auxiliar implementando [IDebugDocumentHost::OnCreateDocumentContext](../winscript/reference/idebugdocumenthost-oncreatedocumentcontext.md). Isso permite que o host substitua a funcionalidade da implementação do contexto de documento padrão.  
  
- Forneça um nome de caminho no sistema de arquivos para o documento. Algumas interfaces do usuário de depuração usam isso para permitir que o usuário edite e salve as alterações ao documento. [IDebugDocumentHost::NotifyChanged](../winscript/reference/idebugdocumenthost-notifychanged.md) é chamado para notificar o host depois que o documento foi salvo.  
  
## <a name="see-also"></a>Confira também  
 [Visão geral de depuração de script ativo](../winscript/active-script-debugging-overview.md)