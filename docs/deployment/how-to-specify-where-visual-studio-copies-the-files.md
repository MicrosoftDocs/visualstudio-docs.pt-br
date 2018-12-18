---
title: Especifique onde copiar os arquivos | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publishing, specifying location
- Publish Location property
ms.assetid: 6c552700-dda3-49fe-af98-4717344fda07
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b4154f7b3a148968347b39911b9a7e9c28830eac
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53068309"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>Como: Especificar onde o Visual Studio copiará os arquivos
Quando você publica um aplicativo usando o ClickOnce, o `Publish Location` propriedade especifica o local onde os arquivos de aplicativo e manifesto são colocados. Isso pode ser um caminho de arquivo ou o caminho para um servidor FTP.  
  
 Você pode especificar o `Publish Location` propriedade no **Publish** página da **Designer de projeto**, ou usando o Assistente de publicação. Confira mais informações em [Como: Publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).  
  
> [!NOTE]
>  Ao instalar mais de uma versão de um aplicativo usando o ClickOnce, a instalação moverá as versões anteriores do aplicativo para uma pasta chamada Arquivo, no local de publicação especificado. O arquivamento de versões anteriores dessa maneira mantém o diretório de instalação livre de pastas da versão anterior.  
  
### <a name="to-specify-a-publishing-location"></a>Para especificar um local de publicação  
  
1. Com um projeto selecionado no **Gerenciador de Soluções**, no menu **Projeto**, clique em **Propriedades**.  
  
2. Clique o **publicar** guia.  
  
3. No **local de publicação** , insira o local de publicação usando um dos seguintes formatos:  
  
   - Para publicar em um caminho de disco ou compartilhamento de arquivo, insira o caminho usando um caminho UNC (*\\\Server\ApplicationName*) ou um caminho de arquivo (*C:\Deploy\ApplicationName*).  
  
   - Para publicar em um servidor FTP, insira o caminho usando o formato <em>ftp://ftp.microsoft.com/\<ApplicationName ></em>.  
  
     Observe que o texto precisa estar presente na caixa **Local de Publicação** para que o botão Procurar (**...**) funcione.  
  
## <a name="see-also"></a>Consulte também  
 [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)   
 [Como: Publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)