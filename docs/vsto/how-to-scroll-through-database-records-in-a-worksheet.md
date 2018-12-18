---
title: 'Como: percorrer registros do banco de dados em uma planilha'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
- worksheets [Office development in Visual Studio], scrolling records
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7e9ffaffdefda98e3e074467fcd4df8cacce91b4
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670103"
---
# <a name="how-to-scroll-through-database-records-in-a-worksheet"></a>Como: percorrer registros do banco de dados em uma planilha
  O procedimento a seguir mostra como usar o designer para exibir um único campo de uma tabela de banco de dados em uma planilha do Microsoft Office Excel, com controles que permitem que o usuário final percorrer todos os registros.  
  
 Você pode usar o designer apenas em projetos de nível de documento. No entanto, você também pode adicionar controles e associá-las aos dados por meio de programação em tempo de execução. Para obter mais informações, consulte [instruções passo a passo: associação de dados simples no projeto do suplemento do VSTO](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md).  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
## <a name="to-scroll-through-database-records-in-a-worksheet"></a>Para percorrer os registros de banco de dados em uma planilha  
  
1.  Abra um projeto de aplicativo do Excel no Visual Studio.  
  
2.  Abra o **fontes de dados** janela e criar uma fonte de dados do banco de dados. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).  
  
3.  Expanda a tabela que contém os dados que você deseja mostrar e selecione a coluna específica.  
  
4.  Abra a lista de controles e selecione **NamedRange**.  
  
5.  Arraste o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para a célula em que você deseja que os dados sejam exibidos.  
  
6.  Do **dos Windows Forms** guia da **caixa de ferramentas**, adicionar um <xref:System.Windows.Forms.BindingNavigator> controlar à sua planilha e configurar os controles que você deseja usar. Para obter mais informações, consulte [visão geral do controle BindingNavigator &#40;Windows Forms&#41;](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms).  
  
## <a name="see-also"></a>Consulte também  
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)  
  
  