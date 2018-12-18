---
title: Adicionando dados de interação de camadas da linha de comando | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- tier interaction profiling method
- profiling tools,tier interaction method
ms.assetid: 5a35647f-03f2-4555-8eeb-fda7e0080e67
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b3912e823a6e6ee32488fcda94616aef414d3d22
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51775297"
---
# <a name="adding-tier-interaction-data-from-the-command-line"></a>Adicionando dados de interação entre camadas da linha de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A criação de perfil de interação de camadas fornece informações adicionais sobre os tempos de execução síncronos que o [!INCLUDE[vstecado](../includes/vstecado-md.md)] chama em funções de aplicativos de várias camadas que se comunicam com um ou mais bancos de dados.  
  
 **Windows 8 e Windows Server 2012**  
  
 Para coletar dados de interação de camadas em aplicativos da área de trabalho do Windows 8 e do Windows Server 2012, você deve usar o método de instrumentação. Não há suporte para a coleta de dados de interação de camadas nos aplicativos da Windows Store.  
  
 **Edições do Visual Studio**  
  
 A criação de perfil de interação de camadas pode ser coletada usando [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] ou [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)]. No entanto, os dados de criação de perfil de interação de camadas somente podem ser exibidos no [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] e no [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)].  
  
 **Coletando dados TIP em um computador remoto**  
  
 Para coletar dados de interação de camadas em um computador remoto, você deve copiar o **vs\_profiler\_**_\<Platform >_ **\_**  _\<Language >_**.exe** arquivo o _% VSInstallDir %_**\Team Tools\Performance Tools\Setups**pasta de um Visual Studio de máquina para o computador remoto e instalá-lo. Você não pode usar as ferramentas de criação de perfil na [as ferramentas remotas do Visual Studio](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c) fazer download do pacote.  
  
 **Relatórios TIP**  
  
 Os dados de interação de camadas somente podem ser exibidos no IDE do [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]. Os relatórios de interação de camadas baseados em arquivo por meio de [VSPerfReport](../profiling/vsperfreport.md) não estão disponíveis.  
  
## <a name="adding-tier-interaction-data-with-vsperfcmd"></a>Adicionando dados de interação de camadas com VSPerfCmd  
 A ferramenta de linha de comando VSPerfASPNETCmd permite acessar toda a funcionalidade disponível nas Ferramentas de Criação de Perfil. Para adicionar interação de camadas a dados de criação de perfil coletados usando VSPerfCmd, você deve usar o utilitário **VSPerfCLREnv** para definir e remover as variáveis de ambiente que permitem dados de interação de camadas. As opções que você especificar e os procedimentos necessários para coletar dados dependem do tipo de aplicativo cujo perfil está sendo criado.  
  
### <a name="profiling-stand-alone-applications"></a>Criando perfil de aplicativos autônomos  
 Para adicionar dados de interação de camadas a um aplicativo que não é executado por outro processo, como um aplicativo da área de trabalho do Windows que faz chamadas do [!INCLUDE[vstecado](../includes/vstecado-md.md)] síncronas para um banco de dados do SQL Server, use a opção **VSPerfClrEnv /InteractionOn** para definir as variáveis de ambiente e a opção **VSPerfClrEnv /InteractionOff** para removê-las.  
  
 No exemplo a seguir, um aplicativo de área de trabalho do Windows tem o perfil criado usando o método de instrumentação e dados de interação de camadas são coletados.  
  
##### <a name="profiling-a-windows-desktop-application-example"></a>Um exemplo de criação de perfil de um aplicativo da área de trabalho do Windows  
  
1. Abra uma janela de prompt de comando com privilégios de administrador. Clique em **Iniciar**, aponte para **Todos os Programas** e, em seguida, aponte para **Acessórios**. Clique com o botão direito do mouse em **Prompt de Comando** e, em seguida, clique em **Executar Como Administrador**.  
  
2. Inicialize a criação de perfil do .NET e as variáveis de ambiente TIP. Digite os seguintes comandos:  
  
   ```  
   vsperfclrenv /traceon  
   vsperfclrenv /interactionon  
   ```  
  
3. Inicie o criador de perfil. Digite o seguinte comando:  
  
   ```  
   vsperfcmd /start:trace /output:Desktop_tip.vsp   
   ```  
  
4. Inicie o aplicativo com VSPerfCmd. Digite o seguinte comando:  
  
   ```  
   vsperfcmd /launch:DesktopApp.exe  
   ```  
  
5. Utilize o aplicativo para coletar dados de criação de perfil e, em seguida, feche o aplicativo da maneira normal.  
  
6. Limpe as variáveis de ambiente TIP. Digite o seguinte comando:  
  
   ```  
   vsperfclrenv /off  
   ```  
  
   Para obter mais informações, consulte [Criando perfil de aplicativos autônomos](../profiling/command-line-profiling-of-stand-alone-applications.md).  
  
### <a name="profiling-services"></a>Serviços de criação de perfil  
 Para criar perfil de serviços, incluindo aplicativos [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], use a opção **VSPerfClrEnv /GlobalInteractionOn** para definir as variáveis de ambiente e a opção **VSPerfClrEnv /GlobalInteractionOff** para removê-las.  
  
 Para criar perfil de serviços, incluindo aplicativos Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], geralmente é necessário reiniciar o computador para habilitar a criação de perfil.  
  
 No exemplo a seguir, um serviço Windows tem o perfil criado usando o método de instrumentação e dados de interação de camadas são coletados.  
  
##### <a name="profiling-a-windows-service-example"></a>Exemplo de criação de perfil de um serviço Windows  
  
1. Se necessário, instale o serviço.  
  
2. Abra uma janela de prompt de comando com privilégios de administrador. Clique em **Iniciar**, aponte para **Todos os Programas** e, em seguida, aponte para **Acessórios**. Clique com o botão direito do mouse em **Prompt de Comando** e, em seguida, clique em **Executar Como Administrador**.  
  
3. Inicialize as variáveis de ambiente de criação de perfil do .NET. Digite o seguinte comando:  
  
   ```  
   vsperfclrenv /globaltraceon  
   ```  
  
4. Inicialize as variáveis de ambiente TIP. Digite o seguinte comando  
  
   ```  
   vsperfclrenv /globalinteractionon  
   ```  
  
5. Reinicie o computador para registrar as variáveis de ambiente.  
  
6. Abra uma janela de prompt de comando com privilégios de administrador.  
  
7. Inicie o criador de perfil. Digite o seguinte comando:  
  
   ```  
   vsperfcmd /start:trace /output:MiddleTier_tip.vsp /user:SYSTEM /crosssession   
   ```  
  
8. Se necessário, inicie o serviço.  
  
9. Anexe o criador de perfil ao serviço. Digite o seguinte comando:  
  
    ```  
    vsperfcmd /attach:MiddleTier.exe /output:MyService_tip.vsp /user:SYSTEM /crosssession   
    ```  
  
10. Utilize o serviço e colete dados de criação de perfil.  
  
11. Pare o criador de perfil. Digite o seguinte comando:  
  
     `vsperfcmd /detach`  
  
12. Limpe as variáveis de ambiente de criação de perfil do .NET e TIP. Digite o seguinte comando:  
  
    ```  
    vsperfclrenv /globaloff  
    ```  
  
13. Reinicie o computador para registrar as variáveis de ambiente limpas.  
  
    Para obter mais informações, consulte um dos seguintes tópicos:  
  
    [Criando perfil de aplicativos Web ASP.NET](../profiling/command-line-profiling-of-aspnet-web-applications.md)  
  
    [Serviços de Criação de Perfil](../profiling/command-line-profiling-of-services.md)  
  
## <a name="adding-tier-interaction-data-with-vsperfaspnetcmd"></a>Adicionando dados de interação de camadas com VSPerfASPNETCmd  
 A ferramenta de linha de comando VSPerfASPNETCmd permite criar facilmente o perfil de aplicativos Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)]. Em comparação com a ferramenta de linha de comando **VSPerfCmd**, as opções são reduzidas, nenhuma variável de ambiente precisa ser definida e não é necessário reinicializar o computador. Esses recursos do VSPerfASPNETCmd deixam extremamente fácil a coleta de dados de interação de camadas.  
  
 Para adicionar interação de camadas a dados de criação de perfil coletados usando o VSPerfASPNETCmd, adicione a opção **/TIP** na linha de comando. Por exemplo, use a linha de comando a seguir para coletar dados de interação de um aplicativo Web do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], usando o método de instrumentação:  
  
```  
vsperfaspnetcmd /tip /trace http://localhost/MyWebApp  
```  
  
 Para obter mais informações sobre o VSPerfASPNETCmd, consulte [Criação de perfil do site rápida com VSPerfASPNETCmd](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md).



