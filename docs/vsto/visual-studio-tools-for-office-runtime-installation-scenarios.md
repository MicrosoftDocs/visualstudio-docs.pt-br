---
title: Ferramentas do Visual Studio para cenários de instalação de tempo de execução do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, installation scenarios
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ebf335291246ac8c3c15d8f04fb064a3bfaa8ef7
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670891"
---
# <a name="visual-studio-tools-for-office-runtime-installation-scenarios"></a>Ferramentas do Visual Studio para cenários de instalação de tempo de execução do Office
  Você pode instalar o Visual Studio 2010 Tools for Office runtime de três maneiras:  
  
- Quando você instala o Visual Studio.  
  
- Quando você instala o Microsoft Office.  
  
- Quando você instala o Visual Studio 2010 Tools for Office runtime redistribuível.  
  
  Os componentes de tempo de execução que são instalados dependem da configuração do computador e o cenário de instalação.  
  
## <a name="runtime-components-that-are-installed-in-each-installation-scenario"></a>Componentes de tempo de execução que estão instalados em cada cenário de instalação  
 O Visual Studio 2010 Tools for Office runtime tem três componentes: o carregador de solução do Office, as extensões do Office para o .NET Framework 3.5 e extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Quando você instala o tempo de execução, o carregador de solução do Office é sempre instalado. A instalação das extensões do Office para o .NET Framework depende da configuração do computador e o cenário de instalação. Se uma das extensões do Office não pode ser instalada quando o tempo de execução é instalado pela primeira vez, o tempo de execução automaticamente instalará as extensões ausentes do Office mais tarde, quando determinados requisitos forem atendidos. Esse recurso de tempo de execução é chamado *instalação sob demanda*.  
  
 A tabela a seguir mostra quais componentes de tempo de execução são instalados por padrão em cada cenário de instalação do tempo de execução. Para obter mais informações sobre cada cenário é exibido mais tarde.  
  
|Cenário de instalação do tempo de execução|Carregador de solução do Office|Extensões do Office para o .NET Framework 3.5|Extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]|Extensões do Office para o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]|  
|-----------------------------------|----------------------------|--------------------------------------------------| - |---------------------------------------------------------------------------|  
|Com [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] e posterior|Sim|Sim, se o .NET Framework 3.5 já está instalado.|Sim|Sim|  
|com o [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|Sim|Sim, se o .NET Framework 3.5 já está instalado.|Não|Não|  
|Com o Office 2010 Service Pack 1 (SP1) ou posterior|Sim|Sim, se o .NET Framework 3.5 já está instalado.|Sim, se o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] já está instalado.|Não|  
|Com o tempo de execução redistribuível|Sim|Sim, se o .NET Framework 3.5 já está instalado|Sim, se o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] já está instalado.|Sim, se o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] já está instalado.|  
  
### <a name="install-the-runtime-with-visual-studio-or-the-microsoft-office-developer-tools-for-visual-studio"></a>Instalar o tempo de execução com o Visual Studio ou o Microsoft Office Developer Tools para Visual Studio  
 Quando você instala o Office developer tools no Visual Studio, as extensões do Office para o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] e o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] são sempre instaladas no computador de desenvolvimento. As extensões do Office para o .NET Framework 3.5 são instaladas somente se o .NET Framework 3.5 já está presente no computador de desenvolvimento. Se você instalar o .NET Framework 3.5, depois de instalar o [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)], o tempo de execução instala automaticamente as extensões do Office para o .NET Framework 3.5 na primeira vez que você criar um projeto do Office que tem como alvo o .NET Framework 3.5.  
  
> [!WARNING]  
>  Você não pode criar um projeto do Office que tem como alvo o .NET Framework 3.5 usando [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] ou posterior.  
  
 Para obter mais informações sobre como instalar o Office developer tools, consulte [como: configurar um computador para desenvolver soluções do Office](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md).  
  
### <a name="install-the-runtime-with-office"></a>Instalar o tempo de execução com o Office  
 Quando você instala o Office, as extensões do Office para o .NET Framework 3.5 são instaladas se o .NET Framework 3.5 já está presente no computador. Se você instalar o .NET Framework 3.5 depois do Office, o tempo de execução automaticamente instala as extensões do Office pela .NET Framework 3.5 na primeira vez que um aplicativo do Office tenta carregar uma solução que tem como alvo o .NET Framework 3.5.  
  
 Extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou versões posteriores não são instalados com o Office, mesmo se o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior já está presente quando você instala o Office.  
  
 Extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] são instalados com o Office. Os usuários finais podem obter extensões do Office para o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] instalando uma atualização do Windows.  
  
 Para garantir que os usuários tenham as extensões necessárias para usar o aplicativo, inclua a versão mais recente do Visual Studio 2010 Tools para Office runtime redistribuível como um pré-requisito para a sua solução. Para obter mais informações sobre pré-requisitos, consulte [pré-requisitos de solução do Office para implantação](https://msdn.microsoft.com/9f672809-43a3-40a1-9057-397ce3b5126e).  
  
### <a name="install-the-runtime-by-using-the-runtime-redistributable"></a>Instalar o tempo de execução, usando o tempo de execução redistribuível  
 Você pode instalar o tempo de execução, executando o Visual Studio 2010 Tools for Office runtime redistribuível manualmente ou incluindo os pacotes redistribuíveis do como um pré-requisito quando você implanta uma solução do Office.  
  
 Quando você instala o tempo de execução usando o Visual Studio 2010 Tools para Office runtime redistribuível, as extensões do Office para o .NET Framework 3.5 e extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior está instalado se as versões correspondentes do .NET Framework já estão presentes no computador. Se o computador não tiver uma dessas versões do .NET Framework quando o tempo de execução é instalado, as extensões do Office para a versão ausente do .NET Framework não estão instaladas no momento. Se você instalar a versão ausente do .NET Framework mais tarde, o tempo de execução instala automaticamente extensões do Office correspondentes na próxima vez em que uma solução que exija as extensões está instalada (se o tempo de execução foi instalado com uma solução que foi implantada usando o ClickOnce) ou carregado (se o tempo de execução foi instalado com uma solução que foi implantada usando o Windows Installer).  
  
 Para obter mais informações sobre como incluir pré-requisitos em uma solução do ClickOnce, consulte [como: instalar pré-requisitos em computadores de usuário final para executar soluções do Office](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98). Para obter mais informações sobre como instalar o tempo de execução do pacote redistribuível manualmente, consulte [como: instalar o Visual Studio Tools for Office runtime redistribuível](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md)   
 [Assemblies no Visual Studio Tools para Office runtime](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)  
  
  