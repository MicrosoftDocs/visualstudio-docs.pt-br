---
title: Especificando o caminho para ferramentas de linha de comando de ferramentas de criação de perfil | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 7047bf18-5779-4f6e-872c-66e2fc47c969
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1afb0b00a7e121c611dedbc235684a67cc9cec53
ms.sourcegitcommit: 1b9c1e333c2f096d35cfc77e846116f8e5054557
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814489"
---
# <a name="specify-the-path-to-profiling-tools-command-line-tools"></a>Especificar o caminho para as ferramentas de linha de comando das Ferramentas de Criação de Perfil
O caminho das ferramentas de linha de comando das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] não é adicionado à variável de ambiente PATH. Em computadores de 32 bits, as ferramentas permanecem em um único diretório. Existem versões de 32 e 64 bits das ferramentas de criação de perfil em computadores de 64 bits.  
  
## <a name="32-bit-computers"></a>Computadores 32 bits  
 Em computadores de 32 bits, o diretório padrão das ferramentas do criador de perfil é *drive\Program Files\Microsoft Visual Studio 11.0\Team Tools\Performance Tools*.  
  
## <a name="64-bit-computers"></a>Computadores de 64 bits  
 Em computadores de 64 bits, especifique o caminho de acordo com a plataforma de destino do aplicativo cujo perfil foi criado.  
  
-   No caso de aplicativos de 32 bits, o diretório padrão das ferramentas de criação de perfil é:  
  
     *drive\Program Files (x86)\Microsoft Visual Studio 11.0\Team Tools\Performance Tools*  
  
-   No caso de aplicativos de 64 bits, o diretório padrão das ferramentas de criação de perfil é:  
  
     *drive\Program Files (x86)\Microsoft Visual Studio 11.0\Team Tools\Performance Tools\x64*