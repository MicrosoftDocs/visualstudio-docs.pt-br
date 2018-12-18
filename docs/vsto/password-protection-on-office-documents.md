---
title: Proteção por senha em documentos do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- permissions [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- passwords [Office development in Visual Studio], document protections
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 02deaccdd615bae0c948d50abdd41758dc701704
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669772"
---
# <a name="password-protection-on-office-documents"></a>Proteção por senha em documentos do Office
  É possível definir uma senha em seus documentos do Microsoft Office Word e pastas de trabalho do Microsoft Office Excel, para que eles não podem ser abertos por alguém que sabe a senha. Esta opção é chamada **senha em aberto**.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Você pode criar projetos de nível de documento usando os documentos existentes e as pastas de trabalho que têm **senha em aberto** habilitado. O comportamento no Visual Studio é diferente para documentos do Word e Excel que tenham **senha em aberto** habilitado.  
  
 Para obter informações sobre como habilitar **senha em aberto**, consulte a Ajuda do Word ou Excel.  
  
## <a name="behavior-of-excel-and-word"></a>Comportamento do Excel e Word  
 Sempre que você abrir uma pasta de trabalho do Excel no Visual Studio que tenha **senha em aberto** habilitado, Excel solicitará a senha. Quando você compila sua solução você será solicitado a senha novamente, porque o documento é aberto durante a compilação.  
  
 Na primeira vez que você abre um documento do Word no Visual Studio que tenha **senha em aberto** habilitado, o Word solicitará a senha. Depois de inserir a senha com êxito **senha em aberto** é removido do documento e abrir o documento não exigir uma senha. Se você quiser que o documento em sua solução exigir uma senha antes que ele pode ser aberto, você deve habilitar **senha em aberto** após a compilação final e antes de implantar a solução.  
  
## <a name="see-also"></a>Consulte também  
 [Proteção do documento em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)   
 [Gerenciamento de direitos de informação e visão geral das extensões de código gerenciado](../vsto/information-rights-management-and-managed-code-extensions-overview.md)   
 [Como: permitir que o código execute documentos code-behind com permissões restritas](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)  
  
  