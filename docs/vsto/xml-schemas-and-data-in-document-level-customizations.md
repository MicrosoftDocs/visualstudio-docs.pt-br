---
title: Esquemas e dados XML em personalizações em nível de documento
description: O Microsoft Excel e o Word fornecem a capacidade de Mapear esquemas para seus documentos e podem simplificar a importação e a exportação de dados XML para dentro e fora do documento.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio]
- schemas [Office development in Visual Studio]
- XML [Office development in Visual Studio], XML schemas
- XML schemas [Office development in Visual Studio], about XML schemas and data
- Office development in Visual Studio, XML
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 54e993f41787cfa44bb0aaa78cc7aff8fbad53d8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826584"
---
# <a name="xml-schemas-and-data-in-document-level-customizations"></a>Esquemas e dados XML em personalizações em nível de documento
  **Importante** As informações definidas neste tópico sobre o Microsoft Word são apresentadas exclusivamente para o benefício e o uso de indivíduos e organizações que estão localizados fora do Estados Unidos e de seus territórios ou que estão usando ou desenvolvendo programas que são executados em produtos do Microsoft Word que foram licenciados pela Microsoft antes de janeiro de 2010, quando a Microsoft removeu uma implementação de funcionalidades específicas relacionadas ao XML personalizado do Microsoft Word. Essas informações sobre o Microsoft Word podem não ser lidas ou usadas por indivíduos ou organizações na Estados Unidos ou em seus territórios que estão usando ou desenvolvendo programas que são executados no, produtos do Microsoft Word que foram licenciados pela Microsoft após 10 de janeiro de 2010; esses produtos não se comportarão da mesma forma que os produtos licenciados antes dessa data ou comprados e licenciados para uso fora do Estados Unidos.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Microsoft Office Excel e Microsoft Office Word fornecem a capacidade de Mapear esquemas para seus documentos. Esse recurso pode simplificar a importação e a exportação de dados XML para dentro e fora do documento.

 O Visual Studio expõe elementos de esquema mapeados em personalizações em nível de documento como controles no modelo de programação. Para o Excel, o Visual Studio adiciona suporte para ligar os controles aos dados em bancos de dado, serviços Web e objetos. Para o Word e o Excel, o Visual Studio adiciona suporte a painéis de ações, que podem ser usados com um documento mapeado por esquema para criar uma experiência aprimorada do usuário final para suas soluções. Para obter mais informações, consulte [visão geral do painel Ações](../vsto/actions-pane-overview.md).

> [!NOTE]
> Você não pode usar esquemas XML com várias partes em soluções do Excel.

## <a name="objects-created-when-schemas-are-attached-to-excel-workbooks"></a>Objetos criados quando esquemas são anexados a pastas de trabalho do Excel
 Quando você anexa um esquema a uma pasta de trabalho, o Visual Studio cria automaticamente vários objetos e os adiciona ao seu projeto. Esses objetos não devem ser excluídos usando as ferramentas do Visual Studio, pois são gerenciados pelo Excel. Para excluí-los, remova os elementos mapeados da planilha ou desanexe o esquema usando as ferramentas do Excel.

 Há dois objetos principais:

- Esquema XML (arquivo XSD). Para cada esquema na pasta de trabalho, o Visual Studio adiciona um esquema ao projeto. Isso aparece como um item de projeto com uma extensão XSD no **Gerenciador de soluções**.

- Uma classe tipada <xref:System.Data.DataSet> . Essa classe é criada com base no esquema. Essa classe de conjunto de um é visível no **modo de exibição de classe**.

## <a name="objects-created-when-schema-elements-are-mapped-to-excel-worksheets"></a>Objetos criados quando elementos de esquema são mapeados para planilhas do Excel
 Quando você mapeia um elemento de esquema do painel de tarefas **origem XML** para uma planilha, o Visual Studio cria automaticamente vários objetos e os adiciona ao seu projeto:

- Controles. Para cada objeto mapeado na pasta de trabalho, um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle (para elementos de esquema não repetidos) ou um <xref:Microsoft.Office.Tools.Excel.ListObject> controle (para elementos de esquema repetitivos) é criado no modelo de programação. O <xref:Microsoft.Office.Tools.Excel.ListObject> controle só pode ser excluído com a exclusão dos mapeamentos e dos objetos mapeados da pasta de trabalho. Para obter mais informações sobre controles, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

- BindingSource. Quando você cria um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> mapeando um elemento de esquema não repetitivo para a planilha, um <xref:System.Windows.Forms.BindingSource> é criado e o <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle é associado ao <xref:System.Windows.Forms.BindingSource> . Você deve associar o <xref:System.Windows.Forms.BindingSource> a uma instância da fonte de dados que corresponde ao esquema mapeado para o documento, como uma instância da classe tipada <xref:System.Data.DataSet> que foi criada. Crie a associação definindo as <xref:System.Windows.Forms.BindingSource.DataSource%2A> Propriedades e <xref:System.Windows.Forms.BindingSource.DataMember%2A> , que são expostas na janela **Propriedades** .

    > [!NOTE]
    > O <xref:System.Windows.Forms.BindingSource> não é criado para <xref:Microsoft.Office.Tools.Excel.ListObject> objetos. Você deve associar manualmente o <xref:Microsoft.Office.Tools.Excel.ListObject> à fonte de dados definindo as <xref:System.Windows.Forms.BindingSource.DataSource%2A> Propriedades e <xref:System.Windows.Forms.BindingSource.DataMember%2A> na janela **Propriedades** .

### <a name="office-mapped-schemas-and-the-visual-studio-data-sources-window"></a>Esquemas mapeados do Office e a janela fontes de dados do Visual Studio
 A funcionalidade de esquema mapeada do Office e a janela **fontes de dados** do Visual Studio podem ajudá-lo a apresentar dados em uma planilha do Excel para relatório ou edição. Em ambos os casos, você pode arrastar elementos de dados para a planilha do Excel. Ambos os métodos criam controles que são associados a dados por meio de um <xref:System.Windows.Forms.BindingSource> a uma fonte de dados, como um <xref:System.Data.DataSet> ou um serviço Web.

> [!NOTE]
> Quando você mapeia um elemento de esquema repetido para uma planilha, o Visual Studio cria um <xref:Microsoft.Office.Tools.Excel.ListObject> . O <xref:Microsoft.Office.Tools.Excel.ListObject> não é associado automaticamente aos dados por meio do <xref:System.Windows.Forms.BindingSource> . Você deve associar manualmente o <xref:Microsoft.Office.Tools.Excel.ListObject> à fonte de dados definindo as <xref:System.Windows.Forms.BindingSource.DataSource%2A> Propriedades e <xref:System.Windows.Forms.BindingSource.DataMember%2A> na janela **Propriedades** .

 A tabela a seguir mostra algumas das diferenças entre os dois métodos.

|esquema XML|janela Fontes de Dados|
|----------------|-------------------------|
|Usa a interface do Office.|Usa a janela **fontes de dados** no Visual Studio.|
|Habilita os recursos internos do Office para importar e exportar dados de arquivos XML.|Você deve fornecer a funcionalidade de importação e exportação programaticamente.|
|Você deve escrever o código para preencher os controles gerados com os dados.|Os controles adicionados da janela **fontes de dados** têm código gerado automaticamente para preenchê-los, juntamente com as cadeias de conexão necessárias quando você usa servidores de banco de dados.|

## <a name="behavior-when-schemas-are-attached-to-word-documents"></a>Comportamento quando esquemas são anexados a documentos do Word
 Os objetos de dados não são criados quando você anexa um esquema a um documento do Word que é usado em um projeto do Office de nível de documento. No entanto, quando você mapeia um elemento de esquema para o documento, os controles são criados. O tipo de controle depende do tipo de elemento que você mapear; os elementos repetitivos geram <xref:Microsoft.Office.Tools.Word.XMLNodes> controles e elementos não repetitivos geram <xref:Microsoft.Office.Tools.Word.XMLNode> controles. Para obter mais informações, [consulte controle](../vsto/xmlnodes-control.md) de [XMLNodes e controle de XMLNode](../vsto/xmlnode-control.md).

## <a name="deployment-of-solutions-that-include-xml-schemas"></a>Implantação de soluções que incluem esquemas XML
 Você deve criar um instalador para implantar uma solução que usa um esquema XML que é mapeado para um documento. O instalador deve registrar o esquema na biblioteca de esquemas no computador do usuário. Se você não registrar o esquema, a solução continuará funcionando porque o Word gera um esquema temporário com base nos elementos que estão no documento quando o usuário o abre. No entanto, o usuário não poderá executar a validação em relação ou salvar o esquema que foi usado para criar o projeto. Para obter mais informações sobre instaladores, consulte [implantar aplicativos, serviços e componentes](../deployment/deploying-applications-services-and-components.md).

 Você também pode adicionar código ao seu projeto para verificar se o esquema está na biblioteca e registrado. Se não estiver, você poderá avisar o usuário.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataWordVB/ThisDocument.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataWordCS/ThisDocument.cs" id="Snippet1":::

## <a name="see-also"></a>Consulte também

- [Como Mapear esquemas para documentos do Word dentro do Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [Como Mapear esquemas para planilhas dentro do Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
