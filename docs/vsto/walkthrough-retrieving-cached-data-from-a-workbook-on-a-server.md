---
title: 'Walkthrough: recuperar dados armazenados em cache de uma pasta de trabalho em um servidor'
description: Saiba como você pode recuperar dados de um DataSet que é armazenado em cache em uma pasta de trabalho do Microsoft Excel sem iniciar o Excel usando a classe ServerDocument.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks [Office development in Visual Studio], retrieving data
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e11099b0ea37856919affb927c3f118572d339af
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826861"
---
# <a name="walkthrough-retrieve-cached-data-from-a-workbook-on-a-server"></a>Walkthrough: recuperar dados armazenados em cache de uma pasta de trabalho em um servidor
  Este passo a passos demonstra como recuperar dados de um DataSet que é armazenado em cache em uma Microsoft Office pasta de trabalho do Excel sem iniciar o Excel usando a <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Definição de um DataSet que contém dados do *AdventureWorksLT* Database.

- Criando instâncias do conjunto de aplicativos em um projeto de pasta de trabalho do Excel e um projeto de aplicativo de console.

- Criar um <xref:Microsoft.Office.Tools.Excel.ListObject> que esteja associado ao conjunto de dados na pasta de trabalho e preenchendo-o <xref:Microsoft.Office.Tools.Excel.ListObject> com data quando a pasta de trabalho for aberta.

- Adicionar o conjunto de dados na pasta de trabalho ao cache de data.

- A leitura de dados do DataSet armazenado em cache para o DataSet no aplicativo de console, sem iniciar o Excel.

  Embora este passo a passos assuma que você esteja executando o código em seu computador de desenvolvimento, o código demonstrado por este passo a passos pode ser usado em um servidor que não tem o Excel instalado.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

- Acesso a uma instância em execução do Microsoft SQL Server ou Microsoft SQL Server Express que tem o banco de dados de exemplo AdventureWorksLT anexado a ele. Você pode baixar o banco de dados AdventureWorksLT do [site do CodePlex](https://archive.codeplex.com/?p=SqlServerSamples). Para obter mais informações sobre como anexar um banco de dados, consulte os seguintes tópicos:

  - Para anexar um banco de dados usando SQL Server Management Studio ou SQL Server Management Studio Express, consulte [como: anexar um banco de dados (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database).

  - Para anexar um banco de dados usando a linha de comando, consulte [como: anexar um arquivo de banco de dados a SQL Server Express](/previous-versions/sql/).

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>Criar um projeto de biblioteca de classes que define um conjunto de uma
 Para usar o mesmo conjunto de mesmos em um projeto de pasta de trabalho do Excel e um aplicativo de console, você deve definir o conjunto de aplicativos em um assembly separado que é referenciado por ambos os projetos. Para esta explicação, defina o DataSet em um projeto de biblioteca de classes.

### <a name="create-the-class-library-project"></a>Criar o projeto da biblioteca de classes

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

3. No painel modelos, expanda **Visual C#** ou **Visual Basic** e clique em **Windows**.

4. Na lista de modelos de projeto, selecione **biblioteca de classes**.

5. Na caixa **nome** , digite **AdventureWorksDataSet**.

6. Clique em **procurar**, navegue até a pasta *%USERPROFILE%\My documentos* (para o Windows XP e versões anteriores) ou *%UserProfile%\Documents* (para Windows Vista) e clique em **Selecionar pasta**.

7. Na caixa de diálogo **novo projeto** , verifique se a caixa de seleção **criar diretório para a solução** não está selecionada.

8. Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o projeto **AdventureWorksDataSet** para **Gerenciador de soluções** e abre o arquivo de código *Class1. cs* ou *Class1. vb* .

9. Em **Gerenciador de soluções**, clique com o botão direito do mouse em *Class1. cs* ou *Class1. vb* e clique em **excluir**. Você não precisa desse arquivo para este passo a passos.

## <a name="define-a-dataset-in-the-class-library-project"></a>Definir um conjunto de um DataSet no projeto de biblioteca de classes
 Defina um dataset tipado que contenha dados do AdventureWorksLT para SQL Server 2005. Mais adiante neste tutorial, você fará referência a esse conjunto de aplicativos de um projeto de pasta de trabalho do Excel e um projeto de aplicativo de console.

 O DataSet é um *dataset tipado* que representa os dados na tabela Product do banco de dados AdventureWorksLT. Para obter mais informações sobre conjuntos de dados tipados, consulte [ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md).

### <a name="define-a-typed-dataset-in-the-class-library-project"></a>Definir um dataset tipado no projeto de biblioteca de classes

1. Em **Gerenciador de soluções**, clique no projeto **AdventureWorksDataSet** .

2. Se a janela **fontes de dados** não estiver visível, exiba-a por, na barra de menus, escolhendo **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

3. Escolha **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

4. Clique em **banco de dados** e em **Avançar**.

5. Se você tiver uma conexão existente com o banco de dados AdventureWorksLT, escolha essa conexão e clique em **Avançar**.

    Caso contrário, clique em **nova conexão** e use a caixa de diálogo **Adicionar conexão** para criar a nova conexão. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

6. Na página **salvar a cadeia de conexão no arquivo de configuração do aplicativo** , clique em **Avançar**.

7. Na página **escolher seus objetos de banco de dados** , expanda **tabelas** e selecione **produto (tabela SalesLT)**.

8. Clique em **Concluir**.

    O arquivo *AdventureWorksLTDataSet. xsd* é adicionado ao projeto **AdventureWorksDataSet** . Esse arquivo define os seguintes itens:

   - Um dataset tipado chamado `AdventureWorksLTDataSet` . Esse DataSet representa o conteúdo da tabela Product no banco de dados AdventureWorksLT.

   - Um TableAdapter chamado `ProductTableAdapter` . Esse TableAdapter pode ser usado para ler e gravar dados no `AdventureWorksLTDataSet` . Para obter mais informações, consulte [visão geral do TableAdapter](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview).

     Você usará esses dois objetos posteriormente neste passo a passos.

9. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **AdventureWorksDataSet** e clique em **Compilar**.

     Verifique se o projeto é compilado sem erros.

## <a name="create-an-excel-workbook-project"></a>Criar um projeto de pasta de trabalho do Excel
 Crie um projeto de pasta de trabalho do Excel para a interface para os dados. Mais adiante neste tutorial, você criará um <xref:Microsoft.Office.Tools.Excel.ListObject> que exibe os dados e adicionará uma instância do conjunto de dados ao cache de data na pasta de trabalho.

### <a name="create-the-excel-workbook-project"></a>Criar o projeto de pasta de trabalho do Excel

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução **AdventureWorksDataSet** , aponte para **Adicionar** e clique em **novo projeto**.

2. No painel modelos, expanda **Visual C#** ou **Visual Basic** e, em seguida, expanda **Office/SharePoint**.

3. No nó do **Office/SharePoint** expandido, selecione o nó **suplementos do Office** .

4. Na lista de modelos de projeto, selecione a **pasta de trabalho do excel 2010** ou o projeto de **pasta de trabalho do Excel 2013** .

5. Na caixa **nome** , digite **AdventureWorksReport**. Não modifique o local.

6. Clique em **OK**.

     O **Assistente de ferramentas do Visual Studio para o Office Project** é aberto.

7. Verifique se **a seleção criar um novo documento** está selecionada e clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre a pasta de trabalho **AdventureWorksReport** no designer e adiciona o projeto **AdventureWorksReport** ao **Gerenciador de soluções**.

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>Adicionar o conjunto de dados a fontes de dado no projeto de pasta de trabalho do Excel
 Antes de exibir o conjunto de dados na pasta de trabalho do Excel, você deve primeiro adicionar o conjunto de dados a fontes de dado no projeto de pasta de trabalho do Excel.

1. Em **Gerenciador de soluções**, clique duas vezes em *Plan1. cs* ou *Plan1. vb* no projeto **AdventureWorksReport** .

     A pasta de trabalho é aberta no designer.

2. No menu **Dados**, clique em **Adicionar Nova Fonte de Dados**.

     O **Assistente de configuração de fonte de dados** é aberto.

3. Clique em **objeto** e, em seguida, clique em **Avançar**.

4. Na página **Selecione o objeto que você deseja associar** a, clique em **Adicionar referência**.

5. Na guia **projetos** , clique em **AdventureWorksDataSet** e em **OK**.

6. No namespace **AdventureWorksDataSet** do assembly **AdventureWorksDataSet** , clique em **AdventureWorksLTDataSet** e em **concluir**.

     A janela **fontes de dados** é aberta e **AdventureWorksLTDataSet** é adicionado à lista de fontes de dados.

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>Criar um ListObject que esteja associado a uma instância do conjunto de um
 Para exibir o conjunto de uma pasta de trabalho, crie um <xref:Microsoft.Office.Tools.Excel.ListObject> que esteja associado a uma instância do conjunto de um. Para obter mais informações sobre como ligar controles a dados, consulte [associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

1. Na janela **fontes de dados** , expanda o nó **AdventureWorksLTDataSet** em **AdventureWorksDataSet**.

2. Selecione o nó **produto** , clique na seta suspensa que aparece e selecione **ListObject** na lista suspensa.

     Se a seta suspensa não for exibida, confirme se a pasta de trabalho está aberta no designer.

3. Arraste a tabela **Product** para a célula a1.

     Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `productListObject` é criado na planilha, começando na célula a1. Ao mesmo tempo, um objeto DataSet chamado `adventureWorksLTDataSet` e um <xref:System.Windows.Forms.BindingSource> nomeado `productBindingSource` são adicionados ao projeto. O <xref:Microsoft.Office.Tools.Excel.ListObject> é associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, é associado ao objeto DataSet.

## <a name="add-the-dataset-to-the-data-cache"></a>Adicionar o DataSet ao cache de dados
 Para habilitar o código fora do projeto de pasta de trabalho do Excel para acessar o conjunto de dados na pasta de trabalho, você deve adicionar o DataSet ao cache de data. Para obter mais informações sobre o cache de dados, consulte [dados armazenados em cache em personalizações em nível de documento](../vsto/cached-data-in-document-level-customizations.md) e [dados de cache](../vsto/caching-data.md).

1. No designer, clique em **AdventureWorksLTDataSet**.

2. Na janela **Propriedades** , defina a propriedade **modificadores** como **público**.

3. Defina a propriedade **CacheInDocument** como **true**.

## <a name="initialize-the-dataset-in-the-workbook"></a>Inicializar o conjunto de os na pasta de trabalho
 Antes de poder recuperar os dados do DataSet armazenado em cache usando o aplicativo de console, você deve primeiro preencher o conjunto de dados armazenado em cache com data.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo *Plan1. cs* ou *Plan1. vb* e clique em **Exibir código**.

2. Substitua o `Sheet1_Startup` manipulador de eventos pelo código a seguir. Esse código usa uma instância da `ProductTableAdapter` classe que é definida no projeto **AdventureWorksDataSet** para preencher o conjunto de dados armazenado em cache com data, se estiver vazio no momento.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/AdventureWorksReport/Sheet1.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/AdventureWorksReport/Sheet1.vb" id="Snippet8":::

## <a name="checkpoint"></a>Ponto de verificação
 Crie e execute o projeto de pasta de trabalho do Excel para garantir que ele seja compilado e executado sem erros. Essa operação também preenche o conjunto de dados armazenado em cache e salva o dado na pasta de trabalho.

### <a name="build-and-run-the-project"></a>Compilar e executar o projeto

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **AdventureWorksReport** , escolha **depurar** e, em seguida, clique em **Iniciar nova instância**.

     O projeto é criado e a pasta de trabalho é aberta no Excel. Verifique o seguinte:

    - Os <xref:Microsoft.Office.Tools.Excel.ListObject> preenchimentos com dados.

    - O valor na coluna **ListPrice** para a primeira linha de <xref:Microsoft.Office.Tools.Excel.ListObject> é 1431,5. Mais adiante neste tutorial, você usará um aplicativo de console para modificar os valores na coluna **ListPrice** .

2. Salve a pasta de trabalho. Não modifique o nome do arquivo ou o local da pasta de trabalho.

3. Feche o Excel.

## <a name="create-a-console-application-project"></a>Criar um projeto de aplicativo de console
 Crie um projeto de aplicativo de console a ser usado para modificar os dados no DataSet armazenado em cache na pasta de trabalho.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução **AdventureWorksDataSet** , aponte para **Adicionar** e clique em **novo projeto**.

2. No painel **tipos de projeto** , expanda **Visual C#** ou **Visual Basic** e clique em **Windows**.

3. No painel **Modelos**, selecione **Aplicativo de Console**.

4. Na caixa **nome** , digite **DataReader**. Não modifique o local.

5. Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o projeto **DataReader** a **Gerenciador de soluções** e abre o arquivo de código *Program. cs* ou *Module1. vb* .

## <a name="retrieve-data-from-the-cached-dataset-by-using-the-console-application"></a>Recuperar dados do conjunto de dados armazenado em cache usando o aplicativo de console
 Use a <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe no aplicativo de console para ler os dados em um `AdventureWorksLTDataSet` objeto local. Para confirmar que o conjunto de dados local foi inicializado com os data do DataSet armazenado em cache, o aplicativo exibirá o número de linhas no DataSet local.

### <a name="retrieve-data-from-the-cached-dataset"></a>Recuperar dados do conjunto de dado armazenado em cache

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **DataReader** e clique em **Adicionar referência**.

2. Na guia **.net** , selecione **Microsoft. VisualStudio. Tools. Applications. ServerDocument**.

3. Clique em **OK**.

4. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **DataReader** e clique em **Adicionar referência**.

5. Na guia **projetos** , selecione **AdventureWorksDataSet** e clique em **OK**.

6. Abra o arquivo *Program. cs* ou *Module1. vb* no editor de código.

7. Adicione a instrução **using** (for C#) ou **Imports** (for Visual Basic) a seguir na parte superior do arquivo de código.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet1":::

8. Adicione o seguinte código ao `Main` método. Esse código declara os seguintes objetos:

   - Uma instância do `AdventureWorksLTDataSet` tipo que é definido no projeto **AdventureWorksDataSet** .

   - O caminho para a pasta de trabalho AdventureWorksReport no diretório de compilação do projeto **AdventureWorksReport** .

   - Um <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> objeto a ser usado para acessar o cache de dados na pasta de trabalho.

     > [!NOTE]
     > O código a seguir pressupõe que a pasta de trabalho seja salva usando a extensão *. xlsx* . Se a pasta de trabalho em seu projeto tiver uma extensão diferente, modifique o caminho conforme necessário.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet10":::

9. Adicione o código a seguir ao `Main` método, após o código que você adicionou na etapa anterior. Esse código executa as seguintes tarefas:

   - Ele usa a <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> propriedade da <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe para acessar o conjunto de armazenamento em cache na pasta de trabalho.

   - Ele lê os dados do DataSet armazenado em cache para o conjunto de dados local.

   - Ele exibe o número de linhas no conjunto de dados local, para confirmar que ela contém os mesmos.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb" id="Snippet11":::

10. No menu **Compilar** , clique em **criar DataReader**.

## <a name="test-the-project"></a>Testar o projeto
 Quando você executa o aplicativo de console, ele exibe o número de linhas no conjunto de registros local.

### <a name="test-the-workbook"></a>Testar a pasta de trabalho

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **DataReader** , aponte para **depurar** e clique em **Iniciar nova instância**.

     Verifique se o aplicativo relata que o conjunto de registros local tem 295 linhas.

2. Pressione **Enter** para fechar o aplicativo.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como trabalhar com dados armazenados em cache a partir destes tópicos:

- Alterar os dados em um conjunto de dado armazenado em cache sem iniciar o Excel. Para obter mais informações, consulte [Walkthrough: alterar dados em cache em uma pasta de trabalho em um servidor](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md).

## <a name="see-also"></a>Consulte também

- [Walkthrough: inserir dados em uma pasta de trabalho em um servidor](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)
- [Walkthrough: alterar os dados armazenados em cache em uma pasta de trabalho em um servidor](../vsto/walkthrough-changing-cached-data-in-a-workbook-on-a-server.md)
