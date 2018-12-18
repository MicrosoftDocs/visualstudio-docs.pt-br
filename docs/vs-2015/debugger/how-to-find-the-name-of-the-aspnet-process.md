---
title: 'Como: localizar o nome do processo do ASP.NET | Microsoft Docs'
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
helpviewer_keywords:
- ASP.NET debugging, ASP.NET process
- ASP.NET process
ms.assetid: 931a7597-b0f0-4a28-931d-46e63344435f
caps.latest.revision: 32
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2ad3bea47bcde0da87bd185fac132c95f26ce4b0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793237"
---
# <a name="how-to-find-the-name-of-the-aspnet-process"></a>Como localizar o nome do processo ASP.NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para anexar a um aplicativo do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] em execução, você precisará saber o nome do processo do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]:  
  
- Se estiver executando o IIS 6.0 ou IIS 7.0, o nome será w3wp.exe.  
  
- Se estiver executando uma versão anterior do IIS, o nome será aspnet_wp.exe.  
  
  Para aplicativos criados usando [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] ou versões posteriores, o [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] código pode residir no sistema de arquivos e executar no servidor de teste WebDev.WebServer.exe. Nesse caso, você deve anexar a WebDev.WebServer.exe em vez do processo do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Essa situação aplica-se somente à depuração local.  
  
  Aplicativos ASP antigos são executados dentro do processo inetinfo.exe do IIS quando ele está sendo executado no processo.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-determine-whether-project-code-resides-on-the-file-system-or-iis"></a>Para determinar se o código de projeto reside no sistema de arquivos ou IIS  
  
1.  No Visual Studio, abra **Gerenciador de soluções** se ele não ainda estiver aberto.  
  
2.  Selecione o nó superior que contém o nome do aplicativo.  
  
3.  Se o **propriedades** título da janela contém um caminho de arquivo, o código do aplicativo reside no sistema de arquivos.  
  
     Caso contrário, o **propriedades** título da janela conterá o nome do site da Web.  
  
### <a name="to-determine-the-iis-version-under-which-the-application-is-running"></a>Para determinar a versão do IIS no qual o aplicativo está sendo executado  
  
1.  Encontre **ferramentas administrativas** e executá-lo. Dependendo do sistema operacional, isso pode ser um ícone dentro **painel de controle**, ou uma entrada de menu que aparece quando você clica **iniciar**.  
  
     No Windows XP, **painel de controle** podem estar no modo de exibição de categoria ou modo de exibição clássico. No modo de exibição de categoria, você precisa clicar **alternar para modo de exibição clássico** ou **desempenho e manutenção** para ver os **ferramentas administrativas** ícone.  
  
2.  Partir **ferramentas administrativas**, execute os serviços de informações da Internet. Uma caixa de diálogo do MMC é exibida.  
  
3.  Se houver mais de um computador listado no painel esquerdo, selecione o computador no qual o código do aplicativo reside.  
  
4.  A versão do IIS está no **versão** coluna do painel direito.  
  
## <a name="see-also"></a>Consulte também  
 [Pré-requisitos para aplicativos Web de depuração remota](../debugger/prerequistes-for-remote-debugging-web-applications.md)   
 [Requisitos de sistema](../debugger/aspnet-debugging-system-requirements.md)   
 [Preparando para depurar ASP.NET](../debugger/preparing-to-debug-aspnet.md)   
 [Depurando aplicativos Web e script](../debugger/debugging-web-applications-and-script.md)



