---
title: Como especificar eventos de build (C#)
ms.date: 03/21/2019
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- pre-build events
- events [Visual Studio], builds
- post-build events
- build events [Visual Studio]
- builds [Visual Studio], events
ms.assetid: b4ce1ad9-5215-4b6f-b6a2-798b249aa335
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: e1a3083b59ad0cec727f753395768a214ff571b7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283990"
---
# <a name="how-to-specify-build-events-c"></a>Como especificar eventos de build (C#)

Use eventos de build para especificar comandos que são executados antes do início do build ou após sua conclusão. Eventos de build serão executados somente se o build atingir com êxito esses pontos no processo de build.

Quando um projeto é compilado, eventos de pré-build são adicionados a um arquivo chamado *PreBuildEvent.bat* e eventos de pós-build são adicionados a um arquivo chamado *PostBuildEvent.bat*. Se quiser garantir a verificação de erros, adicione seus próprios comandos de verificação de erros às etapas de build.

## <a name="specify-a-build-event"></a>Especificar um evento de build

1. No **Gerenciador de Soluções**, selecione o projeto para o qual deseja especificar o evento de build.

2. No menu **Projeto** , clique em **Propriedades**.

3. Selecione a guia **Eventos de Build**.

4. Na caixa **Linha de comando do evento de pré-build**, especifique a sintaxe do evento de build.

   > [!NOTE]
   > Eventos de pré-build não serão executados se o projeto estiver atualizado e nenhum build será disparado.

5. Na caixa **Linha de comando do evento de pós-build**, especifique a sintaxe do evento de build.

   > [!NOTE]
   > Adicione uma instrução `call` antes de todos os comandos pós-build que executam arquivos *.bat*. Por exemplo, `call C:\MyFile.bat` ou `call C:\MyFile.bat call C:\MyFile2.bat`.

6. Na caixa **Executar o evento de pós-build**, especifique em que condições o evento pós-build deve ser executado.

   > [!NOTE]
   > Para adicionar uma sintaxe demorada ou para selecionar qualquer macro de compilação na caixa de diálogo linha de comando do evento de [pré-compilação/pós-](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)compilação, clique no botão de reticências (**...**) para exibir uma caixa de edição.

   A sintaxe do evento de build pode incluir qualquer comando que seja válido em um prompt de comando ou em um arquivo *.bat*. O nome de um arquivo em lote deve ser precedido por `call` para garantir que todos os comandos posteriores sejam executados.

   > [!NOTE]
   > Se o evento de pré ou de pós-build não for concluído com êxito, você poderá encerrar o build fazendo a ação do evento terminar com um código diferente de zero (0), o que indica uma ação bem-sucedida.

## <a name="example"></a>Exemplo

O procedimento a seguir mostra como definir a versão mínima do sistema operacional no manifesto do aplicativo usando um comando *.exe* chamado de um evento de pós-build (o arquivo *.exe.manifest* no diretório do projeto). A versão mínima do sistema operacional é um número de quatro partes, como 4.10.0.0. Para definir a versão mínima do sistema operacional, o comando alterará a seção `<dependentOS>` do manifesto:

```xml
<dependentOS>
   <osVersionInfo>
      <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
   </osVersionInfo>
</dependentOS>
```

### <a name="create-an-exe-command-to-change-the-application-manifest"></a>Criar um comando .exe para alterar o manifesto do aplicativo

1. Crie um projeto de **Aplicativo de Console** para o comando. Dê ao projeto o nome **ChangeOSVersionCS**.

2. No *Program.cs*, adicione a seguinte linha às outras `using` diretivas na parte superior do arquivo:

   ```csharp
   using System.Xml;
   ```

3. No namespace `ChangeOSVersionCS`, substitua a implementação da classe `Program` pelo seguinte código:

   ```csharp
   class Program
   {
      /// <summary>
      /// This function sets the minimum operating system version for a ClickOnce application.
      /// </summary>
      /// <param name="args">
      /// Command Line Arguments:
      /// 0 - Path to application manifest (.exe.manifest)
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

4. Compile o projeto.

5. Copie o arquivo *.exe* para um diretório como *C:\TEMP\ChangeOSVersionVB.exe*.

Em seguida, invoque este comando em um evento de pós-build para modificar o manifesto do aplicativo.

### <a name="invoke-a-post-build-event-to-modify-the-application-manifest"></a>Invocar um evento de pós-build para modificar o manifesto do aplicativo

1. Crie um projeto de **Aplicativo do Windows Forms** e dê a ele o nome **CSWinApp**.

2. Com o projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, escolha **Propriedades**.

3. No **Designer de Projeto**, localize a página **Publicar** e defina o **Local de Publicação** como *C:\TEMP*.

4. Publique o projeto clicando em **Publicar Agora**.

   O arquivo de manifesto é compilado e salvo em *C:\TEMP\CSWinApp_1_0_0_0\CSWinApp.exe.manifest*. Para exibir o manifesto, clique com o botão direito do mouse no arquivo, clique em **Abrir com**, selecione **Selecionar um programa em uma lista de programas instalados** e clique em **Bloco de Notas**.

   Pesquise o elemento `<osVersionInfo>` no arquivo. Por exemplo, a versão pode ser:

   ```xml
   <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
   ```

5. De volta no **Designer de Projeto**, clique na guia **Eventos de Build** e depois em **Editar pós-build**.

6. Na caixa **Linha de Comando do Evento de Pós-Build**, digite o seguinte comando:

   `C:\TEMP\ChangeOSVersionCS.exe "$(TargetPath).manifest" 5.1.2600.0`

   Ao compilar o projeto, esse comando altera a versão mínima do sistema operacional no manifesto do aplicativo para 5.1.2600.0.

   Já que a macro `$(TargetPath)` expressa o caminho completo para o executável que está sendo criado, `$(TargetPath).manifest` especifica o manifesto do aplicativo criado no diretório *bin*. A publicação copia esse manifesto para o local de publicação definido anteriormente.

7. Publique o projeto novamente.

   A versão do manifesto agora deve ser:

   ```xml
   <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" />
   ```

## <a name="see-also"></a>Veja também

- [Página de eventos de compilação, designer de projeto (C#)](../ide/reference/build-events-page-project-designer-csharp.md)
- [Caixa de diálogo linha de comando de evento de pré-compilação/evento de pós-compilação](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
- [Como especificar eventos de compilação (Visual Basic)](../ide/how-to-specify-build-events-visual-basic.md)
- [Compilação e construção](../ide/compiling-and-building-in-visual-studio.md)
