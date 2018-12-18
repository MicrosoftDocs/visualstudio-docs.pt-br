---
title: Relação de confiança de concessão para soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- security [Office development in Visual Studio], trust
- inclusion lists [Office development in Visual Studio], about inclusion lists
- trust [Office development in Visual Studio], 2007 Office system
- granting trust [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: cfce58ca765e7e3710ecb55a1c84c09f0ee14f52
ms.sourcegitcommit: 1466ac0f49ebf7448ea4507ae3f79acb25d51d3e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/22/2018
ms.locfileid: "34447239"
---
# <a name="grant-trust-to-office-solutions"></a>Relação de confiança de concessão para soluções do Office
  Relação de confiança de concessão para meios de soluções Office modificando a política de segurança de cada computador de destino para o conjunto de solução, o manifesto do aplicativo, o manifesto de implantação e documento de confiança. Relação de confiança pode ser concedida para a solução do Office por você ou o usuário final.  
  
 Você pode conceder confiança total para a solução do Office ao assinar os manifestos de aplicativo e implantação.  
  
 Os usuários finais podem conceder confiança para a solução do Office fazendo uma decisão de confiança no [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] prompt confiável.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
##  <a name="Signing"></a> A solução de relação de confiança ao assinar os manifestos de aplicativo e implantação  
 Manifestos de todos os aplicativos e implantação para o Office solutions devem ser assinados com um certificado que identifica o Editor. Os certificados fornecem uma base para tomar decisões de confiança.  
  
 Um certificado temporário é criado para você e receber confiança no momento da compilação para a solução seja executada enquanto você depurá-lo. Se você publicar uma solução que está assinada com um certificado temporário, o usuário final será solicitado a tomar uma decisão de confiança.  
  
 Se você se conectar a solução com um certificado conhecido e confiável, a solução será instalada automaticamente sem avisar o usuário final para tomar uma decisão de confiança. Para obter mais informações sobre como obter um certificado para assinar, consulte [ClickOnce e Authenticode](/visualstudio/deployment/clickonce-and-authenticode). Depois de obter um certificado, o certificado deve ser explicitamente confiável adicionando-o à lista de editores confiáveis. Para obter mais informações, consulte [como: adicionar um fornecedor confiável a um computador cliente para aplicativos ClickOnce](/visualstudio/deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications).  
  
 Se um desenvolvedor fizer a solução com um certificado temporário, um administrador pode assinar novamente a personalização com um certificado conhecido e confiável, usando a ferramenta de edição e geração de manifesto (*mage.exe*), que é uma da Ferramentas do Microsoft .NET Framework. Para obter mais informações sobre como assinar soluções, consulte [como: soluções do Office sinal](../vsto/how-to-sign-office-solutions.md) e [como: assinar manifestos de aplicativo e implantação](/visualstudio/ide/how-to-sign-application-and-deployment-manifests).  
  
##  <a name="TrustPrompt"></a>A solução de relação de confiança usando o prompt de confiança do ClickOnce  
 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] solicita ao usuário final para tomar a decisão de confiança, se não houver nenhuma política de toda a organização confiança do certificado da solução. Se o usuário final concede confiança para a solução, uma entrada da lista de inclusão é criada que contém uma URL e uma chave pública para armazenar a decisão de confiança. Quando uma personalização confiável é executada mais tarde, o usuário final não é solicitado novamente.  
  
 Os administradores podem desabilitar o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] prompt confiável ou exigem que o prompt ocorrer apenas para as soluções são assinadas com um certificado Authenticode. Para obter mais informações sobre como alterar essas configurações para as zonas MyComputer, LocalIntranet, Internet, TrustedSites e UntrustedSites, consulte [como: configurar o comportamento de solicitação de confiança do ClickOnce](/visualstudio/deployment/how-to-configure-the-clickonce-trust-prompt-behavior).  
  
## <a name="see-also"></a>Consulte também  
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)   
 [Conceder confiança a documentos](../vsto/granting-trust-to-documents.md)   
 [Solucionar problemas de segurança de solução do Office](../vsto/troubleshooting-office-solution-security.md)   
 [Considerações sobre segurança específicas para soluções do Office](../vsto/specific-security-considerations-for-office-solutions.md)  
  
  