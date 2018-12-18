---
title: Gerenciamento de componente | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 00a6ea41d631c171700db75361b7aa0beed81cc2
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39510862"
---
# <a name="component-management"></a>Gerenciamento de componente
Unidades de tarefas no instalador do Windows são chamadas de componentes do Windows Installer (às vezes chamados de WICs ou apenas componentes). Um GUID que identifica cada WIC, que é a unidade básica de instalação e a contagem de referências para instalações que usam o Windows Installer.  
  
 Embora você possa usar vários produtos para criar seu instalador VSPackage, essa discussão supõe o uso do Windows Installer (*. msi*) arquivos. Ao criar seu instalador, você deve gerenciar corretamente implantação de arquivos para que a contagem de referência correta ocorra em todos os momentos. Consequentemente, versões diferentes do seu produto não interferir com ou interromperá uns aos outros em uma mistura de instalação e desinstalação de cenários.  
  
 No Windows Installer, a contagem de referência ocorre no nível do componente. Cuidadosamente, você deve organizar seus recursos — arquivos, entradas do registro e assim por diante — em componentes. Há outros níveis da organização — como módulos, recursos e produtos — que pode ajudar em cenários diferentes. Para obter mais informações, consulte [Noções básicas do Windows Installer](../../extensibility/internals/windows-installer-basics.md).  
  
## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>Diretrizes de criação de instalação para instalação lado a lado  
  
-   Arquivos de autor e chaves do registro que são compartilhadas entre versões em seus próprios componentes.  
  
     Isso permite que você facilmente consumi-los na próxima versão. Por exemplo, as bibliotecas de tipos que são registradas globalmente, extensões de arquivo, outros itens registrados no **HKEY_CLASSES_ROOT**e assim por diante.  
  
-   Agrupe componentes compartilhados em módulos de mesclagem separado.  
  
     Essa estratégia ajuda você autor corretamente para a instalação lado a lado seguindo em frente.  
  
-   Instale arquivos compartilhados e chaves do registro, usando os mesmos componentes do Windows Installer entre versões.  
  
     Se você usar um componente diferente, arquivos e entradas do registro são desinstaladas quando um VSPackage de controle de versão é desinstalado, mas outra VSPackage ainda está instalado.  
  
-   Não misture os itens com controle de versão e compartilhados no mesmo componente.  
  
     Isso torna impossível instalar itens compartilhados em um local global e os itens com controle de versão para locais isolados.  
  
-   Não tem chaves de registro compartilhadas que apontam para arquivos com controle de versão.  
  
     Se você fizer isso, as chaves compartilhadas serão substituídas quando outro VSPackage de controle de versão está instalada. Depois de remover a segunda versão, o arquivo ao qual a chave está apontando não existe mais.  
  
## <a name="see-also"></a>Consulte também  
 [Escolher entre VSPackages compartilhados e com controle de versão](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)   
 [Cenários de instalação do VSPackage](../../extensibility/internals/vspackage-setup-scenarios.md)