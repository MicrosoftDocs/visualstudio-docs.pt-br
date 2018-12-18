---
title: 'Passo a passo: Associar controles de conteúdo a partes XML personalizadas'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
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
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1bc8aee0a1294aeda4c57a3416de4a0cc98129f3
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50673026"
---
# <a name="walkthrough-bind-content-controls-to-custom-xml-parts"></a>Passo a passo: Associar controles de conteúdo a partes XML personalizadas
  Este passo a passo demonstra como associar controles de conteúdo em uma personalização no nível de documento para Word a dados XML armazenados no documento.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Word permite que você armazene dados XML, chamados *partes XML personalizadas*, em um documento. Você pode controlar a exibição desses dados, associando a controles de conteúdo a elementos em uma parte XML personalizada. O documento de exemplo neste passo a passo exibe informações de funcionários que são armazenadas em uma parte XML personalizada. Quando você abre o documento, os controles de conteúdo exibem os valores dos elementos XML. As alterações que você faça o texto nos controles de conteúdo são salvos na parte XML personalizada.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Adicionando controles de conteúdo para o documento do Word em um projeto de nível de documento em tempo de design.  
  
- Criando um arquivo de dados XML e um esquema XML que define os elementos para associar aos controles de conteúdo.  
  
- Anexando o esquema XML para o documento em tempo de design.  
  
- Adicionando o conteúdo do arquivo XML para uma parte XML personalizada no documento em tempo de execução.  
  
- Associando os controles de conteúdo a elementos na parte XML personalizada.  
  
- Associando um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> a um conjunto de valores que são definidos no esquema XML.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Word.  
  
## <a name="create-a-new-word-document-project"></a>Criar um novo projeto de documento do Word  
 Crie um documento do Word que você usará no passo a passo.  
  
### <a name="to-create-a-new-word-document-project"></a>Para criar um novo projeto de documento do Word  
  
1.  Criar um projeto de documento do Word com o nome **EmployeeControls**. Crie um novo documento para a solução. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o novo documento do Word no designer e adiciona o **EmployeeControls** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-content-controls-to-the-document"></a>Adicionar controles de conteúdo no documento  
 Crie uma tabela que contém três tipos diferentes de controles de conteúdo em que o usuário pode exibir ou editar informações sobre um funcionário.  
  
### <a name="to-add-content-controls-to-the-document"></a>Para adicionar controles de conteúdo no documento  
  
1. No documento do Word que está hospedado na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] designer, na faixa de opções, escolha o **inserir** guia.  
  
2. No **tabelas** grupo, escolha **tabela**e inserir uma tabela com 2 colunas e 3 linhas.  
  
3. Digite o texto na primeira coluna, para que ele fique parecido com a coluna a seguir:  
  
   ||  
   |-|  
   |**Nome do funcionário**|  
   |**Data de contratação**|  
   |**Título**|  
  
4. Na segunda coluna da tabela, escolha a primeira linha (lado **nome do funcionário**).  
  
5. Na faixa de opções, escolha o **desenvolvedor** guia.  
  
   > [!NOTE]  
   >  Se o **desenvolvedor** guia não estiver visível, você deve primeiro Mostrar. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
6. No **controles** grupo, escolha o **texto** botão ![PlainTextContentControl](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.PlainTextContentControl>para a primeira célula.  
  
7. Na segunda coluna da tabela, escolha a segunda linha (lado **data de contratação**).  
  
8. No **controles** grupo, escolha o **selecionador de data** botão ![DatePickerContentControl](../vsto/media/datepicker.gif "DatePickerContentControl") para adicionar um <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> segunda célula.  
  
9. Na segunda coluna da tabela, escolha a terceira linha (lado **título**).  
  
10. No **controles** grupo, escolha o **lista suspensa** botão ![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl") adicionar um <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> até a última célula.  
  
    Que é a interface do usuário para este projeto. Se você executar o projeto agora, você pode digite texto na primeira linha e selecione uma data na segunda linha. A próxima etapa é anexar os dados que você deseja exibir para o documento em um arquivo XML.  
  
## <a name="create-the-xml-data-file"></a>Criar o arquivo de dados XML  
 Normalmente, você obterá os dados XML para armazenar em uma parte XML personalizada de uma fonte externa, como um arquivo ou um banco de dados. Neste passo a passo, você deve criar um arquivo XML que contém os dados de funcionário, marcados por elementos que você associará aos controles de conteúdo no documento. Para disponibilizar os dados em tempo de execução, inserir o arquivo XML como um recurso no assembly de personalização.  
  
#### <a name="to-create-the-data-file"></a>Para criar o arquivo de dados  
  
1.  No menu **Projeto**, escolha **Adicionar Novo Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é exibida.  
  
2.  No **modelos** painel, selecione **arquivo XML**.  
  
3.  Nomeie o arquivo **Employees**e, em seguida, escolha o **Add** botão.  
  
     O **Employees** arquivo é aberto no Editor de códigos.  
  
4.  Substitua o conteúdo do **Employees** arquivo com o texto a seguir.  
  
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
  
5.  Na **Gerenciador de soluções**, escolha o **Employees** arquivo.  
  
6.  No **propriedades** janela, selecione a **Build Action** propriedade e, em seguida, altere o valor para **Embedded Resource**.  
  
     Esta etapa insere o arquivo XML como um recurso no assembly quando você compila o projeto. Isso permite que você acesse o conteúdo do arquivo XML em tempo de execução.  
  
## <a name="create-an-xml-schema"></a>Criar um esquema XML  
 Se você quiser associar um controle de conteúdo a um único elemento em uma parte XML personalizada, você não precisa usar um esquema XML. No entanto, para associar o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para um conjunto de valores, você deve criar um esquema XML que valida o arquivo de dados XML que você criou anteriormente. O esquema XML define os valores possíveis para o `title` elemento. Você associará o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> a esse elemento posteriormente neste passo a passo.  
  
#### <a name="to-create-an-xml-schema"></a>Para criar um esquema XML  
  
1.  No menu **Projeto**, escolha **Adicionar Novo Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é exibida.  
  
2.  No **modelos** painel, selecione **esquema XML**.  
  
3.  Nomeie o esquema **XSD** e escolha o **Add** botão.  
  
     Abre o designer de esquema.  
  
4.  Na **Gerenciador de soluções**, abra o menu de atalho **XSD**e, em seguida, escolha **Exibir código**.  
  
5.  Substitua o conteúdo do **XSD** arquivo com o esquema a seguir.  
  
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
  
6.  No **arquivo** menu, clique em **Salvar tudo** para salvar suas alterações para o **Employees** e o **XSD** arquivos.  
  
## <a name="attach-the-xml-schema-to-the-document"></a>Anexar o esquema XML no documento  
 Você deve anexar o esquema XML para o documento para associar o <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para os valores válidos do `title` elemento.  
  
### <a name="to-attach-the-xml-schema-to-the-document--includeword15shortvstoincludesword-15-short-mdmd"></a>Para anexar o esquema XML para o documento ( [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)])  
  
1.  Ativar **EmployeeControls.docx** no designer.  
  
2.  Na faixa de opções, escolha o **Developer** guia e, em seguida, escolha o **Add-Ins** botão.  
  
3.  No **modelos e suplementos** diálogo caixa, escolha o **esquema XML** guia e, em seguida, escolha o **adicionar esquema** botão.  
  
4.  Navegue até a **XSD** esquema criado anteriormente, que está localizado no diretório do projeto e, em seguida, escolha o **abrir** botão.  
  
5.  Escolha o **Okey** botão na **configurações de esquema** caixa de diálogo.  
  
6.  Escolha o **Okey** botão para fechar o **modelos e suplementos** caixa de diálogo.  
  
### <a name="to-attach-the-xml-schema-to-the-document-word-2010"></a>Para anexar o esquema XML para o documento (Word 2010)  
  
1.  Ativar **EmployeeControls.docx** no designer.  
  
2.  Na faixa de opções, escolha o **desenvolvedor** guia.  
  
3.  No **XML** grupo, escolha o **esquema** botão.  
  
4.  No **modelos e suplementos** diálogo caixa, escolha o **esquema XML** guia e, em seguida, escolha o **adicionar esquema** botão.  
  
5.  Navegue até a **XSD** esquema que você criou anteriormente, o que está localizada no diretório do projeto e escolha o **abrir** botão.  
  
6.  Escolha o **Okey** botão na **configurações de esquema** caixa de diálogo.  
  
7.  Escolha o **Okey** botão para fechar o **modelos e suplementos** caixa de diálogo.  
  
     O **estrutura XML** é aberto o painel de tarefas.  
  
8.  Fechar o **estrutura XML** painel de tarefas.  
  
## <a name="add-a-custom-xml-part-to-the-document"></a>Adicionar uma parte XML personalizada no documento  
 Antes de associar os controles de conteúdo para os elementos no arquivo XML, você deve adicionar o conteúdo do arquivo XML para uma nova parte XML personalizada no documento.  
  
### <a name="to-add-a-custom-xml-part-to-the-document"></a>Para adicionar uma parte XML personalizada no documento  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho **ThisDocument.cs** ou **ThisDocument**e, em seguida, escolha **Exibir código**.  
  
2.  Adicione as seguintes declarações para o `ThisDocument` classe. Esse código declara vários objetos que você usará para adicionar uma parte XML personalizada no documento.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#1)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#1](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#1)]  
  
3.  Adicione o seguinte método à classe `ThisDocument`. Esse método obtém o conteúdo do arquivo de dados XML que é inserido como um recurso no assembly e retorna o conteúdo como uma cadeia de caracteres XML.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#3)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#3](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#3)]  
  
4.  Adicione o seguinte método à classe `ThisDocument`. O `AddCustomXmlPart` método cria uma nova parte XML personalizada que contém uma cadeia de caracteres XML que é passada para o método.  
  
     Para garantir que a parte XML personalizada é criada apenas uma vez, o método cria o XML personalizado parte somente se uma parte XML personalizada com um GUID correspondente já existe no documento. A primeira vez que esse método é chamado, ele salva o valor da <xref:Microsoft.Office.Core._CustomXMLPart.Id%2A> propriedade para o `employeeXMLPartID` cadeia de caracteres. O valor da `employeeXMLPartID` cadeia de caracteres é persistida no documento porque ele foi declarado usando a <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> atributo.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#4)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#4](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#4)]  
  
## <a name="bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>Associar os controles de conteúdo a elementos na parte XML personalizada  
 Associar cada controle de conteúdo a um elemento na parte XML personalizada usando o **XMLMapping** propriedade de cada controle de conteúdo.  
  
### <a name="to-bind-the-content-controls-to-elements-in-the-custom-xml-part"></a>Para associar os controles de conteúdo a elementos na parte XML personalizada  
  
1.  Adicione o seguinte método à classe `ThisDocument`. Esse método associa cada controle de conteúdo a um elemento na parte XML personalizada e define o formato de exibição de data a <xref:Microsoft.Office.Tools.Word.DatePickerContentControl>.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#5)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#5](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#5)]  
  
## <a name="run-your-code-when-the-document-is-opened"></a>Executar seu código quando o documento é aberto.  
 Criar a parte XML personalizada e associar os controles personalizados aos dados quando o documento é aberto.  
  
### <a name="to-run-your-code-when-the-document-is-opened"></a>Para executar seu código quando o documento é aberto.  
  
1.  Adicione o seguinte código para o `ThisDocument_Startup` método da `ThisDocument` classe. Esse código obtém a cadeia de caracteres de XML o **Employees** arquivo, adiciona a cadeia de caracteres XML para uma nova parte XML personalizada no documento e associa os controles de conteúdo a elementos na parte XML personalizada.  
  
     [!code-csharp[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/CSharp/EmployeeControls/ThisDocument.cs#2)]
     [!code-vb[Trin_ContentControlXmlPartWalkthrough#2](../vsto/codesnippet/VisualBasic/EmployeeControls/ThisDocument.vb#2)]  
  
## <a name="test-the-project"></a>O projeto de teste  
 Quando você abre o documento, os controles de conteúdo exibem dados dos elementos na parte XML personalizada. Você pode clicar na <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> para selecionar um dos três valores válidos para o `title` elemento, que são definidos na **XSD** arquivo. Se você editar os dados em qualquer um dos controles de conteúdo, os novos valores são salvos na parte XML personalizada no documento.  
  
### <a name="to-test-the-content-controls"></a>Para testar os controles de conteúdo  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Verifique se a tabela no documento se parece com a tabela a seguir. Cada uma das cadeias de caracteres na segunda coluna é obtida de um elemento na parte XML personalizada no documento.  
  
    |||  
    |-|-|  
    |**Nome do funcionário**|**Karina Leal**|  
    |**Data de contratação**|**1 de abril de 1999**|  
    |**Título**|**Gerenciador de**|  
  
3.  Escolha a célula à direita do **nome do funcionário** de célula e digite um nome diferente.  
  
4.  Escolha a célula à direita do **data de contratação** de célula e selecione uma data diferente no selecionador de data.  
  
5.  Escolha a célula à direita do **título** de célula e selecione um novo item na lista suspensa.  
  
6.  Salve e feche o documento.  
  
7.  No Explorador de arquivos, abra o *\bin\Debug* pasta sob o local do seu projeto.  
  
8.  Abra o menu de atalho **EmployeeControls.docx** e, em seguida, escolha **Renomear**.  
  
9. Nomeie o arquivo **EmployeeControls.docx.zip**.  
  
     O **EmployeeControls.docx** documento é salvo no formato XML aberto. Renomeando esse documento com o *. zip* extensão de nome de arquivo você pode examinar o conteúdo do documento. Para obter mais informações sobre o Open XML, consulte o artigo técnico [apresentando o Office (2007) Open XML de formatos de arquivo](/previous-versions/office/developer/office-2007/aa338205(v=office.12)).  
  
10. Abra o **EmployeeControls.docx.zip** arquivo.  
  
11. Abra o **customXml** pasta.  
  
12. Abra o menu de atalho **item2.xml** e, em seguida, escolha **abrir**.  
  
     Esse arquivo contém a parte XML personalizada que você adicionou ao documento.  
  
13. Verifique se que o `name`, `hireDate`, e `title` elementos contêm os novos valores que você inseriu nos controles de conteúdo no documento.  
  
14. Fechar o **item2.xml** arquivo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como usar controles de conteúdo com estes tópicos:  
  
-   Use todos os controles de conteúdo disponíveis para criar um modelo. Para obter mais informações, consulte [instruções passo a passo: criar um modelo usando os controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md).  
  
-   Modificar os dados em partes XML personalizadas, enquanto o documento é fechado. Na próxima vez que o usuário abre o documento, os controles de conteúdo que são associados aos elementos XML exibirá os novos dados.  
  
-   Use controles de conteúdo para proteger partes de um documento. Para obter mais informações, consulte [como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md).  
  
## <a name="see-also"></a>Consulte também  
 [Automatizar o Word usando objetos estendidos](../vsto/automating-word-by-using-extended-objects.md)   
 [Controles de conteúdo](../vsto/content-controls.md)   
 [Como: adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)   
 [Como: proteger partes de documentos usando controles de conteúdo](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)  
  
  