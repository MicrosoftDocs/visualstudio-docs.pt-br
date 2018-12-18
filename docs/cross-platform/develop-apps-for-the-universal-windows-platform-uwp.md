---
title: Desenvolver aplicativos para a UWP (Plataforma Universal do Windows) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.technology:
- tgt-pltfrm-cross-plat
ms.topic: conceptual
ms.assetid: eac59cb6-f12e-4a77-9953-6d62b164a643
author: stevehoag
ms.author: shoag
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: de4306b2fa56bf00fd51a741441395b90ed314e5
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44280799"
---
# <a name="develop-apps-for-the-universal-windows-platform-uwp"></a>Desenvolver aplicativos para a UWP (Plataforma Universal do Windows)
Com a Plataforma Universal do Windows e nosso único núcleo do Windows, é possível executar o mesmo aplicativo em qualquer dispositivo Windows 10, de telefones a áreas de trabalho. Crie esses aplicativos universais do Windows com o Visual Studio e as ferramentas de desenvolvimento de aplicativos universais do Windows.

 ![Plataforma Universal do Windows](../cross-platform/media/uwp_coreextensions.png "UWP_CoreExtensions")

 Execute seu aplicativo em um telefone Windows 10, área de trabalho do Windows 10 ou Xbox. O pacote do aplicativo é o mesmo! Com a introdução do núcleo único e unificado do Windows 10, um pacote do aplicativo pode ser executado em todas as plataformas. Várias plataformas têm SDKs de extensão que podem ser adicionados ao aplicativo para aproveitar comportamentos específicos da plataforma. Por exemplo, o SDK de uma extensão para dispositivos móveis manipula o botão Voltar pressionado em um Windows Phone. Se você referenciar um SDK de extensão em seu projeto, bastará adicionar verificações de tempo de execução para testar se esse SDK está disponível nessa plataforma. É assim que você pode usar o mesmo pacote do aplicativo para todas as plataformas!

 **O que é o núcleo do Windows?**

 Pela primeira vez, o Windows foi refatorado para ter um núcleo comum em todas as plataformas Windows 10. Há uma fonte comum, um kernel do Windows comum, um arquivo, uma pilha de E/S e um modelo de aplicativo. Para a interface do usuário, há apenas uma estrutura de interface do usuário em XAML e uma estrutura de interface do usuário em HTML. Você pode se concentrar em criar um ótimo aplicativo, porque ficou mais fácil executá-lo em diferentes dispositivos Windows 10.

 **O que é exatamente a Plataforma Universal do Windows?**

A Plataforma Universal do Windows é simplesmente uma coleção de contratos e versões. Ela permite escolher o destino de execução do aplicativo. Você não direciona mais a um sistema operacional, agora você direciona a uma ou mais famílias de dispositivos. Para obter mais detalhes, leia [Introdução à Plataforma Universal do Windows](/windows/uwp/get-started/universal-application-platform-guide).

## <a name="requirements"></a>Requisitos
 As ferramentas de desenvolvimento de Aplicativo Universal do Windows vêm com emuladores que podem ser usados para mostrar a aparência do aplicativo em diferentes dispositivos. Se você desejar usar esses emuladores, precisará instalar esse software em um computador físico. O computador físico deve executar o Windows 8.1 (x64) Professional Edition ou superior e ter um processador que dá suporte ao Cliente Hyper-V e à SLAT (Conversão de Endereços de Segundo Nível). Os emuladores não podem ser usados quando o Visual Studio está instalado em uma máquina virtual.

 Esta é a lista de software de que você precisa:

-   [Windows 10](http://windows.microsoft.com/windows/downloads). O Visual Studio 2017 dá suporte ao desenvolvimento de UWP somente no Windows 10. Para obter mais detalhes, confira [Direcionamento para plataformas](/visualstudio/productinfo/vs2017-compatibility-vs) e [Requisitos de sistema](/visualstudio/productinfo/vs2017-system-requirements-vs) do Visual Studio.

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). Você também precisará da carga de trabalho de desenvolvimento da Plataforma Universal do Windows opcional.

     ![Carga de trabalho da UWP](media/uwp_workload.png)

Depois de instalar este software, você precisará habilitar o dispositivo Windows 10 para desenvolvimento. Consulte [Habilitar seu dispositivo para desenvolvimento](/windows/uwp/get-started/enable-your-device-for-development). Não é mais necessária uma licença de desenvolvedor para cada dispositivo Windows 10.

## <a name="universal-windows-apps"></a>Aplicativos Universais do Windows
Escolha sua linguagem de desenvolvimento preferencial entre C#, Visual Basic, C++ ou JavaScript para criar um aplicativo da Plataforma Universal do Windows para dispositivos Windows 10. Leia [Criar seu primeiro aplicativo](/windows/uwp/get-started/your-first-app) ou assista ao vídeo [Tools for Windows 10 Overview](https://channel9.msdn.com/Series/ConnectOn-Demand/229) (Visão geral das ferramentas para Windows 10).

Se você já tiver aplicativos da Windows Store 8.1, aplicativos Windows Phone 8.1 ou aplicativos Universais do Windows criados com o Visual Studio 2015, será necessário portar esses aplicativos para que eles usem a última Plataforma Universal do Windows. Consulte [Mudar do Windows Runtime 8.x para a UWP](/windows/uwp/porting/w8x-to-uwp-root).

Depois de criar o aplicativo universal do Windows, você deverá empacotá-lo para instalá-lo em um dispositivo Windows 10 ou enviá-lo para a Windows Store. Consulte [Empacotando aplicativos](/windows/uwp/packaging/index).

## <a name="see-also"></a>Consulte também
[Desenvolvimento móvel multiplataforma no Visual Studio](../cross-platform/cross-platform-mobile-development-in-visual-studio.md)
