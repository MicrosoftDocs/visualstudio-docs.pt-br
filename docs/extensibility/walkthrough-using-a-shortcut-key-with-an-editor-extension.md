---
title: 'Passo a passo: Usando uma tecla de atalho com uma extensão do Editor | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d009351efdd36e0d415d0e2e457f7974608ab665
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886487"
---
# <a name="walkthrough-use-a-shortcut-key-with-an-editor-extension"></a>Passo a passo: Usar uma tecla de atalho com uma extensão do editor
Você pode responder a teclas de atalho em sua extensão de editor. A instrução a seguir mostra como adicionar um adorno de exibição para uma exibição de texto usando uma tecla de atalho. Este passo a passo se baseia no modelo de editor do adorno de visor e permite que você adicionar o adorno, usando o caractere +.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="create-a-managed-extensibility-framework-mef-project"></a>Criar um projeto do Managed Extensibility Framework (MEF)  
  
1. Crie um projeto de VSIX em C#. (Na **novo projeto** caixa de diálogo, selecione **Visual c# / extensibilidade**, em seguida, **projeto VSIX**.) Nomeie a solução `KeyBindingTest`.  
  
2. Adicione um modelo de item de adornos de texto do Editor ao projeto e denomine- `KeyBindingTest`. Para obter mais informações, consulte [criar uma extensão com um modelo de Item Editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).  
  
3. Adicione as seguintes referências e defina **CopyLocal** para `false`:  
  
    Microsoft.VisualStudio.Editor  
  
    Microsoft.VisualStudio.OLE.Interop  
  
    Microsoft.VisualStudio.Shell.14.0  
  
    Microsoft.VisualStudio.TextManager.Interop  
  
   No arquivo de classe KeyBindingTest, altere o nome de classe para PurpleCornerBox. Use a lâmpada que aparece na margem esquerda para fazer outras alterações apropriadas. Dentro do construtor, altere o nome da camada de adorno **KeyBindingTest** à **PurpleCornerBox**:  
  
```csharp  
this.layer = view.GetAdornmentLayer("PurpleCornerBox");  
```  

No arquivo de classe KeyBindingTestTextViewCreationListener.cs, altere o nome de AdornmentLayer a partir **KeyBindingTest** à **PurpleCornerBox**:
  
    ```csharp  
    [Export(typeof(AdornmentLayerDefinition))]  
    [Name("PurpleCornerBox")]  
    [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]  
    public AdornmentLayerDefinition editorAdornmentLayer;  
    ```  

## <a name="handle-typechar-command"></a>Lidar com o comando TIPOCARAC
Antes do Visual Studio 2017 versão 15.6, a única maneira de lidar com comandos em uma extensão do editor foi implementar um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> com base em filtro de comando. Visual Studio 2017 versão 15.6 introduziu uma abordagem simplificada modernos, com base em manipuladores de comandos do editor. As próximas duas seções demonstram como lidar com um comando usando tanto a abordagem herdada e moderna.

## <a name="define-the-command-filter-prior-to-visual-studio-2017-version-156"></a>Definir o filtro de comando (antes do Visual Studio 2017 versão 15.6)

 O filtro de comando é uma implementação de <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>, que manipula o comando instanciando o adorno.  
  
1.  Adicione um arquivo de classe e denomine- `KeyBindingCommandFilter`.  
  
2.  Adicione as seguintes instruções using.  
  
    ```csharp  
    using System;  
    using System.Runtime.InteropServices;  
    using Microsoft.VisualStudio.OLE.Interop;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.Text.Editor;  
  
    ```  
  
3.  A classe denominada KeyBindingCommandFilter deve herdar de <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>.  
  
    ```csharp  
    internal class KeyBindingCommandFilter : IOleCommandTarget  
    ```  
  
4.  Adicione campos privados para o modo de exibição de texto, o próximo comando na cadeia de comando e um sinalizador para representar se o filtro de comando já foi adicionado.  
  
    ```csharp  
    private IWpfTextView m_textView;  
    internal IOleCommandTarget m_nextTarget;  
    internal bool m_added;  
    internal bool m_adorned;  
    ```  
  
5.  Adicione um construtor que define o modo de texto.  
  
    ```csharp  
    public KeyBindingCommandFilter(IWpfTextView textView)  
    {  
        m_textView = textView;  
        m_adorned = false;  
    }  
    ```  
  
6.  Implementar o `QueryStatus()` método da seguinte maneira.  
  
    ```csharp  
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)  
    {  
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);  
    }  
    ```  
  
7.  Implemente a `Exec()` , de modo que ele adiciona uma caixa de roxa para o modo de exibição, se um sinal de adição (**+**) caractere é digitado.  
  
    ```csharp  
    int IOleCommandTarget.Exec(ref Guid pguidCmdGroup, uint nCmdID, uint nCmdexecopt, IntPtr pvaIn, IntPtr pvaOut)  
    {  
        if (m_adorned == false)  
        {  
            char typedChar = char.MinValue;  
  
            if (pguidCmdGroup == VSConstants.VSStd2K && nCmdID == (uint)VSConstants.VSStd2KCmdID.TYPECHAR)  
            {  
                typedChar = (char)(ushort)Marshal.GetObjectForNativeVariant(pvaIn);  
                if (typedChar.Equals('+'))  
                {  
                    new PurpleCornerBox(m_textView);  
                    m_adorned = true;  
                }  
            }  
        }  
        return m_nextTarget.Exec(ref pguidCmdGroup, nCmdID, nCmdexecopt, pvaIn, pvaOut);  
    }  
  
    ```  
  
## <a name="add-the-command-filter-prior-to-visual-studio-2017-version-156"></a>Adicione o filtro de comando (antes do Visual Studio 2017 versão 15.6)
 O provedor de adorno deve adicionar um filtro de comando para a exibição de texto. Neste exemplo, o provedor implementa <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> para escutar eventos de criação de exibição de texto. Este provedor de adorno também exporta a camada de adorno, que define a ordem Z do adorno.  
  
1.  No arquivo KeyBindingTestTextViewCreationListener, adicione as seguintes instruções using:  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ComponentModel.Composition;  
    using Microsoft.VisualStudio;  
    using Microsoft.VisualStudio.OLE.Interop;  
    using Microsoft.VisualStudio.Utilities;  
    using Microsoft.VisualStudio.Editor;  
    using Microsoft.VisualStudio.Text.Editor;  
    using Microsoft.VisualStudio.TextManager.Interop;  
  
    ```  
  
2.  Para obter o adaptador de exibição de texto, você deve importar o <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>.  
  
    ```csharp  
    [Import(typeof(IVsEditorAdaptersFactoryService))]  
    internal IVsEditorAdaptersFactoryService editorFactory = null;  
  
    ```  
  
3.  Alterar o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> , de modo que ele adiciona o `KeyBindingCommandFilter`.  
  
    ```csharp  
    public void TextViewCreated(IWpfTextView textView)  
    {  
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));  
    }  
    ```  
  
4.  O `AddCommandFilter` manipulador obtém o adaptador de exibição de texto e adiciona o filtro de comando.  
  
    ```csharp  
    void AddCommandFilter(IWpfTextView textView, KeyBindingCommandFilter commandFilter)  
    {  
        if (commandFilter.m_added == false)  
        {  
            //get the view adapter from the editor factory  
            IOleCommandTarget next;   
            IVsTextView view = editorFactory.GetViewAdapter(textView);  
  
            int hr = view.AddCommandFilter(commandFilter, out next);  
  
            if (hr == VSConstants.S_OK)  
            {      
                commandFilter.m_added = true;  
                 //you'll need the next target for Exec and QueryStatus   
                if (next != null)  
                commandFilter.m_nextTarget = next;  
            }  
        }  
    }  
    ```  

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>Implemente um manipulador de comando (começando no Visual Studio 2017 versão 15.6)

Primeiro, atualize as referências do projeto Nuget para fazer referência o API de editor mais recente:

1. Clique com botão direito no projeto e selecione **gerenciar pacotes Nuget**.

2. Na **Gerenciador de pacotes Nuget**, selecione o **atualizações** guia, selecione o **selecionar todos os pacotes** caixa de seleção e, em seguida, selecione **atualização**.

O manipulador de comandos é uma implementação de <xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601>, que manipula o comando instanciando o adorno.  
  
1. Adicione um arquivo de classe e denomine- `KeyBindingCommandHandler`.  
  
2. Adicione as seguintes instruções using.  
  
   ```csharp  
   using Microsoft.VisualStudio.Commanding;
   using Microsoft.VisualStudio.Text.Editor;
   using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
   using Microsoft.VisualStudio.Utilities;
   using System.ComponentModel.Composition;   
   ```  
  
3. A classe denominada KeyBindingCommandHandler deve herdar de `ICommandHandler<TypeCharCommandArgs>`e exportá-lo como <xref:Microsoft.VisualStudio.Commanding.ICommandHandler>:
  
   ```csharp  
   [Export(typeof(ICommandHandler))]
   [ContentType("text")]
   [Name("KeyBindingTest")]
   internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>  
   ```  
  
4. Adicione um nome de exibição do manipulador de comando:  
  
   ```csharp  
   public string DisplayName => "KeyBindingTest";
   ```  
    
5. Implementar o `GetCommandState()` método da seguinte maneira. Porque esse manipulador de comandos lida com o comando TIPOCARAC do core editor, poderá delegar habilitando o comando para o editor de núcleo.
  
   ```csharp  
   public CommandState GetCommandState(TypeCharCommandArgs args)
   {
       return CommandState.Unspecified;
   } 
   ```  
  
6. Implemente a `ExecuteCommand()` , de modo que ele adiciona uma caixa de roxa para o modo de exibição, se um sinal de adição (**+**) caractere é digitado. 
  
   ```csharp  
   public bool ExecuteCommand(TypeCharCommandArgs args, CommandExecutionContext executionContext)
   {
       if (args.TypedChar == '+')
       {
           bool alreadyAdorned = args.TextView.Properties.TryGetProperty(
               "KeyBindingTextAdorned", out bool adorned) && adorned;
           if (!alreadyAdorned)
           {
               new PurpleCornerBox((IWpfTextView)args.TextView);
               args.TextView.Properties.AddProperty("KeyBindingTextAdorned", true);
           }
       }

       return false;
   }
   ```  
   7. Copie a definição de camada de adorno do *KeyBindingTestTextViewCreationListener.cs* do arquivo para o *KeyBindingCommandHandler.cs* e, em seguida, excluir  *KeyBindingTestTextViewCreationListener.cs* arquivo:
 
   ```csharp  
   /// <summary>
   /// Defines the adornment layer for the adornment. This layer is ordered
   /// after the selection layer in the Z-order.
   /// </summary>
   [Export(typeof(AdornmentLayerDefinition))]
   [Name("PurpleCornerBox")]
   [Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
   private AdornmentLayerDefinition editorAdornmentLayer;    
   ```  

## <a name="make-the-adornment-appear-on-every-line"></a>Fazer com que o adorno apareça em cada linha  

O adorno original exibido em todos os caracteres 'a' em um arquivo de texto. Agora que alteramos o código para adicionar o adorno em resposta à **+** caractere, ele adiciona o adorno apenas na linha em que o **+** caractere é digitado. Podemos alterar o código de adorno para que seja exibido o adorno mais uma vez em cada 'a'.  
  
No *KeyBindingTest.cs* file, altere o `CreateVisuals()` método para iterar por todas as linhas no modo de exibição para decorar o caractere 'a'.  
  
```csharp  
private void CreateVisuals(ITextViewLine line)  
{  
    IWpfTextViewLineCollection textViewLines = this.view.TextViewLines;  
  
    foreach (ITextViewLine textViewLine in textViewLines)  
    {  
        if (textViewLine.ToString().Contains("a"))  
        {  
            // Loop through each character, and place a box around any 'a'   
            for (int charIndex = textViewLine.Start; charIndex < textViewLine.End; charIndex++)  
            {  
                if (this.view.TextSnapshot[charIndex] == 'a')  
                {  
                    SnapshotSpan span = new SnapshotSpan(this.view.TextSnapshot, Span.FromBounds(charIndex, charIndex + 1));  
                    Geometry geometry = textViewLines.GetMarkerGeometry(span);  
                    if (geometry != null)  
                    {  
                        var drawing = new GeometryDrawing(this.brush, this.pen, geometry);  
                        drawing.Freeze();  
  
                        var drawingImage = new DrawingImage(drawing);  
                        drawingImage.Freeze();  
  
                        var image = new Image  
                        {  
                            Source = drawingImage,  
                        };  
  
                        // Align the image with the top of the bounds of the text geometry  
                        Canvas.SetLeft(image, geometry.Bounds.Left);  
                        Canvas.SetTop(image, geometry.Bounds.Top);  
  
                        this.layer.AddAdornment(AdornmentPositioningBehavior.TextRelative, span, null, image, null);  
                    }  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="build-and-test-the-code"></a>Compilar e testar o código  
  
1.  Compile a solução KeyBindingTest e executá-lo na instância experimental.  
  
2.  Crie ou abra um arquivo de texto. Digite algumas palavras que contém o caractere 'a' e, em seguida, digite **+** em qualquer lugar na exibição de texto.  
  
     Um quadrado roxo deve aparecer em cada caractere 'a' no arquivo.
