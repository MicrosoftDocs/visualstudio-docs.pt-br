---
title: Expondo eventos no SDK do Visual Studio | Microsoft Docs
description: Saiba mais sobre os métodos do SDK do Visual Studio e as entradas do registro que expõem eventos para projetos e itens de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- events [Visual Studio], exposing
- automation [Visual Studio SDK], exposing events
ms.assetid: 70bbc258-c221-44f8-b0d7-94087d83b8fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 99298329b969df3b9d7dbb46a3f4b9e7d4ed7091
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898321"
---
# <a name="expose-events-in-the-visual-studio-sdk"></a>Expor eventos no SDK do Visual Studio
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] permite que você origemie eventos usando automação. É recomendável que você retenha eventos de origem para projetos e itens de projeto.

 Os eventos são recuperados por consumidores de automação do <xref:EnvDTE.DTEClass.Events%2A> objeto ou <xref:EnvDTE.DTEClass.GetObject%2A> (por exemplo, `GetObject("EventObjectName")` ). O ambiente chama `IDispatch::Invoke` usando os `DISPATCH_METHOD` sinalizadores ou `DISPATCH_PROPERTYGET` para retornar um evento.

 O processo a seguir explica como os eventos específicos do VSPackage são retornados.

1. O ambiente é iniciado.

2. Ele lê do registro todos os nomes de valor nas chaves **Automation**, **AutomationEvents** e **AutomationProperties** de todas as VSPackages e armazena esses nomes em uma tabela.

3. Um consumidor de automação chama, neste exemplo, `DTE.Events.AutomationProjectsEvents` ou `DTE.Events.AutomationProjectItemsEvents` .

4. O ambiente localiza o parâmetro de cadeia de caracteres na tabela e carrega o VSPackage correspondente.

5. O ambiente chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método usando o nome passado na chamada; neste exemplo, `AutomationProjectsEvents` ou `AutomationProjectItemsEvents` .

6. O VSPackage cria um objeto raiz que tem métodos como `get_AutomationProjectsEvents` e `get_AutomationProjectItemEvents` e, em seguida, retorna um ponteiro IDispatch para o objeto.

7. O ambiente chama o método apropriado com base no nome passado para a chamada de automação.

8. O `get_` método cria outro objeto de evento baseado em IDispatch que implementa a `IConnectionPointContainer` interface e a `IConnectionPoint` interface e retorna um `IDispatchpointer` para o objeto.

   Para expor um evento usando a automação, você deve responder <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> e observar as cadeias de caracteres adicionadas ao registro. No exemplo de projeto básico, as cadeias de caracteres são *BscProjectsEvents* e *BscProjectItemsEvents*.

## <a name="registry-entries-from-the-basic-project-sample"></a>Entradas do registro do exemplo de projeto básico
 Esta seção mostra onde adicionar valores de evento de automação ao registro.

 **[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Packages\\<PkgGUID \> \AutomationEvents]**

 **AutomationProjectEvents** = retorna o `AutomationProjectEvents` objeto.

 **AutomationProjectItemEvents** = retorna o `AutomationProjectItemsEvents` objeto.

|Nome|Tipo|Intervalo|Descrição|
|----------|----------|-----------|-----------------|
|Padrão (@)|REG_SZ|Não usado|Não utilizado. Você pode usar o campo de dados para documentação.|
|*AutomationProjectsEvents*|REG_SZ|Nome do seu objeto de evento.|Somente o nome da chave é relevante. Você pode usar o campo de dados para documentação.<br /><br /> Este exemplo vem do exemplo de projeto básico.|
|*AutomationProjectItemEvents*|REG_SZ|Nome do seu objeto de evento|Somente o nome da chave é relevante. Você pode usar o campo de dados para documentação.<br /><br /> Este exemplo vem do exemplo de projeto básico.|

 Quando qualquer um dos seus objetos de evento for solicitado por um consumidor de automação, crie um objeto raiz que tenha métodos para qualquer evento que seu VSPackage dê suporte. O ambiente chama o `get_` método apropriado neste objeto. Por exemplo, se `DTE.Events.AutomationProjectsEvents` for chamado, o `get_AutomationProjectsEvents` método no objeto raiz será invocado.

 ![Eventos de projeto do Visual Studio](../../extensibility/internals/media/projectevents.gif "ProjectEvents") Modelo de automação para eventos

 A classe `CProjectEventsContainer` representa o objeto de origem para *BscProjectsEvents* e `CProjectItemsEventsContainer` representa o objeto de origem para *BscProjectItemsEvents*.

 Na maioria dos casos, você deve retornar um novo objeto para cada solicitação de evento, pois a maioria dos objetos de evento pega um objeto de filtro. Quando você acionar seu evento, marque este filtro para verificar se o manipulador de eventos está sendo chamado.

 *AutomationEvents. h* e *AutomationEvents. cpp* contêm declarações e implementações das classes na tabela a seguir.

|Classe|Descrição|
|-----------|-----------------|
|`CAutomationEvents`|Implementa um objeto de raiz de evento, recuperado do `DTE.Events` objeto.|
|`CProjectsEventsContainer` e `CProjectItemsEventsContainer`|Implemente os objetos de origem do evento que acionam os eventos correspondentes.|

 O exemplo de código a seguir mostra como responder a uma solicitação de um objeto de evento.

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

 No código acima, `g_wszAutomationProjects` é o nome de sua coleção de projetos (*FigProjects*), `g_wszAutomationProjectsEvents` (*FigProjectsEvents*) e `g_wszAutomationProjectItemsEvents` (*FigProjectItemEvents*) são os nomes dos eventos de projeto e de itens de projeto que são originados da sua implementação de VSPackage.

 Os objetos de evento são recuperados do mesmo local central, o `DTE.Events` objeto. Dessa forma, todos os objetos de evento são agrupados para que um usuário final não precise procurar o modelo de objeto inteiro para localizar um evento específico. Isso também permite que você forneça seus objetos VSPackage específicos, em vez de exigir que você implemente seu próprio código para eventos de todo o sistema. No entanto, para o usuário final, que deve encontrar um evento para a sua `ProjectItem` interface, ele não é imediatamente limpo de onde o objeto de evento é recuperado.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
