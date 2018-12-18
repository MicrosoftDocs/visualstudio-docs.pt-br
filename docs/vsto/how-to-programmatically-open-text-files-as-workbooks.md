---
title: 'Como: abrir arquivos de texto como pastas de trabalho de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening text files as
- text [Office development in Visual Studio], text files
- text files, opening as workbooks
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b7bc7caa5dbceb727394b8543b7659cc43e64a36
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35257641"
---
# <a name="how-to-programmatically-open-text-files-as-workbooks"></a>Como: abrir arquivos de texto como pastas de trabalho de forma programática
  Você pode abrir um arquivo de texto como uma pasta de trabalho. Você deve passar no nome do arquivo de texto que você deseja abrir. Você pode especificar vários parâmetros opcionais, como qual número de linha de análise em início e o formato de coluna dos dados no arquivo.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[Trin_VstcoreExcelAutomation#80](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#80)]
 [!code-vb[Trin_VstcoreExcelAutomation#80](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#80)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer os seguintes componentes:  
  
-   Um arquivo de texto delimitado por vírgula chamado `Test.txt` que contém pelo menos três linhas de texto.  
  
-   O arquivo de texto `Test.txt` a ser armazenado na unidade C.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com pastas de trabalho](../vsto/working-with-workbooks.md)   
 [Como: abrir pastas de trabalho de forma programática](../vsto/how-to-programmatically-open-workbooks.md)   
 [Como: criar programaticamente novas pastas de trabalho](../vsto/how-to-programmatically-create-new-workbooks.md)   
 [Como: salvar pastas de trabalho de forma programática](../vsto/how-to-programmatically-save-workbooks.md)   
 [Como: Fechar pastas de trabalho de forma programática](../vsto/how-to-programmatically-close-workbooks.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
  
  