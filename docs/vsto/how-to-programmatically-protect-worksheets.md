---
title: 'Como: proteger planilhas programaticamente'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- protection, adding to worksheets
- documents [Office development in Visual Studio], document protection
- document protection, adding to worksheets
- worksheets, protecting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 819a1f4e07397720d806d887408b9e45aeda9ea5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49867176"
---
# <a name="how-to-programmatically-protect-worksheets"></a>Como: proteger planilhas programaticamente
  O recurso de proteção do Microsoft Office Excel ajuda a impedir que os usuários e o código modificar objetos em uma planilha. Por padrão, todas as células são bloqueadas após você ativa a proteção.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Personalizações em nível de documento, você pode proteger planilhas usando o designer do Excel. Você também pode proteger uma planilha programaticamente no tempo de execução em qualquer tipo de projeto.  
  
> [!NOTE]  
>  É possível adicionar controles dos Windows Forms a áreas de uma planilha que são protegidas.  
  
## <a name="use-the-designer"></a>Use o designer  
  
### <a name="to-protect-a-worksheet-in-the-designer"></a>Para proteger uma planilha no designer  
  
1. No **alterações** grupo da **revisão** , clique em **Proteger planilha**.  
  
    O **Proteger planilha** caixa de diálogo é exibida. Você pode definir uma senha e, opcionalmente, especificar determinadas ações que os usuários têm permissão para executar com a planilha, como formatar células ou inserir linhas.  
  
   Você também pode permitir que os usuários editem intervalos específicos em planilhas protegidas.  
  
### <a name="to-allow-editing-in-specific-ranges"></a>Para permitir a edição em intervalos específicos  
  
1.  No **alterações** grupo da **revisão** , clique em **permitem que os usuários editem intervalos**.  
  
     O **permitem que os usuários editem intervalos** caixa de diálogo é exibida. Você pode especificar intervalos sejam desbloqueados usando uma senha e os usuários podem editar intervalos sem uma senha.  
  
## <a name="use-code-at-runtime"></a>Use o código em tempo de execução  
 O código a seguir define a senha (usando a variável getPasswordFromUser, que contém uma senha obtida do usuário) e permite classificar somente.  
  
### <a name="to-protect-a-worksheet-by-using-code-in-a-document-level-customization"></a>Para proteger uma planilha por meio de código em uma personalização no nível de documento  
  
1.  Chamar o <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> método da planilha. Este exemplo pressupõe que você está trabalhando com uma planilha denominada `Sheet1`.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#27](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#27)]
     [!code-vb[Trin_VstcoreExcelAutomation#27](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#27)]  
  
### <a name="to-protect-a-worksheet-by-using-code-in-a-vsto-add-in"></a>Para proteger uma planilha usando código em um suplemento do VSTO  
  
1.  Chamar o <xref:Microsoft.Office.Interop.Excel._Worksheet.Protect%2A> método da planilha ativa.  
  
     [!code-csharp[Trin_VstcoreExcelAutomationAddIn#17](../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs#17)]
     [!code-vb[Trin_VstcoreExcelAutomationAddIn#17](../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb#17)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: remover a proteção de planilhas programaticamente](../vsto/how-to-programmatically-remove-protection-from-worksheets.md)   
 [Como: proteger pastas de trabalho de forma programática](../vsto/how-to-programmatically-protect-workbooks.md)   
 [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Item de host da planilha](../vsto/worksheet-host-item.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  