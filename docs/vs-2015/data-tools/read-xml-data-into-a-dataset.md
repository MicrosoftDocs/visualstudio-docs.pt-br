---
title: Dados XML de leitura para um conjunto de dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
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
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 6eb85fcef78b4b856c47ccb4436d1314ae440136
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219725"
---
# <a name="read-xml-data-into-a-dataset"></a>Ler dados XML em um conjunto de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O ADO.NET fornece métodos simples para trabalhar com dados XML. Neste passo a passo, você deve criar um aplicativo do Windows que carrega dados XML em um conjunto de dados. O conjunto de dados é exibido em um <xref:System.Windows.Forms.DataGridView> controle. Por fim, um esquema XML com base no conteúdo do arquivo XML é exibido em uma caixa de texto.  
  
 Este passo a passo consiste em cinco etapas principais:  
  
1.  Criar um novo projeto  
  
2.  Criando um arquivo XML a ser lido para o conjunto de dados  
  
3.  Criar a interface do usuário  
  
4.  Criar o conjunto de dados, ler o arquivo XML e exibi-lo em um <xref:System.Windows.Forms.DataGridView> controle  
  
5.  Adicionando código para exibir o esquema XML com base no arquivo XML em um <xref:System.Windows.Forms.TextBox> controle  
  
> [!NOTE]
>  As caixas de diálogo e comandos de menu que você vê podem diferir dos descritos na Ajuda, dependendo de suas configurações ativas ou a edição que você está usando. Para alterar suas configurações, nos **ferramentas** menu, selecione**Import and Export Settings**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
## <a name="create-a-new-project"></a>Criar um novo projeto  
 Nesta etapa, você cria um projeto do Visual Basic ou Visual c# que contém este passo a passo.  
  
#### <a name="to-create-the-new-windows-project"></a>Para criar o novo projeto do Windows  
  
1.  Sobre o **arquivo** menu, crie um novo projeto.  
  
2.  Nomeie o projeto `ReadingXML`.  
  
3.  Selecione **aplicativo do Windows**e, em seguida, selecione **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **ReadingXML** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>Gerar o arquivo XML a ser lido para o conjunto de dados  
 Porque este passo a passo se concentra na leitura de dados XML em um conjunto de dados, o conteúdo de um arquivo XML é fornecido.  
  
#### <a name="to-create-the-xml-file-that-will-be-read-into-the-dataset"></a>Para criar o arquivo XML que será lido para o conjunto de dados  
  
1.  Sobre o **Project** menu, selecione**Adicionar Novo Item**.  
  
2.  Selecione **arquivo XML**, nomeie o arquivo `authors.xml`e, em seguida, selecione **Add**.  
  
     O arquivo XML carrega no designer e está pronto para edição.  
  
3.  Cole o seguinte código no editor abaixo da declaração XML:  
  
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
  
4.  Sobre o **arquivo** menu, selecione**salvar Authors**.  
  
## <a name="create-the-user-interface"></a>Criar a interface do usuário  
 A interface do usuário para esse aplicativo consiste no seguinte:  
  
-   Um <xref:System.Windows.Forms.DataGridView> controle que exibe o conteúdo do arquivo XML como dados.  
  
-   Um <xref:System.Windows.Forms.TextBox> controle que exibe o esquema XML para o arquivo XML.  
  
-   Dois <xref:System.Windows.Forms.Button> controles.  
  
    -   Um botão lê o arquivo XML para o conjunto de dados e exibe-o no <xref:System.Windows.Forms.DataGridView> controle.  
  
    -   Um segundo botão extrai o esquema do conjunto de dados e por meio de um <xref:System.IO.StringWriter> exibe-o no <xref:System.Windows.Forms.TextBox> controle.  
  
#### <a name="to-add-controls-to-the-form"></a>Para adicionar controles ao formulário  
  
1.  Abra `Form1` no modo de exibição de design.  
  
2.  Dos **caixa de ferramentas**, arraste os seguintes controles ao formulário:  
  
    -   Um <xref:System.Windows.Forms.DataGridView> controle  
  
    -   Um <xref:System.Windows.Forms.TextBox> controle  
  
    -   Dois <xref:System.Windows.Forms.Button> controles  
  
3.  Defina as seguintes propriedades:  
  
    |Controle|Propriedade|Configuração|  
    |-------------|--------------|-------------|  
    |`TextBox1`|**Multilinha**|`true`|  
    ||**ScrollBars**|**Vertical**|  
    |`Button1`|**Nome**|`ReadXmlButton`|  
    ||**Texto**|`Read XML`|  
    |`Button2`|**Nome**|`ShowSchemaButton`|  
    ||**Texto**|`Show Schema`|  
  
## <a name="create-the-dataset-thatreceives-the-xml-data"></a>Criar o conjunto de dados thatreceives os dados XML  
 Nesta etapa, você cria um novo dataset denominado `authors`. Para obter mais informações sobre conjuntos de dados, consulte [ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md).  
  
#### <a name="to-create-a-new-dataset-that--receives-the-xml-data"></a>Para criar um novo conjunto de dados que recebe os dados XML  
  
1.  No **Gerenciador de soluções**, selecione o arquivo de origem **Form1**e, em seguida, selecione o **View Designer** botão o **Gerenciador de soluções** barra de ferramentas.  
  
2.  Do [caixa de ferramentas, guia dados](../ide/reference/toolbox-data-tab.md), arraste um **DataSet** até **Form1**.  
  
3.  No **Adicionar conjunto de dados** caixa de diálogo, selecione **conjunto de dados não tipado**e, em seguida, selecione **Okey**.  
  
     **DataSet1** é adicionado à bandeja de componentes.  
  
4.  No **propriedades** janela, defina as **nome** e <xref:System.Data.DataSet.DataSetName%2A> propriedades para`AuthorsDataSet`.  
  
## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>Criar o manipulador de eventos para ler o arquivo XML para o conjunto de dados  
 O **Read XML** botão lê o arquivo XML para o conjunto de dados. Ele, em seguida, define as propriedades no <xref:System.Windows.Forms.DataGridView> controle que associá-lo ao conjunto de dados.  
  
#### <a name="to-add-code-to-the-readxmlbuttonclick-event-handler"></a>Para adicionar código ao manipulador de eventos ReadXmlButton_Click  
  
1.  Na **Gerenciador de soluções**, selecione **Form1**e, em seguida, selecione o **View Designer** botão o **Gerenciador de soluções** barra de ferramentas.  
  
2.  Selecione o **Read XML** botão.  
  
     O **Editor de códigos** é aberto no `ReadXmlButton_Click` manipulador de eventos.  
  
3.  Digite o seguinte código para o `ReadXmlButton_Click` manipulador de eventos:  
  
     [!code-csharp[VbRaddataFillingAndExecuting#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#2)]
     [!code-vb[VbRaddataFillingAndExecuting#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#2)]  
  
4.  No `ReadXMLButton_Click` código do manipulador de eventos, altere o `filepath =` entrada para o caminho correto.  
  
## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>Criar o manipulador de eventos para exibir o esquema na caixa de texto  
 O **Show Schema** botão cria uma <xref:System.IO.StringWriter> objeto que é preenchido com o esquema e é exibido no <xref:System.Windows.Forms.TextBox>controle.  
  
#### <a name="to-add-code-to-the-showschemabuttonclick-event-handler"></a>Para adicionar código ao manipulador de eventos ShowSchemaButton_Click  
  
1.  Na **Gerenciador de soluções**, selecione **Form1**e, em seguida, selecione o **View Designer** botão.  
  
2.  Selecione o **Show Schema** botão.  
  
     O **Editor de códigos** é aberto no `ShowSchemaButton_Click` manipulador de eventos.  
  
3.  Digite o seguinte código para o `ShowSchemaButton_Click` manipulador de eventos.  
  
     [!code-csharp[VbRaddataFillingAndExecuting#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs#3)]
     [!code-vb[VbRaddataFillingAndExecuting#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb#3)]  
  
## <a name="test-the-form"></a>Testar o formulário  
 Agora, é possível testar o formulário para garantir que ele se comporta da forma esperada.  
  
#### <a name="to-test-the-form"></a>Para testar o formulário  
  
1.  Selecione **F5** para executar o aplicativo.  
  
2.  Selecione o **Read XML** botão.  
  
     O DataGridView exibe o conteúdo do arquivo XML.  
  
3.  Selecione o **Show Schema** botão.  
  
     A caixa de texto exibe o esquema XML para o arquivo XML.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo ensina as Noções básicas de ler um arquivo XML em um conjunto de dados, bem como a criação de um esquema com base no conteúdo do arquivo XML. Aqui estão algumas tarefas que você pode fazer em seguida:  
  
-   Edite os dados no dataset e grave-os de volta como XML. Para obter mais informações, consulte <xref:System.Data.DataSet.WriteXml%2A>.  
  
-   Editar os dados no conjunto de dados e grave-os em um banco de dados. Para obter mais informações, consulte [salvando dados](../data-tools/saving-data.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Accessing data in Visual Studio](../data-tools/accessing-data-in-visual-studio.md)  (Acessando dados no Visual Studio)  
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Ferramentas XML no Visual Studio](../xml-tools/xml-tools-in-visual-studio.md)

