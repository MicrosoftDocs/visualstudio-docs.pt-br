---
title: 'Como: especificar onde o Visual Studio copiará os arquivos | Microsoft Docs'
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
- publishing, specifying location
- Publish Location property
ms.assetid: 6c552700-dda3-49fe-af98-4717344fda07
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 6661eeeeaa802e482dd540f7a7793186f917edf3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49853799"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>Como especificar onde o Visual Studio copiará os arquivos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você publica um aplicativo usando o ClickOnce, o `Publish Location` propriedade especifica o local onde os arquivos de aplicativo e manifesto são colocados. Isso pode ser um caminho de arquivo ou o caminho para um servidor FTP.  
  
 Você pode especificar o `Publish Location` propriedade no **Publish** página da **Designer de projeto**, ou usando o Assistente de publicação. Para obter mais informações, consulte [como: publicar um aplicativo ClickOnce usando o Assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).  
  
> [!NOTE]
>  Ao instalar mais de uma versão de um aplicativo usando o ClickOnce, a instalação moverá as versões anteriores do aplicativo para uma pasta chamada Arquivo, no local de publicação especificado. O arquivamento de versões anteriores dessa maneira mantém o diretório de instalação livre de pastas da versão anterior.  
  
### <a name="to-specify-a-publishing-location"></a>Para especificar um local de publicação  
  
1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2. Clique o **publicar** guia.  
  
3. No **local de publicação** , insira o local de publicação usando um dos seguintes formatos:  
  
   - Para publicar em um caminho de disco ou compartilhamento de arquivo, insira o caminho usando um caminho UNC (\\\Server\ApplicationName) ou um caminho de arquivo (C:\Deploy\ApplicationName).  
  
   - Para publicar em um servidor FTP, insira o caminho usando o formato ftp://ftp.microsoft.com/ApplicationName.  
  
     Observe que o texto deve estar presente na **local de publicação** caixa para que o botão Procurar (**...** ) botão funcione.  
  
## <a name="see-also"></a>Consulte também  
 [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como publicar um aplicativo ClickOnce usando o Assistente de Publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)



