---
title: Obtendo uma lista de trechos de código instalados (Herdado) | Microsoft Docs
description: Saiba como obter todos os trechos de código para um GUID de idioma específico. Os atalhos para esses trechos de código podem ser inseridos em uma lista de conclusão do IntelliSense.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- snippets, retrieving list
- code snippets, retrieving list
- GetSnippets method
ms.assetid: 7d142f8b-35b1-44c4-a13e-f89f6460c906
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 051f356e7b6b6f1a92ba475617f48e5c6074f402
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898868"
---
# <a name="walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation"></a>Passo a passo: Obtendo uma lista de snippets de código instalados (implementação herdada)
Um trecho de código é uma parte do código que pode ser inserida no buffer de origem com um comando de menu (que permite escolher entre uma lista de trechos de código instalados) ou selecionando um atalho de trecho em uma lista de conclusão do IntelliSense.

 O <xref:Microsoft.VisualStudio.TextManager.Interop.IVsExpansionManager.EnumerateExpansions%2A> método obtém todos os trechos de código para um GUID de idioma específico. Os atalhos para esses trechos de código podem ser inseridos em uma lista de conclusão do IntelliSense.

 Consulte [suporte para trechos de código em um serviço de linguagem herdada](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md) para obter detalhes sobre como implementar trechos de código em um serviço de linguagem MPF (Managed Package Framework).

### <a name="to-retrieve-a-list-of-code-snippets"></a>Para recuperar uma lista de trechos de código

1. O código a seguir mostra como obter uma lista de trechos de código para um determinado idioma. Os resultados são armazenados em uma matriz de <xref:Microsoft.VisualStudio.TextManager.Interop.VsExpansion> estruturas. Esse método usa o <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método estático para obter a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager> interface do <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> serviço. No entanto, você também pode usar o provedor de serviços fornecido para seu VSPackage e chamar o <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider.QueryService%2A> método.

    ```csharp
    using System;
    using System.Collections;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.Package;
    using Microsoft.VisualStudio.Shell;
    using Microsoft.VisualStudio.TextManager.Interop;

    [Guid("00000000-0000-0000-0000-000000000000")] //create a new GUID for the language service
    namespace TestLanguage
    {
        class TestLanguageService : LanguageService
        {
            private void GetSnippets(Guid languageGuid,
                                     ref ArrayList expansionsList)
            {
                IVsTextManager textManager = (IVsTextManager)Package.GetGlobalService(typeof(SVsTextManager));
                if (textManager != null)
                {
                    IVsTextManager2 textManager2 = (IVsTextManager2)textManager;
                    if (textManager2 != null)
                    {
                        IVsExpansionManager expansionManager = null;
                        textManager2.GetExpansionManager(out expansionManager);
                        if (expansionManager != null)
                        {
                            // Tell the environment to fetch all of our snippets.
                            IVsExpansionEnumeration expansionEnumerator = null;
                            expansionManager.EnumerateExpansions(languageGuid,
                            0,     // return all info
                            null,    // return all types
                            0,     // return all types
                            1,     // include snippets without types
                            0,     // do not include duplicates
                            out expansionEnumerator);
                            if (expansionEnumerator != null)
                            {
                                // Cache our expansions in a VsExpansion array
                                uint count   = 0;
                                uint fetched = 0;
                                VsExpansion expansionInfo = new VsExpansion();
                                IntPtr[] pExpansionInfo   = new IntPtr[1];

                                // Allocate enough memory for one VSExpansion structure. This memory is filled in by the Next method.
                                pExpansionInfo[0] = Marshal.AllocCoTaskMem(Marshal.SizeOf(expansionInfo));

                                expansionEnumerator.GetCount(out count);
                                for (uint i = 0; i < count; i++)
                                {
                                    expansionEnumerator.Next(1, pExpansionInfo, out fetched);
                                    if (fetched > 0)
                                    {
                                        // Convert the returned blob of data into a structure that can be read in managed code.
                                        expansionInfo = (VsExpansion)Marshal.PtrToStructure(pExpansionInfo[0], typeof(VsExpansion));

                                        if (!String.IsNullOrEmpty(expansionInfo.shortcut))
                                        {
                                            expansionsList.Add(expansionInfo);
                                        }
                                    }
                                }
                                Marshal.FreeCoTaskMem(pExpansionInfo[0]);
                            }
                        }
                    }
                }
            }
        }
    }
    ```

### <a name="to-call-the-getsnippets-method"></a>Para chamar o método getsnippets

1. O método a seguir mostra como chamar o `GetSnippets` método na conclusão de uma operação de análise. O <xref:Microsoft.VisualStudio.Package.LanguageService.OnParseComplete%2A> método é chamado após uma operação de análise que foi iniciada com o motivo <xref:Microsoft.VisualStudio.Package.ParseReason> .

> [!NOTE]
> A `expansionsList` lista de matrizes é armazenada em cache por motivos de desempenho. As alterações nos trechos de código não são refletidas na lista até que o serviço de idioma seja interrompido e recarregado (por exemplo, interrompendo e reiniciando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ).

```csharp
class TestLanguageService : LanguageService
{
    private ArrayList expansionsList;

    public override void OnParseComplete(ParseRequest req)
    {
        if (this.expansionsList == null)
        {
            this.expansionsList = new ArrayList();
            GetSnippets(this.GetLanguageServiceGuid(),
                ref this.expansionsList);
        }
    }
}
```

### <a name="to-use-the-snippet-information"></a>Para usar as informações de trecho de código

1. O código a seguir mostra como usar as informações de trecho retornadas pelo `GetSnippets` método. O `AddSnippets` método é chamado do analisador em resposta a qualquer motivo de análise usado para preencher uma lista de trechos de código. Isso deve ocorrer após a análise completa ter sido feita pela primeira vez.

     O `AddDeclaration` método cria uma lista de declarações que é exibida posteriormente em uma lista de conclusão.

     A `TestDeclaration` classe contém todas as informações que podem ser exibidas em uma lista de conclusão, bem como o tipo de declaração.

    ```csharp
    class TestAuthoringScope : AuthoringScope
    {
        public void AddDeclarations(TestDeclaration declaration)
        {
            if (m_declarations == null)
                m_declarations = new List<TestDeclaration>();
            m_declarations.Add(declaration);
         }
    }
    class TestDeclaration
    {
        private string m_name;
        private string m_description;
        private string m_type;

        public TestDeclaration(string name, string desc, string type)
        {
            m_name = name;
            m_description = desc;
            m_type = type;
        }

    class TestLanguageService : LanguageService
    {
        internal void AddSnippets(ref TestAuthoringScope scope)
        {
            if (this.expansionsList != null && this.expansionsList.Count > 0)
            {
                int count = this.expansionsList.Count;
                for (int i = 0; i < count; i++)
                {
                    VsExpansion expansionInfo = (VsExpansion)this.expansionsList[i];
                    scope.AddDeclaration(new TestDeclaration(expansionInfo.title,
                         expansionInfo.description,
                         "snippet"));
                }
            }
        }
    }

    ```

## <a name="see-also"></a>Confira também
- [Suporte para snippets de código em um serviço de linguagem herdado](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)
