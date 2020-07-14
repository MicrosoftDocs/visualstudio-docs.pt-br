---
title: Especificar onde copiar os arquivos | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f0618a6e0b74c16efaaf8a70b7b8745e0f3dd142
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381711"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>Como especificar para onde o Visual Studio copia os arquivos
Quando você publica um aplicativo usando o ClickOnce, a `Publish Location` propriedade especifica o local onde os arquivos de aplicativo e o manifesto são colocados. Pode ser um caminho de arquivo ou o caminho para um servidor FTP.

 Você pode especificar a `Publish Location` Propriedade na página **publicar** do designer de **projeto**ou usando o assistente de publicação. Para obter mais informações, consulte [como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md).

> [!NOTE]
> Ao instalar mais de uma versão de um aplicativo usando o ClickOnce, a instalação moverá as versões anteriores do aplicativo para uma pasta chamada Arquivo, no local de publicação especificado. O arquivamento de versões anteriores dessa maneira mantém o diretório de instalação livre de pastas da versão anterior.

### <a name="to-specify-a-publishing-location"></a>Para especificar um local de publicação

1. Com um projeto selecionado no **Gerenciador de soluções**, no menu **projeto** , clique em **Propriedades**.

2. Clique na guia **Publicar**.

3. No campo **publicar local** , insira o local de publicação usando um dos seguintes formatos:

   - Para publicar em um compartilhamento de arquivos ou caminho de disco, insira o caminho usando um caminho UNC (* \\ \Server\ApplicationName*) ou um caminho de arquivo (*C:\Deploy\ApplicationName*).

   - Para publicar em um servidor FTP, insira o caminho usando o formato <em>ftp://ftp.Microsoft.com/ \<ApplicationName> </em>.

     Observe que o texto deve estar presente na caixa **local de publicação** para que o botão procurar (**...**) funcione.

## <a name="see-also"></a>Veja também
- [Publicando aplicativos ClickOnce](../deployment/publishing-clickonce-applications.md)
- [Como publicar um aplicativo ClickOnce usando o assistente de publicação](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)