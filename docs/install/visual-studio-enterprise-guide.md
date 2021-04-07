---
title: Guia do Visual Studio para empresas
description: Configurar e solucionar problemas do Visual Studio em um ambiente corporativo.
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: overview
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: ''
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e5e8a28ac89c2bea85aee8323060bf948266ad2e
ms.sourcegitcommit: 56060e3186086541d9016d4185e6f1bf3471e958
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2021
ms.locfileid: "106547382"
---
# <a name="visual-studio-enterprise-guide"></a>Guia do Visual Studio para empresas
Se você estiver procurando economizar tempo enquanto está fazendo sua empresa em execução no Visual Studio, comece aqui. Este guia da empresa inclui dicas que podem ajudá-lo a instalar e atualizar o Visual Studio em cenários empresariais comuns, ficar desbloqueado se você tiver problemas e aprender a relatar um problema se precisar de mais ajuda. 

## <a name="get-started"></a>Introdução 
Saiba como implantar o Visual Studio em sua empresa em ambientes de rede e offline.

- **[Habilitar atualizações do administrador usando o Microsoft Endpoint Configuration Manager (SCCM)](enabling-administrator-updates.md)**.  As atualizações do Visual Studio estão incluídas no [catálogo Microsoft Update](https://www.catalog.update.microsoft.com/Home.aspx) e no [Windows Server Update Services (WSUS)](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus). Os administradores corporativos podem baixar a atualização e distribuí-la para computadores cliente do Visual Studio em toda a organização usando ferramentas de implantação padrão, como o Microsoft Endpoint Configuration Manager (SCCM).

- **Entenda as opções de implantação empresarial em ambientes de rede**. O [Guia do administrador do Visual Studio](visual-studio-administrator-guide.md) fornece diretrizes baseadas em cenários para administradores do sistema. 

- **[Obtenha dicas de solução de problemas](troubleshooting-installation-issues.md)**. Obtenha ajuda quando estiver instalando ou atualizando o Visual Studio e saiba como relatar um problema se você estiver bloqueado. Essas dicas incluem instruções passo a passo que devem resolver a maioria dos problemas de instalação online ou offline. 

- **[Crie uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)**. Se você não estiver conectado à Internet ou tiver conectividade limitada com a Internet, encontre opções para instalar o Visual Studio. 

- **[Criar pacotes de bootstrapper](../deployment/creating-bootstrapper-packages.md)**. Saiba como criar pacotes de bootstrapper personalizados criando manifestos de produto e pacote. 

- **[Aplicar automaticamente as chaves do produto ao implantar o Visual Studio](automatically-apply-product-keys-when-deploying-visual-studio.md)**. É possível aplicar a chave do produto (Product Key) de forma programática como parte de um script usado para automatizar a implantação do Visual Studio. Você pode definir uma chave do produto (Product Key) em um dispositivo de forma programática, seja durante uma instalação do Visual Studio ou após a conclusão da instalação. 

## <a name="install-visual-studio"></a>Instalar o Visual Studio 

Saiba como instalar o Visual Studio em cenários empresariais comuns. 

- **[Use parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)**. Use uma variedade de parâmetros para controlar ou personalizar a instalação do Visual Studio. Automatize o processo de instalação ou crie um cache dos arquivos de instalação para uso posterior. Para obter mais informações, consulte [exemplos de parâmetro de linha de comando](command-line-parameter-examples.md).

- **[Crie uma instalação de rede do Visual Studio](create-a-network-installation-of-visual-studio.md)**. Armazene em cache os arquivos para a instalação inicial junto com todas as atualizações de produto em uma única pasta. 

- **[Instalar e usar o Visual Studio e os serviços do Azure por trás de um firewall ou servidor proxy](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)**. Se sua organização usa medidas de segurança como um firewall ou um servidor proxy, há URLs de domínio que você talvez queira adicionar a uma "lista de permissões" e portas e protocolos que você talvez queira abrir para que tenha a melhor experiência ao instalar e usar o Visual Studio e os serviços do Azure. 

- **[Instale os certificados necessários para a instalação offline](../install/install-certificates-for-visual-studio-offline.md)**. Instale os certificados necessários se o computador cliente estiver completamente desconectado da Internet.

## <a name="update-visual-studio"></a>Atualizar o Visual Studio 

Saiba como atualizar o Visual Studio com êxito e corrigir problemas de atualização. 

- **[Aplicar atualizações do administrador usando o Microsoft Endpoint Configuration Manager (SCCM)](../install/applying-administrator-updates.md)**. Saiba mais sobre como distribuir atualizações de recursos, segurança e qualidade do Visual Studio por meio do SCCM. 

- **[Atualize uma instalação baseada em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)**. Atualize um layout de instalação de rede do Visual Studio com as atualizações de produto mais recentes para que ele possa ser usado como um ponto de instalação para a atualização mais recente do Visual Studio e também para manter as instalações já implantadas em estações de trabalho cliente.

- **[Atualize o Visual Studio enquanto estiver em uma linha de base de manutenção](update-servicing-baseline.md)**. Entenda o valor da atualização em uma linha de base e aprenda a diferença entre versões secundárias e atualizações de serviço. 

- **[Atualize o Visual Studio usando um layout mínimo de offline](update-minimal-layout.md)**. Para computadores que não estão conectados à Internet, a criação de um layout mínimo é a maneira mais fácil e rápida de atualizar suas instâncias offline do Visual Studio.

- Repare o **[Visual Studio](repair-visual-studio.md) para corrigir problemas de atualização**. Às vezes, a instalação do Visual Studio é danificada ou corrompida. Um reparo é útil para corrigir problemas de tempo de instalação em todas as operações de instalação, incluindo atualizações. 

- **Siga as [linhas de base de segurança do Windows](/windows/security/threat-protection/windows-security-baselines)**. A Microsoft se dedica a fornecer aos clientes um sistema operacional seguro, como o Windows 10 e o Windows Server, bem como aplicativos seguros, como o Microsoft Edge. Além da garantia de segurança de seus produtos, a Microsoft também fornece vários recursos de configuração para permitir que você tenha o controle preciso dos seus ambientes. 

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também 

- [Guia de produtividade do Visual Studio](../ide/productivity-features.md)

