---
title: Como especificar eventos de build (C#)
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
ms.assetid: b4ce1ad9-5215-4b6f-b6a2-798b249aa335
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: aa82c7f12b3932c1e9f5aac7392d6ef2b8e8a773
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49885835"
---
# <a name="how-to-specify-build-events-c"></a>Como especificar eventos de build (C#)

Use eventos de build para especificar comandos que são executados antes do início do build ou após sua conclusão. Eventos de build são executados somente se o build atingir com êxito esses pontos no processo de build.

Quando um projeto é compilado, eventos de pré-build são adicionados a um arquivo chamado *PreBuildEvent.bat* e eventos de pós-build são adicionados a um arquivo chamado *PostBuildEvent.bat*. Se quiser garantir a verificação de erros, adicione seus próprios comandos de verificação de erros às etapas de build.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="how-to-specify-pre-build-and-post-build-events"></a>Como especificar eventos de pré-build e de pós-build

### <a name="to-specify-a-build-event"></a>Para especificar um evento de build

1.  No **Gerenciador de Soluções**, selecione o projeto para o qual deseja especificar o evento de build.

2.  No menu **Projeto**, clique em **Propriedades**.

3.  Selecione a guia **Eventos de Build**.

4.  Na caixa **Linha de comando do evento de pré-build**, especifique a sintaxe do evento de build.

    > [!NOTE]
    > Eventos de pré-build não serão executados se o projeto estiver atualizado e nenhum build será disparado.

5.  Na caixa **Linha de comando do evento de pós-build**, especifique a sintaxe do evento de build.

    > [!NOTE]
    > Adicione uma instrução `call` antes de todos os comandos pós-build que executam arquivos *.bat*. Por exemplo `call C:\MyFile.bat` ou `call C:\MyFile.bat call C:\MyFile2.bat`.

6.  Na caixa **Executar o evento de pós-build**, especifique em que condições o evento pós-build deve ser executado.

    > [!NOTE]
    > Para adicionar uma sintaxe longa ou para selecionar macros de build na [Caixa de diálogo de linha de comando do evento de pré-/pós-build](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md), clique no botão de reticências (**...**) para exibir uma caixa de edição.

     A sintaxe do evento de build pode incluir qualquer comando que seja válido em um prompt de comando ou em um arquivo *.bat*. O nome de um arquivo em lote deve ser precedido por `call` para garantir que todos os comandos posteriores sejam executados.

    > [!NOTE]
    > Se o evento de pré ou de pós-build não for concluído com êxito, você poderá encerrar o build fazendo a ação do evento terminar com um código diferente de zero (0), o que indica uma ação bem-sucedida.

## <a name="example-how-to-change-manifest-information-by-using-a-post-build-event"></a>Exemplo: como alterar informações de manifesto usando um evento de pós-build

O procedimento a seguir mostra como definir a versão mínima do sistema operacional no manifesto do aplicativo usando um comando *.exe* chamado de um evento de pós-build (o arquivo *.exe.manifest* no diretório do projeto). A versão mínima do sistema operacional é um número de quatro partes, como 4.10.0.0. Para fazer isso, o comando alterará a seção `<dependentOS>` do manifesto:

```xml
<dependentOS>
   <osVersionInfo>
      <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
   </osVersionInfo>
</dependentOS>
```

### <a name="to-create-an-exe-command-to-change-the-application-manifest"></a>Para criar um comando .exe para alterar o manifesto do aplicativo

1. Crie um aplicativo de console para o comando. No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.

2. Na caixa de diálogo **Novo Projeto**, expanda **Visual C#**, clique em **Windows** e, em seguida, clique no modelo **Aplicativo de Console**. Nomeie o projeto `ChangeOSVersionCS`.

3. Em *Program.cs*, adicione a seguinte linha às outras instruções `using` na parte superior do arquivo:

   ```csharp
   using System.Xml;
   ```

4. No namespace `ChangeOSVersionCS`, substitua a implementação da classe `Program` pelo seguinte código:

   ```csharp
   class Program
   {
      /// <summary>
      /// This function will set the minimum operating system version for a ClickOnce application.
      /// </summary>
      /// <param name="args">
      /// Command Line Arguments:
      /// 0 - Path to application manifest (.exe.manifest).
      /// 1 - Version of OS
      ///</param>
      static void Main(string[] args)
      {
         string applicationManifestPath = args[0];
         Console.WriteLine("Application Manifest Path: " + applicationManifestPath);

         // Get version name.
         Version osVersion = null;
         if (args.Length >=2 ){
            osVersion = new Version(args[1]);
         }else{
            throw new ArgumentException("OS Version not specified.");
         }
         Console.WriteLine("Desired OS Version: " + osVersion.ToString());

         XmlDocument document;
         XmlNamespaceManager namespaceManager;
         namespaceManager = new XmlNamespaceManager(new NameTable());
         namespaceManager.AddNamespace("asmv1", "urn:schemas-microsoft-com:asm.v1");
         namespaceManager.AddNamespace("asmv2", "urn:schemas-microsoft-com:asm.v2");

         document = new XmlDocument();
         document.Load(applicationManifestPath);

         string baseXPath;
         baseXPath = "/asmv1:assembly/asmv2:dependency/asmv2:dependentOS/asmv2:osVersionInfo/asmv2:os";

         // Change minimum required operating system version.
         XmlNode node;
         node = document.SelectSingleNode(baseXPath, namespaceManager);
         node.Attributes["majorVersion"].Value = osVersion.Major.ToString();
         node.Attributes["minorVersion"].Value = osVersion.Minor.ToString();
         node.Attributes["buildNumber"].Value = osVersion.Build.ToString();
         node.Attributes["servicePackMajor"].Value = osVersion.Revision.ToString();

         document.Save(applicationManifestPath);
      }
   }
   ```

    O comando utiliza dois argumentos: o caminho do manifesto do aplicativo (ou seja, a pasta na qual o processo de build cria o manifesto, normalmente *Projectname.publish*) e a nova versão do sistema operacional.

5. Compile o projeto. No menu **Compilar**, clique em **Compilar Solução**.

6. Copie o arquivo *.exe* para um diretório como *C:\TEMP\ChangeOSVersionVB.exe*.

   Em seguida, invoque este comando em um evento de pós-build para modificar o manifesto do aplicativo.

### <a name="to-invoke-a-post-build-event-to-modify-the-application-manifest"></a>Para invocar um evento de pós-build para modificar o manifesto do aplicativo

1.  Crie um aplicativo do Windows para o projeto a ser publicado. No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.

2.  Na caixa de diálogo **Novo Projeto**, expanda **Visual C#**, clique em **Área de Trabalho do Windows** e, em seguida, clique no modelo **Aplicativo do Windows Forms**. Nomeie o projeto `CSWinApp`.

3.  Com o projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.

4.  No **Designer de Projeto**, localize a página **Publicar** e defina o **Local de Publicação** como *C:\TEMP*.

5.  Publique o projeto clicando em **Publicar Agora**.

     O arquivo de manifesto será compilado e colocado em *C:\TEMP\CSWinApp_1_0_0_0\CSWinApp.exe.manifest*. Para exibir o manifesto, clique com o botão direito do mouse no arquivo, clique em **Abrir com**, selecione **Selecionar um programa em uma lista de programas instalados** e clique em **Bloco de Notas**.

     Pesquise o elemento `<osVersionInfo>` no arquivo. Por exemplo, a versão pode ser:

    ```xml
    <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
    ```

6.  No **Designer de Projeto**, clique na guia **Eventos de Build** e clique no botão **Editar pós-build**.

7.  Na caixa **Linha de comando do evento de pós-build**, digite o seguinte comando:

     `C:\TEMP\ChangeOSVersionCS.exe "$(TargetPath).manifest" 5.1.2600.0`

     Ao compilar o projeto, esse comando alterará a versão mínima do sistema operacional no manifesto do aplicativo para 5.1.2600.0.

     Como a macro `$(TargetPath)` expressa o caminho completo para o executável que está sendo criado, o `$(TargetPath)`*.manifest* especificará o manifesto do aplicativo criado no diretório *bin*. A publicação copiará esse manifesto para o local de publicação definido anteriormente.

8.  Publique o projeto novamente. Acesse a página **Publicar** e clique em **Publicar Agora**.

     Exiba o manifesto novamente. Para exibir o manifesto, abra o diretório de publicação, clique com o botão direito do mouse no arquivo, clique em **Abrir com**, selecione **Selecionar um programa em uma lista de programas instalados** e clique em **Bloco de Notas**.

     A versão agora deve ser:

    ```xml
    <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" />
    ```

## <a name="see-also"></a>Consulte também

- [Página Eventos de Build, Designer de Projeto (C#)](../ide/reference/build-events-page-project-designer-csharp.md)
- [Caixa de diálogo da linha de comando do evento de pré-build/evento de pós-build](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
- [Como especificar eventos de build (Visual Basic)](../ide/how-to-specify-build-events-visual-basic.md)
- [Compilação e build](../ide/compiling-and-building-in-visual-studio.md)