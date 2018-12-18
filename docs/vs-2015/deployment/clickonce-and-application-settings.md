---
title: ClickOnce e configurações de aplicativo | Microsoft Docs
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
- ClickOnce deployment, application settings
ms.assetid: 891caba6-faef-4a3c-8f71-60e6fadb60eb
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 29f51960ad953318c8d9de749f28f684128e52ef
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176964"
---
# <a name="clickonce-and-application-settings"></a>ClickOnce e configurações de aplicativo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Configurações de aplicativo para Windows Forms torna mais fácil criar, armazenar e manter aplicativos personalizados e preferências do usuário no cliente. Este documento descreve como os arquivos de configurações do aplicativo funcionam em um aplicativo ClickOnce e como o ClickOnce migra as configurações quando o usuário é atualizado para a próxima versão.  
  
 As informações a seguir se aplica somente ao provedor de configurações do aplicativo padrão, o <xref:System.Configuration.LocalFileSettingsProvider> classe. Se você fornecer um provedor personalizado, esse provedor determinará como ela armazena seus dados e como ele é atualizado suas configurações entre versões. Para obter mais informações sobre provedores de configurações do aplicativo, consulte [Application Settings Architecture](http://msdn.microsoft.com/library/c8eb2ad0-fac6-4ea2-9140-675a4a44d562).  
  
## <a name="application-settings-files"></a>Arquivos de configurações do aplicativo  
 Configurações do aplicativo consome dois arquivos: *app*. exe e User, onde *aplicativo* é o nome do seu aplicativo de formulários do Windows. User é criado na hora do cliente pela primeira que seu aplicativo armazena configurações no escopo do usuário. *aplicativo*. exe, por outro lado, continuará a existir antes da implantação se você definir valores padrão para configurações. Visual Studio incluirá esse arquivo automaticamente quando você usa seu **publicar** comando. Se você criar seu aplicativo ClickOnce usando Mage.exe ou MageUI.exe, verifique se esse arquivo é incluído com outros arquivos do seu aplicativo ao popular o manifesto do aplicativo.  
  
 Em aplicativos Windows Forms não implantado usando o ClickOnce, um aplicativo *app*. arquivo exe. config é armazenado no diretório do aplicativo, enquanto o arquivo User config é armazenado no usuário **Documents and Settings**  pasta. Em um aplicativo do ClickOnce *aplicativo*. exe reside no diretório do aplicativo dentro do cache do aplicativo ClickOnce e User reside no diretório de dados ClickOnce para o aplicativo.  
  
 Independentemente de como você implanta seu aplicativo, as configurações de aplicativo garante seguro acesso de leitura *aplicativo*. exe e o acesso de leitura/gravação seguro para User.  
  
 Em um aplicativo ClickOnce, o tamanho dos arquivos de configuração usado pelas configurações de aplicativo é restrito pelo tamanho do cache do ClickOnce. Para obter mais informações, consulte [visão geral de Cache do ClickOnce](../deployment/clickonce-cache-overview.md).  
  
## <a name="version-upgrades"></a>Atualizações de versão  
 Assim como cada versão de um aplicativo ClickOnce é isolada de todas as outras versões, as configurações do aplicativo para um aplicativo ClickOnce são isoladas das configurações para outras versões também. Quando o usuário é atualizado para uma versão posterior do seu aplicativo, as configurações do aplicativo compara as configurações de versão mais recente (número mais alto) contra as configurações fornecidas com a versão atualizada e os mescla as configurações em um novo conjunto de arquivos de configurações.  
  
 A tabela a seguir descreve como as configurações do aplicativo decide quais configurações para copiar.  
  
|Tipo de alteração|Ação de atualização|  
|--------------------|--------------------|  
|Configuração adicionada ao *aplicativo*. exe|A nova configuração será mesclada na versão atual *aplicativo*. exe|  
|Configuração retirada *aplicativo*. exe|A configuração antiga é removida da versão atual *aplicativo*. exe|  
|Padrão da configuração alterada; configuração local ainda é definida como padrão original em User|A configuração é mesclada em User da versão atual com o novo padrão como o valor|  
|Padrão da configuração alterada; configuração definida como não-padrão em User|A configuração é mesclada em User da versão atual com o valor não padrão retido|  
  
 Se você tiver criado suas próprias configurações de aplicativo a classe de wrapper e deseja personalizar a lógica de atualização, você pode substituir o <xref:System.Configuration.ApplicationSettingsBase.Upgrade%2A> método.  
  
## <a name="clickonce-and-roaming-settings"></a>ClickOnce e configurações de Roaming  
 ClickOnce não funciona com as configurações de roaming, que permite que seu arquivo de configurações a seguir você entre computadores em uma rede. Se você precisar de configurações de roaming, será necessário implementar um provedor de configurações do aplicativo que armazena as configurações de rede ou desenvolver suas próprias classes de configurações personalizadas para armazenar as configurações em um computador remoto. Para obter mais informações em provedores de configurações, consulte [Application Settings Architecture](http://msdn.microsoft.com/library/c8eb2ad0-fac6-4ea2-9140-675a4a44d562).  
  
## <a name="see-also"></a>Consulte também  
 [Segurança e implantação do ClickOnce](../deployment/clickonce-security-and-deployment.md)   
 [Visão geral sobre configurações de aplicativo](http://msdn.microsoft.com/library/0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc)   
 [Visão geral do Cache do ClickOnce](../deployment/clickonce-cache-overview.md)   
 [Acessando dados locais e remotos em aplicativos ClickOnce](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)



