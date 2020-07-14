---
title: 'Como: popular documentos com dados de objetos'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], populating with data
- data [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 38461fc30f71a811033ea70bfe560a6492f56e12
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547167"
---
# <a name="how-to-populate-documents-with-data-from-objects"></a>Como: popular documentos com dados de objetos

O acessamento de dados em um objeto de dados funciona da mesma maneira em projetos de nível de documento para Microsoft Office Word como no Windows Forms projetos. Você usa as mesmas ferramentas e código para trazer os dados de um objeto para sua solução e pode usar Windows Forms controles para exibir os dados. Além disso, você pode exibir dados usando controles de host. Os controles de host são objetos nativos no Microsoft Office Word que foram aprimorados com a funcionalidade de vinculação de dados e eventos. Para obter mais informações, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

Você deve concluir três etapas básicas para preencher o documento com dados de um objeto:

- Adicione um controle ao documento que você pode associar aos dados.

- Adicione um objeto de dados ao documento.

- Conecte o objeto de dados à BindingSource.

## <a name="to-add-a-data-object"></a>Para adicionar um objeto de dados

Para adicionar um objeto de dados, abra a janela **Data Sources** e crie uma fonte de dados de um objeto. Para obter mais informações, consulte [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).

## <a name="connect-the-data-object-to-the-bindingsource"></a>Conectar o objeto de dados à BindingSource

Em projetos de nível de documento, você adiciona controles ao seu documento e os associa aos dados em tempo de design.

Em projetos de suplemento do VSTO, você cria controles e os associa em tempo de execução.

### <a name="document-level-projects"></a>Projetos de nível de documento

Para conectar o objeto de dados à BindingSource:

1. Arraste o campo de dados desejado da janela **fontes de dados** para o documento. Isso cria automaticamente um controle.

2. Em seu código, crie uma instância do tipo do objeto que você escolheu para a fonte de dados.

3. Atribua a instância à <xref:System.Windows.Forms.BindingSource.DataSource%2A> Propriedade do <xref:System.Windows.Forms.BindingSource> .

### <a name="application-level-projects"></a>Projetos de nível de aplicativo

Para conectar o objeto de dados à BindingSource:

1. Em seu código, crie uma instância do tipo do objeto que está associado à fonte de dados.

2. Crie uma instância de uma <xref:System.Windows.Forms.BindingSource>.

3. Atribua a instância da fonte de dados à <xref:System.Windows.Forms.BindingSource.DataSource%2A> Propriedade do <xref:System.Windows.Forms.BindingSource> .

4. Adicione a fonte de dados como um DataBinding ao controle.

## <a name="see-also"></a>Confira também

- [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)
- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Como: popular documentos com dados de um banco de dado](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)