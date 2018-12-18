---
title: Como criar e editar configurações | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- solution build configurations, editing
- build configurations, creating
- solution build configurations, creating
- build configurations, editing
- builds [Visual Studio], setting up
- property pages
- Configuration Manager
- project build configurations, creating
- project build configurations, editing
ms.assetid: 19be121c-148e-4ece-bbfc-d20b08cfc3f7
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f171c337f73db495b7b71aded24f669b6e613a07
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887781"
---
# <a name="how-to-create-and-edit-configurations"></a>Como criar e editar configurações de teste
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível compilar várias configurações de build para uma solução. Por exemplo, é possível configurar um build de depuração que seus testadores podem usar para localizar e corrigir problemas, e é possível configurar diferentes tipos de builds que podem ser distribuídos a diferentes clientes.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="creating-build-configurations"></a>Criando configurações de build  
 É possível usar a caixa de diálogo **Configuration Manager** ou modificar configurações de build existentes ou compilar novas configurações.  
  
#### <a name="to-open-the-configuration-manager-dialog-box"></a>Para abrir a caixa de diálogo Configuration Manager  
  
- No **Gerenciador de Soluções**, abra o menu de atalho da solução e, em seguida, escolha **Configuration Manager**.  
  
  > [!NOTE]
  >  Se o comando do **Configuration Manager** não for exibido no menu de atalho, procure no menu **Build** na barra de menus. Se ele também não for exibido lá, na barra de menus, escolha **Ferramentas**, **Opções** e, em seguida, no painel esquerdo da caixa de diálogo **Opções**, expanda **Projetos e Soluções**, **Geral** e, no painel direito, marque a caixa de seleção **Mostrar configurações avançadas de build**.  
  
   Na caixa de diálogo **Configuration Manager** é possível usar a lista suspensa **Configuração da solução ativa** para selecionar uma configuração de build em toda a solução, modificar uma existente ou criar uma nova configuração. É possível usar a lista suspensa **Plataforma da solução ativa** para selecionar a plataforma que a configuração define como destino, modificar uma existente ou adicionar uma nova plataforma. O painel **Contextos do projeto** lista os projetos na solução. Para cada projeto, é possível selecionar configuração e plataforma específicas de projeto, modificar existentes ou criar uma nova configuração ou adicionar uma nova plataforma. Também é possível marcar caixas de seleção que indicam se cada projeto está incluído quando você usa a configuração em toda a solução para compilar ou implantar a solução.  
  
  Depois de definir as configurações desejadas, é possível definir as propriedades do projeto adequadas para essas configurações.  
  
#### <a name="to-set-properties-based-on-configurations"></a>Para definir as propriedades com base nas configurações  
  
-   No **Gerenciador de Soluções**, abra o menu de atalho para um projeto e, em seguida, escolha **Propriedades**.  
  
     A janela **Páginas de Propriedades** é aberta.  
  
     É possível definir propriedades para suas configurações. Por exemplo, para uma Configuração de versão, é possível especificar se o código é otimizado quando a solução é criada, e para uma Configuração de depuração, é possível especificar se o símbolo de compilação condicional `DEBUG` está incluído. Para obter mais informações sobre as configurações de página de propriedades, consulte [Introdução ao Designer de Projeto](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).  
  
## <a name="creating-and-modifying-project-configurations"></a>Criando e modificando configurações de projeto  
  
#### <a name="to-create-a-project-configuration"></a>Para criar uma configuração de projeto  
  
1.  Abra a caixa de diálogo **Configuration Manager**.  
  
2.  Selecione um projeto na coluna **Projeto**.  
  
3.  Na lista suspensa **Configuração** desse projeto, escolha **Novo**.  
  
     A caixa de diálogo **Nova Configuração de Projeto** é aberta.  
  
4.  Na caixa **Nome**, insira um nome para a nova configuração.  
  
5.  Para usar as configurações de propriedade com base em uma configuração de projeto existente, na lista suspensa **Copiar configurações de**, escolha uma configuração.  
  
6.  Para criar uma configuração em toda a solução ao mesmo tempo, a marque a caixa de seleção **Criar nova configuração de solução**.  
  
#### <a name="to-rename-a-project-configuration"></a>Para renomear uma configuração de projeto  
  
1.  Abra a caixa de diálogo **Configuration Manager**.  
  
2.  Na coluna **Projeto**, selecione o projeto que tenha a configuração de projeto que você deseja renomear.  
  
3.  Na lista suspensa **Configuração** desse projeto, escolha **Editar**.  
  
     A caixa de diálogo **Editar Configurações de Projeto** é aberta.  
  
4.  Selecione o nome de configuração de projeto que você deseja alterar.  
  
5.  Selecione **Renomear** e, em seguida, digite um novo nome.  
  
## <a name="creating-and-modifying-solution-wide-build-configurations"></a>Criando e modificando configurações de build em toda a solução  
  
#### <a name="to-create-a-solution-wide-build-configuration"></a>Para compilar uma configuração de build em toda a solução  
  
1.  Abra a caixa de diálogo **Configuration Manager**.  
  
2.  Na lista suspensa **Configuração da solução ativa**, escolha **Nova**.  
  
     A caixa de diálogo **Nova configuração de solução** é aberta.  
  
3.  Na caixa de texto **Nome**, insira um nome para a nova configuração.  
  
4.  Para usar as configurações de uma configuração de solução existente, na lista suspensa **Copiar configurações de**, escolha uma configuração.  
  
5.  Se você desejar criar configurações de projeto ao mesmo tempo, marque a caixa de seleção **Criar novas configurações de projeto**.  
  
#### <a name="to-rename-a-solution-wide-build-configuration"></a>Para renomear uma configuração de build em toda a solução  
  
1.  Abra a caixa de diálogo **Configuration Manager**.  
  
2.  Na lista suspensa **Configuração da Solução Ativa**, escolha **Editar**.  
  
     A caixa de diálogo **Editar Configurações da Solução** é aberta.  
  
3.  Selecione o nome de configuração da solução que você deseja alterar.  
  
4.  Selecione **Renomear** e, em seguida, digite um novo nome.  
  
#### <a name="to-modify-a-solution-wide-build-configuration"></a>Para modificar uma configuração de build em toda a solução  
  
1.  Abra a caixa de diálogo **Configuration Manager**.  
  
2.  Na lista suspensa **Configuração da solução ativa**, selecione a configuração desejada.  
  
3.  No painel **Contextos do projeto**, para cada projeto, selecione a **Configuração** e a **Plataforma** desejadas e selecione se deseja **Compilá-la** e se deseja **Implantá-la**.  
  
## <a name="see-also"></a>Consulte também  
 [Noções sobre configurações de build](../ide/understanding-build-configurations.md)   
 [Compilando e limpando projetos e soluções no Visual Studio](../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)   
 [NIB: como modificar as propriedades do projeto e as definições de configuração](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)



