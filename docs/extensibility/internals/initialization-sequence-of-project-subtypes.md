---
title: Sequência de inicialização de subtipos de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: fe7e7a574d04ec9a49252e32e0fbb8b5685778aa
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131601"
---
# <a name="initialization-sequence-of-project-subtypes"></a>Sequência de inicialização de subtipos de projeto
O ambiente constrói um projeto, chamando a implementação de fábrica de projeto base de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>. A construção de um subtipo de projeto é iniciado quando o ambiente determina se a lista GUID do tipo de projeto para a extensão de um arquivo de projeto não está vazia. A extensão de arquivo de projeto e o GUID do projeto especificam se o projeto é um [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ou [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] tipo de projeto. Por exemplo, a extensão. vbproj e {F184B08F-C81C-45F6-A57F-5ABD9991F28F} identificar um [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] projeto.

## <a name="environments-initialization-of-project-subtypes"></a>Inicialização do ambiente de subtipos de projeto
 O procedimento a seguir fornece detalhes sobre a sequência de inicialização para um sistema de projeto agregado por vários subtipos de projeto.

1.  O ambiente chama o projeto base <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>, e enquanto o projeto analisa o arquivo de projeto descobre que o tipo de projeto de agregação lista de GUIDs não é `null`. O projeto interrompe diretamente a criação de seu projeto.

2.  As chamadas de projeto `QueryService` na <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> service para criar um subtipo de projeto usando a implementação do ambiente do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> método. Dentro desse método, o ambiente faz chamadas de função recursiva para suas implementações de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>, <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> métodos enquanto ele é percorra a lista de projeto tipo GUIDs, começando com o subtipo de projeto externo.

     A tabela a seguir detalha as etapas de inicialização.

    1.  A implementação do ambiente do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> chamadas de método de `HrCreateInnerProj` método com a declaração de função a seguir:

         <CodeContentPlaceHolder>0</CodeContentPlaceHolder>

         Quando essa função é chamada pela primeira vez, ou seja, para o subtipo de projeto mais externo, os parâmetros `pOuter` e `pOwner` são passados como `null` e a função define o subtipo de projeto externo `IUnknown` para `pOuter`.

    2.  Em seguida o ambiente chama `HrCreateInnerProj` função com o segundo tipo de projeto GUID na lista. Esse GUID correspondente para o subtipo de projeto interna segundo passo a passo para o projeto base na sequência de agregação.

    3.  O `pOuter` agora está apontando para o `IUnknown` do subtipo do projeto mais externo, e `HrCreateInnerProj` chama sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> seguido por uma chamada para a implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>. Em <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> método você passar o controle `IUnknown` do subtipo do projeto mais externo, `pOuter`. O projeto de propriedade (subtipo de projeto interna) precisa criar o objeto de projeto agregado aqui. No <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> implementação do método você transmitir um ponteiro para o `IUnknown` do projeto interno que está sendo agregado. Esses dois métodos criam o objeto de agregação e suas implementações precisam seguir as regras de agregação COM para garantir que um subtipo de projeto não termine mantendo uma contagem de referência a mesmo.

    4.  `HrCreateInnerProj` chama sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>. Nesse método, o subtipo de projeto faz seu trabalho de inicialização. Por exemplo, você pode registrar eventos de solução em <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>.

    5.  `HrCreateInnerProj` é chamado repetidamente até que o último GUID (projeto base) na lista seja atingido. Para cada uma dessas chamadas, as etapas c a d, são repetidas. `pOuter` aponta para o subtipo de projeto externo `IUnknown` para cada nível de agregação.

## <a name="example"></a>Exemplo

O exemplo a seguir detalha o processo de programação em uma representação aproximado do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> método como ele é implementado pelo ambiente. O código é um exemplo. não é destinado a ser compilado, e a verificação de todos os erros tiverem sido removidas para maior clareza.

```cpp
HRESULT CreateAggregateProject
(
    LPCOLESTR lpstrGuids,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    REFIID iidProject,
    void **ppvProject)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpunkProj;
    CComPtr<IVsAggregatableProject> srpAggProject;
    CComBSTR bstrGuids = lpstrGuids;
    BOOL fCanceled = FALSE;
    *ppvProject = NULL;

    HrCreateInnerProj(
         bstrGuids, NULL, NULL, pszFilename, pszLocation,
         pszName, grfCreateFlags, &srpunkProj, &fCanceled);
    srpunkProj->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggProject));
    srpAggProject->OnAggregationComplete();
    srpunkProj->QueryInterface(iidProject, ppvProject);
}

HRESULT HrCreateInnerProj
(
    WCHAR *pwszGuids,
    IUnknown *pOuter,
    IVsAggregatableProject *pOwner,
    LPCOLESTR pszFilename,
    LPCOLESTR pszLocation,
    LPCOLESTR pszName,
    VSCREATEPROJFLAGS grfCreateFlags,
    IUnknown **ppInner,
    BOOL *pfCanceled
)
{
    HRESULT hr = NOERROR;
    CComPtr<IUnknown> srpInner;
    CComPtr<IVsAggregatableProject> srpAggInner;
    CComPtr<IVsProjectFactory> srpProjectFactory;
    CComPtr<IVsAggregatableProjectFactory> srpAggPF;
    GUID guid = GUID_NULL;
    WCHAR *pwszNextGuids = wcschr(pwszGuids, L';');
    WCHAR wszText[_MAX_PATH+150] = L"";

    if (pwszNextGuids)
    {
        *pwszNextGuids++ = 0;
    }

    CLSIDFromString(pwszGuids, &guid);
    GetProjectTypeMgr()->HrGetProjectFactoryOfGuid(
        guid, &srpProjectFactory);
    srpProjectFactory->QueryInterface(
        IID_IVsAggregatableProjectFactory,
        (void **)&srpAggPF);
    srpAggPF->PreCreateForOuter(pOuter, &srpInner);
    srpInner->QueryInterface(
        IID_IVsAggregatableProject, (void **)&srpAggInner);

    if (pOwner)
    {
        IfFailGo(pOwner->SetInnerProject(srpInner));
    }

    if (pwszNextGuids)
    {
        CComPtr<IUnknown> srpNextInner;
        HrCreateInnerProj(
            pwszNextGuids, pOuter ? pOuter : srpInner,
            srpAggInner, pszFilename, pszLocation, pszName,
            grfCreateFlags, &srpNextInner, pfCanceled);
    }

    return srpAggInner->InitializeForOuter(
        pszFilename, pszLocation, pszName, grfCreateFlags,
        IID_IUnknown, (void **)ppInner, pfCanceled);
}
```

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)