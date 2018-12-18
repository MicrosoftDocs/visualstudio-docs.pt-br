---
title: Visual C++ para Desenvolvimento Móvel em Multiplataforma | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
ms.assetid: 0bb872d6-981b-4c96-9143-fcec5336bf0d
caps.latest.revision: 12
author: corob-msft
ms.author: corob
manager: ghogen
ms.openlocfilehash: 1e0dfe11fc35ed452010592548e4bd2cba63e14b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781108"
---
# <a name="visual-c-for-cross-platform-mobile-development"></a>Visual C++ para Desenvolvimento Móvel Multiplataforma
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode criar aplicativos C++ nativos para dispositivos iOS, Android e Windows e compartilhar código comum em bibliotecas criadas para iOS, Android e Windows, usando Visual C++ para Desenvolvimento Móvel de Multiplataforma. Essa é uma opção disponível no Visual Studio 2015 que instala os SDKs e ferramentas necessárias para o desenvolvimento de plataforma cruzada de bibliotecas compartilhadas e aplicativos nativos. Quando ele estiver instalado, você poderá usar o Visual C++ para criar código que é executado em dispositivos iOS e Android, além de Windows, Windows Phone e Xbox.  
  
 A gravação de código para várias plataformas pode ser frustrante. As linguagens de desenvolvimento principais e as ferramentas para iOS, Android e Windows são diferentes em cada plataforma. No entanto, todas as plataformas dão suporte à gravação de código em C++. Esse é o denominador comum que você pode usar para permitir a reutilização de código principal entre plataformas. Código nativo gravado em C++ pode ser mais eficaz e resistente à engenharia reversa. A reutilização de código pode economizar tempo e esforço durante a criação de aplicativos para várias plataformas.  
  
 O desenvolvimento usando Visual C++ para Desenvolvimento Móvel de Multiplataforma apresenta várias vantagens:  
  
1.  **Fácil instalação.** O instalador do Visual Studio obtém e instala as ferramentas de terceiros necessárias e SDKs que você precisa para compilar bibliotecas ou aplicativos para Android e iOS. A instalação e a configuração são simples e praticamente automáticas.  
  
2.  **Um ambiente de build poderoso e familiar.** Crie soluções de plataforma cruzada compartilháveis e projetos facilmente com modelos do Visual Studio. Gerencie as propriedades de todos os projetos usando uma interface comum. Edite todos os seus códigos no editor do Visual Studio e desfrute da plataforma cruzada interna IntelliSense para conclusão de código e realce de erros.  
  
3.  **Experiência de depuração unificada.** Use as ferramentas de depuração de altíssima qualidade no Visual Studio para observar e percorrer código C++ em todas as plataformas, incluindo dispositivos com Android e emuladores, simuladores e dispositivos iOS, Windows ou Windows Phone.  
  
## <a name="get-the-tools"></a>Obtenha as ferramentas  
 Visual C++ para Desenvolvimento Móvel de Multiplataforma é uma opção instalável que vem com o Visual Studio 2015. Para obter instruções de instalação e pré-requisitos, consulte [Instalar o Visual C++ para Desenvolvimento Móvel de Multiplataforma](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md). Para compilar código para iOS, você também precisa de um computador Mac e uma Conta de Desenvolvedor do Apple iOS. Para obter mais informações, consulte [Instalar e Configurar Ferramentas para Compilar usando o iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md).  
  
## <a name="come-up-to-speed"></a>Excelente operação  
 Se você estiver vindo do desenvolvimento Android ou iOS, temos materiais excelente sobre como começar. O Visual Studio é um ambiente de desenvolvimento completo expressivo e capaz. Para saber como usá-lo, tente o [Introdução para desenvolvedores do Android](https://msdn.microsoft.com/library/windows/apps/dn275875.aspx) ou [Introdução para desenvolvedores do iOS](https://msdn.microsoft.com/library/windows/apps/xaml/jj657966.aspx). Esses tópicos o apresentarão ao Visual Studio e os conceitos que você precisará para desenvolver aplicativos de plataforma cruzada para Windows e Windows Phone. Para começar a gravar seu primeiro aplicativo de plataforma cruzada para iOS e Android, consulte [Compilar um Aplicativo do OpenGL ES no Android e iOS](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md).  
  
 O Visual C++ para Desenvolvimento Móvel de Multiplataforma inclui vários modelos para ajudá-lo a começar com seus aplicativos:  
  
-   Aplicativo OpenGLES 2 (Android, iOS e Windows Universal)  
  
     Cria uma solução que inclui um conjunto de projetos para compilar um aplicativo de Atividade Nativa do Android, um aplicativo iOS, um aplicativo Universal do Windows, junto com uma biblioteca compartilhada de C++. Estes aplicativos usam bibliotecas específicas da plataforma criada ao usar o código C++ OpenGL ES comum para desenhar o mesmo cubo rotatório em cada aplicativo. Você deve incluir a opção de Ferramenta de Desenvolvimento de Aplicativo do Windows Universal quando você instalar o Visual Studio para usar este modelo.  
  
-   Aplicativo de Atividade Nativa (Android)  
  
     Cria um aplicativo C++ OpenGL completo como um projeto de Atividade Nativa do Android.  
  
-   Aplicativo OpenGLES (Android, iOS)  
  
     Cria uma solução com um conjunto de projetos para compilar um aplicativo de Atividade Nativa do Android e um aplicativo iOS. Estes aplicativos usam bibliotecas específicas da plataforma criada ao usar o código C++ OpenGL ES comum para desenhar o mesmo cubo rotatório em cada aplicativo.  
  
-   Biblioteca Compartilhada (Android, iOS)  
  
     Cria uma solução com projetos para criar um arquivo de biblioteca Android dinâmica (.so) e um arquivo de biblioteca estática (.a) do iOS com código C++ comum em um projeto compartilhado.  
  
-   Aplicativo Básico (Android, Ant)  
  
     Cria um projeto de aplicativo do Android "Olá, mundo" que usa somente um código-fonte Java e o sistema de build Ant.  
  
-   Aplicativo Básico (Android, Gradle)  
  
     Cria um projeto de aplicativo do Android "Olá, mundo" que usa somente um código-fonte Java e o sistema de build Gradle.  
  
-   Biblioteca Básica (Android, Ant)  
  
     Cria um projeto de biblioteca do Android "Olá, mundo" que usa somente um código-fonte Java e o sistema de build Ant.  
  
-   Biblioteca Básica (Android, Gradle)  
  
     Cria um projeto de biblioteca do Android "Olá, mundo" que usa somente um código-fonte Java e o sistema de build Gradle.  
  
-   Biblioteca Dinâmica Compartilhada (Android)  
  
     Cria um arquivo de biblioteca dinâmica Android (.so) usando código C++.  
  
-   Aplicativo OpenGLES 2 (iOS)  
  
     Cria uma solução com um conjunto de projetos para compilar um aplicativo iOS OpenGL ES 2. O aplicativo usa uma biblioteca de código C++ OpenGL ES para desenhar o cubo giratório em um aplicativo iOS. Este aplicativo pode ser um bom ponto de partida para ver como importar bibliotecas C++ para seu aplicativo iOS.  
  
-   Biblioteca Estática (Android)  
  
     Cria um projeto para compilar uma biblioteca estática para Android. Você pode apenas vincular uma biblioteca dinâmica em um aplicativo Android, mas você pode vincular qualquer número de bibliotecas estáticas.  
  
-   Biblioteca Estática (iOS)  
  
     Cria um projeto para compilar uma biblioteca estática para iOS.  
  
-   Projeto do Makefile (Android)  
  
     Cria um wrapper de projeto para seus próprios projetos de makefile Android.  
  
## <a name="try-out-sample-code"></a>Testar o código de exemplo  
 Baixe exemplos que mostram como criar bibliotecas de código compartilhado que você pode usar em aplicativos do iOS, Android e Windows e como criar aplicativos de Atividade Nativa completos para o Android. Para iniciar, consulte [Exemplos de Desenvolvimento Móvel de Multiplataforma](../cross-platform/cross-platform-mobile-development-examples.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
1.  [Instalar o Visual C++ para Desenvolvimento Móvel Multiplataforma](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)  
  
2.  [Instalar e configurar ferramentas para criação usando iOS](../cross-platform/install-and-configure-tools-to-build-using-ios.md)  
  
3.  [Criar um aplicativo de Atividade Nativa do Android](../cross-platform/create-an-android-native-activity-app.md)  
  
4.  [Criar um aplicativo OpenGL ES no Android e iOS](../cross-platform/build-an-opengl-es-application-on-android-and-ios.md)  
  
5.  [Exemplos de desenvolvimento móvel multiplataforma](../cross-platform/cross-platform-mobile-development-examples.md)

