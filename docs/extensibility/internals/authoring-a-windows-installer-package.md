---
title: Criando um pacote de Windows Installer | Microsoft Docs
description: Saiba como criar um pacote de Windows Installer para o Visual Studio que consiste em tabelas de banco de dados que contêm arquivos de registro e arquivo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .msi files, VSPackages
- msi files, VSPackages
ms.assetid: 0ce7c21d-0d3f-47fe-a0bb-eed506e32609
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: afc21237b72d76b73e619740cab0b196e29e928d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078949"
---
# <a name="author-a-windows-installer-package"></a>Criar um pacote de Windows Installer
Os dados orientam o modelo de Windows Installer. Em vez de escrever um script de procedimento para copiar arquivos e gravar entradas do registro, por exemplo, crie linhas e colunas em tabelas de banco de dados que contenham arquivos de registro e arquivo.

## <a name="database-entries"></a>Entradas de banco de dados
Para instalar um VSPackage, um pacote de Windows Installer deve conter entradas de banco de dados para executar as seguintes tarefas:

- Pesquise o sistema para localizar as versões do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] seu VSPackage dão suporte (usando Windows Installer tabelas que incluem AppSearch, CompLocator, RegLocator, DrLocator e Signature).

- Cancele a instalação se nenhuma versão com suporte do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] estiver instalada ou se outro requisito de sistema do VSPackage não for atendido (usando a tabela LaunchCondition).

- Instale o VSPackage e os arquivos dependentes (usando o diretório, o componente e as tabelas de arquivos).

- Adicione as informações apropriadas para o VSPackage ao registro (usando a tabela de registro).

- Integre o VSPackage no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] chamando **devenv.exe/setup** (usando a tabela CustomAction).

Para obter mais informações, consulte [Windows Installer](/windows/desktop/Msi/windows-installer-portal).

## <a name="setup-tools"></a>Ferramentas de instalação
Uma variedade de ferramentas de instalação de terceiros fornece um ambiente de desenvolvimento para pacotes Windows Installer. As seguintes ferramentas gratuitas estão disponíveis:

- Edição limitada do InstallShield

   Você pode obter uma versão limitada do InstallShield por meio da caixa de diálogo **novo projeto** do Visual Studio. Expanda **outros tipos de projeto** e, em seguida, selecione **instalação e implantação**. Selecione o modelo do InstallShield.

- Conjunto de ferramentas XML Windows Installer

   O conjunto de ferramentas do Windows Installer XML (WiX) cria Windows Installer pacotes de arquivos de origem XML. O conjunto de ferramentas do WiX é um projeto de código-fonte aberto da Microsoft. Você pode baixar o código-fonte e os executáveis do [conjunto de ferramentas do WiX](https://sourceforge.net/projects/wix/).

   Para produtos comerciais que se integram ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usando o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] , consulte [Visual Studio Marketplace](https://marketplace.visualstudio.com/).

## <a name="see-also"></a>Confira também
- [Instalar o VSPackages com Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)
