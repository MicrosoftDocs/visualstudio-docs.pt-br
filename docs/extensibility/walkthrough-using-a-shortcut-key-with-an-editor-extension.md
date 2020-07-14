---
title: 'Walkthrough: usando uma tecla de atalho com uma extensão de editor | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - link keystrokes to commands
ms.assetid: cf6cc6c6-5a65-4f90-8f14-663decf74672
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 094cb590d5b2a3bf062916985bfc61b1cf76d365
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904400"
---
# <a name="walkthrough-use-a-shortcut-key-with-an-editor-extension"></a>Walkthrough: usar uma tecla de atalho com uma extensão do editor
Você pode responder às teclas de atalho na extensão do editor. A instrução a seguir mostra como adicionar uma exibição Adornment a uma exibição de texto usando uma tecla de atalho. Este passo a passos é baseado no modelo do editor de Adornment do visor e permite que você adicione o Adornment usando o caractere +.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio do centro de download. Ele está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-managed-extensibility-framework-mef-project"></a>Criar um projeto Managed Extensibility Framework (MEF)

1. Crie um projeto VSIX em C#. (Na caixa de diálogo **novo projeto** , selecione **Visual C#/extensibilidade**e, em seguida, **projeto VSIX**.) Nomeie a solução `KeyBindingTest` .

2. Adicione um modelo de item Adornment de texto do editor ao projeto e nomeie-o `KeyBindingTest` . Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

3. Adicione as seguintes referências e defina **CopyLocal** como `false` :

    Microsoft. VisualStudio. editor

    Microsoft. VisualStudio. OLE. Interop

    Microsoft. VisualStudio. Shell. 14.0

    Microsoft. VisualStudio. Textmanager. Interop

   No arquivo da classe KeyBindingTest, altere o nome da classe para PurpleCornerBox. Use a lâmpada que aparece na margem esquerda para fazer as outras alterações apropriadas. Dentro do Construtor, altere o nome da camada Adornment de **KeyBindingTest** para **PurpleCornerBox**:

```csharp
this.layer = view.GetAdornmentLayer("PurpleCornerBox");
```

No arquivo da classe KeyBindingTestTextViewCreationListener.cs, altere o nome do AdornmentLayer de **KeyBindingTest** para **PurpleCornerBox**:

```csharp
[Export(typeof(AdornmentLayerDefinition))]
[Name("PurpleCornerBox")]
[Order(After = PredefinedAdornmentLayers.Selection, Before = PredefinedAdornmentLayers.Text)]
public AdornmentLayerDefinition editorAdornmentLayer;
```

## <a name="handle-typechar-command"></a>Manipular o comando TYPECHAR
Antes do Visual Studio 2017 versão 15,6, a única maneira de manipular comandos em uma extensão do editor era implementar um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> filtro de comando baseado. O Visual Studio 2017 versão 15,6 introduziu uma abordagem simplificada moderna com base nos manipuladores de comandos do editor. As próximas duas seções demonstram como lidar com um comando usando a abordagem herdada e moderna.

## <a name="define-the-command-filter-prior-to-visual-studio-2017-version-156"></a>Definir o filtro de comando (antes do Visual Studio 2017 versão 15,6)

 O filtro de comando é uma implementação do <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> , que manipula o comando ao instanciar o Adornment.

1. Adicione um arquivo de classe e nomeie-o `KeyBindingCommandFilter` .

2. Adicione as seguintes diretivas using.

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio.OLE.Interop;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Text.Editor;

    ```

3. A classe denominada KeyBindingCommandFilter deve herdar de <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> .

    ```csharp
    internal class KeyBindingCommandFilter : IOleCommandTarget
    ```

4. Adicione campos particulares para a exibição de texto, o próximo comando na cadeia de comandos e um sinalizador para representar se o filtro de comando já foi adicionado.

    ```csharp
    private IWpfTextView m_textView;
    internal IOleCommandTarget m_nextTarget;
    internal bool m_added;
    internal bool m_adorned;
    ```

5. Adicione um construtor que define a exibição de texto.

    ```csharp
    public KeyBindingCommandFilter(IWpfTextView textView)
    {
        m_textView = textView;
        m_adorned = false;
    }
    ```

6. Implemente o `QueryStatus()` método da seguinte maneira.

    ```csharp
    int IOleCommandTarget.QueryStatus(ref Guid pguidCmdGroup, uint cCmds, OLECMD[] prgCmds, IntPtr pCmdText)
    {
        return m_nextTarget.QueryStatus(ref pguidCmdGroup, cCmds, prgCmds, pCmdText);
    }
    ```

7. Implemente o `Exec()` método para que ele adicione uma caixa roxa à exibição se um caractere de sinal de adição ( **+** ) for digitado.

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

## <a name="add-the-command-filter-prior-to-visual-studio-2017-version-156"></a>Adicionar o filtro de comando (antes do Visual Studio 2017 versão 15,6)
 O provedor Adornment deve adicionar um filtro de comando à exibição de texto. Neste exemplo, o provedor implementa <xref:Microsoft.VisualStudio.Editor.IVsTextViewCreationListener> para escutar eventos de criação de exibição de texto. Esse provedor Adornment também exporta a camada Adornment, que define a ordem Z do Adornment.

1. No arquivo KeyBindingTestTextViewCreationListener, adicione as seguintes diretivas using:

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

2. Para obter o adaptador de exibição de texto, você deve importar o <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> .

    ```csharp
    [Import(typeof(IVsEditorAdaptersFactoryService))]
    internal IVsEditorAdaptersFactoryService editorFactory = null;

    ```

3. Altere o <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> método para que ele adicione o `KeyBindingCommandFilter` .

    ```csharp
    public void TextViewCreated(IWpfTextView textView)
    {
        AddCommandFilter(textView, new KeyBindingCommandFilter(textView));
    }
    ```

4. O `AddCommandFilter` manipulador obtém o adaptador de exibição de texto e adiciona o filtro de comando.

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

## <a name="implement-a-command-handler-starting-in-visual-studio-2017-version-156"></a>Implementar um manipulador de comandos (a partir do Visual Studio 2017 versão 15,6)

Primeiro, atualize as referências do NuGet do projeto para referenciar a API mais recente do editor:

1. Clique com o botão direito do mouse no projeto e selecione **gerenciar pacotes NuGet**.

2. No **Gerenciador de pacotes NuGet**, selecione a guia **atualizações** , marque a caixa de seleção **selecionar todos os pacotes** e, em seguida, selecione **Atualizar**.

O manipulador de comandos é uma implementação do <xref:Microsoft.VisualStudio.Commanding.ICommandHandler%601> , que manipula o comando ao instanciar o Adornment.

1. Adicione um arquivo de classe e nomeie-o `KeyBindingCommandHandler` .

2. Adicione as seguintes diretivas using.

   ```csharp
   using Microsoft.VisualStudio.Commanding;
   using Microsoft.VisualStudio.Text.Editor;
   using Microsoft.VisualStudio.Text.Editor.Commanding.Commands;
   using Microsoft.VisualStudio.Utilities;
   using System.ComponentModel.Composition;
   ```

3. A classe chamada KeyBindingCommandHandler deve herdar de `ICommandHandler<TypeCharCommandArgs>` e exportá-la como <xref:Microsoft.VisualStudio.Commanding.ICommandHandler> :

   ```csharp
   [Export(typeof(ICommandHandler))]
   [ContentType("text")]
   [Name("KeyBindingTest")]
   internal class KeyBindingCommandHandler : ICommandHandler<TypeCharCommandArgs>
   ```

4. Adicione um nome de exibição do manipulador de comandos:

   ```csharp
   public string DisplayName => "KeyBindingTest";
   ```

5. Implemente o `GetCommandState()` método da seguinte maneira. Como esse manipulador de comandos manipula o comando TYPECHAR do editor de núcleo, ele pode delegar a habilitação do comando para o editor central.

   ```csharp
   public CommandState GetCommandState(TypeCharCommandArgs args)
   {
       return CommandState.Unspecified;
   }
   ```

6. Implemente o `ExecuteCommand()` método para que ele adicione uma caixa roxa à exibição se um caractere de sinal de adição ( **+** ) for digitado.

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

   7. Copie a definição de camada Adornment do arquivo *KeyBindingTestTextViewCreationListener.cs* para o *KeyBindingCommandHandler.cs* e, em seguida, exclua o arquivo *KeyBindingTestTextViewCreationListener.cs* :

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

## <a name="make-the-adornment-appear-on-every-line"></a>Fazer o Adornment aparecer em todas as linhas

O Adornment original apareceu em cada caractere ' a ' em um arquivo de texto. Agora que alteramos o código para adicionar o Adornment em resposta ao **+** caractere, ele adiciona o Adornment somente na linha em que o **+** caractere é digitado. Podemos alterar o código Adornment para que o Adornment mais uma vez apareça em cada ' a '.

No arquivo *KeyBindingTest.cs* , altere o `CreateVisuals()` método para iterar em todas as linhas na exibição para decorar o caractere ' a '.

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

1. Crie a solução KeyBindingTest e execute-a na instância experimental.

2. Criar ou abrir um arquivo de texto. Digite algumas palavras que contenham o caractere ' a ' e digite em **+** qualquer lugar na exibição de texto.

     Um quadrado roxo deve aparecer em cada caractere ' a ' no arquivo.
