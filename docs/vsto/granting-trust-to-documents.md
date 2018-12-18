---
title: Conceder confiança a documentos
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
ms.openlocfilehash: 5dfa0ad9b27b94c472feabc0e202bd9eee58f08d
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670904"
---
# <a name="grant-trust-to-documents"></a>Conceder confiança a documentos
  Um projeto de nível de documento tem os mesmos requisitos de segurança que projetos de nível de aplicativo: os manifestos com um certificado de assinatura ou clicando no prompt de confiança. Além disso, o documento ou pasta de trabalho deve estar localizada em um diretório que é designado como um local confiável.  
  
 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]  
  
## <a name="trusted-locations"></a>Locais confiáveis  
 Aplicativos em [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] e Office 2010 têm centros de relação de confiança em que os usuários podem configurar configurações de segurança e privacidade, como locais confiáveis. Para soluções do Office, o computador local é considerado um local confiável. No entanto, devido a um risco maior, há determinados diretórios que não podem nunca ser confiáveis, como as pastas temporárias para o sistema, para cada usuário e para o Internet Explorer.  
  
 Para obter mais informações sobre a Central de confiabilidade, consulte [configurações de segurança e políticas e no Office 2010](http://go.microsoft.com/fwlink/?LinkId=89202). Para obter mais informações sobre como criar, gerenciar, remover e configurar pastas confiáveis, consulte [definir configurações de editores confiáveis e de locais confiáveis no 2007 Office system](http://go.microsoft.com/fwlink/?LinkId=89203) e [criar, remover ou alterar um local para seus arquivos confiável](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62).  
  
## <a name="security-considerations-for-office-solutions"></a>Considerações de segurança para soluções do Office  
 Há várias questões de segurança que você considere quais pastas adicionar aos locais confiáveis:  
  
-   Pastas locais são consideradas mais seguros e são implicitamente confiáveis. Locais remotos, como compartilhamentos de arquivos devem ser designados como locais confiáveis.  
  
-   Quando você adiciona um diretório para os locais confiáveis, essa ação concede confiança total não apenas para soluções do Office, mas também ao código VBA e ActiveX. Por esse motivo, o diretório raiz e o *Meus documentos* pastas não devem ser designadas como confiáveis.  
  
-   Embora o documento em si é confiável por meio de locais confiáveis, permissões adicionais são necessárias para a personalização de confiança. Você pode conceder confiança total para a personalização usando a assinatura dos manifestos com um certificado, clicando em prompt de confiança ou instalar a solução do Office para o *arquivos de programas* directory.  
  
-   Você pode armazenar o documento ou pasta de trabalho de uma solução de nível de documento no mesmo diretório que o assembly ou em um diretório diferente. Por exemplo, o documento pode estar localizado em um servidor do SharePoint e o assembly pode estar localizado em um compartilhamento de arquivos de rede. Para obter mais informações, consulte [como: publicar uma solução do Office em nível de documento em um servidor do SharePoint usando o ClickOnce](https://msdn.microsoft.com/2408e809-fb78-42a1-9152-00afa1522e58).  
  
## <a name="see-also"></a>Consulte também  
 [Conceder confiança a soluções do Office](../vsto/granting-trust-to-office-solutions.md)   
 [Solucionar problemas de segurança de solução do Office](../vsto/troubleshooting-office-solution-security.md)   
 [Proteger as soluções do Office](../vsto/securing-office-solutions.md)  
  
  