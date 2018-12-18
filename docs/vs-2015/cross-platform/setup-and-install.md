---
title: Instalar e configurar | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2cfcad00-352c-4161-814c-f5ae32d8ada8
caps.latest.revision: 19
ms.author: crdun
manager: crdun
ms.openlocfilehash: f3a72c197963332ad433f88e6cb7fffde5a9a41b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730406"
---
# <a name="setup-and-install"></a>Instalar e configurar
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Para criar aplicativos nativos do iOS, Android e Windows de uma base de código comum C#/.NET usando Xamarin, você precisa do seguinte:  
  
- Para trabalhar com aplicativos do Windows e Android: um computador de desenvolvimento Windows com o Visual Studio 2015 e Xamarin 4 instalados (consulte a observação abaixo). (Você também pode usar o Visual Studio 2013, seguindo as instruções para [instalação direta do Xamarin](https://developer.xamarin.com/guides/cross-platform/getting_started/requirements/#install) (xamarin.com).)   
  
- Para trabalhar com aplicativos do iOS: um Mac com OS X Yosemite (10.10.5) ou acima, com XCode e Xamarin instalados.  
  
  Você poderá configurar os computadores Windows e Mac ao mesmo tempo e, enquanto os instaladores estiverem em execução, poderá analisar [Saiba mais sobre desenvolvimento móvel com Xamarin](../cross-platform/learn-about-mobile-development-with-xamarin.md) para ler e inspecionar o material básico necessário.  
 
Se você tiver problemas para usar o Xamarin depois de fazer essa configuração e instalação, envie sua pergunta para [forums.xamarin.com](http://forums.xamarin.com/).
  
> [!NOTE]
>  A partir de 31 de março de 2016, todo o conteúdo do Xamarin é incluído com todas as edições do Visual Studio sem custo adicional e ele não precisa de uma licença separada. O Xamarin Studio Community para Mac também é gratuito para estudantes, desenvolvedores de OSS e pequenas equipes. Observe que, para as instalações existentes do Visual Studio que são configuradas com licenças do Xamarin mais antigas, você deve atualizar o Xamarin para a versão 4.0.3.214 ou superior. Para fazer isso, vá para **Ferramentas > Opções > Xamarin > Outros**, clique no link **Verificar Agora** e baixe a atualização 4.0.3.214. Quando você reiniciar o Visual Studio, vá para **Ferramentas > Conta do Xamarin...**  e você deverá ver o status atualizado.  
  
 **Neste tópico:**  
  
-   [Pré-requisitos](#prereq)  
  
-   [Instalação do Windows (Visual Studio e Xamarin)](#windows)  
  
-   [Configuração do Mac (Apple ID, Xcode e Xamarin)](#mac)  
  
##  <a name="prereq"></a> Pré-requisitos  
  
1.  Para direcionamento a Windows e Android:  
  
    1.  Recomendado: um computador físico Windows (não uma VM) executando o Windows 8 ou posterior, que permite o uso do rápido emulador do Visual Studio com base em Hyper-V para Android se você não tem um dispositivo Android. (Já mencionamos que você precisa de um computador físico e não de uma VM?)  
  
    1.  Você poderá usar um computador com Windows 7 ou anterior, caso em que você usará o Xamarin Player para Android como o emulador. 
    
    1. Para qualquer configuração, você também pode executar aplicativos diretamente em dispositivos físicos conectados.  
  
1.  Para direcionamento ao iOS:  
  
    1.  A um Mac ou Mac mini com rede com OS X Yosemite executando OS X 10.10.5 ou posterior (necessário para Xcode 7.1).  
  
    1.  Ao usar o Visual Studio em um computador com Windows (7+) como seu principal ambiente de desenvolvimento, um Mac em rede é necessário apenas para compilar e depurar aplicativos iOS, anexar o simulador de iOS ou dispositivos vinculados e usar o designer de storyboard no Visual Studio para criar a interface do usuário. Os modelos mais antigos do Mac são totalmente suficientes para esta função secundária.  
  
##  <a name="windows"></a> Instalação do Windows (Visual Studio e Xamarin)  
  
> [!TIP]
>  Essas instruções se aplicam ao Visual Studio 2015. Para usar o Xamarin com o Visual Studio 2013 (A Atualização 2 é necessária), siga as instruções para [instalação direta do Xamarin](https://developer.xamarin.com/guides/cross-platform/getting_started/requirements/#install) (xamarin.com).  
  
1. [Baixe e inicie o instalador para qualquer edição do Visual Studio 2015](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) (Community, Professional ou Enterprise). O Visual Studio 2015 Community é a versão gratuita; as edições Professional e Enterprise poderão ser usadas em uma base de avaliação por 30 dias, após os quais você precisará adquirir uma licença.  
  
   1.  Se você já tiver instalado o Visual Studio, abra **Painel de Controle > Programas e Recursos**, escolha o item **Visual Studio 2015** e clique em **Alterar**. Quando o instalador é aberto, clique em **Modificar** e vá para a etapa 3 abaixo.  
  
2. (Apenas novas instalações) No instalador, selecione uma instalação **Personalizada**:  
  
    ![Escolhendo a opção Personalizada na instalação do Visual Studio](../cross-platform/media/cross-plat-xamarin-setup-1.png "Instalação 1 entre várias plataformas do Xamarin")  
  
3. Verifique as seguintes caixas:  
  
   1.  **Desenvolvimento Móvel Multiplataforma > C#/.NET (Xamarin)**. Isso também selecionará automaticamente várias ferramentas Android em Ferramentas Comuns e Kits de desenvolvimento de Software. Essa opção também deve atualizar uma instalação existente do Xamarin.  
  
        ![Selecione a opção Xamarin em Desenvolvimento Móvel de Multiplataforma](../cross-platform/media/cross-plat-xamarin-setup-2.png "Instalação 2 entre várias plataformas do Xamarin")  
  
   2.  Para o Windows 8 +: **Desenvolvimento Móvel Entre Plataformas > Emulador do Microsoft Visual Studio para Android**. Observação: se você estiver usando um computador Windows 7 ou anterior ou então executando o Windows em um Mac, certifique-se de que essa opção está *desmarcada*. Consulte a "Observação sobre emuladores em computadores Windows" após a etapa 5. Você também pode deixar isso desmarcado se você pretende depurar somente em dispositivos físicos Android.  
  
   3.  (Opcional) Se você planeja direcionar para dispositivos do Windows, verifique também **Desenvolvimento Web e Windows > Ferramentas de Desenvolvimento de Aplicativos universal do Windows** e/ou **Ferramentas do Windows Phone 8.0/8.1 e Windows 8.1**. Essas opções incluem opções de instalação de imagens de emulador que levarão mais tempo para baixar; você sempre pode retornar ao instalador do Visual Studio para adicioná-las mais tarde.  
  
4. Clique no botão Instalar e permita que o processo seja executado. Novamente, isso levará algum tempo para ser concluído; durante esse período, você pode continuar com as instruções de configuração do Mac e percorrer [Saiba mais sobre desenvolvimento móvel com Xamarin](../cross-platform/learn-about-mobile-development-with-xamarin.md).  
  
5. Depois que a instalação for concluída, inicie o Visual Studio e entre com sua conta da Microsoft se solicitado (é a mesma conta que você usa com o Windows). Em seguida, verifique se há atualizações do Xamarin em **Ferramentas > Opções > Xamarin** ou **Ferramentas > Opções > Xamarin > Outros**, em que você encontrará um link **Verificar Agora**:  
  
    ![Verificando atualizações do Xamarin em Opções do Visual Studio](../cross-platform/media/cross-plat-xamarin-setup-3.png "Instalação 3 entre várias plataformas do Xamarin")  
  
   > [!NOTE]
   >  Conforme observado anteriormente, certifique-se de atualizar o Xamarin para a versão 4.0.3.214 ou superior para evitar problemas com licenças anteriores do Xamarin.  

   Se você não vê uma opção para Xamarin em **Ferramentas > Opções**, verifique novamente a instalação ou tente reiniciar o Visual Studio. Você também pode pesquisar pelo Xamarin na caixa de diálogo Opções.
      
6. Para Windows 7 e anteriores ou Windows executando em um Mac, use o [emulador do SDK do Android](https://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debug-on-emulator/android-sdk-emulator/) se você não tiver dispositivos físicos. Consulte a observação abaixo.  
  
   **Observação sobre emuladores em computadores Windows:** já que CPUs dão suporte apenas uma tecnologia de virtualização por vez, é melhor ter apenas uma em uso em um computador de desenvolvimento. Há três tecnologias de virtualização principais, que são Hyper-V (usada pelo emulador do Visual Studio para Android e pelo emulador do Windows Phone), Virtual Box (usada pelo Genymotion) e Intel HAXM (usada pelo emulador do SDK do Android). Devido a vários problemas entre o Hyper-V e o Virtual Box, é melhor usar emuladores de apenas um tipo em um determinado computador, por isso as recomendações acima para usar o Hyper-V em computadores com Windows 8 e superior e emuladores Intel HAXM no Windows 7 e versões anteriores e também ao executar o Windows em um Mac.  
  
##  <a name="mac"></a> Configuração do Mac (Apple ID, Xcode e Xamarin)  
  
1.  Criar uma ID Apple gratuita em [ https://appleid.apple.com ](https://appleid.apple.com/) se você ainda não tiver um. Isso é necessário para instalar e entrar no Xcode.  
  
2.  Baixe e instale o Xcode de [https://developer.apple.com/xcode/](https://developer.apple.com/xcode/) e adicione sua ID Apple, conforme é descrito em [Adicionando sua conta no XCode](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/AddingYourAccounttoXcode/AddingYourAccounttoXcode.html#//apple_ref/doc/uid/TP40013839-CH40-SW1) (apple.com).  
  
3.  Baixe e instale o Xamarin, seguindo as instruções em [Instalando e configurando o Xamarin.iOS](http://developer.xamarin.com/guides/ios/getting_started/installation/mac/) (xamarin.com).  
  
4.  Depois de concluir a instalação do Xamarin em computadores Windows e Mac, siga as instruções em [conectando ao Mac](http://developer.xamarin.com/guides/ios/getting_started/installation/windows/xamarin-mac-agent/) (xamarin.com) para que você possa trabalhar com iOS e Mac do Visual Studio no computador Windows.  
  
     Observe que ambos os computadores devem estar na mesma rede local.

