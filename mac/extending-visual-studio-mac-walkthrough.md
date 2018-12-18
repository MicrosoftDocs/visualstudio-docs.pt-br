---
title: 'Passo a passo: estendendo o Visual Studio para Mac'
author: conceptdev
ms.author: crdun
ms.date: 04/14/2017
ms.technology: vs-ide-sdk
ms.assetid: 7D00512B-9688-4D8D-87A7-F04F207E3D02
ms.openlocfilehash: cbf0d99bd87b31484b6c74e9a6d67ac88dc5ba99
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51294299"
---
# <a name="extending-visual-studio-for-mac-walkthrough"></a>Passo a passo: estendendo o Visual Studio para Mac

Este tópico guiará você pela compilação de [um pacote de extensão simples](https://github.com/mjh4/AddIns/tree/master/DateInserter). O pacote de extensão criará um novo Comando no menu Editar do Visual Studio para Mac que permite ao usuário inserir a data e a hora atuais em um documento open text.

Este exemplo usa o Criador de Suplementos. O Criador de Suplementos cria um novo modelo de Projeto e o popula com os arquivos necessários para o nosso pacote de extensão personalizado.

1. Começar iniciando o Visual Studio para Mac, se ele ainda não estiver aberto:

   ![Captura de tela do Visual Studio para Mac](media/extending-visual-studio-mac-addin3.png)

2. Instale o _Pacote de extensão do Criador de Suplementos_ usando o Gerenciador de Extensões. No menu do Visual Studio, escolha **Extensões...**:

   ![Guia de Gerenciador de Suplementos](media/extending-visual-studio-mac-addin4.png)

3. Navegue para a guia Galeria e digite `Addin Maker` na barra de pesquisa no canto superior direito. Selecione o Criador de Suplementos na categoria Desenvolvimento de Suplementos e clique em <kbd>Instalar</kbd>. Se nada aparecer, clique em Atualizar e pesquisar novamente:

   ![Gerenciador de Suplementos](media/extending-visual-studio-mac-addin5.png)

4. Agora que o Criador de Suplementos está instalado, você poderá começar a criar um pacote de extensão. Comece criando uma nova solução.

5. Na **caixa de diálogo Nova Solução**, escolha o modelo **Outros > Diversos > Geral > Suplemento do Xamarin Studio > C#** e, na tela seguinte, escolha um nome para a nova solução `DateInserter`:

   ![Criando uma nova solução](media/extending-visual-studio-mac-addin7New.png)

6. O Visual Studio para Mac populará uma nova Solução:

   ![Solução populada](media/extending-visual-studio-mac-addin8.png)

7. Remova todo o código de modelo em `Manifest.addin.xml` substitua-o pelo código a seguir:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
      <ExtensionModel>
          <Extension path = "/MonoDevelop/Ide/Commands/Edit">
              <Command id = "DateInserter.DateInserterCommands.InsertDate"
                  _label = "Insert Date"
                  defaultHandler = "DateInserter.InsertDateHandler" />
          </Extension>

          <Extension path = "/MonoDevelop/Ide/MainMenu/Edit">
              <CommandItem id="DateInserter.DateInserterCommands.InsertDate" />
          </Extension>
      </ExtensionModel>
   ```

8. Agora você precisa configurar os arquivos que eventualmente tratarão a inserção de data e hora no editor de texto. Clique com botão direito do mouse no nó do projeto e adicione um novo arquivo. Selecione **Geral > Classe Vazia** e nomeie o novo arquivo *InsertDateHandler*:

   ![Inserir o manipulador de datas](media/extending-visual-studio-mac-addin9.png)

9. Remova todo o código de modelo de `InsertDateHandler.cs` e substitua-o pelo código a seguir:

   ```cs
   using MonoDevelop.Components.Commands;
   using MonoDevelop.Ide;
   using MonoDevelop.Ide.Gui;
   using System;

   namespace DateInserter
   {
      class InsertDateHandler : CommandHandler
      {
          protected override void Run()
          {

          }

          protected override void Update(CommandInfo info)
          {

          }
      }
   }
   ```

   Expandiremos esses dois métodos de espaço reservado mais tarde.

10. Clique com o botão direito do mouse no Projeto **DateInserter** e selecione **Adicionar > Novo Arquivo**. Selecione **Geral > Enumeração Vazia** e nomeie o novo arquivo como *DateInserterCommands*:

    ![DateInserterCommands](media/extending-visual-studio-mac-addin10.png)

11. Adicione o comando `InsertDate` como uma nova enumeração no arquivo `DateInserterCommands.cs`:

    ``` cs
    using System;

    namespace DateInserter
    {
      public enum DateInserterCommands
      {
          InsertDate,
      }
    }
    ```

12. Neste ponto, você deve ter um pacote de extensão em funcionamento. Você pode testá-lo salvando seu trabalho e executando o aplicativo. O IDE iniciará uma nova instância do Visual Studio para Mac com o novo pacote de extensão instalado. Se você navegar para o **menu Editar**, verá que o Visual Studio para Mac tem uma nova opção chamada **Inserir Dados**, conforme ilustrado na captura de tela abaixo:

    ![Comando Inserir Data](media/extending-visual-studio-mac-addin11.png)

    Observe que selecionar Inserir Data no menu não surte efeito porque a implementação atual só tem métodos de espaço reservado.

13. A estrutura está em vigor para o pacote de extensão e é hora de escrever o código que habilita a inserção da data. Primeiro, verifique se o **comando Inserir Data** está habilitado apenas quando o usuário tiver arquivo de texto aberto substituindo o método `Update` em `InsertDateHandler.cs` pelo código a seguir:

    ```cs
    protected override void Update(CommandInfo info)
    {
      info.Enabled = IdeApp.Workbench.ActiveDocument?.Editor != null;
    }
    ```

14. Atualize o método `Run` do comando para inserir a data e a hora com o código a seguir:

    ``` cs
    protected override void Run () {
      var editor = IdeApp.Workbench.ActiveDocument.Editor;
      var date = DateTime.Now.ToString ();
      editor.InsertAtCaret (date);

    }
    ```

15. Por fim, vamos executar nosso pacote de extensão para testá-lo. Na nova instância do Visual Studio para Mac, selecione **Editar > Inserir Data**. A data e hora atual é inserida em nosso cursor, conforme ilustrado na captura de tela abaixo:

    ![Inserir captura de tela de data](media/extending-visual-studio-mac-addin12.png)

## <a name="see-also"></a>Consulte também

- [Criar sua primeira extensão (Visual Studio no Windows)](/visualstudio/extensibility/extensibility-hello-world)