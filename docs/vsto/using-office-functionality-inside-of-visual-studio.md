---
title: Usar a funcionalidade do Office no Visual Studio
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], document protection
- Office applications [Office development in Visual Studio]
- Office functionality inside Visual Studio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6a1db785b4758236c4a50e694d868cecc269324a
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34767501"
---
# <a name="use-office-functionality-inside-of-visual-studio"></a>Usar a funcionalidade do Office no Visual Studio
  Quando você cria um projeto no nível do documento, o documento e o aplicativo associado são hospedados dentro do Visual Studio para criar e trabalhar diretamente com o documento. Quando você tiver um aplicativo abrir no Visual Studio do Microsoft Office, geralmente funciona conforme o esperado. No entanto, algumas das funcionalidades do aplicativo é diferente ou inacessível.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="document-protection"></a>Proteção de documentos  
 O Microsoft Office Word e Microsoft Office Excel oferecem recursos de proteção que você pode usar em seus projetos para documento. No entanto, se a proteção do documento estiver habilitada enquanto o documento está aberto no Visual Studio, pode impedir você de fazer algumas alterações de design. Para obter mais informações, consulte [proteção em nível de documento soluções do documento](../vsto/document-protection-in-document-level-solutions.md).  
  
## <a name="information-rights-management"></a>Gerenciamento de direitos de informação  
 Gerenciamento de direitos de informação (IRM) está disponível no Microsoft Office Word e Microsoft Office Excel. IRM pode ajudar a impedir que pessoas não autorizadas de exibir ou alterar informações confidenciais. No entanto, IRM também pode impedir que seu código em execução. Para obter mais informações, consulte [do gerenciamento de direitos de informação e visão geral de extensões de código gerenciado](../vsto/information-rights-management-and-managed-code-extensions-overview.md).  
  
## <a name="password-protection"></a>Proteção por senha  
 Documentos do Microsoft Office Word e pastas de trabalho do Microsoft Office Excel podem ser definidas para que eles não podem ser abertos por alguém que não sabe a senha. Proteção por senha será tratada no Word e Excel e pode afetar o processo de desenvolvimento. Para obter mais informações, consulte [proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md).  
  
## <a name="see-also"></a>Consulte também  
 [Proteção de documento em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)   
 [Gerenciamento de direitos de informação e visão geral de extensões de código gerenciado](../vsto/information-rights-management-and-managed-code-extensions-overview.md)   
 [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)   
 [Como: soluções do Office aberto sem executar código](../vsto/how-to-open-office-solutions-without-running-code.md)  
  
  