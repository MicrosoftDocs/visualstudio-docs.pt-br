---
title: 'Como: preencher documentos com dados de objetos'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], populating with data
- data [Office development in Visual Studio], adding to documents
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ef3d1441f9587bceeca0c4aacdc054a4769a2369
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36758106"
---
# <a name="how-to-populate-documents-with-data-from-objects"></a>Como: preencher documentos com dados de objetos

Acessando em dados em um objeto de dados funcionam da mesma maneira no nível de documento para o Microsoft Office Word, como faz em projetos do Windows Forms. Você usa as mesmas ferramentas e código trazer os dados de um objeto para sua solução, e você pode usar controles dos Windows Forms para exibir os dados. Além disso, você pode exibir dados usando controles de host. Controles de host são objetos nativos no Microsoft Office Word que foram aprimorados com eventos e a funcionalidade de associação de dados. Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

Você deve concluir as três etapas básicas para popular o documento com os dados de um objeto:

-   Adicione um controle para o documento que você pode associar a dados.

-   Adicione um objeto de dados para o documento.

-   Conecte-se o objeto de dados ao BindingSource.

## <a name="to-add-a-data-object"></a>Para adicionar um objeto de dados

Para adicionar um objeto de dados, abra o **fontes de dados** janela e criar uma fonte de dados de um objeto. Para obter mais informações, consulte [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).

## <a name="connect-the-data-object-to-the-bindingsource"></a>Conectar-se o objeto de dados para o BindingSource

Em projetos de nível de documento, você adicionar controles ao documento e associá-las a dados em tempo de design.

Em projetos de suplemento do VSTO, você cria controles e associá-las em tempo de execução.

### <a name="document-level-projects"></a>Projetos de nível de documento

Para conectar-se o objeto de dados ao BindingSource:

1.  Arraste o campo de dados desejado a **fontes de dados** janela ao documento. Isso cria automaticamente um controle.

2.  Em seu código, crie uma instância do tipo do objeto que você escolheu para a fonte de dados.

3.  Atribua a instância para o <xref:System.Windows.Forms.BindingSource.DataSource%2A> propriedade do <xref:System.Windows.Forms.BindingSource>.

### <a name="application-level-projects"></a>Projetos de nível de aplicativo

Para conectar-se o objeto de dados ao BindingSource:

1.  Em seu código, crie uma instância do tipo do objeto que está associado com a fonte de dados.

2.  Criar uma instância de um <xref:System.Windows.Forms.BindingSource>.

3.  Atribua a instância de fonte de dados para o <xref:System.Windows.Forms.BindingSource.DataSource%2A> propriedade do <xref:System.Windows.Forms.BindingSource>.

4.  Adicione a fonte de dados como uma ligação de dados ao controle.

## <a name="see-also"></a>Consulte também

- [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)
- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Como: preencher documentos com dados de um banco de dados](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)