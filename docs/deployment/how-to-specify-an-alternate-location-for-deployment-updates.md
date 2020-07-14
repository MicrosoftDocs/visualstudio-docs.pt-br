---
title: Como especificar um local alternativo para atualizações de implantação | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- deployment update, alternative locations
ms.assetid: 7faacd35-2638-492d-80f6-6b57e5f820de
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c71586c43fa1a71205d61ae21fb94c267daf497d
ms.sourcegitcommit: 3f491903e0c10db9a3f3fc0940f7b587fcbf9530
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85381906"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>Como especificar um local alternativo para atualizações da implantação
Você pode instalar seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo inicialmente de um CD ou de um compartilhamento de arquivos, mas o aplicativo deve verificar se há atualizações periódicas na Web. Você pode especificar um local alternativo para as atualizações em seu manifesto de implantação para que seu aplicativo possa se atualizar da Web após a instalação inicial.

> [!NOTE]
> Seu aplicativo deve ser configurado para ser instalado localmente para usar esse recurso. Para obter mais informações, consulte [Walkthrough: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Além disso, se você instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo da rede, definir um local alternativo fará com [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] que o use esse local para a instalação inicial e todas as atualizações subsequentes. Se você instalar o aplicativo localmente (por exemplo, de um CD), a instalação inicial será executada usando a mídia original e todas as atualizações subsequentes usarão o local alternativo.

### <a name="specify-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>Especificar um local alternativo para atualizações usando o MageUI.exe (utilitário baseado em Windows Forms)

1. Abra um prompt de comando .NET Framework e digite:

     **mageui.exe**

2. No menu **arquivo** , escolha **abrir** para abrir o manifesto de implantação do aplicativo.

3. Selecione a guia **Opções de implantação** .

4. Na caixa de texto denominada **local de inicialização**, insira a URL para o diretório que conterá o manifesto de implantação para atualizações de aplicativo.

5. Salve o manifesto de implantação.

### <a name="specify-an-alternate-location-for-updates-by-using-mageexe"></a>Especifique um local alternativo para as atualizações usando Mage.exe

1. Abra um prompt de comando .NET Framework.

2. Defina o local de atualização usando o comando a seguir. Neste exemplo, *HelloWorld.exe. Application* é o caminho para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto do aplicativo, que sempre tem a extensão. Application e `http://adatum.com/Update/Path` é a URL que verificará se há [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] atualizações do aplicativo.

    **Mage-Update HelloWorld.exe. Application-ProviderUrl http: \/ /adatum.com/Update/Path**

3. Salve o arquivo.

   > [!NOTE]
   > Agora você precisa assinar novamente o arquivo com *Mage.exe*. Para obter mais informações, consulte [Walkthrough: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).

## <a name="net-framework-security"></a>Segurança do .NET Framework
 Se você instalar seu aplicativo de um meio offline, como um CD, e o computador estiver online, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] primeiro o verificará a URL especificada pela `<deploymentProvider>` marca no manifesto de implantação para determinar se o local de atualização contém uma versão mais recente do aplicativo. Se tiver, o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] instalará o aplicativo diretamente de lá, em vez do diretório de instalação inicial, e o Common Language Runtime (CLR) determinará o nível de confiança do aplicativo usando `<deploymentProvider>` . Se o computador estiver offline ou `<deploymentProvider>` inacessível, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] o instalará a partir do CD e o CLR concederá confiança com base no ponto de instalação; para uma instalação em CD, isso significará que seu aplicativo recebe confiança total. Todas as atualizações subsequentes herdarão esse nível de confiança.

 Todos os [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos que usam `<deploymentProvider>` devem declarar explicitamente as permissões de que precisam no manifesto do aplicativo, para que o aplicativo não receba diferentes níveis de confiança em computadores diferentes.

## <a name="see-also"></a>Veja também
- [Passo a passo: Implantar um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)
- [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)
- [Escolher uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md)