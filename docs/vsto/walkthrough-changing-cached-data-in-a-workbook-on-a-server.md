---
title: 'Passo a passo: Alterar os dados armazenados em cache em uma pasta de trabalho em um servidor'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks [Office development in Visual Studio], changing server data
- datasets [Office development in Visual Studio], accessing on server
- server-side data access [Office development in Visual Studio]
- data [Office development in Visual Studio], accessing on server
- documents [Office development in Visual Studio], server-side data access
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f9f2ac3873bf59b30f8efa3e45d6cbdd0aebd4f6
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672854"
---
# <a name="walkthrough-change-cached-data-in-a-workbook-on-a-server"></a>Passo a passo: Alterar os dados armazenados em cache em uma pasta de trabalho em um servidor
  Este passo a passo demonstra como modificar um conjunto de dados é armazenado em cache em uma pasta de trabalho do Microsoft Office Excel sem iniciar o Excel usando o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Esta explicação passo a passo ilustra as seguintes tarefas:

- Definindo um conjunto de dados que contém os dados do banco de dados AdventureWorksLT.

- Criação de instâncias do conjunto de dados em um projeto de pasta de trabalho do Excel e um projeto de aplicativo de console.

- Criando um <xref:Microsoft.Office.Tools.Excel.ListObject> que é associada ao conjunto de dados na pasta de trabalho e preencher o <xref:Microsoft.Office.Tools.Excel.ListObject> com os dados quando a pasta de trabalho é aberta.

- Adicionando o conjunto de dados na pasta de trabalho para o cache de dados.

- Modificando uma coluna de dados no conjunto de dados armazenados em cache, executando código no aplicativo de console, sem iniciar o Excel.

  Embora este passo a passo pressupõe que você está executando o código no computador de desenvolvimento, o código demonstrado por este passo a passo pode ser usado em um servidor que não tenha o Excel instalado.

> [!NOTE]
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

-   [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

-   Acesso a uma instância em execução do Microsoft SQL Server ou Microsoft SQL Server Express que tem o banco de dados de exemplo AdventureWorksLT anexado a ele. Você pode baixar o banco de dados AdventureWorksLT a [site da CodePlex](http://go.microsoft.com/fwlink/?linkid=87843). Para obter mais informações sobre como anexar um banco de dados, consulte os tópicos a seguir:

    -   Para anexar um banco de dados usando o SQL Server Management Studio ou o SQL Server Management Studio Express, consulte [como: anexar um banco de dados (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database).

    -   Para anexar um banco de dados usando a linha de comando, consulte [como: anexar um arquivo de banco de dados para o SQL Server Express](/previous-versions/sql/).

## <a name="create-a-class-library-project-that-defines-a-dataset"></a>Criar um projeto de biblioteca de classe que define um conjunto de dados
 Para usar o mesmo conjunto de dados em um projeto de pasta de trabalho do Excel e um aplicativo de console, você deve definir o conjunto de dados em um assembly separado que é referenciado por ambos esses projetos. Para este passo a passo, defina o conjunto de dados em um projeto de biblioteca de classe.

### <a name="to-create-the-class-library-project"></a>Para criar o projeto de biblioteca de classe

1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.

3.  No painel de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, clique em **Windows**.

4.  Na lista de modelos de projeto, selecione **biblioteca de classes**.

5.  No **nome** , digite **AdventureWorksDataSet**.

6.  Clique em **navegue**, navegue até seu *documentos %UserProfile%\My* (para o Windows XP e versões anteriores) ou *%UserProfile%\Documents* (para Windows Vista) pasta e clique **Selecionar pasta**.

7.  No **novo projeto** diálogo caixa, certifique-se de que o **criar diretório para solução** caixa de seleção não estiver selecionada.

8.  Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **AdventureWorksDataSet** projeto ao **Gerenciador de soluções** e abre o **Class1.cs** ou **Class1.vb** arquivo de código.

9. Na **Gerenciador de soluções**, clique com botão direito **Class1.cs** ou **Class1.vb**e, em seguida, clique em **excluir**. Esse arquivo não será necessário para este passo a passo.

## <a name="define-a-dataset-in-the-class-library-project"></a>Definir um conjunto de dados no projeto de biblioteca de classes
 Defina um dataset tipado que contém os dados do banco de dados AdventureWorksLT para SQL Server 2005. Posteriormente neste passo a passo, você fará referência a esse conjunto de dados de um projeto de pasta de trabalho do Excel e um projeto de aplicativo de console.

 O conjunto de dados é um *conjunto de dados digitados* que representa os dados na tabela de produto do banco de dados AdventureWorksLT. Para obter mais informações sobre conjuntos de dados tipados, consulte [ferramentas de conjunto de dados no Visual Studio](/visualstudio/data-tools/dataset-tools-in-visual-studio).

### <a name="to-define-a-typed-dataset-in-the-class-library-project"></a>Para definir um conjunto de dados tipado no projeto de biblioteca de classes

1. Na **Gerenciador de soluções**, clique no **AdventureWorksDataSet** projeto.

2. Se o **fontes de dados** janela não estiver visível, exibi-lo, na barra de menus, escolhendo **exibição** > **Other Windows**  >   **Fontes de dados**.

3. Escolher **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.

4. Clique em **banco de dados**e, em seguida, clique em **próxima**.

5. Se você tiver uma conexão existente no banco de dados AdventureWorksLT, escolha essa conexão e clique em **próxima**.

    Caso contrário, clique em **nova Conexão**e usar o **Adicionar Conexão** caixa de diálogo para criar a nova conexão. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

6. No **salvar a cadeia de Conexão no arquivo de configuração de aplicativo** , clique em **próxima**.

7. No **Choose Your Database Objects** página, expanda **tabelas** e selecione **produto (SalesLT)**.

8. Clique em **Finalizar**.

    O *Adventureworksltdataset* arquivo é adicionado para o **AdventureWorksDataSet** projeto. Esse arquivo define os seguintes itens:

   - Um dataset tipado chamado `AdventureWorksLTDataSet`. Esse conjunto de dados representa o conteúdo da tabela Produtos no banco de dados AdventureWorksLT.

   - Um TableAdapter nomeado `ProductTableAdapter`. Este TableAdapter pode ser usado para ler e gravar dados no `AdventureWorksLTDataSet`. Para obter mais informações, consulte [visão geral de TableAdapter](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview).

     Você usará dois desses objetos posteriormente neste passo a passo.

9. Na **Gerenciador de soluções**, clique com botão direito **AdventureWorksDataSet** e clique em **Build**.

     Verifique se o projeto é compilado sem erros.

## <a name="create-an-excel-workbook-project"></a>Criar um projeto de pasta de trabalho do Excel
 Crie um projeto de pasta de trabalho do Excel para a interface para os dados. Posteriormente neste passo a passo, você criará um <xref:Microsoft.Office.Tools.Excel.ListObject> que exibe os dados, e você irá adicionar uma instância do conjunto de dados para o cache de dados na pasta de trabalho.

### <a name="to-create-the-excel-workbook-project"></a>Para criar o projeto de pasta de trabalho do Excel

1.  No **Gerenciador de soluções**, clique com botão direito do **AdventureWorksDataSet** solução, aponte para **adicionar**e, em seguida, clique em **novo projeto**.

2.  No painel de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, expanda **Office**.

3.  Sob o expandida **Office** nó, selecione o **2010** nó.

4.  Na lista de modelos de projeto, selecione o projeto de pasta de trabalho do Excel.

5.  No **nome** , digite **AdventureWorksReport**. Não modifique o local.

6.  Clique em **OK**.

     O **Visual Studio Tools for Office Project Wizard** é aberta.

7.  Certifique-se de que **criar um novo documento** está selecionado e, em seguida, clique em **Okey**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o **AdventureWorksReport** pasta de trabalho no designer e adiciona os **AdventureWorksReport** projeto ao **Gerenciador de soluções**.

## <a name="add-the-dataset-to-data-sources-in-the-excel-workbook-project"></a>Adicionar o conjunto de dados a fontes de dados no projeto de pasta de trabalho do Excel
 Para poder exibir o conjunto de dados na pasta de trabalho do Excel, você deve primeiro adicionar o conjunto de dados a fontes de dados no projeto de pasta de trabalho do Excel.

### <a name="to-add-the-dataset-to-the-data-sources-in-the-excel-workbook-project"></a>Para adicionar o conjunto de dados para as fontes de dados no projeto de pasta de trabalho do Excel

1.  Na **Gerenciador de soluções**, clique duas vezes em **Sheet1.cs** ou **Sheet1.vb** sob o **AdventureWorksReport** projeto.

     A pasta de trabalho é aberto no designer.

2.  Sobre o **dados** menu, clique em **Add New Data Source**.

     O **Data Source Configuration Wizard** é aberta.

3.  Clique em **objeto**e, em seguida, clique em **próxima**.

4.  No **selecionar o objeto que deseja vincular aos** , clique em **adicionar referência**.

5.  Sobre o **projetos** , clique em **AdventureWorksDataSet** e, em seguida, clique em **Okey**.

6.  Sob o **AdventureWorksDataSet** namespace do **AdventureWorksDataSet** assembly, clique em **AdventureWorksLTDataSet** e, em seguida, clique em **concluir** .

     O **fontes de dados** janela é aberta, e **AdventureWorksLTDataSet** é adicionado à lista de fontes de dados.

## <a name="create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>Criar um ListObject que está associado a uma instância do conjunto de dados
 Para exibir o conjunto de dados na pasta de trabalho, crie um <xref:Microsoft.Office.Tools.Excel.ListObject> que está associado a uma instância do conjunto de dados. Para obter mais informações sobre controles de vinculação de dados, consulte [ligar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

### <a name="to-create-a-listobject-that-is-bound-to-an-instance-of-the-dataset"></a>Para criar um ListObject que está associado a uma instância do conjunto de dados

1.  No **fontes de dados** janela, expanda o **AdventureWorksLTDataSet** nó sob **AdventureWorksDataSet**.

2.  Selecione o **produto** nó, clique na seta suspensa que aparece e, em seguida, selecione **ListObject** na lista suspensa.

     Se a seta suspensa não aparecer, confirme se a pasta de trabalho é aberta no designer.

3.  Arraste o **produto** tabela para a célula A1.

     Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `productListObject` é criado na planilha, começando na célula A1. Ao mesmo tempo, um objeto de conjunto de dados chamado `adventureWorksLTDataSet` e uma <xref:System.Windows.Forms.BindingSource> denominado `productBindingSource` são adicionados ao projeto. O <xref:Microsoft.Office.Tools.Excel.ListObject> está associado a <xref:System.Windows.Forms.BindingSource>, que por sua vez é associado ao objeto de conjunto de dados.

## <a name="add-the-dataset-to-the-data-cache"></a>Adicionar o conjunto de dados para o cache de dados
 Para habilitar o código fora do projeto de pasta de trabalho do Excel para acessar o conjunto de dados na pasta de trabalho, você deve adicionar o conjunto de dados para o cache de dados. Para obter mais informações sobre o cache de dados, consulte [armazenado em cache dados personalizações no nível do documento](../vsto/cached-data-in-document-level-customizations.md) e [armazena em Cache dados](../vsto/caching-data.md).

### <a name="to-add-the-dataset-to-the-data-cache"></a>Para adicionar o conjunto de dados para o cache de dados

1.  No designer, clique em **adventureWorksLTDataSet**.

2.  No **propriedades** janela, defina as **modificadores** propriedade a ser **público**.

3.  Defina a **CacheInDocument** propriedade **verdadeiro**.

## <a name="initialize-the-dataset-in-the-workbook"></a>Inicializar o conjunto de dados na pasta de trabalho
 Antes de você pode recuperar os dados do conjunto de dados em cache usando o aplicativo de console, você deve primeiro preencher o conjunto de dados armazenados em cache com os dados.

### <a name="to-initialize-the-dataset-in-the-workbook"></a>Para inicializar o conjunto de dados na pasta de trabalho

1.  No **Gerenciador de soluções**, clique com botão direito do **Sheet1.cs** ou **Sheet1.vb** de arquivo e clique em **Exibir código**.

2.  Substitua o `Sheet1_Startup` manipulador de eventos com o código a seguir. Esse código usa uma instância das `ProductTableAdapter` classe que é definida na **AdventureWorksDataSet** projeto para preencher o conjunto de dados armazenados em cache com dados, se ele está vazio no momento.

     [!code-csharp[Trin_CachedDataWalkthroughs#8](../vsto/codesnippet/CSharp/AdventureWorksDataSet/AdventureWorksReport/Sheet1.cs#8)]
     [!code-vb[Trin_CachedDataWalkthroughs#8](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/AdventureWorksReport/Sheet1.vb#8)]

## <a name="checkpoint"></a>Ponto de verificação
 Compile e execute o projeto de pasta de trabalho do Excel para garantir que ele é compilado e executado sem erros. Essa operação também preenche o conjunto de dados armazenados em cache e salva os dados na pasta de trabalho.

### <a name="to-build-and-run-the-project"></a>Para compilar e executar o projeto

1.  No **Gerenciador de soluções**, clique com botão direito do **AdventureWorksReport** do projeto, escolha **depurar**e, em seguida, clique em **iniciar nova instância**.

     O projeto é compilado, e a pasta de trabalho é aberta no Excel. Verifique o seguinte:

    -   O <xref:Microsoft.Office.Tools.Excel.ListObject> preenche com dados.

    -   O valor na **ListPrice** coluna para a primeira linha do <xref:Microsoft.Office.Tools.Excel.ListObject> é 1431.5. Posteriormente neste passo a passo, você usará um aplicativo de console para modificar os valores de **ListPrice** coluna.

2.  Salve a pasta de trabalho. Não modifique o nome do arquivo ou o local da pasta de trabalho.

3.  Feche o Excel.

## <a name="create-a-console-application-project"></a>Crie um projeto de aplicativo de console
 Crie um projeto de aplicativo de console para usar para modificar dados no conjunto de dados armazenados em cache na pasta de trabalho.

### <a name="to-create-the-console-application-project"></a>Para criar o projeto de aplicativo de console

1.  No **Gerenciador de soluções**, clique com botão direito do **AdventureWorksDataSet** solução, aponte para **adicionar**e, em seguida, clique em **novo projeto**.

2.  No **tipos de projeto** painel, expanda **Visual c#** ou **Visual Basic**e, em seguida, clique em **Windows**.

3.  No **modelos** painel, selecione **aplicativo de Console**.

4.  No **nome** , digite **DataWriter**. Não modifique o local.

5.  Clique em **OK**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **DataWriter** projeto ao **Gerenciador de soluções** e abre o **Program.cs** ou **Module1.vb** arquivo de código.

## <a name="change-data-in-the-cached-dataset-by-using-the-console-application"></a>Alterar dados no conjunto de dados em cache usando o aplicativo de console
 Use o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe no aplicativo de console para ler os dados em um local `AdventureWorksLTDataSet` do objeto, modificar esses dados e, em seguida, salvá-lo novamente o conjunto de dados armazenados em cache.

### <a name="to-change-data-in-the-cached-dataset"></a>Para alterar dados no conjunto de dados armazenados em cache

1. No **Gerenciador de soluções**, clique com botão direito do **DataWriter** do projeto e clique em **adicionar referência**.

2. Sobre o **.NET** guia, selecione **Microsoft.VisualStudio.Tools.Applications**.

3. Clique em **OK**.

4. No **Gerenciador de soluções**, clique com botão direito do **DataWriter** do projeto e clique em **adicionar referência**.

5. Sobre o **projetos** guia, selecione **AdventureWorksDataSet**e clique em **Okey**.

6. Abra o *Program.cs* ou *Module1.vb* arquivo no Editor de códigos.

7. Adicione o seguinte **usando** (para c#) ou **Imports** (para Visual Basic) à parte superior do arquivo de código.

    [!code-csharp[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#1)]
    [!code-vb[Trin_CachedDataWalkthroughs#1](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#1)]

8. Adicione o seguinte código ao método de `Main` . Esse código declara os seguintes objetos:

   - Uma instância das `AdventureWorksLTDataSet` tipo que é definido na **AdventureWorksDataSet** projeto.

   - O caminho para a pasta de trabalho na pasta de compilação de AdventureWorksReport a **AdventureWorksReport** projeto.

   - Um <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> objeto a ser usado para acessar o cache de dados na pasta de trabalho.

     > [!NOTE]
     >  O código a seguir pressupõe que você está usando uma pasta de trabalho que tem o *. xlsx* extensão de arquivo. Se a pasta de trabalho em seu projeto tem uma extensão de arquivo diferente, modifique o caminho conforme necessário.

     [!code-csharp[Trin_CachedDataWalkthroughs#6](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#6)]
     [!code-vb[Trin_CachedDataWalkthroughs#6](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#6)]

9. Adicione o seguinte código para o `Main` método após o código que você adicionou na etapa anterior. Esse código executa as seguintes tarefas:

   - Ele usa o <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> propriedade do <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> classe para acessar o conjunto de dados armazenados em cache na pasta de trabalho.

   - Ele lê os dados do conjunto de dados armazenados em cache no conjunto de dados local.

   - Ele altera o `ListPrice` valor de cada produto na tabela de produto do conjunto de dados.

   - Ele salva as alterações ao conjunto de dados armazenados em cache na pasta de trabalho.

     [!code-csharp[Trin_CachedDataWalkthroughs#7](../vsto/codesnippet/CSharp/AdventureWorksDataSet/DataWriter/Program.cs#7)]
     [!code-vb[Trin_CachedDataWalkthroughs#7](../vsto/codesnippet/VisualBasic/AdventureWorksDataSet/DataWriter/Module1.vb#7)]

10. No **Gerenciador de soluções**, clique com botão direito do **DataWriter** do projeto, aponte para **depurar**e, em seguida, clique em **iniciar nova instância**.

     O aplicativo de console exibe mensagens enquanto ele lê o conjunto de dados armazenados em cache para o conjunto de dados local, modifica os preços dos produtos no conjunto de dados local e salva os novos valores ao conjunto de dados armazenados em cache. Pressione **Enter** para fechar o aplicativo.

## <a name="test-the-workbook"></a>A pasta de trabalho de teste
 Quando você abre a pasta de trabalho, o <xref:Microsoft.Office.Tools.Excel.ListObject> agora exibe as alterações feitas a `ListPrice` coluna de dados no conjunto de dados armazenados em cache.

### <a name="to-test-the-workbook"></a>Para testar a pasta de trabalho

1.  Feche a pasta de trabalho AdventureWorksReport no designer do Visual Studio, se ele ainda estiver aberto.

2.  Abra a pasta de trabalho AdventureWorksReport que está na pasta de compilação do **AdventureWorksReport** projeto. Por padrão, a pasta de compilação está em um dos seguintes locais:

    -   *%USERPROFILE%\My Documents\AdventureWorksReport\bin\Debug* (para o Windows XP e versões anteriores)

    -   *%USERPROFILE%\Documents\AdventureWorksReport\bin\Debug* (para Windows Vista)

3.  Verificar se o valor na **ListPrice** coluna para a primeira linha do <xref:Microsoft.Office.Tools.Excel.ListObject> agora é 1574.65.

4.  Feche a pasta de trabalho.

## <a name="see-also"></a>Consulte também

- [Passo a passo: Inserir dados em uma pasta de trabalho em um servidor](../vsto/walkthrough-inserting-data-into-a-workbook-on-a-server.md)