---
title: 'Como: personalizar a página da Web padrão para um aplicativo ClickOnce | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish.htm Web page
- ClickOnce deployment default Web page
- deploying applications [ClickOnce], publishing
- publishing, ClickOnce
ms.assetid: 418de18c-bee9-4f24-9cd9-0252d175070d
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: b87019a824acada616865fd65cfd6aade8aa6ec9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49243419"
---
# <a name="how-to-customize-the-default-web-page-for-a-clickonce-application"></a>Como personalizar a página da Web padrão para um aplicativo ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao publicar um aplicativo ClickOnce para a Web, uma página da Web é gerada automaticamente e publicada com o aplicativo. A página padrão contém o nome do aplicativo e links para instalar o aplicativo, instale os pré-requisitos ou acessar a Ajuda no MSDN.  
  
> [!NOTE]
>  Os links reais que você vê na página dependem do computador em que a página estiver sendo exibida e o que você está incluindo de pré-requisitos.  
  
 O nome padrão para a página da Web é Publish. htm; Você pode alterar o nome na **Designer de projeto**. Para obter mais informações, consulte [como: especificar uma página de publicação para um aplicativo ClickOnce](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md).  
  
 A página da Web de Publish. htm é publicada somente se for detectada uma versão mais recente.  
  
> [!NOTE]
>  As alterações feitas ao seu **publicar** configurações não afetarão a página Publish. htm, com uma exceção: se você adicionar ou remove os pré-requisitos depois de publicar inicialmente, a lista de pré-requisitos não ser precisa. Você precisará editar o texto do link de pré-requisito refletir as alterações.  
  
### <a name="to-customize-the-publish-web-page"></a>Para personalizar a página Web publicar  
  
1.  Publica seu aplicativo ClickOnce em um local da Web. Para obter mais informações, consulte [como: publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).  
  
2.  No servidor Web, abra o arquivo publish. htm no Visual Web Designer ou outro editor de HTML.  
  
3.  Personalizar a página conforme desejado e salve-o.  
  
4.  Opcional. Para impedir que o Visual Studio substituindo sua página da Web de publicação personalizadas, desmarque a opção **gerar automaticamente a página da web de implantação após cada publicação** na caixa de diálogo Opções de publicação.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como instalar pré-requisitos com um aplicativo ClickOnce](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)   
 [Como especificar uma página de publicação para um aplicativo ClickOnce](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)



