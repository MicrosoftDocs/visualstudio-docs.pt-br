---
title: Gerenciamento de componentes | Microsoft Docs
description: Saiba como gerenciar componentes do Windows Installer ao criar um instalador do VSPackage no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], components
- installation [Visual Studio SDK], file management
ms.assetid: 029bffa2-6841-4caa-a41a-442467e1aedc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9767af4c30957111526303600f9e8eda815b42f0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057085"
---
# <a name="component-management"></a>Gerenciamento de componentes
As unidades de tarefas no Windows Installer são chamadas de componentes Windows Installer (às vezes chamados de WICs ou apenas componentes). Um GUID identifica cada WIC, que é a unidade básica de instalação e a contagem de referência para as configurações que usam Windows Installer.

 Embora você possa usar vários produtos para criar o instalador do VSPackage, essa discussão pressupõe o uso de arquivos Windows Installer (*. msi*). Ao criar o instalador, você deve gerenciar corretamente a implantação de arquivos para que a contagem de referência correta ocorra em todos os momentos. Consequentemente, versões diferentes do seu produto não interferem ou se interrompem em uma combinação de cenários de instalação e desinstalação.

 No Windows Installer, a contagem de referência ocorre no nível do componente. Você deve organizar seus recursos cuidadosamente — arquivos, entradas de registro e assim por diante — em componentes. Há outros níveis de organização, como módulos, recursos e produtos, que podem ajudar em cenários diferentes. Para obter mais informações, consulte [noções básicas do Windows Installer](../../extensibility/internals/windows-installer-basics.md).

## <a name="guidelines-of-authoring-setup-for-side-by-side-installation"></a>Diretrizes de criação da instalação para instalação lado a lado

- Crie arquivos e chaves do registro que são compartilhados entre versões em seus próprios componentes.

     Isso permite que você os consuma facilmente na próxima versão. Por exemplo, as bibliotecas de tipos que são registradas globalmente, extensões de arquivo, outros itens registrados em **HKEY_CLASSES_ROOT** e assim por diante.

- Agrupe componentes compartilhados em módulos de mesclagem separados.

     Essa estratégia ajuda você a criar corretamente para a instalação lado a lado, avançando.

- Instale arquivos compartilhados e chaves do registro usando os mesmos componentes Windows Installer entre versões.

     Se você usar um componente diferente, os arquivos e as entradas do registro serão desinstalados quando um VSPackage com versão for desinstalado, mas outro VSPackage ainda estiver instalado.

- Não misture itens com versão e compartilhados no mesmo componente.

     Isso torna impossível instalar itens compartilhados em um local global e itens com controle de versão em locais isolados.

- Não têm chaves de registro compartilhadas que apontam para arquivos com versão.

     Se você fizer isso, as chaves compartilhadas serão substituídas quando outro VSPackage com versão for instalado. Depois de remover a segunda versão, o arquivo para o qual a chave está apontando é desaparecido.

## <a name="see-also"></a>Confira também
- [Escolha entre VSPackages compartilhadas e com controle de versão](../../extensibility/choosing-between-shared-and-versioned-vspackages.md)
- [Cenários de instalação do VSPackage](../../extensibility/internals/vspackage-setup-scenarios.md)
