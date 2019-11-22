---
title: Saiba mais sobre desenvolvimento móvel com o Xamarin | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: e970d936-1df4-4c0c-96e3-ef6191295882
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: 9924eee661f917334aed586506a107486cd5be0f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299779"
---
# <a name="learn-about-mobile-development-with-xamarin"></a>Saiba mais sobre desenvolvimento móvel com o Xamarin
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico direciona você a materiais de visão geral que ajudam a entender o desenvolvimento de aplicativos móveis de plataforma cruzada com o Xamarin. Se você não ainda tiver instalado o Visual Studio e o Xamarin, inicie primeiro o processo de [Instalação](../cross-platform/setup-and-install.md), depois volte aqui para trabalhar com esses recursos enquanto os instaladores estão em execução.  
  
> [!NOTE]
> Salvo indicação em contrário, sugerimos inicialmente ler somente as páginas vinculadas diretamente aqui, e não páginas subsidiárias. Se o processo de instalação ainda estiver em execução após você concluir esta lista, fique à vontade para voltar e explorar tópicos adicionais.  
>   
> Também fique à vontade para examinar os tópicos marcados como "Fundamentos" e para voltar aos tópicos de "Aprofundamento" mais tarde.  
  
## <a name="essentials-introduction-to-xamarin"></a>Fundamentos: Introdução ao Xamarin  
 *10 a 20 minutos*  
  
1. [Aplicativos móveis no Visual Studio com Xamarin](https://www.visualstudio.com/explore/xamarin-vs) (visualstudio.com) fornece um breve resumo das principais características do Xamarin.  
  
2. [Building Cross-Platform Mobile Apps using C# and Visual Studio](https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2015-Final-Release-Event/Building-cross-platform-mobile-apps-using-C-and-Visual-Studio-2015) (Criando aplicativos móveis de plataforma cruzada usando C# e Visual Studio) (Channel9, 15m16s) com o grande especialista em Xamarin, James Montemagno. Os primeiros três minutos são uma visão geral do Xamarin, seguida de demonstrações de código.  
  
## <a name="essentials-overview-of-the-visual-studio-and-xamarin-environment"></a>Fundamentos: Visão geral do ambiente do Visual Studio e do Xamarin  
 *5 a 15 minutos*  
  
- O computador Windows com Visual Studio e Xamarin é onde você fará a maior parte de seu trabalho. Nesse computador, você compila diretamente aplicativos Android e Windows e os executa e depura em um dispositivo ou emulador. Além disso, remotamente, você compila, executa e depura aplicativos iOS por meio do Mac. O Visual Studio no computador Windows também pode se conectar ao designer de storyboard iOS e ao simulador de iOS.  
  
- O Mac com Xcode e Xamarin serve como o host de build/assinatura e o ambiente de runtime para aplicativos iOS. Compilações para iOS do Visual Studio no computador Windows são delegadas a esse Mac. Ao depurar um aplicativo iOS do Visual Studio, ele é executado no simulador de iOS no Mac ou diretamente em um dispositivo vinculado conectado ao Mac. Nesse caso, você interagirá com o aplicativo no Mac ou próximo a ele, e terá sua experiência de depuração no Visual Studio.  
  
  Esses relacionamentos são ilustradas abaixo, e você pode ler mais sobre como trabalhar com aplicativos iOS em [Introdução ao Xamarin.IOS para Visual Studio](https://docs.microsoft.com/xamarin/ios/get-started/installation/windows/introduction-to-xamarin-ios-for-visual-studio) (xamarin.com).  
  
  ![A relação entre computadores de desenvolvimento do Windows e do Mac em um ambiente do Xamarin](../cross-platform/media/crossplat-xamarin-learn-1.png "CrossPlat Xamarin Learn 1")  
  
## <a name="essentials-how-projects-are-structured"></a>Fundamentos: Como projetos são estruturados  
 *10 a 30 minutos*  
  
1. [Opções de compartilhamento de código](https://docs.microsoft.com/xamarin/cross-platform/app-fundamentals/code-sharing) (xamarin.com). Recomendamos usar a opção de bibliotecas de classes portáteis, pois ela dá melhor suporte ao uso apenas das APIs do .NET que têm suporte em todas as plataformas de destino. A maior parte do código de lógica de negócios residirá na PCL, incluindo o acesso a bancos de dados, chamadas para APIs REST e chamadas para componentes de Xamarin portáteis (consulte [Aprofundamento: Componentes do Xamarin](#components) no final deste tópico). Código de interface do usuário comum gravado com Xamarin.Forms também pode residir em uma PCL.  
  
2. (Opcional) [Estudo de caso: Tasky](https://docs.microsoft.com/xamarin/cross-platform/app-fundamentals/building-cross-platform-applications/case-study-tasky) (xamarin.com), descreve algumas das melhores práticas de design e estrutura de um aplicativo completo, como estruturar o projeto com uma PCL para o código compartilhado que separa os dados, acesso a dados e camadas de negócios.  
  
## <a name="essentials-native-and-xamarinforms-ui-layers"></a>Fundamentos: camadas de interface do usuário nativas e do Xamarin.Forms  
 *10 a 40 minutos*  
  
 O Xamarin fornece duas maneiras de compilar ótimos aplicativos nativos: Xamarin nativo e Xamarin.Forms.  
  
 Com o Xamarin nativo, você escrever código de interface do usuário separado para cada plataforma de destino: iOS, Android e Windows.  Com essa abordagem, você tem acesso direto a APIs específicas da plataforma, o que permite uma experiência de interface do usuário personalizada por plataforma.  Você também tem acesso completo aos controles e ao designer nativo para cada plataforma para ajudar na compilação da interface do usuário respectiva.  
  
 O Xamarin.Forms fornece um conjunto geral de APIs que permite que você escreva uma camada de interface do usuário compartilhada para todas as plataformas em uma biblioteca de classes portátil.  O Xamarin.Forms renderiza para controles nativos em cada plataforma de destino para dar uma aparência nativa.  Em vez de usar um designer, com o Xamarin.Forms, você compila sua interface do usuário usando C# e XAML.  
  
 Não é necessário decidir qual abordagem adotar antecipadamente; os aplicativos podem ser implementados usando uma combinação de Xamarin nativo e Xamarin.Forms:  
  
- Use o Xamarin.Forms para criar telas de finalidade geral que fornecem interface do usuário e recursos semelhantes entre plataformas, como logons, formulários de contato e resultados da pesquisa.  
  
- Use uma variedade de funcionalidades de personalização no Xamarin.Forms para ajustar a interface do usuário por plataforma. Isso inclui a API OnPlatform, que pode ser usada do código e do XAML, criar uma exibição personalizada, estender um renderizador existente e criar um renderizador personalizado.  
  
- Se necessário, use o Xamarin nativo para criar telas que usam recursos interface do usuário exclusivos de cada plataforma, por exemplo, uma tela que usa manipulação de imagem e captura com a câmera nativa.  
  
  É recomendável sempre iniciar com uma solução do Xamarin.Forms para configurar o compartilhamento de código de interface do usuário entre plataformas e usar as funcionalidades de personalização para fazer ajustes específicos da plataforma. Se e quando precisar de telas totalmente específicas da plataforma, você poderá adicioná-las individualmente usando o Xamarin nativo.  
  
  Para saber mais:  
  
1. [Xamarin.Forms](https://docs.microsoft.com/xamarin/xamarin-forms/) (xamarin.com) fornece uma breve visão geral e os prós e contras do Xamarin.Forms versus camadas nativas da interface do usuário (ou seja, Xamarin.iOS e Xamarin.Android).  
  
2. Os primeiros três minutos do vídeo de James Montemagno, [Xamarin.Forms: Native iOS, Android & Windows apps with C# & XAML](https://channel9.msdn.com/events/Visual-Studio/Connect-event-2015/704) (Xamarin.Forms: aplicativos iOS, Android e Windows nativos com C# e XAML), (Channel9 13m3s) fornece outra visão geral, e você pode continuar assistindo a demonstrações.  
  
3. (Opcional) [Uma Introdução ao Xamarin.Forms](https://docs.microsoft.com/xamarin/get-started/quickstarts/deepdive?pivots=windows) (xamarin.com)  
  
4. (Opcional) Veja exemplos de como usar o OnPlatform para personalização na documentação de [Classe de Dispositivo](https://docs.microsoft.com/xamarin/xamarin-forms/platform/device) (xamarin.com)  
  
5. (Opcional) [Multiplataforma – Compartilhar código de interface do usuário em plataformas móveis com Xamarin.Forms](https://msdn.microsoft.com/magazine/dn904669.aspx) de Jason Smith (MSDN Magazine) descreve as diferentes opções de personalização com o Xamarin.Forms, cujos detalhes são abordados em [Personalizando controles em cada plataforma](https://docs.microsoft.com/xamarin/xamarin-forms/app-fundamentals/custom-renderer/) (xamarin.com).  
  
## <a name="deeper-dive-debugging-with-emulators"></a>Aprofundamento: Depurando com emuladores  
 *10 a 15 minutos*  
  
 Para depurar seus aplicativos de plataforma cruzada sem precisar usar um dispositivo físico, você precisará usar o seguinte:  
  
1. **Um emulador do Android.** Dependendo da versão do Windows que você está usando, recomendamos o Emulador do Microsoft Visual Studio para Android ou o Xamarin Player, que oferecem desempenho rápido e dão suporte a uma variedade de funcionalidades de dispositivo:  
  
    - **Computadores Windows 8+:** é altamente recomendável usar o [Emulador do Visual Studio para Android](https://www.visualstudio.com/features/msft-android-emulator-vs.aspx) da Microsoft, que é instalado com o Visual Studio.  O vídeo [Visual Studio Emulator for Android](https://channel9.msdn.com/events/Visual-Studio/Connect-event-2015/711) (Emulador do Visual Studio para Android) (Channel9, 5m55s) oferece uma visão geral e uma demonstração.  
  
    - **Windows 7 ou anterior/Windows em execução no Mac OS X**: use o [Xamarin Android Player](https://docs.microsoft.com/xamarin/android/deploy-test/debugging/debug-on-emulator?tabs=windows) (xamarin.com).  
  
2. **Simulador de iOS da Apple.** Para saber mais, leia [Getting Started with the iOS Simulator](https://developer.apple.com/library/prerelease/content/documentation/IDEs/Conceptual/iOS_Simulator_Guide/GettingStartedwithiOSSimulator/GettingStartedwithiOSSimulator.html#//apple_ref/doc/uid/TP40012848-CH5-SW1) (Introdução ao Simulador de iOS) (apple.com).  
  
3. **Emulador do Windows Phone da Microsoft.** Para saber mais, leia [Windows Phone Emulator for Windows Phone 8](https://msdn.microsoft.com/library/dn632391.aspx) (Emulador do Windows Phone para Windows Phone 8).  
  
## <a name="components"></a> Aprofundamento: Componentes do Xamarin  
 *10 minutos*  
  
 Muitas funcionalidades estendidas estão disponíveis para aplicativos Xamarin por meio de componentes Xamarin. Encontre o catálogo completo disponível para download em [http://components.xamarin.com/](https://docs.microsoft.com/xamarin/cross-platform/troubleshooting/component-nuget?tabs=windows), que inclui componentes para outros controles adicionais da interface do usuário, autenticação, uma variedade de serviços de nuvem, como o Microsoft Azure, e muito mais.
