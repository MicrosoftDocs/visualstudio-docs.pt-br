---
title: 'Como: popular documentos com dados de um banco de dado'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents, populating with data
- data, adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8470ec4acf686c016088c5f474539a1ab7ed85df
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547193"
---
# <a name="how-to-populate-documents-with-data-from-a-database"></a>Como: popular documentos com dados de um banco de dado

Você pode acessar dados em projetos de nível de documento para Microsoft Office da mesma maneira que acessa os dados em projetos Windows Forms. Você usa as mesmas ferramentas e código para trazer os dados de um banco de dado para sua solução e pode usar Windows Forms controles para exibir os dados.

Além disso, você pode exibir dados usando controles de host. Os controles de host são objetos nativos no Microsoft Office Word que foram aprimorados com a funcionalidade de vinculação de dados e eventos. Para obter mais informações, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

[!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

O exemplo a seguir mostra como adicionar controles vinculados a dados em projetos de nível de documento usando um designer. Para obter um exemplo de como adicionar controles vinculados a dados em projetos de suplemento do VSTO em tempo de execução, consulte [passo a passos: vinculação de dados simples no projeto de suplemento do VSTO](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md).

![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") Para ver uma demonstração de vídeo relacionada, consulte [associar dados a controles de conteúdo do Word 2007 usando o ferramentas do Visual Studio para o sistema do Office (3,0)](/previous-versions/office/developer/office-2007/bb967663(v=office.12)).

## <a name="add-a-control-to-a-document-at-design-time"></a>Adicionar um controle a um documento em tempo de design

### <a name="to-populate-a-document-with-data-from-a-database"></a>Para preencher um documento com dados de um banco de dado

1. Abra um projeto de nível de documento do Word no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , com o documento aberto no designer.

2. Abra a janela **Data Sources** e crie uma fonte de dados de um banco de dado. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

3. Arraste o campo desejado da janela **fontes de dados** para o documento.

Um controle de conteúdo é adicionado ao documento. O tipo de controle de conteúdo depende do tipo de dados do campo selecionado. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).

Você pode adicionar um controle diferente selecionando o campo de dados na janela **fontes de dados** e escolhendo um controle diferente na lista suspensa.

## <a name="objects-in-the-project"></a>Objetos no projeto

Além do controle, os seguintes objetos relacionados a dados são adicionados automaticamente ao seu projeto:

- Um dataset tipado que encapsula as tabelas de dados às quais você se conectou no Database. Para obter mais informações, consulte [ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md).

- Um <xref:System.Windows.Forms.BindingSource> que conecta o controle ao dataset tipado. Para obter mais informações, consulte [visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview).

- Um TableAdapter que conecta o dataset tipado ao banco de dados. Para obter mais informações, consulte [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).

- Um TableAdaptermanager, que é usado para coordenar adaptadores de tabela no conjunto de conjuntos para habilitar atualizações hierárquicas. Para obter mais informações, consulte [atualização hierárquica](../data-tools/hierarchical-update.md) e [referência do TableAdapterManager](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference).

Quando você executa o projeto, o controle exibe o primeiro registro na fonte de dados. Você pode usar o <xref:System.Windows.Forms.BindingSource> para permitir que os usuários percorram os registros.

### <a name="to-scroll-through-the-records"></a>Para percorrer os registros

- Use <xref:System.Windows.Forms.BindingSource> métodos como <xref:System.Windows.Forms.BindingSource.MoveNext%2A> e <xref:System.Windows.Forms.BindingSource.MovePrevious%2A> .

Para obter informações sobre como enviar atualizações para o dataset tipado e o banco de [dados, consulte How to: Update a data source with data of a host Control](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md).

## <a name="see-also"></a>Consulte também

- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)
- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Como: popular documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Visão geral de usar arquivos de banco de dados local em soluções do Office](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)