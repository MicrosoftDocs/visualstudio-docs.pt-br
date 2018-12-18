---
title: 'Preparação de depuração: Aplicativos Web ASP.NET | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
helpviewer_keywords:
- debugging ASP.NET Web applications
- debugging [Visual Studio], Web applications
ms.assetid: bcfb1080-98d1-42f9-96af-186fb14f232a
caps.latest.revision: 38
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 59f4f3e1db92c5f7b46a9bb9e1e164fc25b01010
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730684"
---
# <a name="debugging-preparation-aspnet-web-applications"></a>Preparação de depuração: aplicativos Web ASP.NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]modelo de site da Web cria um aplicativo de formulário da Web. Quando você cria um site usando esse modelo, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria as configurações padrão para depuração. No **propriedades do projeto** caixa de diálogo, você pode especificar se deseja que a página da Web seja uma página de inicialização. Quando você inicia a depuração de um [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]Site da Web com essas configurações padrão, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] inicia o Internet Explorer e anexa o depurador para o [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] processo de trabalho (aspnet_wp.exe ou w3wp.exe). Para obter mais informações, consulte [System Requirements](../debugger/aspnet-debugging-system-requirements.md).  
  
### <a name="to-create-a-web-forms-application"></a>Para criar um aplicativo de Web Forms  
  
1.  Sobre o **arquivo** menu, escolha **New Web Site**.  
  
2.  No **New Web Site** caixa de diálogo, selecione [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] **Site da Web**.  
  
3.  Clique em **OK**.  
  
### <a name="to-debug-your-web-form"></a>Para depurar seu Web form  
  
1.  Defina um ou mais pontos de interrupção em suas funções e manipuladores de eventos.  
  
     Para obter mais informações, consulte [pontos de interrupção e Tracepoints](http://msdn.microsoft.com/en-us/fe4eedc1-71aa-4928-962f-0912c334d583).  
  
2.  Quando um ponto de interrupção é atingido, insira o código na função. Observe a execução do código até isolar o problema.  
  
     Para obter mais informações, consulte [Stepping](http://msdn.microsoft.com/en-us/8791dac9-64d1-4bb9-b59e-8d59af1833f9) e [Depurando aplicativos da Web e Script](../debugger/debugging-web-applications-and-script.md).  
  
## <a name="changing-default-configurations"></a>Alterar Configurações padrão  
 Se você quiser alterar a depuração padrão e liberar as configurações criadas pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], poderá fazer isso. Para obter mais informações, consulte [Como definir configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md).  
  
#### <a name="to-change-the-default-debug-configuration"></a>Para alterar a configuração de depuração padrão  
  
1.  Na **Gerenciador de soluções**, o site da Web com o botão direito e selecione **páginas de propriedades** para abrir o **páginas de propriedade** caixa de diálogo.  
  
2.  Clique em **opções de inicialização**.  
  
3.  Definir **iniciar ação** à página da Web deve ser exibida primeiro.  
  
4.  Sob **depuradores**, verifique se **depuração ASP.NET** está selecionado.  
  
     Para obter mais informações, consulte [configurações de páginas de propriedade para projetos Web](../debugger/property-pages-settings-for-web-projects.md).  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)   
 [Noções básicas do depurador](../debugger/debugger-basics.md)   
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)



