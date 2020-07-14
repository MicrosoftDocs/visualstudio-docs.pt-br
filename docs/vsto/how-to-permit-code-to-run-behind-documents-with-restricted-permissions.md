---
title: Permitir que o código seja executado por trás de documentos com permissões restritas
ms.date: 02/02/2017
ms.topic: how-to
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 15cfb7ebf2f4f71e892820206f0dd1d006639992
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547505"
---
# <a name="how-to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>Como: permitir que o código execute por trás de documentos com permissões restritas
  Você pode usar o recurso de Rights Management de informações (IRM) de Microsoft Office para restringir permissões a um documento ou pasta de trabalho. Por padrão, o código por trás de um documento Microsoft Office do Word restrito ou Microsoft Office pasta de trabalho do Excel não tem permissão para ser executado. Você pode alterar o padrão para que suas extensões de código gerenciado possam acessar o modelo de objeto e sua solução funcionará.

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Você deve ser o autor do documento ou da pasta de trabalho ou ter acesso de controle total para poder alterar as configurações de permissão.

## <a name="to-permit-code-to-run-behind-documents-with-restricted-permissions"></a>Para permitir que o código execute por trás de documentos com permissões restritas

1. Abra o documento ou pasta de trabalho no Word ou Excel.

2. Clique na guia **arquivo** , aponte para **preparar**, aponte para **restringir permissão**e clique em **acesso restrito**.

   > [!NOTE]
   > Na primeira utilização, será solicitado que você instale o cliente do Windows Rights Management. Depois de instalar o cliente, talvez seja necessário repetir as etapas.

3. Na caixa de diálogo **permissão** , selecione **restringir permissão para este documento**e clique em **mais opções**.

4. Em **permissões adicionais para usuários**, selecione **acessar conteúdo programaticamente**.

   O Word ou o Excel permitirá o acesso programático ao modelo de objeto.

## <a name="see-also"></a>Confira também
- [Visão geral do gerenciamento de direitos de informação e extensões de código gerenciado](../vsto/information-rights-management-and-managed-code-extensions-overview.md)
- [Proteção de documentos em soluções de nível de documento](../vsto/document-protection-in-document-level-solutions.md)
- [Proteção por senha em documentos do Office](../vsto/password-protection-on-office-documents.md)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
- [Proteger soluções do Office](../vsto/securing-office-solutions.md)
- [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)
