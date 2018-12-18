---
title: Criar um Editor de núcleo e registrar um tipo de arquivo do Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - walkthrough
ms.assetid: 24d2bffd-a35c-46db-8515-fd60b884b7fb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3e00b96d1f5361d3d5260296532be47636f430d6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49921451"
---
# <a name="walkthrough-create-a-core-editor-and-registering-an-editor-file-type"></a>Passo a passo: Criar um editor de núcleo e registrar um tipo de arquivo do editor
Este passo a passo demonstra como criar um VSPackage que inicia o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo quando um arquivo com o *.myext* extensão de nome de arquivo é carregado.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>Locais para o modelo de projeto do Visual Studio Package  
 O modelo de projeto de pacote do Visual Studio pode ser encontrado em três locais diferentes nos **novo projeto** caixa de diálogo:  
  
1.  Sob **extensibilidade do Visual Basic**. O idioma padrão do projeto é o Visual Basic.  
  
2.  Sob **c# extensibilidade**. O idioma padrão do projeto é c#.  
  
3.  Sob **outros tipos de projetos extensibilidade**. O idioma padrão do projeto é C++.  
  
### <a name="to-create-the-vspackage"></a>Para criar o VSPackage  
  
- Inicie [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e crie um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] VSPackage nomeado `MyPackage`, conforme descrito na [passo a passo: criar um comando de menu VSPackage](https://msdn.microsoft.com/library/d699c149-5d1e-47ff-94c7-e1222af02c32).  
  
### <a name="to-add-the-editor-factory"></a>Para adicionar a fábrica do editor  
  
1. Clique com botão direito do **MyPackage** do projeto, aponte para **Add**e, em seguida, clique em **classe**.  
  
2. No **Adicionar Novo Item** diálogo caixa, certifique-se a **classe** modelo é selecionado, tipo `EditorFactory.cs` para o nome e, em seguida, clique **Add** para adicionar a classe ao seu projeto.  
  
    O *EditorFactory.cs* arquivo deve ser aberto automaticamente.  
  
3. Referencie os seguintes assemblies do seu código.  
  
   ```vb  
   Imports System.Runtime.InteropServices  
   Imports Microsoft.VisualStudio  
   Imports Microsoft.VisualStudio.Shell  
   Imports Microsoft.VisualStudio.Shell.Interop  
   Imports Microsoft.VisualStudio.OLE.Interop  
   Imports Microsoft.VisualStudio.TextManager.Interop  
   Imports IOleServiceProvider = Microsoft.VisualStudio.OLE.Interop.IServiceProvider  
   ```  
  
   ```csharp  
   using System.Runtime.InteropServices;  
   using Microsoft.VisualStudio;  
   using Microsoft.VisualStudio.Shell;  
   using Microsoft.VisualStudio.Shell.Interop;  
   using Microsoft.VisualStudio.OLE.Interop;  
   using Microsoft.VisualStudio.TextManager.Interop;  
   using IOleServiceProvider = Microsoft.VisualStudio.OLE.Interop.IServiceProvider;  
  
   ```  
  
4. Adicionar um GUID para o `EditorFactory` classe adicionando o `Guid` atributo imediatamente antes da declaração de classe.  
  
    Você pode gerar um novo GUID usando o *guidgen.exe* programar no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] prompt de comando, ou clicando em **criar GUID** no **ferramentas** menu. O GUID usado aqui é apenas um exemplo; não usá-lo em seu projeto.  
  
   ```vb  
   <Guid("0eea3187-c5fa-48d4-aa72-b5eecd3b17b1")> _  
   ```  
  
   ```csharp  
   [Guid("0eea3187-c5fa-48d4-aa72-b5eecd3b17b1")]   
   ```  
  
5. Na definição de classe, adicione duas variáveis particulares para conter o pacote pai e um provedor de serviços.  
  
   ```vb  
   Class EditorFactory  
       Private parentPackage As Package  
       Private serviceProvider As IOleServiceProvider  
   ```  
  
   ```csharp  
   class EditorFactory  
   {  
       private Package parentPackage;  
       private IOleServiceProvider serviceProvider;  
   }  
  
   ```  
  
6. Adicione um construtor de classe pública que assume um parâmetro de tipo <xref:Microsoft.VisualStudio.Shell.Package>:  
  
   ```vb  
   Public Sub New(ByVal parentPackage As Package)  
       Me.parentPackage = parentPackage  
   End Sub  
   ```  
  
   ```csharp  
   public EditorFactory(Package parentPackage)  
   {  
       this.parentPackage = parentPackage;  
   }  
   ```  
  
7. Modificar a `EditorFactory` declaração derivar de classe a <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface.  
  
   ```vb  
   Class EditorFactory Implements IVsEditorFacto  
   ```  
  
   ```csharp  
   class EditorFactory : IVsEditorFactory  
  
   ```  
  
8. Clique com botão direito <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>, clique em **implementar Interface**e, em seguida, clique em **implementar Interface explicitamente**.  
  
    Esta etapa adiciona os quatro métodos que devem ser implementados no <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface.  
  
9. Substitua o conteúdo do método de `IVsEditorFactory.Close` com o código a seguir.  
  
    ```vb  
    Return VSConstants.S_OK  
    ```  
  
    ```csharp  
    return VSConstants.S_OK;  
    ```  
  
10. Substitua o conteúdo do `IVsEditorFactory.SetSite` com o código a seguir.  
  
    ```vb  
    Me.serviceProvider = psp  
    Return VSConstants.S_OK  
    ```  
  
    ```csharp  
    this.serviceProvider = psp;  
    return VSConstants.S_OK;  
    ```  
  
11. Substitua o conteúdo do método de `IVsEditorFactory.MapLogicalView` com o código a seguir.  
  
    ```vb  
    Dim retval As Integer = VSConstants.E_NOTIMPL  
    pbstrPhysicalView = Nothing ' We support only one view.  
    If rguidLogicalView.Equals(VSConstants.LOGVIEWID_Designer)OrElse _  
    rguidLogicalView.Equals(VSConstants.LOGVIEWID_Primary) Then  
        retval = VSConstants.S_OK  
    End If  
    Return retval  
    ```  
  
    ```csharp  
    int retval = VSConstants.E_NOTIMPL;  
    pbstrPhysicalView = null;   // We support only one view.  
    if (rguidLogicalView.Equals(VSConstants.LOGVIEWID_Designer) ||  
    rguidLogicalView.Equals(VSConstants.LOGVIEWID_Primary))  
    {  
        retval = VSConstants.S_OK;  
    }  
    return retval;  
    ```  
  
12. Substitua o conteúdo do método de `IVsEditorFactory.CreateEditorInstance` com o código a seguir.  
  
    ```vb  
    Dim retval As Integer = VSConstants.E_FAIL          
  
    ' Initialize these to empty to start with   
    ppunkDocView = IntPtr.Zero  
    ppunkDocData = IntPtr.Zero  
    pbstrEditorCaption = ""  
    pguidCmdUI = Guid.Empty  
    pgrfCDW = 0  
  
    If (grfCreateDoc And (VSConstants.CEF_OPENFILE Or _  
    VSConstants.CEF_SILENT)) = 0 Then  
        Throw New ArgumentException("Only Open or Silent is valid")  
    End If  
    If punkDocDataExisting <> IntPtr.Zero Then  
        Return VSConstants.VS_E_INCOMPATIBLEDOCDATA  
    End If  
  
    ' Instantiate a text buffer of type VsTextBuffer.   
    ' Note: we only need an IUnknown (object) interface for   
    ' this invocation.   
    Dim clsidTextBuffer As Guid = GetType(VsTextBufferClass).GUID  
    Dim iidTextBuffer As Guid = VSConstants.IID_IUnknown  
    Dim pTextBuffer As Object = pTextBuffer = _  
    parentPackage.CreateInstance(clsidTextBuffer, iidTextBuffer, _  
    GetType(Object))  
  
    If Not pTextBuffer Is Nothing Then  
        ' "Site" the text buffer with the service provider we were   
        ' provided.   
        Dim textBufferSite As IObjectWithSite = TryCast(pTextBuffer, _  
        IObjectWithSite)  
        If Not textBufferSite Is Nothing Then  
            textBufferSite.SetSite(Me.serviceProvider)  
        End If  
  
        ' Instantiate a code window of type IVsCodeWindow.   
        Dim clsidCodeWindow As Guid = GetType(VsCodeWindowClass).GUID  
        Dim iidCodeWindow As Guid = GetType(IVsCodeWindow).GUID  
        Dim pCodeWindow As IVsCodeWindow = _  
        CType(Me.parentPackage.CreateInstance(clsidCodeWindow, _  
        iidCodeWindow, GetType(IVsCodeWindow)), IVsCodeWindow)  
        If Not pCodeWindow Is Nothing Then  
            ' Give the text buffer to the code window.   
            ' We are giving up ownership of the text buffer!   
            pCodeWindow.SetBuffer(CType(pTextBuffer, IVsTextLines))  
  
            ' Now tell the caller about all this new stuff   
            ' that has been created.   
            ppunkDocView = Marshal.GetIUnknownForObject(pCodeWindow)  
            ppunkDocData = Marshal.GetIUnknownForObject(pTextBuffer)  
  
            ' Specify the command UI to use so keypresses are   
            ' automatically dealt with.   
            pguidCmdUI = VSConstants.GUID_TextEditorFactory  
  
            ' This caption is appended to the filename and   
            ' lets us know our invocation of the core editor   
            ' is up and running.   
            pbstrEditorCaption = " [MyPackage]"  
  
            retval = VSConstants.S_OK  
        End If  
    End If  
    Return retval  
    ```  
  
    ```csharp  
    int retval = VSConstants.E_FAIL;  
  
    // Initialize these to empty to start with  
    ppunkDocView       = IntPtr.Zero;  
    ppunkDocData       = IntPtr.Zero;  
    pbstrEditorCaption = "";  
    pguidCmdUI         = Guid.Empty;   
    pgrfCDW            = 0;  
  
    if ((grfCreateDoc & (VSConstants.CEF_OPENFILE |   
          VSConstants.CEF_SILENT)) == 0)  
    {   
        throw new ArgumentException("Only Open or Silent is valid");  
    }  
    if (punkDocDataExisting != IntPtr.Zero)  
    {  
        return VSConstants.VS_E_INCOMPATIBLEDOCDATA;  
    }  
  
    // Instantiate a text buffer of type VsTextBuffer.  
    // Note: we only need an IUnknown (object) interface for   
    // this invocation.  
    Guid clsidTextBuffer = typeof(VsTextBufferClass).GUID;  
    Guid iidTextBuffer   = VSConstants.IID_IUnknown;  
    object pTextBuffer   = pTextBuffer = parentPackage.CreateInstance(  
          ref clsidTextBuffer,  
          ref iidTextBuffer,  
          typeof(object));  
  
    if (pTextBuffer != null)  
    {  
        // "Site" the text buffer with the service provider we were  
        // provided.  
        IObjectWithSite textBufferSite = pTextBuffer as IObjectWithSite;  
        if (textBufferSite != null)  
        {  
            textBufferSite.SetSite(this.serviceProvider);  
        }  
  
        // Instantiate a code window of type IVsCodeWindow.  
        Guid clsidCodeWindow = typeof(VsCodeWindowClass).GUID;  
        Guid iidCodeWindow   = typeof(IVsCodeWindow).GUID;  
        IVsCodeWindow pCodeWindow =  
        (IVsCodeWindow)this.parentPackage.CreateInstance(   
              ref clsidCodeWindow,  
              ref iidCodeWindow,  
              typeof(IVsCodeWindow));  
        if (pCodeWindow != null)  
        {  
            // Give the text buffer to the code window.  
            // We are giving up ownership of the text buffer!  
            pCodeWindow.SetBuffer((IVsTextLines)pTextBuffer);  
  
            // Now tell the caller about all this new stuff   
            // that has been created.  
            ppunkDocView = Marshal.GetIUnknownForObject(pCodeWindow);  
            ppunkDocData = Marshal.GetIUnknownForObject(pTextBuffer);  
  
            // Specify the command UI to use so keypresses are   
            // automatically dealt with.  
            pguidCmdUI = VSConstants.GUID_TextEditorFactory;  
  
            // This caption is appended to the filename and  
            // lets us know our invocation of the core editor   
            // is up and running.  
            pbstrEditorCaption = " [MyPackage]";  
  
            retval = VSConstants.S_OK;  
        }   
    }   
    return retval;   
    ```  
  
13. Compilar o projeto e verifique se que não existem erros.  
  
### <a name="to-register-the-editor-factory"></a>Para registrar a fábrica do editor  
  
1. Na **Gerenciador de soluções**, clique duas vezes o **Resources** arquivo para abri-lo à tabela de cadeia de caracteres, em que a entrada **String1 é** selecionado.  
  
2. Altere o nome do identificador para `IDS_EDITORNAME` e o texto a ser **MyPackage Editor.** Essa cadeia de caracteres aparece como o nome do seu editor.  
  
3. Abra o **VSPackage.resx** do arquivo, adicione uma nova cadeia de caracteres, defina o nome como **101**e defina o valor como `IDS_EDITORNAME`. Essa etapa fornece o pacote com uma ID de recurso para acessar a cadeia de caracteres que você criou.  
  
   > [!NOTE]
   >  Se o **VSPackage.resx** arquivo contém outra cadeia de caracteres que o `name` atributo definido como **101**, substituir por outro valor numérico, exclusivo, aqui e nas etapas a seguir.  
  
4. Na **Gerenciador de soluções**, abra o **MyPackagePackage.cs** arquivo.  
  
    Esse arquivo é o arquivo de pacote principal.  
  
5. Adicione os seguintes atributos de usuário antes de `Guid` atributo.  
  
   ```vb  
   <ProvideEditorFactoryAttribute(GetType(EditorFactory), 101)> _  
   <ProvideEditorExtensionAttribute(GetType(EditorFactory), _  
         ".myext", 32, NameResourceID:=101 )> _  
   ```  
  
   ```csharp  
   [ProvideEditorFactory(typeof(EditorFactory), 101)]  
   [ProvideEditorExtension(typeof(EditorFactory),   
         ".myext", 32, NameResourceID = 101)]   
   ```  
  
    O <xref:Microsoft.VisualStudio.Shell.ProvideEditorExtensionAttribute> atributo associa o *.myext* extensão com sua fábrica de editor de arquivo para que sempre que um arquivo com que a extensão será carregada, sua fábrica de editor é invocada.  
  
6. Adicione uma variável particular para o `MyPackage` classe, logo antes do construtor e dê a ele o tipo `EditorFactory`.  
  
   ```vb  
   Private editorFactory As EditorFactory  
   ```  
  
   ```csharp  
   private EditorFactory editorFactory;  
   ```  
  
7. Localizar o `Initialize` método (talvez você precise abrir o `Package Members` região oculta) e adicione o seguinte código após a chamada para `base.Initialize()`.  
  
   ```vb  
   'Create our editor factory and register it.   
   Me.editorFactory = New EditorFactory(Me)  
   MyBase.RegisterEditorFactory(Me.editorFactory)  
   ```  
  
   ```csharp  
   // Create our editor factory and register it.  
   this.editorFactory = new EditorFactory(this);  
   base.RegisterEditorFactory(this.editorFactory);  
  
   ```  
  
8. Compile o programa e verifique se que não existem erros.  
  
    Esta etapa registra a fábrica do editor no hive do registro experimental para [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Se você for solicitado a substituir a *Resource. h* arquivo, clique em **Okey**.  
  
9. Crie um arquivo de exemplo chamado *TextFile1.myext*.  
  
10. Pressione **F5** para abrir uma instância de experimental [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].  
  
11. Em experimental [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]diante a **arquivo** , aponte para **abra** e, em seguida, clique em **arquivo**.  
  
12. Encontre **TextFile1.myext** e, em seguida, clique em **abrir**.  
  
     O arquivo agora deverá ser carregado.  
  
## <a name="robust-programming"></a>Programação robusta  
 O [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor principal do lida com uma ampla variedade de tipos de arquivo de texto e trabalha em cooperação com serviços de linguagem para fornecer um conjunto avançado de recursos como realce de sintaxe, correspondência de chaves e preenchimento de palavra do IntelliSense e a lista de preenchimento de membro. Se você estiver trabalhando com arquivos de texto, você pode usar o editor principal junto com um serviço de linguagem personalizados que dá suporte a seus tipos de arquivo específico.  
  
 Um VSPackage pode invocar o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo, fornecendo uma fábrica de editor. Esta fábrica de editor é usada sempre que um arquivo que foi associado a ele é carregado. Se o arquivo for parte de um projeto, o editor de núcleo é invocado automaticamente, a menos que substituído pelo VSPackage. No entanto, se o arquivo for carregado fora de um projeto, o editor principal deve ser chamado explicitamente pelo VSPackage.  
  
 Para obter mais informações sobre o editor de núcleo, consulte [dentro do editor de núcleo](../extensibility/inside-the-core-editor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Dentro do editor de núcleo](../extensibility/inside-the-core-editor.md)   
 [Criar uma instância o editor principal usando a API herdada](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)