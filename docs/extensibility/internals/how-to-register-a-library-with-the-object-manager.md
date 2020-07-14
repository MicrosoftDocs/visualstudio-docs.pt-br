---
title: 'Como: registrar uma biblioteca com o Gerenciador de objetos | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- libraries, registering with object manager
- IVsLibrary2 interface, registering library with object manager
- IVsSimpleLibrary2 interface, registering library with object manager
- IVsObjectManager2 interface, registering library with object manager
- libraries, symbol-browsing tools
ms.assetid: f124dd05-cb0f-44ad-bb2a-7c0b34ef4038
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7179bd87fdfd9a2c3fc36958a9d964ec4f790dbd
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905229"
---
# <a name="how-to-register-a-library-with-the-object-manager"></a>Como registrar uma biblioteca com o Gerenciador de objetos
Símbolos – ferramentas de navegação, como **modo de exibição de classe**, **pesquisador de objetos**, **pesquisador de chamadas** e **Localizar resultados de símbolos**, permitem Exibir símbolos em seu projeto ou em componentes externos. Os símbolos incluem namespaces, classes, interfaces, métodos e outros elementos de linguagem. As bibliotecas acompanham esses símbolos e os expõem ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Gerenciador de objetos que popula as ferramentas com os dados.

 O Gerenciador de objetos controla todas as bibliotecas disponíveis. Cada biblioteca deve ser registrada com o Gerenciador de objetos antes de fornecer símbolos para as ferramentas de navegação de símbolos.

 Normalmente, você registra uma biblioteca quando um VSPackage é carregado. No entanto, isso pode ser feito em outro momento, conforme necessário. Você cancela o registro da biblioteca quando o VSPackage é desligado.

 Para registrar uma biblioteca, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterLibrary%2A> método. Para uma biblioteca de código gerenciado, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> método.

 Para cancelar o registro de uma biblioteca, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A> método.

 Para obter uma referência ao Gerenciador de objetos, <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> , passe a <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> ID de serviço para o `GetService` método.

## <a name="register-and-unregister-a-library-with-the-object-manager"></a>Registrar e cancelar o registro de uma biblioteca com o Gerenciador de objetos

### <a name="to-register-a-library-with-the-object-manager"></a>Para registrar uma biblioteca com o Gerenciador de objetos

1. Crie uma biblioteca.

    ```vb
    Private m_CallBrowserLibrary As CallBrowser.Library = Nothing
    Private m_nLibraryCookie As UInteger = 0
    ' Create Library.
    m_CallBrowserLibrary = New CallBrowser.Library()
    ```

    ```csharp
    private CallBrowser.Library m_CallBrowserLibrary = null;
    private uint m_nLibraryCookie = 0;
    // Create Library.
    m_CallBrowserLibrary = new CallBrowser.Library();

    ```

2. Obtenha uma referência a um objeto do <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> tipo e chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> método.

    ```vb
    Private Sub RegisterLibrary()
        If m_nLibraryCookie <> 0 Then
            Throw New Exception("Library already registered with Object Manager")
        End If

        ' Obtain a reference to IVsObjectManager2 type object.
        Dim objManager As IVsObjectManager2 = TryCast(GetService(GetType(SVsObjectManager)), IVsObjectManager2)
        If objManager Is Nothing Then
            Throw New NullReferenceException("GetService failed for SVsObjectManager")
        End If

        Try
            Dim hr As Integer = objManager.RegisterSimpleLibrary(m_CallBrowserLibrary, m_nLibraryCookie)
            Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr)
        Catch e As Exception
            ' Code to handle any CLS-compliant exception.
            Trace.WriteLine(e.Message)
            Throw
        End Try
    End Sub
    ```

    ```csharp
    private void RegisterLibrary()
    {
        if (m_nLibraryCookie != 0)
            throw new Exception("Library already registered with Object Manager");

        // Obtain a reference to IVsObjectManager2 type object.
        IVsObjectManager2 objManager =
                          GetService(typeof(SVsObjectManager)) as IVsObjectManager2;
        if (objManager == null)
            throw new NullReferenceException("GetService failed for SVsObjectManager");

        try
        {
            int hr =
                objManager.RegisterSimpleLibrary(m_CallBrowserLibrary,
                                                 out m_nLibraryCookie);
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);
        }
        catch (Exception e)
        {
            // Code to handle any CLS-compliant exception.
            Trace.WriteLine(e.Message);
            throw;
        }
    }

    ```

### <a name="to-unregister-a-library-with-the-object-manager"></a>Para cancelar o registro de uma biblioteca com o Gerenciador de objetos

1. Obtenha uma referência a um objeto do <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> tipo e chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.UnregisterLibrary%2A> método.

    ```vb
    Private Sub UnregisterLibrary()
        If m_nLibraryCookie <> 0 Then
            ' Obtain a reference to IVsObjectManager2 type object.
            Dim objManager As IVsObjectManager2 = TryCast(GetService(GetType(SVsObjectManager)), IVsObjectManager2)
            If objManager Is Nothing Then
                Throw New NullReferenceException("GetService failed for SVsObjectManager")
            End If

            Try
                objManager.UnregisterLibrary(m_nLibraryCookie)
            Catch e As Exception
                ' Code to handle any CLS-compliant exception.
                Trace.WriteLine(e.Message)
                Throw
            Finally
                m_nLibraryCookie = 0
            End Try
        End If
    End Sub
    ```

    ```csharp
    private void UnregisterLibrary()
    {
        if (m_nLibraryCookie != 0)
        {
            // Obtain a reference to IVsObjectManager2 type object.
            IVsObjectManager2 objManager = GetService(typeof(SVsObjectManager)) as IVsObjectManager2;
            if (objManager == null)
                throw new NullReferenceException("GetService failed for SVsObjectManager");

            try
            {
                objManager.UnregisterLibrary(m_nLibraryCookie);
            }
            catch (Exception e)
            {
                // Code to handle any CLS-compliant exception.
                Trace.WriteLine(e.Message);
                throw;
            }
            finally
            {
                m_nLibraryCookie = 0;
            }
        }
    }

    ```

## <a name="see-also"></a>Confira também
- [Extensibilidade do serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-extensibility.md)
- [Símbolo de suporte – ferramentas de navegação](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [Como: expor listas de símbolos fornecidos pela biblioteca para o Gerenciador de objetos](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
