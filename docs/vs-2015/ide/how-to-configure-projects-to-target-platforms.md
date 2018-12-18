---
title: Como configurar projetos para terem plataformas como destino | Microsoft Docs
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
- project settings [Visual Studio], targeting platforms
- platforms, targeting specific CPUs
- project properties [Visual Studio], targeting platforms
- projects [Visual Studio], targeting platforms
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- CPUs, targeting specific
- 64-bit applications [Visual Studio]
ms.assetid: 845302fc-273d-4f81-820a-7296ce91bd76
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4e2b39aa13316b1b9ca47c5587ffabf6f6a14e68
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49843048"
---
# <a name="how-to-configure-projects-to-target-platforms"></a>Como configurar projetos para destinar plataformas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] permite que você configure seus aplicativos para direcionar as plataformas diferentes, incluindo plataformas de 64 bits. Para obter mais informações sobre o suporte à plataforma de 64 bits no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], consulte [Aplicativos de 64 bits](http://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181).  
  
## <a name="targeting-platforms-with-the-configuration-manager"></a>Definindo plataformas como destino com o Configuration Manager  
 O **Configuration Manager** oferece uma maneira de adicionar rapidamente uma nova plataforma de destino para seu projeto. Se você selecionar uma das plataformas incluídas com [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], as propriedades do projeto serão modificadas para compilar seu projeto para a plataforma selecionada.  
  
#### <a name="to-configure-a-project-to-target-a-64-bit-platform"></a>Para configurar um projeto para ter uma plataforma de 64 bits como destino  
  
1. Na barra de menus, escolha **Build**, **Configuration Manager**.  
  
2. Na lista **Plataforma da solução ativa**, escolha uma plataforma de 64 bits para a solução a ter como destino e, em seguida, escolha o botão **Fechar**.  
  
   1.  Se a plataforma que você deseja não aparecer na lista **Plataforma da Solução Ativa**, escolha **Nova**.  
  
        A caixa de diálogo **Nova Plataforma da Solução** será exibida.  
  
   2.  Na lista **Digitar ou selecionar a nova plataforma**, escolha **x64**.  
  
       > [!NOTE]
       >  Se você der um novo nome à sua configuração, precisará modificar as configurações no **Designer de Projeto** para ter a plataforma correta como destino.  
  
   3.  Se você quiser copiar as configurações de uma configuração de plataforma atual, escolha-a e selecione o botão **OK**.  
  
   As propriedades de todos os projetos que têm a plataforma de 64 bits como destino são atualizadas e o próximo build do projeto será otimizado para plataformas de 64 bits.  
  
## <a name="targeting-platforms-in-the-project-designer"></a>Definindo plataformas como destino no Designer de Projeto  
 O Designer de Projeto também fornece uma maneira de definir diferentes plataformas como destino para seu projeto. Se selecionar uma das plataformas incluídas na lista na caixa de diálogo **Nova Plataforma de Solução** não funcionar para sua solução, você poderá criar um nome de configuração personalizado e modificar as configurações no **Designer de Projeto** para ter a plataforma correta como destino.  
  
 A execução dessa tarefa varia de acordo com a linguagem de programação que você está usando. Consulte os seguintes links para obter mais informações:  
  
-   Para projetos [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], consulte [/platform (Visual Basic)](http://msdn.microsoft.com/library/f9bc61e6-e854-4ae1-87b9-d6244de23fd1).  
  
-   Para projetos [!INCLUDE[csprcs](../includes/csprcs-md.md)], consulte [Página de Build, Designer de Projeto (C#)](../ide/reference/build-page-project-designer-csharp.md).  
  
-   Para projetos [!INCLUDE[vcprvc](../includes/vcprvc-md.md)], consulte [/clr (Compilação do Common Language Runtime)](http://msdn.microsoft.com/library/fec5a8c0-40ec-484c-a213-8dec918c1d6c).  
  
## <a name="see-also"></a>Consulte também  
 [Noções sobre plataformas de build](../ide/understanding-build-platforms.md)   
 [/platform (Opções do Compilador C#)](http://msdn.microsoft.com/library/c290ff5e-47f4-4a85-9bb3-9c2525b0be04)   
 [Aplicativos de 64 bits](http://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181)   
 [Suporte ao IDE do Visual Studio de 64 bits](../ide/visual-studio-ide-64-bit-support.md)



