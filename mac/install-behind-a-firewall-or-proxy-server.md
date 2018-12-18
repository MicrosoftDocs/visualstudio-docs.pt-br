---
title: Instalar e usar o Visual Studio para Mac por trás de um firewall ou servidor proxy
description: Este documento fornece uma lista de hosts que devem estar na lista de permissões no firewall para permitir que o Visual Studio para Mac (e suas cargas de trabalho, incluindo Xamarin) funcionem em um ambiente corporativo.
ms.topic: troubleshooting
ms.assetid: 79C0F1A3-0C13-4E55-A820-1138A4082B77
author: asb3993
ms.author: amburns
ms.date: 10/23/2018
ms.openlocfilehash: 70ac8defdcea9cccd8a3b3f9be71d38fb78c9c50
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295183"
---
# <a name="install-and-use-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>Instalar e usar o Visual Studio para Mac por trás de um firewall ou servidor proxy

Se você ou sua organização usa medidas de segurança como um firewall ou um servidor proxy, há URLs de domínio que você talvez queira adicionar à "lista de permissões" e portas e protocolos que talvez você queira abrir para que tenha a melhor experiência ao instalar e usar o Visual Studio para Mac e os Serviços do Azure.

- [**Instalar o Visual Studio para Mac**](#install-visual-studio-for-mac): essas tabelas incluem as URLs na lista de permissões para que você tenha acesso a todos os recursos e cargas de trabalho do Visual Studio para Mac.

- [**Usar o Visual Studio para Mac**](#use-visual-studio-for-mac): essas tabelas incluem as URLs na lista de permissões para que você tenha acesso a todos os serviços e recursos desejados.

## <a name="install-visual-studio-for-mac"></a>Instalar o Visual Studio para Mac

Como o Instalador do Visual Studio para Mac baixa de vários domínios e servidores de download, aqui estão os domínios e URLs que convém adicionar como confiáveis às suas configurações.

### <a name="microsoft-domains"></a>Domínios da Microsoft

| Domain| Finalidade |
| ----------------------------------- |---------------------------|
| *.live.com| Gerenciamento de Credenciais |
| app.vssps.visualstudio.com| Metadados do Instalador|
| vortex.data.microsoft.com | Relatórios de Erros e Falhas |
| az667904.vo.msecnd.net| Relatórios de Erros e Falhas |
| xamarin.com | Metadados do Instalador|
| xampubdl.blob.core.windows.net| Pacotes do Instalador|
| download.visualstudio.microsoft.com | Pacotes do Instalador|
| xamarin.azureedge.net | Pacotes do Instalador|
| developer.xamarin.com | Pacotes do Instalador|
| dc.services.visualstudio.com| Relatórios de Falhas |

### <a name="third-party-domains"></a>Domínios de terceiros

| Domain| Finalidade |
| --------------------------|-------------------------|
| dl.google.com | SDK do Android |
| download.oracle.com | SDK do Java|
| api.apple-cloudkit.com| Serviços de Segurança da Apple |

## <a name="use-visual-studio-for-mac"></a>Usar o Visual Studio para Mac

Para garantir que você tenha acesso a todos os recursos de que precisa no Visual Studio para Mac ao usar um proxy ou firewall, é recomendável adicionar à lista de permissões os domínios e portas a seguir.

### <a name="general"></a>Geral

| Domain | Porta(s)|Finalidade|
| ----------------------|------------------|------------------|
| go.microsoft.com | 80/443|Resolução da URL da Microsoft |
| vsstartpage.blob.core.windows.net| 80/443| Dados da Página Inicial|
| software.xamarin.com |  80/443|Serviço de Atualizador|
| addins.monodevelop.com | 80/443| Serviços de Extensão |
| visualstudio-devdiv-c2s.msedge.net | 80/443| Recurso Experimental e Notificações |
| targetednotifications.azurewebsites.net|  80/443| Usada para filtrar uma lista global de notificações para uma lista aplicável somente a tipos específicos de cenários de uso/computadores|

### <a name="identity"></a>Identidade

| Domain | Porta(s)|Finalidade|
| ----------------------|------------------|------------------|
| login.microsoftonline.com | 80/443| Provedor de Identidade|
| secure.aadcdn.microsoftonline-p.com | 80/443|Provedor de Identidade|
| dc.services.visualstudio.com| 80/443|Relatórios de Falhas|
| management.azure.com|80/443| API de Serviços do Azure |

### <a name="nuget"></a>NuGet

| Domain | Porta(s)|Finalidade|
| ----------------------|------------------|------------------|
| api.nuget.org | 80/443|API do NuGet|
| secure.aadcdn.microsoftonline-p.com |80/443| Provedor de Identidade|

### <a name="android-projects"></a>Projetos do Android

| Domain| Finalidade|
| ------------------------------------|------------------------------------|
| time.android.com| Servidor de Horário para o Android Emulator |
| connectivitycheck.gstatic.com | Conectividade para o Android Emulator|
| cloudconfig.googleapis.com| APIs para o Android Emulator|

## <a name="see-also"></a>Consulte também

- [Instalar e usar o Visual Studio 2017 e os Serviços do Azure atrás de um firewall ou servidor proxy](/visualstudio/install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server)
- [Solucionar problemas semelhantes no Windows](/visualstudio/install/troubleshooting-network-related-errors-in-visual-studio)
