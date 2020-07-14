---
title: 'Como: popular documentos com dados de serviços'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], populating with data
- Web services [Office development in Visual Studio], populating documents
- data [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 01e2a83f464576d1ca780daa17c0d9478f0caa14
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547141"
---
# <a name="how-to-populate-documents-with-data-from-services"></a>Como: popular documentos com dados de serviços

O acesso a dados funciona da mesma maneira em projetos de nível de documento para Microsoft Office como faz em projetos Windows Forms. Você usa as mesmas ferramentas e código para colocar os dados em sua solução, e você pode até mesmo usar Windows Forms controles para exibir os dados. Além disso, você pode aproveitar os controles chamados de controles de host, que são objetos nativos no Microsoft Office Excel e Microsoft Office Word que foram aprimorados com a funcionalidade de vinculação de dados e eventos. Para obter mais informações, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

[!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

O exemplo a seguir mostra como adicionar controles vinculados a dados a documentos em tempo de design. Para obter um exemplo de como adicionar controles vinculados a dados em suplementos do VSTO em tempo de execução, consulte [passo a passos: associar dados de um serviço em um projeto de suplemento do VSTO](../vsto/walkthrough-binding-to-data-from-a-service-in-a-vsto-add-in-project.md).

## <a name="to-populate-a-document-level-project-with-data-from-a-web-service"></a>Para preencher um projeto de nível de documento com dados de um serviço Web

1. Abra a janela **Data Sources** e crie uma fonte de dados de serviço para seu projeto. Para obter mais informações, consulte [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).

2. Arraste a tabela ou o campo desejado da janela **fontes de dados** para o documento.

     Um controle é criado no documento, um <xref:System.Windows.Forms.BindingSource> é criado e associado à classe de objeto em seu projeto, e as classes são geradas para o serviço.

3. Em seu código, crie uma instância da classe de serviço Web à qual você se conectou na etapa 1.

4. Se houver propriedades que são necessárias para a comunicação com o serviço Web, crie instâncias dessas propriedades.

5. Crie e envie uma solicitação de dados usando métodos expostos pelo serviço Web e quaisquer instâncias de propriedade criadas na etapa 4.

     Os métodos que você usa dependem do que o serviço Web oferece.

6. Atribua a resposta de dados do serviço Web à <xref:System.Windows.Forms.BindingSource.DataSource%2A> Propriedade do <xref:System.Windows.Forms.BindingSource> .

Quando você executa o projeto, os controles exibem o primeiro registro na fonte de dados. Você pode habilitar a rolagem pelos registros manipulando os eventos de moeda usando os objetos no <xref:System.Windows.Forms.BindingSource> .

## <a name="see-also"></a>Confira também

- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)
- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Como: preencher planilhas com dados de um banco de dado](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [Como: popular documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como: popular documentos com dados de um banco de dado](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)