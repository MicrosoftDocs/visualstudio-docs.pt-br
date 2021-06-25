---
title: Expondo objetos de projeto | Microsoft Docs
description: Saiba como expor objetos para tipos de projeto personalizados no Visual Studio, fornecendo objetos de automação que permitem o acesso ao projeto usando interfaces de automação.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- project objects, exposing
- extensibility, project objects
ms.assetid: 5bb24967-434a-4ef4-87a0-2f3250c9e22d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c3e89b4c80d64bedb77e68c648ba993794f8b658
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898286"
---
# <a name="expose-project-objects"></a>Expor objetos do projeto

Os tipos de projeto personalizados podem fornecer objetos de automação para permitir o acesso ao projeto usando interfaces de automação. Espera-se que cada tipo de projeto forneça o <xref:EnvDTE.Project> objeto de automação padrão que é acessado do <xref:EnvDTE.Solution> , que contém uma coleção de todos os projetos que estão abertos no IDE. Espera-se que cada item no projeto seja exposto por um <xref:EnvDTE.ProjectItem> objeto acessado com o `Project.ProjectItems` . Além desses objetos de automação padrão, os projetos podem optar por oferecer objetos de automação específicos do projeto.

Você pode criar objetos de automação de nível raiz personalizados que podem acessar a associação tardia do objeto DTE raiz usando `DTE.<customObjectName>` ou `DTE.GetObject("<customObjectName>")` . Por exemplo, Visual C++ cria uma coleção de projetos específica do projeto do C++ chamada *vcprojects* que você pode acessar usando o `DTE.VCProjects` ou o `DTE.GetObject("VCProjects")` . Você também pode criar um `Project.Object` , que é exclusivo para o tipo de projeto, a `Project.CodeModel` , que pode ser consultado para o objeto mais derivado e a `ProjectItem` , que expõe `ProjectItem.Object` e a `ProjectItem.FileCodeModel` .

É uma convenção comum para que os projetos exponham uma coleção de projetos personalizada e específica do projeto. Por exemplo, [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] cria uma coleção de projetos específica do C++ que você pode acessar usando o `DTE.VCProjects` ou o `DTE.GetObject("VCProjects")` . Você também pode criar um `Project.Object` , que é exclusivo para o tipo de projeto, a `Project.CodeModel` , que pode ser consultado para o objeto mais derivado, um `ProjectItem` , que expõe `ProjectItem.Object` e um `ProjectItem.FileCodeModel` .

## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>Para contribuir com um objeto específico do VSPackage para um projeto

1. Adicione as chaves apropriadas ao arquivo *. pkgdef* de seu VSPackage.

     Por exemplo, aqui estão as configurações de *. pkgdef* para o projeto de linguagem C++:

    ```
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]
    "VCProjects"=""
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]
    "VCProjectEngineEventsObject"=""
    ```

2. Implemente o código no <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método, como no exemplo a seguir.

    ```cpp
    STDMETHODIMP CVsPackage::GetAutomationObject(
    /* [in]  */ LPCOLESTR       pszPropName,
    /* [out] */ IDispatch **    ppIDispatch)
    {
    ExpectedPtrRet(pszPropName);
    ExpectedPtrRet(ppIDispatch);
    *ppIDispatch = NULL;

        if (m_fZombie)
            return E_UNEXPECTED;

        if (_wcsicmp(pszPropName, g_wszAutomationProjects) == 0)
        {
            return GetAutomationProjects(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        else if (_wcsicmp(pszPropName, g_wszAutomationProjectItemsEvents) == 0)
        {
            return CAutomationEvents::GetAutomationEvents(ppIDispatch);
        }
        return E_INVALIDARG;
    }
    ```

     No código, `g_wszAutomationProjects` é o nome da sua coleção de projetos. O `GetAutomationProjects` método cria um objeto que implementa a `Projects` interface e retorna um `IDispatch` ponteiro para o objeto de chamada, conforme mostrado no exemplo de código a seguir.

    ```cpp
    HRESULT CVsPackage::GetAutomationProjects(/* [out] */ IDispatch ** ppIDispatch)
    {
        ExpectedPtrRet(ppIDispatch);
        *ppIDispatch = NULL;

        if (!m_srpAutomationProjects)
        {
            HRESULT hr = CACProjects::CreateInstance(&m_srpAutomationProjects);
            IfFailRet(hr);
            ExpectedExprRet(m_srpAutomationProjects != NULL);
        }
        return m_srpAutomationProjects.CopyTo(ppIDispatch);
    }
    ```

     Escolha um nome exclusivo para o objeto de automação. Conflitos de nome são imprevisíveis e as colisões fazem com que um nome de objeto conflitante seja Descartado arbitrariamente se vários tipos de projeto usam o mesmo nome. Você deve incluir seu nome corporativo ou algum aspecto exclusivo de seu nome de produto no nome do objeto de automação.

     O `Projects` objeto de coleção personalizado é um ponto de entrada de conveniência para a parte restante do seu modelo de automação de projeto. O objeto de projeto também pode ser acessado da <xref:EnvDTE.Solution> coleção de projetos. Depois de criar o código apropriado e as entradas do registro que fornecem aos consumidores os `Projects` objetos de coleção, sua implementação deve fornecer objetos padrão restantes para o modelo de projeto. Para obter mais informações, consulte [modelagem de projeto](../../extensibility/internals/project-modeling.md).

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
