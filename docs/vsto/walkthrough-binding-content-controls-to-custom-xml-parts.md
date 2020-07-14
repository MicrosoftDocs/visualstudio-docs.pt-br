---
title: 'Walkthrough: associar controles de conteúdo a partes XML personalizadas'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- PlainTextContentControl, binding to a custom XML part
- custom XML parts, binding to content controls
- content controls [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], content controls
- DropDownListContentControl, binding items to a custom XML part
- DatePickerContentControl, binding to a custom XML part
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a80488408f680530ed3c9b4094b2997e97484ce3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544437"
---
# <a name="walkthrough-bind-content-controls-to-custom-xml-parts"></a>Walkthrough: associar controles de conteúdo a partes XML personalizadas
  Este tutorial demonstra como associar controles de conteúdo em uma personalização em nível de documento para dados do Word em XML que são armazenados no documento.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 O Word permite que você armazene dados XML, chamados de *partes XML personalizadas*, em um documento. Você pode controlar a exibição desses dados ligando controles de conteúdo a elementos em uma parte XML personalizada. O documento de exemplo neste passo a passos exibe informações de funcionários que são armazenadas em uma parte XML personalizada. Quando você abre o documento, os controles de conteúdo exibem os valores dos elementos XML. As alterações feitas no texto nos controles de conteúdo são salvas na parte XML personalizada.

 Este passo a passo ilustra as seguintes tarefas:

- Adicionar controles de conteúdo ao documento do Word em um projeto de nível de documento em tempo de design.

- Criar um arquivo de dados XML e um esquema XML que define os elementos a serem associados aos controles de conteúdo.

- Anexando o esquema XML ao documento em tempo de design.

- Adicionar o conteúdo do arquivo XML a uma parte XML personalizada no documento em tempo de execução.

- Ligar os controles de conteúdo a elementos na parte XML personalizada.

- Associação a <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> a um conjunto de valores que são definidos no esquema XML.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word.

## <a name="create-a-new-word-document-project"></a>Criar um novo projeto de documento do Word
 Crie um documento do Word que você usará no passo a passo.

### <a name="to-create-a-new-word-document-project"></a>Para criar um novo projeto de documento do Word

1. Crie um projeto de documento do Word com o nome **EmployeeControls**. Crie um novo documento para a solução. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Abre o novo documento do Word no designer e adiciona o projeto **EmployeeControls** ao **Gerenciador de soluções**.

## <a name="add-content-controls-to-the-document"></a>Adicionar controles de conteúdo ao documento
 Crie uma tabela que contenha três tipos diferentes de controles de conteúdo em que o usuário possa exibir ou editar informações sobre um funcionário.

### <a name="to-add-content-controls-to-the-document"></a>Para adicionar controles de conteúdo ao documento

1. No documento do Word hospedado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Designer, na faixa de palavras, escolha a guia **Inserir** .

2. No grupo **tabelas** , escolha **tabela**e insira uma tabela com 2 colunas e 3 linhas.

3. Digite o texto na primeira coluna para que seja semelhante à seguinte coluna:

   ||
   |-|
   |**Nome do funcionário**|
   |**Hire Date**|
   |**Título**|

4. Na segunda coluna da tabela, escolha a primeira linha (ao lado do **nome do funcionário**).

5. Na faixa de seleção, escolha a guia **desenvolvedor** .

   > [!NOTE]
   > Se a guia **desenvolvedor** não estiver visível, você deverá primeiro mostrá-la. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

6. No grupo **controles** , escolha o botão **Text** de texto ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> à primeira célula.

7. Na segunda coluna da tabela, escolha a segunda linha (ao lado da **data de contratação**).

8. No grupo **controles** , escolha o botão **seletor de data** ![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> à segunda célula.

9. Na segunda coluna da tabela, escolha a terceira linha (ao lado de **título**).

10. No grupo **controles** , escolha o botão de **lista suspensa** ![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> à última célula.

    Essa é a interface do usuário inteira para este projeto. Se você executar o projeto agora, poderá digitar o texto na primeira linha e selecionar uma data na segunda linha. A próxima etapa é anexar os dados que você deseja exibir ao documento em um arquivo XML.

## <a name="create-the-xml-data-file"></a>Criar o arquivo de dados XML
 Normalmente, você obterá dados XML para armazenar em uma parte XML personalizada de uma fonte externa, como um arquivo ou um banco de dados. Neste tutorial, você cria um arquivo XML que contém os dados do funcionário, marcados por elementos que serão vinculados aos controles de conteúdo no documento. Para disponibilizar os dados em tempo de execução, incorpore o arquivo XML como um recurso no assembly de personalização.

#### <a name="to-create-the-data-file"></a>Para criar o arquivo de dados

1. No menu **Projeto**, escolha **Adicionar Novo Item**.

     A caixa de diálogo **Adicionar Novo Item** aparecerá.

2. No painel **modelos** , selecione **arquivo XML**.

3. Nomeie o arquivo **employees.xml**e, em seguida, escolha o botão **Adicionar** .

     O arquivo de **employees.xml** é aberto no editor de código.

4. Substitua o conteúdo do arquivo de **employees.xml** pelo texto a seguir.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <employees xmlns="http://schemas.microsoft.com/vsto/samples">
      <employee>
        <name>Karina Leal</name>
        <hireDate>1999-04-01</hireDate>
        <title>Manager</title>
      </employee>
    </employees>
    ```

5. Em **Gerenciador de soluções**, escolha o arquivo de **employees.xml** .

6. Na janela **Propriedades** , selecione a propriedade **criar ação** e, em seguida, altere o valor para **recurso incorporado**.

     Essa etapa incorpora o arquivo XML como um recurso no assembly quando você compila o projeto. Isso permite que você acesse o conteúdo do arquivo XML em tempo de execução.

## <a name="create-an-xml-schema"></a>Criar um esquema XML
 Se você quiser associar um controle de conteúdo a um único elemento em uma parte XML personalizada, não será necessário usar um esquema XML. No entanto, para associar o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> a um conjunto de valores, você deve criar um esquema XML que valida o arquivo de dados XML que você criou anteriormente. O esquema XML define os valores possíveis para o `title` elemento. Você vinculará o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> a esse elemento posteriormente neste passo a passos.

#### <a name="to-create-an-xml-schema"></a>Para criar um esquema XML

1. No menu **Projeto**, escolha **Adicionar Novo Item**.

     A caixa de diálogo **Adicionar Novo Item** aparecerá.

2. No painel **modelos** , selecione **esquema XML**.

3. Nomeie o esquema **Employees. xsd** e escolha o botão **Adicionar** .

     O designer de esquema é aberto.

4. No **Gerenciador de soluções**, abra o menu de atalho para **Employees. xsd**e escolha **Exibir código**.

5. Substitua o conteúdo do arquivo **Employees. xsd** pelo esquema a seguir.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <xs:schema xmlns="http://schemas.microsoft.com/vsto/samples"
        targetNamespace="http://schemas.microsoft.com/vsto/samples"
        xmlns:xs="http://www.w3.org/2001/XMLSchema"
        elementFormDefault="qualified">
      <xs:element name="employees" type="EmployeesType"></xs:element>
      <xs:complexType name="EmployeesType">
        <xs:all>
          <xs:element name="employee" type="EmployeeType"/>
        </xs:all>
      </xs:complexType>
      <xs:complexType name="EmployeeType">
        <xs:sequence>
          <xs:element name="name" type="xs:string" minOccurs="1" maxOccurs="1"/>
          <xs:element name="hireDate" type="xs:date" minOccurs="1" maxOccurs="1"/>
          <xs:element name="title" type="TitleType" minOccurs="1" maxOccurs="1"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="TitleType">
        <xs:restriction base="xs:string">
          <xs:enumeration value ="Engineer"/>
          <xs:enumeration value ="Designer"/>
          <xs:enumeration value ="Manager"/>
        </xs:restriction>
      </xs:simpleType>
    </xs:schema>
    ```

6. No menu **arquivo** , clique em **salvar tudo** para salvar as alterações nos **employees.xml** e nos arquivos **Employees. xsd** .

## <a name="attach-the-xml-schema-to-the-document"></a>Anexar o esquema XML ao documento
 Você deve anexar o esquema XML ao documento para associar os <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> valores válidos do `title` elemento.

### <a name="to-attach-the-xml-schema-to-the-document--word_15_short"></a>Para anexar o esquema XML ao documento ( [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] )

1. Ative **EmployeeControls.docx** no designer.

2. Na faixa de bits, escolha a guia **desenvolvedor** e, em seguida, escolha o botão **suplementos** .

3. Na caixa de diálogo **modelos e suplementos** , escolha a guia **esquema XML** e, em seguida, escolha o botão **Adicionar esquema** .

4. Navegue até o esquema **Employees. xsd** criado anteriormente, que está localizado no diretório do projeto e, em seguida, escolha o botão **abrir** .

5. Escolha o botão **OK** na caixa de diálogo **configurações de esquema** .

6. Escolha o botão **OK** para fechar a caixa de diálogo **modelos e suplementos** .

### <a name="to-attach-the-xml-schema-to-the-document-word-2010"></a>Para anexar o esquema XML ao documento (Word 2010)

1. Ative **EmployeeControls.docx** no designer.

2. Na faixa de seleção, escolha a guia **desenvolvedor** .

3. No grupo **XML** , escolha o botão **esquema** .

4. Na caixa de diálogo **modelos e suplementos** , escolha a guia **esquema XML** e, em seguida, escolha o botão **Adicionar esquema** .

5. Navegue até o esquema **Employees. xsd** que você criou anteriormente, que está localizado no diretório do projeto e escolha o botão **abrir** .

6. Escolha o botão **OK** na caixa de diálogo **configurações de esquema** .

7. Escolha o botão **OK** para fechar a caixa de diálogo **modelos e suplementos** .

     O painel de tarefas **estrutura XML** é aberto.

8. Feche o painel de tarefas **estrutura XML** .

## <a name="add-a-custom-xml-part-to-the-document"></a>Adicionar uma parte XML personalizada ao documento
 Antes de poder associar os controles de conteúdo aos elementos no arquivo XML, você deve adicionar o conteúdo do arquivo XML a uma nova parte XML personalizada no documento.

### <a name="to-add-a-custom-xml-part-to-the-document"></a>Para adicionar uma parte XML personalizada ao documento

1. No **Gerenciador de soluções**, abra o menu de atalho para **ThisDocument.cs** ou **ThisDocument. vb**e escolha **Exibir código**.

2. Adicione as seguintes declarações à `ThisDocument` classe. Esse código declara vários objetos que serão usados para adicionar uma parte XML personalizada ao documento.

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#1)]

3. Adicione o método a seguir à classe `ThisDocument`. Esse método obtém o conteúdo do arquivo de dados XML que é inserido como um recurso no assembly e retorna o conteúdo como uma cadeia de caracteres XML.

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#3)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#3)]

4. Adicione o método a seguir à classe `ThisDocument`. O `AddCustomXmlPart` método cria uma nova parte XML personalizada que contém uma cadeia de caracteres XML que é passada para o método.

     Para garantir que a parte XML personalizada seja criada apenas uma vez, o método criará a parte XML personalizada somente se uma parte XML personalizada com um GUID correspondente ainda não existir no documento. Na primeira vez que esse método é chamado, ele salva o valor da <xref:Microsoft.Office.Core._CustomXMLPart.Id%2A> Propriedade na `employeeXMLPartID` cadeia de caracteres. O valor da `employeeXMLPartID` cadeia de caracteres é persistido no documento porque ele foi declarado usando o <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> atributo.

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#4)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#4)]

## <a name="bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>Associar os controles de conteúdo a elementos na parte XML personalizada
 Associar cada controle de conteúdo a um elemento na parte XML personalizada usando a propriedade **XMLMapping** de cada controle de conteúdo.

### <a name="to-bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>Para associar os controles de conteúdo a elementos na parte XML personalizada

1. Adicione o método a seguir à classe `ThisDocument`. Esse método associa cada controle de conteúdo a um elemento na parte XML personalizada e define o formato de exibição de data do <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> .

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#5)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#5)]

## <a name="run-your-code-when-the-document-is-opened"></a>Executar seu código quando o documento for aberto
 Crie a parte XML personalizada e associe os controles personalizados aos dados quando o documento for aberto.

### <a name="to-run-your-code-when-the-document-is-opened"></a>Para executar seu código quando o documento é aberto

1. Adicione o código a seguir ao `ThisDocument_Startup` método da `ThisDocument` classe. Esse código obtém a cadeia de caracteres XML do arquivo de **employees.xml** , adiciona a cadeia de caracteres XML a uma nova parte XML personalizada no documento e associa os controles de conteúdo a elementos na parte XML personalizada.

     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#2)]

## <a name="test-the-project"></a>Teste do projeto
 Quando você abre o documento, os controles de conteúdo exibem dados dos elementos na parte XML personalizada. Você pode clicar em <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para selecionar um dos três valores válidos para o `title` elemento, que são definidos no arquivo **Employees. xsd** . Se você editar os dados em qualquer um dos controles de conteúdo, os novos valores serão salvos na parte XML personalizada no documento.

### <a name="to-test-the-content-controls"></a>Para testar os controles de conteúdo

1. Pressione **F5** para executar o projeto.

2. Verifique se a tabela no documento é semelhante à tabela a seguir. Cada uma das cadeias de caracteres na segunda coluna é Obtida de um elemento na parte XML personalizada no documento.

    |Coluna|Valor|
    |-|-|
    |**Nome do funcionário**|**Karina Leal**|
    |**Hire Date**|**1º de abril de 1999**|
    |**Título**|**Gerente**|

3. Escolha a célula à direita da célula **nome do funcionário** e digite um nome diferente.

4. Escolha a célula à direita da célula **data de contratação** e selecione uma data diferente no seletor de data.

5. Escolha a célula à direita da célula de **título** e selecione um novo item na lista suspensa.

6. Salve e feche o documento.

7. No explorador de arquivos, abra a pasta *\bin\Debug* sob o local do seu projeto.

8. Abra o menu de atalho para **EmployeeControls.docx** e, em seguida, escolha **renomear**.

9. Nomeie o arquivo **EmployeeControls.docx.zip**.

     O documento de **EmployeeControls.docx** é salvo no formato XML aberto. Ao renomear este documento com a extensão de nome de arquivo *. zip* , você pode examinar o conteúdo do documento. Para obter mais informações sobre o XML aberto, consulte o artigo técnico [apresentando os formatos de arquivo XML abertos do Office (2007)](/previous-versions/office/developer/office-2007/aa338205(v=office.12)).

10. Abra o arquivo **EmployeeControls.docx.zip** .

11. Abra a pasta **customXml** .

12. Abra o menu de atalho para **item2.xml** e, em seguida, escolha **abrir**.

     Esse arquivo contém a parte XML personalizada que você adicionou ao documento.

13. Verifique se os `name` `hireDate` elementos, e `title` contêm os novos valores que você inseriu nos controles de conteúdo no documento.

14. Feche o arquivo **item2.xml** .

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como usar os controles de conteúdo destes tópicos:

- Use todos os controles de conteúdo disponíveis para criar um modelo. Para obter mais informações, consulte [Walkthrough: criar um modelo usando controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md).

- Modifique os dados nas partes XML personalizadas enquanto o documento estiver fechado. Na próxima vez que o usuário abrir o documento, os controles de conteúdo associados aos elementos XML exibirão os novos dados.

- Use controles de conteúdo para proteger partes de um documento. Para obter mais informações, consulte [como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md).

## <a name="see-also"></a>Confira também
- [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)
- [Controles de conteúdo](../vsto/content-controls.md)
- [Como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)
- [Como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
