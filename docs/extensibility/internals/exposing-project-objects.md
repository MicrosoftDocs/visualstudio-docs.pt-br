---
title: Expor objetos do projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project objects, exposing
- extensibility, project objects
ms.assetid: 5bb24967-434a-4ef4-87a0-2f3250c9e22d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ae7b34df55593f07adeaffe8d654b59629baaae5
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510904"
---
# <a name="expose-project-objects"></a>Expor objetos do projeto

Tipos de projeto personalizado podem fornecer objetos de automação para permitir o acesso ao projeto usando interfaces de automação. Cada tipo de projeto deve fornecer o padrão <xref:EnvDTE.Project> objeto de automação que é acessado de <xref:EnvDTE.Solution>, que contém uma coleção de todos os projetos que estão abertos no IDE. Cada item no projeto deve ser exposta por um <xref:EnvDTE.ProjectItem> objeto acessado com `Project.ProjectItems`. Além desses objetos de automação padrão, os projetos podem optar por oferecer objetos de automação específico do projeto.

Você pode criar objetos de automação de nível raiz personalizado que você pode acessar associação tardia da raiz DTE objeto usando `DTE.<customObjectName>` ou `DTE.GetObject("<customObjectName>")`. Por exemplo, o Visual C++ cria uma coleção de projeto específicos do projeto C++ chamada *VCProjects* que você pode acessar usando `DTE.VCProjects` ou `DTE.GetObject("VCProjects")`. Você também pode criar uma `Project.Object`, que é exclusivo para o tipo de projeto, um `Project.CodeModel`, que pode ser consultado para seu objeto mais derivado e uma `ProjectItem`, que expõe `ProjectItem.Object` e um `ProjectItem.FileCodeModel`.

É uma convenção comum para projetos para expor uma coleção de projeto personalizados, específicos do projeto. Por exemplo, [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] cria uma coleção de projeto específico do C++ que, em seguida, você pode acessar usando `DTE.VCProjects` ou `DTE.GetObject("VCProjects")`. Você também pode criar uma `Project.Object`, que é exclusivo para o tipo de projeto, um `Project.CodeModel`, que pode ser consultado para seu objeto mais derivado, um `ProjectItem`, que expõe `ProjectItem.Object`e um `ProjectItem.FileCodeModel`.  
  
## <a name="to-contribute-a-vspackage-specific-object-for-a-project"></a>Para contribuir com um objeto de VSPackage específico para um projeto  
  
1.  Adicionar as chaves apropriadas para o *pkgdef* arquivo de seu VSPackage.  
  
     Por exemplo, aqui estão os *pkgdef* configurações para o projeto de linguagem C++:  
  
    ```  
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\Automation]  
    "VCProjects"=""  
    [$RootKey$\Packages\{F1C25864-3097-11D2-A5C5-00C04F7968B4}\AutomationEvents]  
    "VCProjectEngineEventsObject"=""  
    ```  
  
2.  Implementar o código no <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A> método, como no exemplo a seguir.  
  
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
  
     No código, `g_wszAutomationProjects` é o nome da sua coleção de projeto. O `GetAutomationProjects` método cria um objeto que implementa o `Projects` interface e retorna um `IDispatch` ponteiro para o objeto de chamada, conforme mostrado no exemplo de código a seguir.  
  
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
  
     Escolha um nome exclusivo para seu objeto de automação. Conflitos de nome são imprevisíveis e colisões de fazer com que um nome de objeto conflitante para arbitrariamente gerado se a vários tipos de projeto usam o mesmo nome. Você deve incluir o nome da sua empresa ou alguns aspectos exclusivos do seu nome de produto no nome do objeto de automação.  
  
     Personalizado `Projects` objeto da coleção é um ponto de entrada de conveniência para a parte restante do seu modelo de automação do projeto. Seu objeto de projeto também é acessível a partir de <xref:EnvDTE.Solution> coleção de projeto. Depois que você criou as entradas apropriadas de código e do registro que fornecem os consumidores com `Projects` objetos de coleção, sua implementação deve fornecer o restante objetos padrão para o modelo de projeto. Para obter mais informações, consulte [modelagem do projeto](../../extensibility/internals/project-modeling.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetAutomationObject%2A>
