---
title: Gerenciamento de direitos de informação e visão geral de extensões de código gerenciado
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Information Rights Management [Office development in Visual Studio]
- workbooks [Office development in Visual Studio], restricted permissions
- IRM [Office development in Visual Studio]
- documents [Office development in Visual Studio], restricted permissions
- rights management [Office development in Visual Studio]
- Office documents [Office development in Visual Studio, restricted permissions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 35a118774d50bcc697cd3ff5663fc26d8580ac88
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34263755"
---
# <a name="information-rights-management-and-managed-code-extensions-overview"></a>Gerenciamento de direitos de informação e visão geral de extensões de código gerenciado
  O Microsoft Office Word e Microsoft Office Excel fornecem gerenciamento de direitos de informação (IRM), um recurso que pode ajudá-lo a evitar que pessoas não autorizadas de exibir ou alterar informações confidenciais. Para obter detalhes sobre como funciona o gerenciamento de direitos de informações, consulte a Ajuda no aplicativo do Office específico.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="run-code-behind-documents-with-restricted-permissions"></a>Execute o código por trás de documentos com permissões restritas  
 Se sua solução contiver um documento ou a pasta de trabalho que usa o IRM, por padrão, Word e Excel não permitem execução de qualquer código. Se você for o autor do documento ou ter acesso de controle total, você pode alterar o padrão para que a solução funciona. Para obter mais informações, consulte [como: permitir que o código seja executado atrás de documentos com permissões restritas](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md).  
  
 IRM impede o uso de <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ServerDocument> para recuperar ou manipular dados armazenados em cache no documento.  
  
## <a name="end-users-to-restrict-permissions-to-documents-that-use-managed-code-extensions"></a>Usuários finais para restringir permissões para documentos que usam extensões de código gerenciado  
 Qualquer pessoa que tenha acesso de controle total para o documento ou a pasta de trabalho em sua solução pode usar o IRM para restringir as permissões. Por exemplo, se um usuário final no departamento de contabilidade usa uma solução que preenche automaticamente uma planilha com os dados de um banco de dados, o que o usuário desejar permitir que alterar o acesso somente a pessoas em seu departamento e acesso de leitura a outros. Quando o usuário adiciona as permissões restritas, por padrão, não é possível executar o código por trás da planilha, e a planilha não será populada com dados.  
  
 Para corrigir o problema, uma pessoa com acesso de controle total para o documento ou a pasta de trabalho deve alterar as configurações de permissão padrão para permitir o acesso programático ao modelo de objeto. Para obter mais informações, consulte [como: permitir que o código seja executado atrás de documentos com permissões restritas](../vsto/how-to-permit-code-to-run-behind-documents-with-restricted-permissions.md).  
  
## <a name="see-also"></a>Consulte também  
 [Proteção de documento em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)   
 [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)   
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)  
  
  