---
title: 'Como: especificar um local alternativo para atualizações de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: conceptual
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
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 76be049c670fb91911be70132b459cad5e5183bd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49902458"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>Como: especificar um local alternativo para atualizações da implantação
Você pode instalar seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo inicialmente a partir de um CD ou um compartilhamento de arquivos, mas o aplicativo deve verificar se há atualizações periódicas na Web. Você pode especificar um local alternativo para atualizações em seu manifesto de implantação para que seu aplicativo pode se atualizar da Web após sua instalação inicial.  
  
> [!NOTE]
>  Seu aplicativo deve ser configurado para instalar localmente para usar esse recurso. Para obter mais informações, consulte [instruções passo a passo: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md). Além disso, se você instalar um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo de rede, configuração de um local alternativo faz com que [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] para usar esse local para a instalação inicial e todas as atualizações subsequentes. Se você instalar o aplicativo localmente (por exemplo, a partir de um CD), a instalação inicial é executada usando a mídia original e todas as atualizações subsequentes usarão o local alternativo.  
  
### <a name="specify-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>Especifique um local alternativo para atualizações usando o MageUI.exe (utilitário baseado em Windows Forms)  
  
1.  Abra um prompt de comando do .NET Framework e digite:  
  
     **MageUI.exe**  
  
2.  Sobre o **arquivo** menu, escolha **abrir** para abrir o manifesto de implantação do seu aplicativo.  
  
3.  Selecione o **opções de implantação** guia.  
  
4.  Na caixa de texto denominada **local da inicialização**, insira a URL para o diretório que contém o manifesto de implantação para atualizações de aplicativos.  
  
5.  Salve o manifesto de implantação.  
  
### <a name="specify-an-alternate-location-for-updates-by-using-mageexe"></a>Especifique um local alternativo para atualizações usando Mage.exe  
  
1. Abra um prompt de comando do .NET Framework.  
  
2. Defina o local de atualização usando o comando a seguir. Neste exemplo, *HelloWorld.exe.application* é o caminho para seu [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] manifesto do aplicativo, que sempre tem a extensão. Application, e *<http://adatum.com/Update/Path>* é a URL que [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] verificará se há atualizações de aplicativo.  
  
    **Mage-atualizar HelloWorld.exe.application - ProviderUrl http://adatum.com/Update/Path**  
  
3. Salve o arquivo.  
  
   > [!NOTE]
   >  Agora você precisa assinar novamente o arquivo com *Mage.exe*. Para obter mais informações, consulte [instruções passo a passo: implantar manualmente um aplicativo ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-application.md).  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Se você instalar o aplicativo de uma mídia offline como um CD, e o computador está online, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] primeiro verifica a URL especificada pelo `<deploymentProvider>` marca no manifesto de implantação para determinar se o local de atualização contém uma versão mais recente das aplicativo. Se isso acontecer, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] instala o aplicativo diretamente a partir daí, em vez do diretório de instalação inicial, e o common language runtime (CLR) determina a relação de confiança do seu aplicativo usando o nível `<deploymentProvider>`. Se o computador estiver offline, ou `<deploymentProvider>` estiver inacessível, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] instalações do CD e o CLR concede confiança com base no ponto de instalação; para uma instalação com CD, isso significa que seu aplicativo recebe confiança total. Todas as atualizações subsequentes herdará esse nível de confiança.  
  
 Todos os [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativos que usam `<deploymentProvider>` deve declarar explicitamente as permissões necessárias no manifesto do aplicativo, para que o aplicativo não receberá diferentes níveis de confiança em computadores diferentes.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Implantar um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [Manifesto de implantação do ClickOnce](../deployment/clickonce-deployment-manifest.md)   
 [Proteger aplicativos ClickOnce](../deployment/securing-clickonce-applications.md)   
 [Escolha uma estratégia de atualização do ClickOnce](../deployment/choosing-a-clickonce-update-strategy.md)