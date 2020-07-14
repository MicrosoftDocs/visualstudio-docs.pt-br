---
title: Instalar e usar o Visual Studio para Mac por trás de um firewall ou servidor proxy
description: Este documento fornece uma lista de hosts que precisam ser permitidos no firewall para que o Visual Studio para Mac (e suas cargas de trabalho, incluindo Xamarin) funcione em um ambiente corporativo.
ms.assetid: 79C0F1A3-0C13-4E55-A820-1138A4082B77
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.openlocfilehash: 817fce7958ce2b3e4bc3684e639197da8f69e40d
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85938982"
---
# <a name="install-and-use-visual-studio-for-mac-behind-a-firewall-or-proxy-server"></a>Instalar e usar o Visual Studio para Mac por trás de um firewall ou servidor proxy

Se você ou sua organização usa medidas de segurança como um firewall ou um servidor proxy, há domínios que é recomendável adicionar a uma "lista de permissões", além de portas e protocolos que podem ser abertos para que você tenha a melhor experiência ao instalar e usar o Visual Studio para Mac e os Serviços do Azure.

- [**Instalar Visual Studio para Mac**](#install-visual-studio-for-mac): essas tabelas incluem os domínios que devem permitir conectividade para que você tenha acesso a todos os recursos e cargas de trabalho do Visual Studio para Mac.

- [**Usar Visual Studio para Mac**](#use-visual-studio-for-mac): essas tabelas incluem domínios que devem permitir conectividade para que você tenha acesso aos recursos relacionados.

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
| static.xamarin.com | Pacotes do Instalador|
| dl.xamarin.com | Pacotes do Instalador|
| dc.services.visualstudio.com| Relatórios de Falhas |

### <a name="third-party-domains"></a>Domínios de terceiros

| Domain| Finalidade |
| --------------------------|-------------------------|
| dl.google.com | SDK do Android |
| download.oracle.com | Java SDK|
| api.apple-cloudkit.com| Serviços de Segurança da Apple |

## <a name="use-visual-studio-for-mac"></a>Usar o Visual Studio para Mac

Para garantir que você tenha acesso a todos os recursos de que precisa no Visual Studio para Mac ao usar um proxy ou firewall, é recomendável adicionar à lista de acesso permitido os domínios e portas a seguir.

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
| login.microsoftonline.com | 80/443| Provedor de identidade|
| Secure.aadcdn.microsoftonline p.com | 80/443|Provedor de identidade|
| dc.services.visualstudio.com| 80/443|Relatórios de Falhas|
| management.azure.com|80/443| API de Serviços do Azure |

### <a name="nuget"></a>NuGet

| Domain | Porta(s)|Finalidade|
| ----------------------|------------------|------------------|
| api.nuget.org | 80/443|API do NuGet|
| Secure.aadcdn.microsoftonline p.com |80/443| Provedor de identidade|

### <a name="android-projects"></a>Projetos do Android

| Domain| Finalidade|
| ------------------------------------|------------------------------------|
| time.android.com| Servidor de Horário para o Android Emulator |
| connectivitycheck.gstatic.com | Conectividade para o Android Emulator|
| cloudconfig.googleapis.com| APIs para o Android Emulator|

## <a name="see-also"></a>Confira também

- [Instalar e usar o Visual Studio e os Serviços do Azure atrás de um firewall ou servidor proxy](/visualstudio/install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server)
- [Solucionar problemas semelhantes no Windows](/visualstudio/install/troubleshooting-network-related-errors-in-visual-studio)
