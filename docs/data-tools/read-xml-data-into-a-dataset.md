---
title: Ler dados XML em um conjunto de dados
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- reading XML
- data access [Visual Studio], XML data
- reading files, XML
- data [Visual Studio], reading from XML files
- reading data, XML files
- XML [Visual Studio], reading
- XML documents, reading
- datasets [Visual Basic], reading XML data
ms.assetid: fae72958-0893-47d6-b3dd-9d42418418e4
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 1e43d118a5fcfe00a8eb6eaa7f34a17ff1f6a4be
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389209"
---
# <a name="read-xml-data-into-a-dataset"></a>Ler dados XML em um conjunto de dados

O ADO.NET fornece métodos simples para trabalhar com dados XML. Neste passo a passo, você deve criar um aplicativo do Windows que carrega dados XML em um conjunto de dados. O conjunto de dados é exibido em um <xref:System.Windows.Forms.DataGridView> controle. Por fim, um esquema XML com base no conteúdo do arquivo XML é exibido em uma caixa de texto.

## <a name="create-a-new-project"></a>Criar um novo projeto

Nesta etapa, você cria um projeto do Visual Basic ou Visual c#.

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **ReadingXML**e, em seguida, escolha **Okey**.

   O **ReadingXML** projeto é criado e adicionado ao **Gerenciador de soluções**.

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>Gerar o arquivo XML a ser lido para o conjunto de dados

Porque este passo a passo se concentra na leitura de dados XML em um conjunto de dados, o conteúdo de um arquivo XML é fornecido.

1. No menu **Projeto**, selecione **Adicionar Novo Item**.

2. Selecione **arquivo XML**, nomeie o arquivo **Authors**e, em seguida, selecione **adicionar**.

   O arquivo XML carrega no designer e está pronto para edição.

3. Cole os seguintes dados XML no editor abaixo da declaração XML:

   ```xml
   <Authors_Table>
     <authors>
       <au_id>172-32-1176</au_id>
       <au_lname>White</au_lname>
       <au_fname>Johnson</au_fname>
       <phone>408 496-7223</phone>
       <address>10932 Bigge Rd.</address>
       <city>Menlo Park</city>
       <state>CA</state>
       <zip>94025</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>213-46-8915</au_id>
       <au_lname>Green</au_lname>
       <au_fname>Margie</au_fname>
       <phone>415 986-7020</phone>
       <address>309 63rd St. #411</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94618</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>238-95-7766</au_id>
       <au_lname>Carson</au_lname>
       <au_fname>Cheryl</au_fname>
       <phone>415 548-7723</phone>
       <address>589 Darwin Ln.</address>
       <city>Berkeley</city>
       <state>CA</state>
       <zip>94705</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>267-41-2394</au_id>
       <au_lname>Hunter</au_lname>
       <au_fname>Anne</au_fname>
       <phone>408 286-2428</phone>
       <address>22 Cleveland Av. #14</address>
       <city>San Jose</city>
       <state>CA</state>
       <zip>95128</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>274-80-9391</au_id>
       <au_lname>Straight</au_lname>
       <au_fname>Dean</au_fname>
       <phone>415 834-2919</phone>
       <address>5420 College Av.</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94609</zip>
       <contract>true</contract>
     </authors>
   </Authors_Table>
   ```

4. Sobre o **arquivo** menu, selecione **salvar Authors**.

## <a name="create-the-user-interface"></a>Criar a interface do usuário

A interface do usuário para esse aplicativo consiste no seguinte:

-   Um <xref:System.Windows.Forms.DataGridView> controle que exibe o conteúdo do arquivo XML como dados.

-   Um <xref:System.Windows.Forms.TextBox> controle que exibe o esquema XML para o arquivo XML.

-   Dois <xref:System.Windows.Forms.Button> controles.

    -   Um botão lê o arquivo XML para o conjunto de dados e exibe-o no <xref:System.Windows.Forms.DataGridView> controle.

    -   Um segundo botão extrai o esquema do conjunto de dados e por meio de um <xref:System.IO.StringWriter> exibe-o no <xref:System.Windows.Forms.TextBox> controle.

### <a name="to-add-controls-to-the-form"></a>Para adicionar controles ao formulário

1.  Abra `Form1` no modo de exibição de design.

2.  Dos **caixa de ferramentas**, arraste os seguintes controles ao formulário:

    -   Um <xref:System.Windows.Forms.DataGridView> controle

    -   Um <xref:System.Windows.Forms.TextBox> controle

    -   Dois <xref:System.Windows.Forms.Button> controles

3.  Defina as propriedades a seguir:

    |Controle|Propriedade|Configuração|
    |-------------|--------------|-------------|
    |`TextBox1`|**Multilinha**|`true`|
    ||**ScrollBars**|**Vertical**|
    |`Button1`|**Nome**|`ReadXmlButton`|
    ||**Texto**|`Read XML`|
    |`Button2`|**Nome**|`ShowSchemaButton`|
    ||**Texto**|`Show Schema`|

## <a name="create-the-dataset-that-receives-the-xml-data"></a>Criar o conjunto de dados que recebe os dados XML

Nesta etapa, você cria um novo dataset denominado `authors`. Para obter mais informações sobre conjuntos de dados, consulte [ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md).

1.  No **Gerenciador de soluções**, selecione o arquivo de origem **Form1**e, em seguida, selecione o **View Designer** botão o **Gerenciador de soluções** barra de ferramentas.

2.  Do [caixa de ferramentas, guia dados](../ide/reference/toolbox-data-tab.md), arraste um **DataSet** até **Form1**.

3.  No **Adicionar conjunto de dados** caixa de diálogo, selecione **conjunto de dados não tipado**e, em seguida, selecione **Okey**.

     **DataSet1** é adicionado à bandeja de componentes.

4.  No **propriedades** janela, defina as **nome** e <xref:System.Data.DataSet.DataSetName%2A> propriedades para`AuthorsDataSet`.

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>Criar o manipulador de eventos para ler o arquivo XML para o conjunto de dados

O **Read XML** botão lê o arquivo XML para o conjunto de dados. Ele, em seguida, define as propriedades no <xref:System.Windows.Forms.DataGridView> controle que associá-lo ao conjunto de dados.

1.  Na **Gerenciador de soluções**, selecione **Form1**e, em seguida, selecione o **View Designer** botão o **Gerenciador de soluções** barra de ferramentas.

2.  Selecione o **Read XML** botão.

     O **Editor de códigos** é aberto no `ReadXmlButton_Click` manipulador de eventos.

3.  Digite o seguinte código para o `ReadXmlButton_Click` manipulador de eventos:

     [!code-csharp[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_1.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_1.vb)]

4.  No `ReadXMLButton_Click` código do manipulador de eventos, altere o `filepath =` entrada para o caminho correto.

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>Criar o manipulador de eventos para exibir o esquema na caixa de texto

O **Show Schema** botão cria uma <xref:System.IO.StringWriter> objeto que é preenchido com o esquema e é exibido no <xref:System.Windows.Forms.TextBox>controle.

1.  Na **Gerenciador de soluções**, selecione **Form1**e, em seguida, selecione o **View Designer** botão.

2.  Selecione o **Show Schema** botão.

     O **Editor de códigos** é aberto no `ShowSchemaButton_Click` manipulador de eventos.

3.  Cole o seguinte código para o `ShowSchemaButton_Click` manipulador de eventos.

     [!code-csharp[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/CSharp/read-xml-data-into-a-dataset_2.cs)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../data-tools/codesnippet/VisualBasic/read-xml-data-into-a-dataset_2.vb)]

## <a name="test-the-form"></a>Testar o formulário

Agora, é possível testar o formulário para garantir que ele se comporta da forma esperada.

1.  Selecione **F5** para executar o aplicativo.

2.  Selecione o **Read XML** botão.

     O DataGridView exibe o conteúdo do arquivo XML.

3.  Selecione o **Show Schema** botão.

     A caixa de texto exibe o esquema XML para o arquivo XML.

## <a name="next-steps"></a>Próximas etapas

Este passo a passo ensina as Noções básicas de ler um arquivo XML em um conjunto de dados, bem como a criação de um esquema com base no conteúdo do arquivo XML. Aqui estão algumas tarefas que você pode fazer em seguida:

-   Edite os dados no dataset e grave-os de volta como XML. Para obter mais informações, consulte <xref:System.Data.DataSet.WriteXml%2A>.

-   Editar os dados no conjunto de dados e grave-os em um banco de dados.

## <a name="see-also"></a>Consulte também

- [Acessar dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)
- [Ferramentas XML no Visual Studio](../xml-tools/xml-tools-in-visual-studio.md)