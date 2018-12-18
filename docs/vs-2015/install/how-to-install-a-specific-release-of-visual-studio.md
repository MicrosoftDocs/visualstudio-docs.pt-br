---
title: 'Como: instalar uma versão específica do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-install
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- install a specific release, Visual Studio
ms.assetid: d69ad0f8-f0a0-438e-a0ef-777c4868f139
caps.latest.revision: 20
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.openlocfilehash: e25c7e47b1d80cbdf30304ed3f4e6568704bb3d7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792810"
---
# <a name="how-to-install-a-specific-release-of-visual-studio"></a>Como: instalar uma versão específica do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Podemos atualizar a instalação do Visual Studio com frequência para que você obtenha a versão mais atual, otimizada de nossos recursos opcionais.  Mas se você quiser instalar uma versão anterior do Visual Studio 2015 — por exemplo, uma versão anterior à atualização 1 do Visual Studio com suporte para iOS, e em seguida, você deve forçar a instalação do Visual Studio para usar uma versão anterior de seus arquivos de manifesto de recurso. Este artigo descreve como fazê-lo.  
  
## <a name="installing-the-current-release"></a>Instalando a versão atual  
 Desde o lançamento inicial do Visual Studio 2015, nós atualizamos o mecanismo de instalação e os arquivos de manifesto várias vezes.  Isso significa que, se você baixar o instalador da web do [Downloads do Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) site em um computador limpo, conectado à internet, atualizar instalações de instalação mais recente Visual Studio 2015, que inclui os aprimoramentos mais recentes do produto bem como versões mais recentes e recentes de ferramentas e recursos opcionais.  
  
## <a name="installing-earlier-releases"></a>Instalando versões anteriores  
 Você pode criar e montar uma imagem ISO, ou você pode baixar e inicie o instalador diretamente a partir [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015) e, em seguida, acrescente o arquivo .exe com parâmetros de linha de comando adicionais (como /CustomInstallPath, / completo, / InstallSelectableItems, /NoRestart, etc.) para controlar como o Visual Studio é instalado.  
  
 A tabela a seguir inclui alguns cenários específicos de point-in-time e os parâmetros de linha de comando necessários, que você deve passar para o instalador do Enterprise edition. (Os mesmos parâmetros funcionará com os comunidade ou Professional edition instaladores também.)  
  
|Edição do Visual Studio 2015|O que executar|Linha de comando para usar|Qual configuração faz|  
|--------------------------------|-----------------|--------------------------|---------------------|  
|Visual Studio Enterprise (o lançamento mais recente)|Visual Studio Enterprise com atualizações (disponível no [My.VisualStudio.com](https://my.visualstudio.com/downloads?q=visual%20studio%20enterprise%202015))|`vs_enterprise.exe` **Observação:** o comportamento padrão da instalação oferece os mais recentes recursos opcionais e, portanto, ele não requer nenhum parâmetro de linha de comando.|Instalação do Visual Studio usará o feed.xml mais recente e instalar os arquivos mais recentes|  
|Visual Studio Enterprise Update 3 (o original 3 sem nenhuma outra atualização 3-era atualização)|Visual Studio Enterprise RTM (disponível a partir de [página de download de assinaturas do MSDN](https://msdn.microsoft.com/subscriptions/downloads/))|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/6/B/B/6BBD3561-D764-4F39-AB8E-05356A122545/20160628.2/enu/feed.xml`|Instalação do Visual Studio usará o feed.xml que estava disponível quando a atualização 3 lançada|  
|Enterprise atualização 2 do Visual Studio (atualização 2 original, mas com atualizações que a atualização 3 previamente atualizados)|Visual Studio Enterprise RTM (disponível a partir de [página de download de assinaturas do MSDN](https://msdn.microsoft.com/subscriptions/downloads/))|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/6/B/B/6BBD3561-D764-4F39-AB8E-05356A122545/20160620.2/enu/feed.xml`|Instalação do Visual Studio usará o feed.xml que foi atual antes da atualização 3 lançado|  
|Visual Studio Enterprise (o original de atualização 2 sem nenhuma outra atualização 2 era atualização)|Visual Studio Enterprise RTM (disponível a partir de [página de download de assinaturas do MSDN](https://msdn.microsoft.com/subscriptions/downloads/))|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/0/6/B/06BB0C5C-C767-4250-91DA-AB463377597E/20160405.3/enu/feed.xml`|Instalação do Visual Studio usará o feed.xml que estava disponível quando lançado de atualização 2|  
|Visual o Studio Enterprise Update 1 (atualização 1 original, mas com atualizações que previamente atualizados atualização 2)|Visual Studio Enterprise RTM (disponível a partir de [página de download de assinaturas do MSDN](https://msdn.microsoft.com/subscriptions/downloads/))|`vs_enterprise.exe /OverrideFeedURI http://download.microsoft.com/download/3/2/A/32A1974F-D236-43C1-8981-97DDCBAEF14A/20160225.3/enu/feed.xml`|Instalação do Visual Studio usará o feed.xml que foi atual antes da atualização 2 lançado|  
|Visual Studio Enterprise Update 1 (o original Update 1 sem nenhuma outra atualização era 1 atualização)|Visual Studio Enterprise RTM (disponível a partir de [página de download de assinaturas do MSDN](https://msdn.microsoft.com/subscriptions/downloads/))|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/3/2/A/32A1974F-D236-43C1-8981-97DDCBAEF14A/20151201.1/enu/feed.xml`|Instalação do Visual Studio usará o feed.xml que estava disponível quando lançado de atualização 1|  
|Visual Studio Enterprise (RTM original, mas com atualizações que previamente atualizados atualização 1)|Visual Studio Enterprise RTM (disponível a partir de [página de download de assinaturas do MSDN](https://msdn.microsoft.com/en-us/subscriptions/downloads/))|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/3/6/1/36188D5F-479F-4A46-BF55-6AE5928D1EBB/20151102.3/enu/feed.xml`|Instalação do Visual Studio usará o feed.xml que foi atual antes da atualização 1 lançado|  
|Visual Studio Enterprise (RTM original sem atualizações)|Visual Studio Enterprise RTM (disponível a partir de [página de download de assinaturas do MSDN](https://msdn.microsoft.com/subscriptions/downloads/))|`vs_enterprise.exe /OverrideFeedURI https://download.microsoft.com/download/5/7/B/57BF5016-E4F0-4EB5-BE27-2BFA87E7723F/20150713.1/enu/feed.xml`|Instalação do Visual Studio usará o feed.xml que estava disponível quando o RTM lançado|  
  
> [!IMPORTANT]
>  Dependendo do idioma que você deseja usar, substitua "enu" (para inglês) com um dos seguintes valores:  
> 
> - CHS (para chinês (simplificado))  
>   -   CHT (em chinês (tradicional))  
>   -   csy (para tcheco)  
>   -   deu (para o alemão)  
>   -   ESN (para espanhol)  
>   -   FRA (para francês)  
>   -   ITA (para italiano)  
>   -   JPA (para japonês)  
>   -   KOR (para coreano)  
>   -   plk (para polonês)  
>   -   PTB (em português)  
>   -   RUS (para Russo)  
>   -   TRK (para o turco)  
  
## <a name="see-also"></a>Consulte também  
 [Guia do administrador do Visual Studio](../install/visual-studio-administrator-guide.md)