---
title: 'Preparação da depuração: Tipos de projeto do Visual C++ | Microsoft Docs'
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
- C++
helpviewer_keywords:
- project templates, debugging
- Visual C++ projects, debugging
- debug builds, project settings
- debugging [C++]
ms.assetid: 912b4ba2-7719-43d5-b087-db33e3f9329a
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 802b34d47501d3538008838f9bb6ddec93ac827a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752396"
---
# <a name="debugging-preparation-visual-c-project-types"></a>Preparação de depuração: tipos de projeto Visual C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esta seção descreve como depurar os tipos de projeto básicos criados pelos modelos de projeto do [!INCLUDE[vcprvc](../includes/vcprvc-md.md)].  
  
 Observe que esses tipos de projeto que criam dll como suas saídas foram agrupados em [depuração de projetos de DLL](../debugger/debugging-dll-projects.md) devido aos recursos comuns eles compartilham.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [Configurações de propriedade recomendadas](#BKMK_Recommended_Property_Settings)  
  
 [Projetos Win32](#BKMK_Win32_Projects)  
  
- [Para depurar um aplicativo Win32 C ou C++](#BKMK_To_debug_a_C_or_C___Win32_application)  
  
- [Para definir manualmente uma configuração de depuração](#BKMK_To_manually_set_a_Debug_configuration)  
  
  [Aplicativos do Windows Forms (.NET)](#BKMK_Windows_Forms_Applications___NET_)  
  
##  <a name="BKMK_Recommended_Property_Settings"></a> Configurações de propriedade recomendadas  
 Certas propriedades devem ser definidas da mesma maneira para todos os cenários não gerenciados de depuração. As tabelas a seguir exibem as configurações de propriedade recomendadas. As configurações não listadas aqui podem variar entre os tipos de projeto não gerenciados diferentes. Para obter mais informações, consulte [configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)  
  
### <a name="configuration-properties-124-cc-124-optimization-node"></a>Propriedades de configuração &#124; C/C++ &#124; nó de otimização  
  
|Nome da Propriedade|Configuração|  
|-------------------|-------------|  
|**Optimization**|Definido como **desabilitado (/ 0D).** O código otimizado é mais difícil de depurar porque as instruções geradas não correspondem diretamente ao código-fonte. Se você achar que seu programa tem um bug que aparece apenas em código otimizado, você pode ativar essa configuração, mas lembre-se de que o código mostrado na **desmontagem** janela é gerada de origem otimizada que pode não corresponder ao que você vê no seu código-fonte Windows. Outros recursos, como depuração, podem não se comportar como esperado.|  
  
### <a name="configuration-properties-124-linker-124-debugging-node"></a>Propriedades de configuração &#124; vinculador &#124; nó de depuração  
  
|Nome da Propriedade|Configuração|  
|-------------------|-------------|  
|**Gerar informações de depuração**|Você sempre deve definir essa opção como **Sim (/debug)** para criar os arquivos necessários para depuração e símbolos de depuração. Quando o aplicativo entra em produção, você pode defini-lo como desativado.|  
  
 [Neste tópico](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)  
  
##  <a name="BKMK_Win32_Projects"></a> Projetos Win32  
 Os aplicativos Win32 são programas do Windows tradicionais escritos em C ou C++. Depurar esse tipo de aplicativo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é simples.  
  
 Os aplicativos Win32 incluem aplicativos do MFC e projetos do ATL. Eles usam APIs do Windows e podem usar MFC ou ATL, mas não usam Common Language Runtime (CLR). Podem, no entanto, chamar código gerenciado que usa o CLR.  
  
 O procedimento a seguir explica como depurar um projeto do Win32 de dentro do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Outro modo de depurar um aplicativo Win32 é iniciar o aplicativo fora do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e anexar a ele. Para obter mais informações, consulte [anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
###  <a name="BKMK_To_debug_a_C_or_C___Win32_application"></a> Para depurar um aplicativo Win32 C ou C++  
  
1.  Abra o projeto no Visual Studio.  
  
2.  Sobre o **Debug** menu, escolha **iniciar**.  
  
3.  Depuração usando as técnicas discutidas [Noções básicas do depurador](../debugger/debugger-basics.md).  
  
###  <a name="BKMK_To_manually_set_a_Debug_configuration"></a> Para definir manualmente uma configuração de depuração  
  
1. Sobre o **modo de exibição** menu, clique em **páginas de propriedade**.  
  
2. Clique o **propriedades de configuração** nó para abri-lo se ele não ainda estiver  
  
3. Selecione **gerais**e defina o valor da **saída** linha à **depurar**.  
  
4. Abra o **C/C++** nó e selecione **geral**.  
  
    No **depurar** linha que você especifique o tipo de informações de depuração para ser gerado pelo compilador. Você pode escolher os valores incluem **banco de dados do programa (/Zi)** ou **banco de dados do programa para edição & continuar (/ZI)**.  
  
5. Selecione **otimização**e, nas **otimização** linha, selecione **desabilitado (/ 0D)** na lista suspensa.  
  
    O código otimizado é mais difícil de depurar porque as instruções geradas não correspondem diretamente ao código-fonte. Se você descobrir que seu programa tem um bug que aparece apenas em código otimizado, poderá ativar essa configuração, mas lembre-se de que o código mostrado na janela Desmontagem é gerado de origem otimizada que pode não corresponder ao que é visto em suas janelas de origem. Os recursos como o depuração provavelmente mostram incorretamente pontos de interrupção e ponto de execução.  
  
6. Abra o **vinculador** nó e selecione **depuração**. No primeiro **Generate** linha, selecione **Sim (/debug)** na lista suspensa. Sempre defina isso quando você estiver depurando.  
  
   Para obter mais informações, consulte[configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md).  
  
   [Neste tópico](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)  
  
##  <a name="BKMK_Windows_Forms_Applications___NET_"></a> Aplicativos do Windows Forms (.NET)  
 O **aplicativo de formulários do Windows (.NET)** modelo cria um [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] aplicativo Windows Forms. Para obter mais informações, consulte [Como criar um projeto de aplicativos do Windows](http://msdn.microsoft.com/en-us/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
 Depurar esse tipo de aplicativo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é semelhante a depurar em aplicativos gerenciados do Windows Forms.  
  
 Quando você cria um projeto do Windows Forms com o modelo de projeto, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria automaticamente as configurações necessárias para as configurações de depuração e versão. Se necessário, você pode alterar essas configurações na  **\<nome do projeto > páginas de propriedade** caixa de diálogo. Para obter mais informações, consulte [Debug and Release Configurations](../debugger/how-to-set-debug-and-release-configurations.md).  
  
 Para obter mais informações, consulte [configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md).  
  
 Outro modo de depurar um aplicativo do Windows Forms 2 é iniciar o aplicativo fora do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e anexar a ele. Para obter mais informações, consulte [anexando a um programa em execução ou vários programas](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
 [Neste tópico](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)  
  
## <a name="see-also"></a>Consulte também  
 [Noções básicas do depurador](../debugger/debugger-basics.md)   
 [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [Anexando a um programa em execução ou vários programas](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md)   
 [Como: criar um projeto de aplicativo do Windows](http://msdn.microsoft.com/en-us/b2f93fed-c635-4705-8d0e-cf079a264efa)



