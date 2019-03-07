---
title: Expor eventos no SDK do Visual Studio | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- events [Visual Studio], exposing
- automation [Visual Studio SDK], exposing events
ms.assetid: 70bbc258-c221-44f8-b0d7-94087d83b8fe
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3cc905e359d7bcb2946d627ebcb3c28067233fa0
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56603151"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>Expor eventos no SDK do Visual Studio
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] permite a fonte de eventos usando a automação. É recomendável que a fonte de eventos para projetos e itens de projeto.

 Eventos são recuperados pelos consumidores de automação do <xref:EnvDTE.DTEClass.Events%2A> objeto ou <xref:EnvDTE.DTEClass.GetObject%2A> (por exemplo, `GetObject("EventObjectName")`). As chamadas de ambiente `IDispatch::Invoke` usando o `DISPATCH_METHOD` ou `DISPATCH_PROPERTYGET` sinalizadores para retornar um evento.

 O processo a seguir explica como os eventos específicos de VSPackage são retornados.

1. O ambiente inicia.

2. Ele lê a partir do registro todos os nomes de valor sob a **automação**, **AutomationEvents**, e **AutomationProperties** chaves de todos os VSPackages e armazena os nomes em um tabela.

3. Chama um consumidor de automação, neste exemplo, `DTE.Events.AutomationProjectsEvents` ou `DTE.Events.AutomationProjectItemsEvents`.

4. O ambiente localiza o parâmetro de cadeia de caracteres na tabela e carrega o VSPackage correspondente.

5. O ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método usando o nome passado na chamada; neste exemplo, `AutomationProjectsEvents` ou `AutomationProjectItemsEvents`.

6. O VSPackage cria um objeto de raiz que tem métodos como `get_AutomationProjectsEvents` e `get_AutomationProjectItemEvents` e, em seguida, retorna um ponteiro de IDispatch para o objeto.

7. O ambiente chama o método apropriado com base no nome passado para a chamada de automação.

8. O `get_` método cria outro objeto IDispatch com base em eventos que implementa ambos o `IConnectionPointContainer` interface e o `IConnectionPoint` interface e retorna um `IDispatchpointer` ao objeto.

   Para expor um evento usando a automação, você deve responder às <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> e inspeção para cadeias de caracteres que você adiciona ao registro. No exemplo de projeto básico, as cadeias de caracteres são *BscProjectsEvents* e *BscProjectItemsEvents*.

## <a name="registry-entries-from-the-basic-project-sample"></a>Entradas do registro do exemplo de projeto básico
 Esta seção mostra onde adicionar valores de evento de automação para o registro.

 **[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Packages\\<PkgGUID\>\AutomationEvents]**

 **AutomationProjectEvents** = retorna o `AutomationProjectEvents` objeto.

 **AutomationProjectItemEvents** = retorna o `AutomationProjectItemsEvents` objeto.

|Nome|Tipo|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|Padrão (@)|REG_SZ|Não usado|Não utilizado. Você pode usar o campo de dados para obter a documentação.|
|*AutomationProjectsEvents*|REG_SZ|Nome do seu objeto de evento.|Somente o nome da chave é relevante. Você pode usar o campo de dados para obter a documentação.<br /><br /> Este exemplo vem do exemplo de projeto básico.|
|*AutomationProjectItemEvents*|REG_SZ|Nome do seu objeto de evento|Somente o nome da chave é relevante. Você pode usar o campo de dados para obter a documentação.<br /><br /> Este exemplo vem do exemplo de projeto básico.|

 Quando qualquer um dos seus objetos de evento são solicitados por um consumidor de automação, crie um objeto de raiz que tem métodos para qualquer evento que suporta o VSPackage. O ambiente chama apropriado `get_` método nesse objeto. Por exemplo, se `DTE.Events.AutomationProjectsEvents` é chamado, o `get_AutomationProjectsEvents` método no objeto raiz é invocado.

 ![Eventos de projeto do Visual Studio](../../extensibility/internals/media/projectevents.gif "ProjectEvents") modelo de automação para eventos

 A classe `CProjectEventsContainer` representa o objeto de fonte para *BscProjectsEvents*, e `CProjectItemsEventsContainer` representa o objeto de origem para *BscProjectItemsEvents*.

 Na maioria dos casos, você deve retornar um novo objeto para cada solicitação de evento como a maioria dos objetos de evento usa um objeto de filtro. Quando você acionar seu evento, verifique esse filtro para verificar que o manipulador de eventos está sendo chamado.

 *AutomationEvents.h* e *AutomationEvents.cpp* contêm declarações e implementações das classes na tabela a seguir.

|Classe|Descrição|
|-----------|-----------------|
|`CAutomationEvents`|Implementa um objeto de raiz de evento, recuperado do `DTE.Events` objeto.|
|`CProjectsEventsContainer` e `CProjectItemsEventsContainer`|Implemente os objetos de fonte de eventos que acionam os eventos correspondentes.|

 O exemplo de código a seguir mostra como responder a uma solicitação para um objeto de evento.

```cpp
STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
{
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

    if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        //Is the requested name our Projects object?
    {
        return GetAutomationProjects(ppIDispatch);
        // Gets our Projects object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        //Is the requested name our ProjectsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectEvents object.
    }
    else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)  //Is the requested name our ProjectsItemsEvents object?
    {
        return CAutomationEvents::GetAutomationEvents(ppIDispatch);
          // Gets our ProjectItemsEvents object.
    }
    return E_INVALIDARG;
}
```

 No código acima, `g_wszAutomationProjects` é o nome da sua coleção de projeto (*FigProjects*), `g_wszAutomationProjectsEvents` (*FigProjectsEvents*) e `g_wszAutomationProjectItemsEvents` (*FigProjectItemEvents* ) são os nomes dos eventos do projeto e eventos que são originados de sua implementação de VSPackage itens do projeto.

 Objetos de evento são recuperados do mesmo local central, o `DTE.Events` objeto. Dessa forma, todos os objetos de evento são agrupados juntos para que um usuário final não precisa procurar o modelo de objeto inteiro para localizar um evento específico. Isso também permite fornecer seus objetos de VSPackage específicos, em vez de exigir que você implemente seu próprio código para todo o sistema de eventos. No entanto, para o usuário final, que deve encontrar um evento para seu `ProjectItem` interface, não é imediatamente clara de onde esse objeto é recuperado.

## <a name="see-also"></a>Consulte também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
