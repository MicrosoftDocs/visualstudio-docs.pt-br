---
title: Desenvolver aplicativos para a UWP (Plataforma Universal do Windows) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eac59cb6-f12e-4a77-9953-6d62b164a643
caps.latest.revision: 50
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 24dfca5d4ac8432cbe659bb42ca54d0398c47c04
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766471"
---
# <a name="develop-apps-for-the-universal-windows-platform-uwp"></a>Desenvolver aplicativos para a UWP (Plataforma Universal do Windows)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Com a Plataforma Universal do Windows e nosso único núcleo do Windows, é possível executar o mesmo aplicativo em qualquer dispositivo Windows 10, de telefones a áreas de trabalho. Crie esses aplicativos Universais do Windows com o Visual Studio 2015 e as ferramentas de Desenvolvimento de Aplicativos Universais do Windows.  
  
 ![Plataforma Universal do Windows](../cross-platform/media/uwp-coreextensions.png "UWP_CoreExtensions")  
  
 Execute seu aplicativo em um telefone Windows 10, área de trabalho do Windows 10 ou Xbox. É o mesmo pacote do aplicativo! Com a introdução do núcleo único e unificado do Windows 10, um pacote do aplicativo pode ser executado em todas as plataformas. Várias plataformas têm SDKs de Extensão que podem ser adicionados ao aplicativo para aproveitar comportamentos específicos à plataforma. Por exemplo, o SDK de uma extensão para dispositivos móveis manipula o botão Voltar pressionado em um Windows Phone. Se você referenciar um SDK de Extensão em seu projeto, basta adicionar verificações em tempo de execução para testar se esse SDK está disponível nessa plataforma. É assim que você pode ter o mesmo pacote do aplicativo para cada plataforma!  
  
 **O que é o Windows Core?**  
  
 Pela primeira vez, o Windows foi refatorado para ter um núcleo comum em todas as plataformas Windows 10. Há uma fonte comum, um kernel do Windows comum, um arquivo, uma pilha de E/S e um modelo de aplicativo. Para a interface do usuário, há apenas uma estrutura de interface do usuário em XAML e uma estrutura de interface do usuário em HTML. Portanto, você pode se concentrar em criar um ótimo aplicativo, porque facilitamos a execução dele em diferentes dispositivos Windows 10.  
  
 **O que é exatamente a Plataforma Universal do Windows?**  
  
 É apenas uma coleção de contratos e versões. Ela permite escolher o destino de execução do aplicativo. Você não tem mais como destino um sistema operacional. Agora você pode destinar seu aplicativo a uma ou mais famílias de dispositivos. Saiba mais detalhes neste [guia da plataforma](http://msdn.microsoft.com/library/windows/apps/dn894631.aspx).  
  
## <a name="requirements"></a>Requisitos  
 As ferramentas de Desenvolvimento de Aplicativo Universal do Windows vêm com emuladores que podem ser usados para ver a aparência de seu aplicativo em diferentes dispositivos. Se você desejar usar esses emuladores, precisará instalar esse software em um computador físico. O computador físico deve executar o Windows 8.1 (x64) Professional Edition ou superior e ter um processador que dá suporte ao Cliente Hyper-V e à SLAT (Conversão de Endereços de Segundo Nível). Os emuladores não podem ser usados quando o Visual Studio está instalado em uma máquina virtual.  
  
 Esta é a lista de software de que você precisa:  
  
- [Windows 10](http://windows.microsoft.com/windows/downloads)  
  
- [Visual Studio 2015](http://go.microsoft.com/fwlink/p/?LinkId=526725). Verifique se as Ferramentas de Desenvolvimento de Aplicativo Universal do Windows estão selecionadas na lista de recursos opcionais. Sem essas ferramentas, você não conseguirá criar os aplicativos universais.  
  
  Depois de instalar esse software, você precisa [habilitar seu dispositivo Windows 10](https://msdn.microsoft.com/library/windows/apps/xaml/dn706236.aspx) para desenvolvimento. (Não é mais necessária uma licença de desenvolvedor para cada dispositivo Windows 10.)  
  
  **Suporte ao Windows 8.1 e ao Windows 7**  
  
  Se você optar por desenvolver aplicativos Universais do Windows com o Visual Studio 2015 em uma plataforma diferente do Windows 10, estas serão as restrições:  
  
- Windows 8.1: não é possível executar o aplicativo localmente (apenas em um dispositivo Windows 10 remoto). É possível usar os emuladores no Visual Studio, mas não o simulador.  
  
- Windows 7: não é possível executar o aplicativo localmente (apenas em um dispositivo Windows 10 remoto). Não é possível usar os emuladores nem o simulador no Visual Studio.  
  
  Você poderá usar o designer XAML apenas se sua plataforma de desenvolvimento for o Windows 10.  
  
## <a name="universal-windows-apps"></a>Aplicativos Universais do Windows  
 Escolha sua linguagem de desenvolvimento preferencial entre C#, Visual Basic, C++ ou JavaScript para [criar um aplicativo Universal do Windows para dispositivos Windows 10](http://msdn.microsoft.com/library/windows/apps/xaml/dn609832.aspx#target_win10). Se preferir, assista a [este vídeo de introdução](http://channel9.msdn.com/Series/ConnectOn-Demand/229).  
  
 Se você tiver aplicativos da Windows Store 8.1, aplicativos Windows Phone 8.1 ou aplicativos Universais do Windows criados com o Visual Studio 2015 RC, [porte esses aplicativos existentes](http://msdn.microsoft.com/library/windows/apps/xaml/mt238321.aspx) para que eles usem a última Plataforma Universal do Windows.  
  
 Depois de criar seu aplicativo Universal do Windows, é necessário [empacotar o aplicativo](https://msdn.microsoft.com/library/windows/apps/hh454036.aspx) para instalá-lo em um dispositivo Windows 10 ou enviá-lo para a Windows Store.

