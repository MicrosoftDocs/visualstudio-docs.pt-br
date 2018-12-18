---
title: 'Como: preencher documentos com dados de um banco de dados'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents, populating with data
- data, adding to documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: af068fc9cdacc0f681232ee4c7424d67d77f3a11
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36756795"
---
# <a name="how-to-populate-documents-with-data-from-a-database"></a>Como: preencher documentos com dados de um banco de dados

Você pode acessar dados em projetos de nível de documento para o Microsoft Office da mesma forma que você acessar dados em projetos do Windows Forms. Você usa as mesmas ferramentas e código de trazer os dados de um banco de dados para sua solução, e você pode usar controles dos Windows Forms para exibir os dados.

Além disso, você pode exibir dados usando controles de host. Controles de host são objetos nativos no Microsoft Office Word que foram aprimorados com eventos e a funcionalidade de associação de dados. Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).

[!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

O exemplo a seguir mostra como adicionar controles ligados a dados em projetos de nível de documento usando um designer. Para obter um exemplo de como adicionar controles ligados a dados em projetos de suplemento do VSTO em tempo de execução, consulte [instruções passo a passo: associação de dados simples no projeto do suplemento do VSTO](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md).

![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [associar dados ao conteúdo do Word 2007 controla usando o Visual Studio Tools para o Office system (3.0)](http://go.microsoft.com/fwlink/?LinkId=136785).

## <a name="add-a-control-to-a-document-at-design-time"></a>Adicionar um controle a um documento em tempo de design

### <a name="to-populate-a-document-with-data-from-a-database"></a>Para preencher um documento com os dados de um banco de dados

1.  Abra um projeto de nível de documento do Word no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], com o documento aberto no designer.

2.  Abra o **fontes de dados** janela e criar uma fonte de dados de um banco de dados. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

3.  Arraste o campo desejado a **fontes de dados** janela ao documento.

Um controle de conteúdo é adicionado ao documento. O tipo de controle de conteúdo depende do tipo de dados do campo selecionado. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md).

Você pode adicionar um controle diferente, selecionando o campo de dados do **fontes de dados** janela e, em seguida, escolhendo um controle diferente na lista suspensa.

## <a name="objects-in-the-project"></a>Objetos do projeto

Além do controle, os seguintes objetos de dados são automaticamente adicionados ao seu projeto:

-   Um dataset tipado que encapsula as tabelas de dados para o qual você se conectou no banco de dados. Para obter mais informações, consulte [ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md).

-   Um <xref:System.Windows.Forms.BindingSource> que conecta-se com o controle para o conjunto de dados tipado. Para obter mais informações, consulte [visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview).

-   Um TableAdapter que conecta-se o conjunto de dados tipado para o banco de dados. Para obter mais informações, consulte [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).

-   Um TableAdapterManager, que é usado para coordenar a adaptadores de tabela no conjunto de dados para habilitar as atualizações hierárquicas. Para obter mais informações, consulte [atualização hierárquica](../data-tools/hierarchical-update.md) e [TableAdapterManager reference](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference).

Quando você executa o projeto, o controle exibe o primeiro registro na fonte de dados. Você pode usar o <xref:System.Windows.Forms.BindingSource> para permitir aos usuários percorrer os registros.

### <a name="to-scroll-through-the-records"></a>Para percorrer os registros

-   Use <xref:System.Windows.Forms.BindingSource> métodos como <xref:System.Windows.Forms.BindingSource.MoveNext%2A> e <xref:System.Windows.Forms.BindingSource.MovePrevious%2A>.

Para obter informações sobre como enviar atualizações para o conjunto de dados tipado e o banco de dados, consulte [como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md).

## <a name="see-also"></a>Consulte também

- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)
- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Como: preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Usar arquivos de banco de dados local na visão geral das soluções do Office](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)