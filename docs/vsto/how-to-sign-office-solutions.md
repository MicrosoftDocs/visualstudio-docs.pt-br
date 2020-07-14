---
title: 'Como: assinar soluções do Office'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- certificates [Office development in Visual Studio], Office solutions
- security [Office development in Visual Studio], signing Office solutions
- signing manifests [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 23afc171fd97620b3e6801b8d199da6890198d8b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545750"
---
# <a name="how-to-sign-office-solutions"></a>Como: assinar soluções do Office
  Se você assinar uma solução, poderá conceder confiança à solução usando o certificado como evidência. Você pode usar o mesmo certificado para várias soluções e todas as soluções serão confiáveis sem nenhuma atualização de política de segurança adicional.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Se você editar manualmente os manifestos de aplicativo e implantação usando o Manifest Generation and Editing Tool (*mage.exe* e *mageui.exe*), deverá assinar novamente os manifestos antes de poder usá-los. Para obter mais informações, consulte [como: assinar novamente manifestos de aplicativo e implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md).

## <a name="sign-by-using-a-certificate"></a>Assinar usando um certificado
 Um certificado é um arquivo que contém uma chave exclusiva e a identidade do editor da solução. Você pode comprar certificados de uma autoridade de certificação ou criar seu próprio certificado e fazer com que uma autoridade de certificação a assine.

 O Visual Studio assina soluções do Office com um certificado temporário para habilitar a depuração. Você não deve usar o certificado temporário em soluções implantadas como evidência.

### <a name="to-sign-an-office-solution-by-using-a-certificate"></a>Para assinar uma solução do Office usando um certificado

1. No menu **projeto** , clique em _SolutionName_**Propriedades**de SolutionName.

2. Clique na guia **Assinatura** .

3. Selecione **assinar os manifestos ClickOnce**.

4. Localize o certificado clicando em **selecionar na loja** ou **selecione do arquivo** e navegando até o certificado.

5. Para verificar se o certificado correto está sendo usado, clique em **mais detalhes** para exibir as informações do certificado.

## <a name="see-also"></a>Consulte também

- [Proteger soluções do Office](../vsto/securing-office-solutions.md)
- [Conceder confiança às soluções do Office](../vsto/granting-trust-to-office-solutions.md)
- [Página de Assinatura, Designer de Projeto](../ide/reference/signing-page-project-designer.md)
