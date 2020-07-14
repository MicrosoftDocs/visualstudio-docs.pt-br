---
title: Como configurar projetos para terem várias plataformas como destino
ms.date: 11/04/2016
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- projects [Visual Studio], targeting platforms
- platforms, changing target platforms
ms.assetid: affa2392-7aed-45ac-9ffa-1d8e0496d590
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0618d571258817b5e9653a38a7801c2e4d14e687
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284562"
---
# <a name="how-to-configure-projects-to-target-multiple-platforms"></a>Como configurar projetos para terem várias plataformas como destino

O Visual Studio fornece uma maneira de uma solução se destinar a várias plataformas ou arquiteturas de CPU ao mesmo tempo. As propriedades para defini-las são acessadas por meio da caixa de diálogo **Configuration Manager**.

## <a name="target-a-platform"></a>Ter uma plataforma como destino

A caixa de diálogo **Configuration Manager** permite criar e definir configurações e plataformas no nível do projeto e da solução. Cada combinação de destinos e configurações no nível da solução pode ter um conjunto exclusivo de propriedades associadas a ela, permitindo mudar facilmente entre, por exemplo, uma configuração de Versão destinada a uma plataforma [!INCLUDE[vcprx64](../extensibility/internals/includes/vcprx64_md.md)], uma configuração de versão destinada a uma plataforma x86 e uma configuração de Depuração destinada a uma plataforma x86.

1. No menu **Compilar**, clique em **Gerenciador de Configurações**.

2. Na **caixa plataforma de solução ativa**, selecione a plataforma que você deseja que sua solução direcione ou selecione **\<New>** para criar uma nova plataforma. O Visual Studio compilará seu aplicativo para direcionar a plataforma definida como a plataforma ativa na caixa de diálogo **Configuration Manager**.

## <a name="remove-a-platform"></a>Remover uma plataforma

Se perceber que não precisa de uma plataforma, você pode removê-la usando a caixa de diálogo **Gerenciador de Configurações**. Isso removerá todas as configurações de solução e projeto que você definiu para essa combinação de configuração e destino.

1. No menu **Compilar**, clique em **Gerenciador de Configurações**.

2. Na **caixa plataforma de solução ativa**, selecione **\<Edit>** . A caixa de diálogo **Editar Plataformas de Solução** é aberta.

3. Clique na plataforma que deseja remover e clique em **Remover**.

## <a name="target-multiple-platforms-with-one-solution"></a>Ter várias plataformas como destino com uma solução

Uma vez que pode alterar as configurações com base na combinação de definições de plataforma e de configuração, você pode configurar uma solução que pode ter mais de uma plataforma de destino.

### <a name="to-target-multiple-platforms"></a>Para destinar-se a várias plataformas

1. Use o **Configuration Manager** para adicionar pelo menos duas plataformas de destino para a solução.

2. Selecione a plataforma a que deseja se destinar na lista **Plataforma da solução ativa**.

3. Compile a solução.

### <a name="to-build-multiple-solution-configurations-at-once"></a>Para criar várias configurações de solução de uma vez

1. Use o **Configuration Manager** para adicionar pelo menos duas plataformas de destino para a solução.

2. Use a janela **Build em Lotes** para criar várias configurações de solução de uma vez.

   É possível ter uma plataforma de solução definida como, por exemplo, [!INCLUDE[vcprx64](../extensibility/internals/includes/vcprx64_md.md)], e não ter projetos na solução destinados à mesma plataforma. Também é possível ter vários projetos em sua solução, cada um destinado a plataformas diferentes. É recomendável que, se tiver uma dessas situações, você crie uma nova configuração com um nome descritivo para evitar confusão.

## <a name="see-also"></a>Veja também

- [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)
- [Noções sobre configurações de build](../ide/understanding-build-configurations.md)
- [Criar e limpar projetos e soluções no Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
