---
title: Ferramentas do Visual Studio para cenários de instalação do Office Runtime
description: Saiba como você pode instalar o tempo de execução das ferramentas do Visual Studio 2010 para Office. Este artigo descreve três cenários de instalação.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, installation scenarios
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 671d8e929ebef1085f0bf2aedad2a3280c36514c
ms.sourcegitcommit: f430d014f912aa7874e1db65026dc72688b973e4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111448331"
---
# <a name="visual-studio-tools-for-office-runtime-installation-scenarios"></a>Ferramentas do Visual Studio para cenários de instalação do Office Runtime

  Você pode instalar o tempo de execução das ferramentas do Visual Studio 2010 para Office de três maneiras:

- Quando você instala o Visual Studio.

- Quando você instala o Microsoft Office.

- Quando você instala o Visual Studio 2010 Tools for Office Runtime Redistributable.

  Os componentes de tempo de execução instalados dependem da configuração do computador e do cenário de instalação.

## <a name="runtime-components-that-are-installed-in-each-installation-scenario"></a>Componentes de tempo de execução instalados em cada cenário de instalação

 O tempo de execução das ferramentas do Visual Studio 2010 para Office tem três componentes: o carregador de soluções do Office, as extensões do Office para o .NET Framework 3,5 e as extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior. Quando você instala o tempo de execução, o carregador de solução do Office é sempre instalado. A instalação das extensões do Office para o .NET Framework depende da configuração do computador e do cenário de instalação. Se uma das extensões do Office não puder ser instalada quando o tempo de execução for instalado pela primeira vez, o tempo de execução instalará automaticamente as extensões ausentes do Office posteriormente, quando determinados requisitos forem atendidos. Esse recurso do tempo de execução é chamado *instalação sob demanda*.

 A tabela a seguir mostra quais componentes de tempo de execução são instalados por padrão em cada cenário de instalação de tempo de execução. Mais informações sobre cada cenário são exibidas posteriormente.

|Cenário de instalação de tempo de execução|Carregador de solução do Office|Extensões do Office para o .NET Framework 3,5|Extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]|Extensões do Office para o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]|
|-----------------------------------|----------------------------|--------------------------------------------------| - |---------------------------------------------------------------------------|
|Com [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] e posterior|Sim|Sim, se o .NET Framework 3,5 já estiver instalado.|Sim|Sim|
|Com [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|Sim|Sim, se o .NET Framework 3,5 já estiver instalado.|Não|Não|
|Com o Office 2010 Service Pack 1 (SP1) ou posterior|Sim|Sim, se o .NET Framework 3,5 já estiver instalado.|Sim, se o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] já estiver instalado.|Não|
|Com o Office 2013 e mais recente|Sim|Sim, se o .NET Framework 3,5 já estiver instalado|Sim, se o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] já estiver instalado.|Sim, se o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] já estiver instalado.|
|Com o tempo de execução redistribuível|Sim|Sim, se o .NET Framework 3,5 já estiver instalado|Sim, se o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] já estiver instalado.|Sim, se o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] já estiver instalado.|

### <a name="install-the-runtime-with-visual-studio-or-the-microsoft-office-developer-tools-for-visual-studio"></a>Instalar o tempo de execução com o Visual Studio ou o Microsoft Office Developer Tools para Visual Studio

 Quando você instala o Office Developer Tools no Visual Studio, as extensões do Office para o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] e o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] são sempre instalados no computador de desenvolvimento. As extensões do Office para o .NET Framework 3,5 serão instaladas somente se o .NET Framework 3,5 já estiver presente no computador de desenvolvimento. Se você instalar o .NET Framework 3,5 depois de instalar o [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] , o tempo de execução instalará automaticamente as extensões do Office para o .NET Framework 3,5 na primeira vez que você criar um projeto do Office que tenha como alvo o .NET Framework 3,5.

> [!WARNING]
> Você não pode criar um projeto do Office que tenha como destino o .NET Framework 3,5 usando o [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] ou posterior.

 Para obter mais informações sobre como instalar o Office Developer Tools, consulte [como configurar um computador para desenvolver soluções do Office](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md).

### <a name="install-the-runtime-with-office"></a>Instalar o tempo de execução com o Office

 Quando você instalar o Office, as extensões do Office para o .NET Framework 3,5 serão instaladas se o .NET Framework 3,5 já estiver presente no computador. Se você instalar o .NET Framework 3,5 após o Office, o tempo de execução instalará automaticamente as extensões do Office para o .NET Framework 3,5 na primeira vez que um aplicativo do Office tentar carregar uma solução que tem como alvo o .NET Framework 3,5.

 As extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior também são instaladas com o Office se as versões correspondentes do .NET Framework já estiverem presentes no computador.

 Para garantir que os usuários tenham as extensões necessárias para usar seu aplicativo, inclua a versão mais recente do Visual Studio 2010 Tools for Office Runtime Redistributable como um pré-requisito para sua solução. Para obter mais informações sobre os pré-requisitos, consulte [pré-requisitos da solução do Office para implantação](/previous-versions/bb608617(v=vs.110)).

### <a name="install-the-runtime-by-using-the-runtime-redistributable"></a>Instalar o tempo de execução usando o tempo de execução Redistributable

 Você pode instalar o tempo de execução executando o Visual Studio 2010 Tools for Office Runtime Redistributable manualmente ou incluindo o redistribuível como um pré-requisito ao implantar uma solução do Office.

 Quando você instala o tempo de execução usando o Visual Studio 2010 Tools for Office Runtime Redistributable, as extensões do Office para o .NET Framework 3,5 e as extensões do Office para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior são instaladas se as versões correspondentes do .NET Framework já estiverem presentes no computador. Se o computador não tiver uma dessas versões do .NET Framework quando o tempo de execução for instalado, as extensões do Office para a versão ausente do .NET Framework não serão instaladas nesse momento. Se você instalar a versão ausente do .NET Framework mais tarde, o tempo de execução instalará automaticamente as extensões do Office correspondentes na próxima vez que uma solução que requer as extensões for instalada (se o tempo de execução tiver sido instalado com uma solução implantada usando o ClickOnce) ou carregado (se o tempo de execução tiver sido instalado com uma solução implantada usando Windows Installer).

 Para obter mais informações sobre como incluir pré-requisitos em uma solução ClickOnce, consulte [como instalar pré-requisitos em computadores de usuários finais para executar soluções do Office](/previous-versions/bb608608(v=vs.110)). Para obter mais informações sobre como instalar o tempo de execução do pacote redistribuível manualmente, consulte [como instalar o ferramentas do Visual Studio para o Office Runtime Redistributable](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md).

## <a name="see-also"></a>Confira também

- [Visão geral do Ferramentas do Visual Studio para Office Runtime](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [Assemblies no Ferramentas do Visual Studio para o tempo de execução do Office](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)
