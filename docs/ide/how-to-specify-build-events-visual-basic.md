---
title: Como especificar eventos de build (Visual Basic)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- pre-build events
- events [Visual Studio], builds
- post-build events
- build events [Visual Studio]
- builds [Visual Studio], events
ms.assetid: 40dc83bf-a7c5-4a14-816a-fa0980b6e4c3
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 24eb6d7637f949abf60eeb2d0659fac1bfa1cae7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49831725"
---
# <a name="how-to-specify-build-events-visual-basic"></a>Como especificar eventos de build (Visual Basic)

Eventos de build no Visual Basic podem ser usados para executar scripts, macros ou outras ações como parte do processo de compilação. Eventos de pré-build ocorrem antes da compilação; eventos de pós-build ocorrem após a compilação.

Eventos de build são especificados na caixa de diálogo **Eventos de Build**, disponível na página **Compilar** do **Designer de Projeto**.

> [!NOTE]
> O Visual Basic Express não dá suporte à entrada de eventos de build. Isso tem suporte apenas no produto Visual Studio completo.

## <a name="how-to-specify-pre-build-and-post-build-events"></a>Como especificar eventos de pré-build e de pós-build

### <a name="to-specify-a-build-event"></a>Para especificar um evento de build

1.  Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

2.  Clique na guia **Compilar**.

3.  Clique no botão **Eventos de Build** para abrir a caixa de diálogo **Eventos de Build**.

4.  Insira os argumentos de linha de comando para a ação pré ou pós-build e, em seguida, clique em **OK**.

    > [!NOTE]
    > Adicione uma instrução `call` antes de todos os comandos pós-build que executam arquivos *.bat*. Por exemplo `call C:\MyFile.bat` ou `call C:\MyFile.bat call C:\MyFile2.bat`.

    > [!NOTE]
    > Se o evento de pré ou de pós-build não for concluído com êxito, você poderá encerrar o build fazendo a ação do evento terminar com um código diferente de zero (0), o que indica uma ação bem-sucedida.

## <a name="example-how-to-change-manifest-information-using-a-post-build-event"></a>Exemplo: como alterar informações de manifesto usando um evento de pós-build

O procedimento a seguir mostra como definir a versão mínima do sistema operacional no manifesto do aplicativo usando um comando *.exe* chamado de um evento de pós-build (o arquivo *.exe.manifest* no diretório do projeto). A versão mínima do sistema operacional é um número de quatro partes, como 4.10.0.0. Para fazer isso, o comando alterará a seção `<dependentOS>` do manifesto:

```xml
<dependentOS>
   <osVersionInfo>
      <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
   </osVersionInfo>
</dependentOS>
```

### <a name="to-create-an-exe-command-to-change-the-application-manifest"></a>Para criar um comando .exe para alterar o manifesto do aplicativo

1. Crie um aplicativo de console para o comando. No menu **Arquivo**, clique em **Novo** e em **Projeto**.

2. Na caixa de diálogo **Novo Projeto**, no nó **Visual Basic**, selecione **Windows** e, em seguida, o modelo **Aplicativo de Console**. Nomeie o projeto `ChangeOSVersionVB`.

3. Em *Module1.vb*, adicione a seguinte linha às outras instruções `Imports` na parte superior do arquivo:

   ```vb
   Imports System.Xml
   ```

4. Adicione o seguinte código em `Sub Main`:

   ```vb
   Sub Main()
      Dim applicationManifestPath As String
      applicationManifestPath = My.Application.CommandLineArgs(0)
      Console.WriteLine("Application Manifest Path: " & applicationManifestPath.ToString)

      'Get version name
      Dim osVersion As Version
      If My.Application.CommandLineArgs.Count >= 2 Then
         osVersion = New Version(My.Application.CommandLineArgs(1).ToString)
      Else
         Throw New ArgumentException("OS Version not specified.")
      End If
      Console.WriteLine("Desired OS Version: " & osVersion.ToString())

      Dim document As XmlDocument
      Dim namespaceManager As XmlNamespaceManager
      namespaceManager = New XmlNamespaceManager(New NameTable())
      With namespaceManager
         .AddNamespace("asmv1", "urn:schemas-microsoft-com:asm.v1")
         .AddNamespace("asmv2", "urn:schemas-microsoft-com:asm.v2")
      End With

      document = New XmlDocument()
      document.Load(applicationManifestPath)

      Dim baseXPath As String
      baseXPath = "/asmv1:assembly/asmv2:dependency/asmv2:dependentOS/asmv2:osVersionInfo/asmv2:os"

      'Change minimum required OS Version.
      Dim node As XmlNode
      node = document.SelectSingleNode(baseXPath, namespaceManager)
      node.Attributes("majorVersion").Value = osVersion.Major.ToString()
      node.Attributes("minorVersion").Value = osVersion.Minor.ToString()
      node.Attributes("buildNumber").Value = osVersion.Build.ToString()
      node.Attributes("servicePackMajor").Value = osVersion.Revision.ToString()

      document.Save(applicationManifestPath)
   End Sub
   ```

   O comando utiliza dois argumentos. O primeiro argumento é o caminho para o manifesto do aplicativo (ou seja, a pasta na qual o processo de build cria o manifesto, geralmente, *<Projectname>.publish*). O segundo argumento é a nova versão do sistema operacional.

5. No menu **Compilar**, clique em **Compilar Solução**.

6. Copie o arquivo *.exe* para um diretório como *C:\TEMP\ChangeOSVersionVB.exe*.

   Em seguida, invoque esse comando em um evento de pós-build para modificar o manifesto do aplicativo.

### <a name="to-invoke-a-post-build-event-to-change-the-application-manifest"></a>Para invocar um evento de pós-build para alterar o manifesto do aplicativo

1.  Crie um aplicativo do Windows para o projeto a ser publicado. No menu **Arquivo**, clique em **Novo** e em **Projeto**.

2.  Na caixa de diálogo **Novo Projeto**, no nó **Visual Basic**, selecione **Área de Trabalho do Windows** e, em seguida, o modelo **Aplicativo do Windows Forms**. Nomeie o projeto `VBWinApp`.
3.  Com o projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

4.  No **Designer de Projeto**, acesse a página **Publicar** e defina o **Local de publicação** como *C:\TEMP*.

5.  Publique o projeto clicando em **Publicar Agora**.

     O arquivo de manifesto será compilado e colocado em *C:\TEMP\VBWinApp_1_0_0_0\VBWinApp.exe.manifest*. Para exibir o manifesto, clique com o botão direito do mouse no arquivo, clique em **Abrir com**, então clique em **Selecionar um programa em uma lista de programas instalados** e clique em **Bloco de Notas**.

     Pesquise o elemento `<osVersionInfo>` no arquivo. Por exemplo, a versão pode ser:

    ```xml
    <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
    ```

6.  No **Designer de Projeto**, vá para a guia **Compilar** e clique no botão **Eventos de Build** para abrir a caixa de diálogo **Eventos de Build**.

7.  Na caixa **Linha de Comando do Evento de Pós-Build**, digite o seguinte comando:

     `C:\TEMP\ChangeOSVersionVB.exe "$(TargetPath).manifest" 5.1.2600.0`

     Ao compilar o projeto, esse comando alterará a versão mínima do sistema operacional no manifesto do aplicativo para 5.1.2600.0.

     A macro `$(TargetPath)` expressa o caminho completo para o arquivo executável que está sendo criado. Portanto, *$(TargetPath).manifest* especificará o manifesto do aplicativo criado no diretório *bin*. A publicação copiará esse manifesto para o local de publicação definido anteriormente.

8.  Publique o projeto novamente. Acesse a página **Publicar** e clique em **Publicar Agora**.

     Exiba o manifesto novamente. Para exibir o manifesto, vá para o diretório de publicação, clique com o botão direito do mouse no arquivo, clique em **Abrir com**, então em **Selecionar o programa em uma lista** e, em seguida, clique no **Bloco de Notas**.

     A versão agora deve ser:

    ```xml
    <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" />
    ```

## <a name="see-also"></a>Consulte também

- [Página de compilação, Designer de Projeto (Visual Basic)](../ide/reference/compile-page-project-designer-visual-basic.md)
- [Página de Publicação, Designer de Projeto](../ide/reference/publish-page-project-designer.md)
- [Caixa de diálogo da linha de comando do evento de pré-build/evento de pós-build](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
- [Como especificar eventos de build (C#)](../ide/how-to-specify-build-events-csharp.md)