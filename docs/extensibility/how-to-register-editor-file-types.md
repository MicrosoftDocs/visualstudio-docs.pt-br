---
title: 'Como: registrar os tipos de arquivo do Editor | Microsoft Docs'
ms.date: 03/22/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - register file types
ms.assetid: 54846779-8290-48de-90ab-81011559d9a5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 326b29574d8ff2562196652cdcde9865aee24c0e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49896920"
---
# <a name="how-to-register-editor-file-types"></a>Como: registrar os tipos de arquivo do editor
A maneira mais fácil de registrar tipos de arquivo do editor é usando os atributos de registro fornecidos como parte do [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] pacote framework (MPF) classes gerenciadas. Se você estiver implementando seu pacote no formato nativo [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)], você também pode escrever um script de registro que registra seu editor e aos ramais associados.

## <a name="registration-using-mpf-classes"></a>Usando classes MPF de registro

### <a name="to-register-editor-file-types-using-mpf-classes"></a>Para registrar tipos de arquivo do editor usando classes MPF

1. Forneça o <xref:Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute> classe com os parâmetros apropriados para seu editor na classe do VSPackage.

   ```
   [Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute(typeof(EditorFactory), ".Sample", 32,
        ProjectGuid = "{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}",
        TemplateDir = "..\\..\\Templates",
        NameResourceID = 106)]
   ```

    Onde *. Exemplo* é a extensão que está registrada para este editor e "32" é o seu nível de prioridade.

    O `projectGuid` é o GUID para tipos de arquivo diverso, definidos em <xref:Microsoft.VisualStudio.VSConstants.CLSID.MiscellaneousFilesProject_guid>. O tipo de arquivo diverso for fornecido, para que o arquivo resultante não pretende ser uma parte do processo de compilação.

    *TemplateDir* representa a pasta que contém os arquivos de modelo são incluídos com o exemplo de editor básico gerenciado.

    `NameResourceID` é definido na *Resources.h* arquivo do projeto BasicEditorUI e identifica o editor como "Meu Editor".

2. Substituir o método <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>.

    Em sua implementação do <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método, chame o <xref:Microsoft.VisualStudio.Shell.Package.RegisterEditorFactory%2A> método e passar a instância de sua fábrica de editor, como demonstrada a seguir.

   ```csharp
   protected override void Initialize()
   {
       Trace.WriteLine (string.Format(CultureInfo.CurrentCulture,
       "Entering Initialize() of: {0}", this.ToString()));
       base.Initialize();
          //Create Editor Factory
       editorFactory = new EditorFactory(this);
       base.RegisterEditorFactory(editorFactory);
   }
   ```

    Esta etapa registra a fábrica do editor e as extensões de arquivo do editor.

3. Cancelar o registro as fábricas de editor.

    As fábricas de editor são canceladas automaticamente quando o VSPackage é descartado. Se o objeto de fábrica de editor implementa o <xref:System.IDisposable> interface, seu `Dispose` método é chamado depois que a fábrica tem sido cancelada com [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

## <a name="registration-using-a-registry-script"></a>Usando um script de registro do registro
 Registrar fábricas e tipos de arquivo no formato nativo [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] é feito usando um script de registro para gravar no registro do windows, conforme ilustrado a seguir.

### <a name="to-register-editor-file-types-using-a-registry-script"></a>Para registrar tipos de arquivo do editor usando um script de registro

1.  No seu script de registro, definir a fábrica do editor e a cadeia de caracteres do GUID de fábrica do editor conforme mostra o `GUID_BscEditorFactory` seção do script de registro a seguir. Além disso, defina a extensão e a prioridade da extensão do editor:

    ```
          NoRemove Editors     {         %GUID_BscEditorFactory% = s 'RTF Editor'         {             val Package = s '%CLSID_Package%'             val DisplayName = s 'An RTF Editor'             val ExcludeDefTextEditor = d 1             val AcceptBinaryFiles = d 0

            LogicalViews
            {
                val %LOGVIEWID_TextView% = s ''
            }

            OpenWithEntries
            {
            }

            Extensions            {                val rtf = d 50            }
        }
    }
    ```

     A extensão de arquivo do editor neste exemplo é identificada como *. rtf* e a prioridade for "50". As cadeias de caracteres do GUID são definidas no *h* arquivo do projeto de exemplo BscEdit.

2.  Registre o VSPackage.

3.  Registre-se a fábrica do editor.

     A fábrica do editor é registrada no <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors.RegisterEditor%2A> implementação.

    ```cpp
    // create editor factory.
    if (m_srpEdFact == NULL)
    {
        CComObject<CBscEditorFactory> *pEdFact = new CComObject<CBscEditorFactory>;
        if (NULL == pEdFact)
          return E_OUTOFMEMORY;

        if (!pEdFact->FInit(this))
          return E_UNEXPECTED;

        m_srpEdFact = (IVsEditorFactory *) pEdFact;    // Note: assignment to a smart pointer does an AddRef()
    }
    // Query service for IVsRegisterEditors, register the editor factory
    CComPtr<IVsRegisterEditors> srpRegEd;
    if ((SUCCEEDED(m_srpPkgSiteSP->QueryService(SID_SVsRegisterEditors, IID_IVsRegisterEditors,(void **)&srpRegEd ))) && (srpRegEd != NULL))
      {
        ATLTRACE(TEXT(">> CVsPackage, registering editor factory.\n"));
          if (FAILED(srpRegEd->RegisterEditor(GUID_BscEditorFactory,
                      m_srpEdFact, &m_dwEditorCookie)))
          {
             ATLTRACE(TEXT(">> CVsPackage, RegisterEditor() failed.\n"));
            return E_FAIL;
          }
      }
        return S_OK;
    }
    ```

     As cadeias de caracteres do GUID são definidas no *h* arquivo do projeto BscEdit.