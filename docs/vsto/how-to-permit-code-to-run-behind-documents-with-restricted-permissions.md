---
title: 'Como: Permitir que o código execute documentos code-behind com permissões restritas'
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
- permissions [Office development in Visual Studio]
- IRM [Office development in Visual Studio]
- code [Office development in Visual Studio], running behind restricted documents
- documents [Office development in Visual Studio], restricted permissions
- Office documents [Office development in Visual Studio, restricted permissions
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: be77ed9aa6ad3c94a41cd9dfab3ec47c5c48931f
ms.sourcegitcommit: a205ff1b389fba1803acd32c54df7feb0ef7a203
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53648620"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>Como: Permitir que o código execute documentos code-behind com permissões restritas
  Você pode usar o recurso de gerenciamento de direitos de informação (IRM) do Microsoft Office para restringir as permissões para um documento ou pasta de trabalho. Por padrão, o código por trás de um documento do Microsoft Office Word restrito ou a pasta de trabalho do Microsoft Office Excel não é permitido para execução. Você pode alterar o padrão para que suas extensões de código gerenciado podem acessar o modelo de objeto e sua solução funcionará.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
 Você deve ser o autor do documento ou pasta de trabalho ou ter acesso de controle total para ser capaz de alterar as configurações de permissão.  
  
## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>Para permitir que o código execute documentos code-behind com permissões restritas  
  
1. Abra a pasta de trabalho ou documento no Word ou Excel.  
  
2. Clique o **arquivo** guia, aponte para **preparar**, aponte para **Restringir permissão**e, em seguida, clique em **acesso restrito**.  
  
   > [!NOTE]  
   >  No primeiro uso, você precisará instalar o cliente Windows Rights Management. Depois de instalar o cliente, talvez seja necessário repetir as etapas.  
  
3. No **permissão** caixa de diálogo, selecione **Restringir permissão neste documento**e, em seguida, clique em **mais opções**.  
  
4. Sob **permissões adicionais para usuários**, selecione **acessar programaticamente o conteúdo**.  
  
   Word ou Excel permitirá acesso programático ao modelo de objeto.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento de direitos de informação e visão geral das extensões de código gerenciado](../vsto/information-rights-management-and-managed-code-extensions-overview.md)   
 [Proteção do documento em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)   
 [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)   
 [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)   
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)  
  
  