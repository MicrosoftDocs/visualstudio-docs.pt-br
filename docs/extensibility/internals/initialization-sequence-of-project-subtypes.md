---
title: Sequência de inicialização de subtipos de projeto | Microsoft Docs
description: Saiba mais sobre a sequência de inicialização no ambiente do Visual Studio para um sistema de projeto agregado por vários subtipos de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 88a8aa39c513ed6317a6b57509810e16a58f192b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069537"
---
# <a name="initialization-sequence-of-project-subtypes"></a>Sequência de inicialização de subtipos de projeto
O ambiente constrói um projeto chamando a implementação de fábrica do projeto base do <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> . A construção de um subtipo de projeto é iniciada quando o ambiente determina que a lista de GUIDs do tipo de projeto para a extensão de um arquivo de projeto não está vazia. A extensão de arquivo de projeto e o GUID do projeto especificam se o projeto é um [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] tipo de projeto ou. Por exemplo, a extensão. vbproj e {F184B08F-C81C-45F6-A57F-5ABD9991F28F} identificam um [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] projeto.

## <a name="environments-initialization-of-project-subtypes"></a>Inicialização do ambiente de subtipos de projeto
 O procedimento a seguir detalha a sequência de inicialização para um sistema de projeto agregado por vários subtipos de projeto.

1. O ambiente chama o projeto base <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> e, enquanto o projeto analisa seu arquivo de projeto, ele descobre que a lista de GUIDs do tipo de projeto agregado não é `null` . O projeto descontinua criando seu projeto diretamente.

2. O projeto chama `QueryService` o <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> serviço para criar um subtipo de projeto usando a implementação do ambiente do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> método. Dentro desse método, o ambiente faz chamadas de função recursivas para suas implementações <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> métodos enquanto está percorrendo a lista de GUIDs de tipo de projeto, começando com o subtipo de projeto mais externo.

     Veja a seguir os detalhes das etapas de inicialização.

    1. A implementação do ambiente do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> método chama o `HrCreateInnerProj` método com a seguinte declaração de função:

         \<CodeContentPlaceHolder>0</CodeContentPlaceHolder>

         Quando essa função é chamada pela primeira vez, ou seja, para o subtipo de projeto mais externo, os parâmetros `pOuter` e `pOwner` são passados como `null` e a função define o subtipo de projeto mais externo `IUnknown` como `pOuter` .

    2. Em seguida, o ambiente chama `HrCreateInnerProj` a função com o segundo tipo de projeto GUID na lista. Esse GUID corresponde à segunda etapa de subtipo de projeto interno em direção ao projeto base na sequência de agregação.

    3. O `pOuter` agora está apontando para o `IUnknown` do subtipo de projeto mais externo e `HrCreateInnerProj` chama sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> seguido por uma chamada para sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> . No <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> método, você passa o controle `IUnknown` do subtipo de projeto mais externo, `pOuter` . O projeto de propriedade (subtipo de projeto interno) precisa criar seu objeto de projeto agregado aqui. Na <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> implementação do método, você passa um ponteiro para o `IUnknown` do projeto interno que está sendo agregado. Esses dois métodos criam o objeto de agregação, e suas implementações precisam seguir as regras de agregação COM para garantir que um subtipo de projeto não acabe segurando uma contagem de referência para si mesmo.

    4. `HrCreateInnerProj` chama a implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> . Nesse método, o subtipo de projeto faz sua inicialização funcionar. Você pode, por exemplo, registrar eventos de solução no <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> .

    5. `HrCreateInnerProj` é chamado recursivamente até que o último GUID (o projeto base) na lista seja atingido. Para cada uma dessas chamadas, as etapas, c a d, são repetidas. `pOuter` aponta para o subtipo de projeto mais externo `IUnknown` para cada nível de agregação.

## <a name="example"></a>Exemplo

O exemplo a seguir detalha o processo programático em uma representação aproximada do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> método conforme ele é implementado pelo ambiente. O código é apenas um exemplo; Ele não deve ser compilado e toda a verificação de erros foi removida para fins de clareza.

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

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Flavor>
- [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)
