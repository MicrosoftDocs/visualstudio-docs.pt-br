---
title: Especificando o caminho para ferramentas de linha de comando de ferramentas de criação de perfil | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7047bf18-5779-4f6e-872c-66e2fc47c969
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7fadcff84c4b927a7718d7d4ad1311918ae0f18a
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60066930"
---
# <a name="specifying-the-path-to-profiling-tools-command-line-tools"></a>Especificando o demarcador para ferramentas de linha de comando de ferramentas de criação de perfil
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O caminho das ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não é adicionado à variável de ambiente PATH. Em computadores de 32 bits, as ferramentas permanecem em um único diretório. Existem versões de 32 e 64 bits das ferramentas de criação de perfil em computadores de 64 bits.  
  
## <a name="32-bit-computers"></a>Computadores 32 bits  
 Em computadores de 32 bits, o diretório das ferramentas de criador de perfil padrão é *Unidade*Arquivos de Programas\Microsoft Visual Studio 11.0\Team Tools\Performance Tools.  
  
## <a name="64-bit-computers"></a>Computadores de 64 bits  
 Em computadores de 64 bits, especifique o caminho de acordo com a plataforma de destino do aplicativo cujo perfil foi criado.  
  
- No caso de aplicativos de 32 bits, o diretório padrão das ferramentas de criação de perfil é:  
  
     *Unidade*Arquivos de Programas (x86)\Microsoft Visual Studio 11.0\Team Tools\Performance Tools  
  
- No caso de aplicativos de 64 bits, o diretório padrão das ferramentas de criação de perfil é:  
  
     *Unidade*\Arquivos de Programas (x86)\Microsoft Visual Studio 11.0\Team Tools\Performance Tools\x64
