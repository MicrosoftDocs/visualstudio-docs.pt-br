---
title: Sequência de inicialização dos subtipos do projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- project subtypes, initialization sequence
ms.assetid: f657f8c3-5e68-4308-9971-e81e3099ba29
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 53c0a474a5a5caf887599bc50e623bd25e7be782
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51746519"
---
# <a name="initialization-sequence-of-project-subtypes"></a>Sequência de inicialização de subtipos de projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O ambiente constrói um projeto, chamando a implementação da fábrica de projeto base <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>. A construção de um subtipo de projeto é iniciado quando o ambiente determina se a lista GUID de tipo de projeto para a extensão do arquivo de projeto não está vazia. A extensão de arquivo de projeto e o GUID do projeto especificam se o projeto é um [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ou [!INCLUDE[csprcs](../../includes/csprcs-md.md)] tipo de projeto. Por exemplo, a extensão. vbproj e {F184B08F-C81C-45F6-A57F-5ABD9991F28F} identificar um [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] projeto.  
  
## <a name="environments-initialization-of-project-subtypes"></a>Inicialização do ambiente de subtipos de projeto  
 O procedimento a seguir fornece detalhes sobre a sequência de inicialização para um sistema de projeto agregado por vários subtipos do projeto.  
  
1. O ambiente chama o projeto base <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>, e enquanto o projeto analisa seu arquivo de projeto descobre que o tipo de projeto de agregação lista de GUIDs não é `null`. O projeto interrompe diretamente a criação de seu projeto.  
  
2. As chamadas de projeto `QueryService` na <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> service para criar um subtipo de projeto usando a implementação do ambiente do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> método. Dentro desse método, o ambiente faz chamadas de função recursiva para suas implementações de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>, `M:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject(System.Object)` e <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A> métodos enquanto ele é percorrer a lista de projeto de tipo de GUIDs, começando com o subtipo de projeto mais externo.  
  
    O exemplo a seguir fornece detalhes sobre as etapas de inicialização.  
  
   1.  A implementação do ambiente do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> chamadas de método ' HrCreateInnerProj ' ' método com a seguinte declaração de função:  
  
       ```  
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
           BOOL *pfCancelled  
       )  
       ```  
  
        Quando essa função é chamada pela primeira vez, ou seja, para o subtipo de projeto mais externo, os parâmetros `pOuter` e `pOwner` são passados como `null` e a função define o subtipo de projeto mais externo `IUnknown` para `pOuter`.  
  
   2.  Em seguida o ambiente chama `HrCreateInnerProj` função com o segundo tipo de projeto GUID na lista. Esse GUID corresponde ao subtipo de projeto interna segundo passo a passo na direção do projeto base na sequência de agregação.  
  
   3.  O `pOuter` agora está apontando para o `IUnknown` do subtipo de projeto mais externo, e `HrCreateInnerProj` chama sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> seguido por uma chamada a sua implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A>. Na <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A> método passa o controle `IUnknown` do subtipo de projeto mais externo, `pOuter`. O projeto de propriedade (subtipo de projeto interno) precisa criar o seu objeto de projeto de agregação aqui. No <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.SetInnerProject%2A> implementação do método que você passe um ponteiro para o `IUnknown` do projeto interno que está sendo agregado. Esses dois métodos criam o objeto de agregação e suas implementações devem seguir as regras de agregação de COM para garantir que um subtipo de projeto não acabar mantendo uma contagem de referência a mesmo.  
  
   4.  `HrCreateInnerProj` chama a sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProjectFactory.PreCreateForOuter%2A>. Nesse método, o subtipo de projeto faz seu trabalho de inicialização. Você pode, por exemplo, registrar eventos de solução em <xref:Microsoft.VisualStudio.Shell.Interop.IVsAggregatableProject.InitializeForOuter%2A>.  
  
   5.  `HrCreateInnerProj` é chamada recursivamente até que o último GUID (no projeto base) na lista seja atingido. Para cada uma dessas chamadas, as etapas c a d, são repetidas. `pOuter` aponta para o subtipo de projeto mais externo `IUnknown` para cada nível de agregação.  
  
   O exemplo a seguir fornece detalhes sobre o processo através de programação em uma representação aproximado do <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject.CreateAggregateProject%2A> método como ele é implementado pelo ambiente. O código é apenas um exemplo; ele não se destina a ser compilado e todas as verificações de erro foi removido por motivos de clareza.  
  
## <a name="example"></a>Exemplo  
  
### <a name="code"></a>Código  
  
```  
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
 <xref:Microsoft.VisualStudio.Shell.Flavor>   
 [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)

