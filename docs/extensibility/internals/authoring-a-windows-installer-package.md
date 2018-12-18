---
title: Criação de um pacote do Windows Installer | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: edb0a1d385129600372fc26693aec729751a768c
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39512862"
---
# <a name="author-a-windows-installer-package"></a>Criar um pacote do Windows Installer
O modelo do Windows Installer unidades de dados. Em vez de escrever um script de procedimento para copiar arquivos e gravar as entradas do registro, por exemplo, você cria linhas e colunas em tabelas de banco de dados que contêm dados de arquivo e registro.  
  
## <a name="database-entries"></a>Entradas de banco de dados  
Para instalar um VSPackage, um pacote do Windows Installer deve conter entradas de banco de dados para executar as seguintes tarefas:  
  
- Pesquisar para localizar as versões do sistema [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o VSPackage dá suporte a (usando tabelas do Windows Installer que incluem AppSearch, CompLocator, RegLocator, DrLocator e assinatura).  
  
- Cancelar a instalação, se nenhuma versão com suporte do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] está instalado ou se outro requisito de sistema do VSPackage não for atendido (usando a tabela de LaunchCondition).  
  
- Instale o VSPackage e os arquivos dependentes (usando o diretório, componente e tabelas de arquivo).  
  
- Adicione as informações apropriadas para o VSPackage no registro (usando a tabela de registro).  
  
- Integrar o VSPackage na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] chamando **devenv.exe /setup** (usando a tabela CustomAction).  
  
Para obter mais informações, consulte [Windows Installer](/windows/desktop/Msi/windows-installer-portal).
  
## <a name="setup-tools"></a>Ferramentas de instalação  
Uma variedade de ferramentas de configuração de produtos de terceiros fornecem um ambiente de desenvolvimento para pacotes do Windows Installer. As seguintes ferramentas gratuitas estão disponíveis:  
  
- O InstallShield limited edition  
  
   Você pode obter uma versão limitada do InstallShield por meio do Visual Studio **novo projeto** caixa de diálogo. Expandir **Other Project Types** e, em seguida, selecione **instalação e implantação**. Selecione o modelo do InstallShield.  
  
- Conjunto de ferramentas do Windows Installer XML  
  
   O conjunto de ferramentas do Windows Installer XML (WiX) compila pacotes do Windows Installer XML dos arquivos de origem. O conjunto de ferramentas WiX é um projeto de código-fonte aberto da Microsoft. Você pode baixar o código-fonte e os executáveis do [conjunto de ferramentas Wix](http://sourceforge.net/projects/wix).  
  
   Para os produtos comerciais que se integram [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usando o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)], consulte [ http://visualstudiogallery.com ](http://visualstudiogallery.com/).  
  
## <a name="see-also"></a>Consulte também  
 [Instalar VSPackages com o Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)