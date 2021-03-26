---
title: Registrando um Service1 de linguagem herdada | Microsoft Docs
description: Saiba mais sobre o registro de um serviço de linguagem herdado de um VSPackage com o Visual Studio adicionando chaves e entradas do registro.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], registering
ms.assetid: d33b08af-09e0-4c79-87b2-5536b27fbacf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d5fa94fbd514e5fb162bc569438197dd8c65444b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060764"
---
# <a name="registering-a-legacy-language-service-1"></a>Registrando um serviço de idioma herdado 1
Na MPF (estrutura de pacote gerenciada), o serviço de linguagem é proffered por um VSPackage (consulte [VSPackages](../../extensibility/internals/vspackages.md)) e é registrado com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] adicionando chaves e entradas do registro. Esse processo de registro é feito parcialmente durante a instalação e, em parte, no tempo de execução.

## <a name="register-the-language-service-by-using-attributes"></a>Registrar o serviço de idioma usando atributos
 Os atributos a seguir são usados para registrar um serviço de idioma.

- <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageExtensionAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageCodeExpansionAttribute>

- <xref:Microsoft.VisualStudio.Shell.ProvideLanguageEditorOptionPageAttribute>

  Esses atributos são explicados abaixo

### <a name="provideserviceattribute"></a>ProvideServiceAttribute
 Esse atributo registra o serviço de idioma como um serviço.

### <a name="example"></a>Exemplo

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideServiceAttribute(typeof(TestLanguageService),
                             ServiceName = "Test Language Service")]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguageserviceattribute"></a>ProvideLanguageServiceAttribute
 Esse atributo registra o serviço de idioma especificamente como um serviço de linguagem. Ele permite que você defina opções que especificam os recursos que o serviço de linguagem oferece. O exemplo mostra um subconjunto das opções que um serviço de linguagem pode fornecer. Para obter o conjunto completo de opções de serviço de linguagem, consulte <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> .

### <a name="example"></a>Exemplo

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageServiceAttribute(typeof(TestLanguageService),
                             "Test Language",
                             106,             // resource ID of localized language name
                             CodeSense = true,             // Supports IntelliSense
                             RequestStockColors = false,   // Supplies custom colors
                             EnableCommenting = true,      // Supports commenting out code
                             EnableAsyncCompletion = true  // Supports background parsing
                             )]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguageextensionattribute"></a>ProvideLanguageExtensionAttribute
 Esse atributo associa o serviço de linguagem a uma extensão de arquivo. Sempre que um arquivo com essa extensão é carregado, em qualquer projeto, seu serviço de idioma é iniciado e usado para exibir o conteúdo do arquivo.

### <a name="example"></a>Exemplo

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageExtensionAttribute(typeof(TestLanguageService),
                                       ".Testext")]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguagecodeexpansionattribute"></a>ProvideLanguageCodeExpansionAttribute
 Esse atributo registra um local do qual os modelos de expansão de código ou de trecho são obtidos. Essas informações são usadas pelo **navegador de trechos de código** e pelo editor quando um trecho de código é inserido no arquivo de origem.

### <a name="example"></a>Exemplo

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageCodeExpansionAttribute(
             typeof(TestLanguageService),
             "Test Language", // Name of language used as registry key.
             106,           // Resource ID of localized name of language service.
             "testlanguage",  // language key used in snippet templates.
             @"%InstallRoot%\Test Language\SnippetsIndex.xml",  // Path to snippets index
             SearchPaths = @"%InstallRoot%\Test Language\Snippets\%LCID%\Snippets\;" +
                           @"%TestDocs%\Code Snippets\Test Language\Test Code Snippets"
             )]

    public class TestLanguagePackage : Package
    {
    }
}
```

### <a name="providelanguageeditoroptionpageattribute"></a>ProvideLanguageEditorOptionPageAttribute
 Esse atributo registra uma página de propriedades a ser exibida na caixa de diálogo **Opções** na categoria **Editor de texto** . Use um desses atributos para cada página a ser exibida para o serviço de idioma. Se você precisar organizar suas páginas em uma estrutura de árvore, use atributos adicionais para definir cada nó da árvore.

### <a name="example"></a>Exemplo
 Este exemplo mostra duas páginas de propriedades, **Opções** e **recuo** e um nó que contém a segunda página de propriedades.

```csharp
using Microsoft.VisualStudio.Shell;

namespace TestLanguagePackage
{
    [ProvideLanguageEditorOptionPageAttribute(
             "Test Language",  // Registry key name for language
             "Options",      // Registry key name for property page
             "#242",         // Localized name of property page
             OptionPageGuid = "{A2FE74E1-FFFF-3311-4342-123052450768}"  // GUID of property page
             )]
    [ProvideLanguageEditorOptionPageAttribute(
             "Test Language",  // Registry key name for language
             "Advanced",     // Registry key name for node
             "#243",         // Localized name of node
             )]
    [ProvideLanguageEditorOptionPageAttribute(
             "Test Language",  // Registry key name for language
             @"Advanced\Indenting",     // Registry key name for property page
             "#244",         // Localized name of property page
             OptionPageGuid = "{A2FE74E2-FFFF-3311-4342-123052450768}"  // GUID of property page
             )]

    public class TestLanguagePackage : Package
    {
    }
}
```

## <a name="proffer-the-language-service-at-run-time"></a>Oferecer o serviço de idioma em tempo de execução
 Quando o pacote de idiomas for carregado, você deverá informar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] que o serviço de idioma está pronto. Para fazer isso, Proffering o serviço. Isso é feito no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método. Além disso, você precisa iniciar um temporizador que chama seu serviço de idioma durante períodos ociosos para que a análise em segundo plano possa ser realizada. Esse temporizador ocioso também é usado para atualizar as propriedades do documento se você tiver implementado qualquer por meio da <xref:Microsoft.VisualStudio.Package.DocumentProperties> classe. Para dar suporte a um temporizador, seu pacote deve implementar a <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponent> interface (somente o <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponent.FDoIdle%2A> método precisa ser totalmente implementado; os métodos restantes podem retornar valores padrão).

### <a name="example"></a>Exemplo
 Este exemplo mostra uma abordagem típica para Proffering um serviço e fornecer um temporizador ocioso.

```csharp

using System;
using System.Runtime.InteropServices;
using System.ComponentModel.Design;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.OLE.Interop;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    [Microsoft.VisualStudio.Shell.ProvideService(typeof(TestLanguageService))]
    [Microsoft.VisualStudio.Shell.ProvideLanguageExtension(typeof(TestLanguageService), ".testext")]
    [Microsoft.VisualStudio.Shell.ProvideLanguageService(typeof(TestLanguageService), "Test Language", 0,
        AutoOutlining = true,
        EnableCommenting = true,
        MatchBraces = true,
        ShowMatchingBrace = true)]
    [Guid("00000000-0000-0000-0000-00000000000")] //provide a unique GUID for the package

    public class TestLanguagePackage : Package, IOleComponent
    {
        private uint m_componentID;

        protected override void Initialize()
        {
            base.Initialize();  // required

            // Proffer the service.
            IServiceContainer serviceContainer = this as IServiceContainer;
            TestLanguageService langService      = new TestLanguageService();
            langService.SetSite(this);
            serviceContainer.AddService(typeof(TestLanguageService),
                                        langService,
                                        true);

            // Register a timer to call our language service during
            // idle periods.
            IOleComponentManager mgr = GetService(typeof(SOleComponentManager))
                                       as IOleComponentManager;
            if (m_componentID == 0 && mgr != null)
            {
                OLECRINFO[] crinfo = new OLECRINFO[1];
                crinfo[0].cbSize            = (uint)Marshal.SizeOf(typeof(OLECRINFO));
                crinfo[0].grfcrf            = (uint)_OLECRF.olecrfNeedIdleTime |
                                              (uint)_OLECRF.olecrfNeedPeriodicIdleTime;
                crinfo[0].grfcadvf          = (uint)_OLECADVF.olecadvfModal |
                                              (uint)_OLECADVF.olecadvfRedrawOff |
                                              (uint)_OLECADVF.olecadvfWarningsOff;
                crinfo[0].uIdleTimeInterval = 1000;
                int hr = mgr.FRegisterComponent(this, crinfo, out m_componentID);
            }
        }

        protected override void Dispose(bool disposing)
        {
            if (m_componentID != 0)
            {
                IOleComponentManager mgr = GetService(typeof(SOleComponentManager))
                                           as IOleComponentManager;
                if (mgr != null)
                {
                    int hr = mgr.FRevokeComponent(m_componentID);
                }
                m_componentID = 0;
            }

            base.Dispose(disposing);
        }

        #region IOleComponent Members

        public int FDoIdle(uint grfidlef)
        {
            bool bPeriodic = (grfidlef & (uint)_OLEIDLEF.oleidlefPeriodic) != 0;
            // Use typeof(TestLanguageService) because we need to
            // reference the GUID for our language service.
            LanguageService service = GetService(typeof(TestLanguageService))
                                      as LanguageService;
            if (service != null)
            {
                service.OnIdle(bPeriodic);
            }
            return 0;
        }

        public int FContinueMessageLoop(uint uReason,
                                        IntPtr pvLoopData,
                                        MSG[] pMsgPeeked)
        {
            return 1;
        }

        public int FPreTranslateMessage(MSG[] pMsg)
        {
            return 0;
        }

        public int FQueryTerminate(int fPromptUser)
        {
            return 1;
        }

        public int FReserved1(uint dwReserved,
                              uint message,
                              IntPtr wParam,
                              IntPtr lParam)
        {
            return 1;
        }

        public IntPtr HwndGetWindow(uint dwWhich, uint dwReserved)
        {
            return IntPtr.Zero;
        }

        public void OnActivationChange(IOleComponent pic,
                                       int fSameComponent,
                                       OLECRINFO[] pcrinfo,
                                       int fHostIsActivating,
                                       OLECHOSTINFO[] pchostinfo,
                                       uint dwReserved)
        {
        }

        public void OnAppActivate(int fActive, uint dwOtherThreadID)
        {
        }

        public void OnEnterState(uint uStateID, int fEnter)
        {
        }

        public void OnLoseActivation()
        {
        }

        public void Terminate()
        {
        }

        #endregion
    }
}
```
