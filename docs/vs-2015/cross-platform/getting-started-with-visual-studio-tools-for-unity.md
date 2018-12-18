---
title: Introdução às Ferramentas do Visual Studio para Unity | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
caps.latest.revision: 12
author: conceptdev
ms.author: crdun
manager: ghogen
ms.openlocfilehash: 9ed6cb4127ba57c6b9b84a32996968dbf9fac4fe
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51762716"
---
# <a name="getting-started-with-visual-studio-tools-for-unity"></a>Introdução às Ferramentas do Visual Studio para Unity
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Nesta seção, você aprenderá a instalar as Ferramentas do Visual Studio para Unity e a configurar seu projeto do Unity para trabalhar com o Visual Studio.  
  
> [!IMPORTANT]
>  O Unity 5.2 adiciona suporte interno às Ferramentas do Visual Studio para Unity 2.1, que simplifica a configuração do projeto. Para tirar proveito disso, você precisará do Unity versão 5.2.0 ou superior no Windows e das Ferramentas do Visual Studio para Unity versão 2.1 ou posterior.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para usar as Ferramentas do Visual Studio para Unity, você precisará:  
  
-   de uma versão do **Visual Studio** que dê suporte a extensões, como o Visual Studio Community, Professional, Premium ou Enterprise. É possível baixar o Visual Studio Community gratuitamente.  
  
     [Baixar o Visual Studio Community](http://www.visualstudio.com/downloads/download-visual-studio-vs)  
  
-   do **Unity** versão 4.0.0 ou superior ou do **Unity** versão 5.2.0 para tirar proveito do suporte interno às Ferramentas do Visual Studio para Unity versão 2.1 ou posterior.  
  
     [Baixar o Unity](https://unity3d.com/get-unity/download)  
  
## <a name="install-visual-studio-tools-for-unity"></a>Instalar as Ferramentas do Visual Studio para Unity  
 Baixe e instale as Ferramentas do Visual Studio para Unity da Galeria do Visual Studio. Você precisará instalar o pacote correto para a sua versão do Visual Studio. Instale as Ferramentas do Visual Studio para Unity versão 2.1 ou superior para tirar proveito do suporte interno ao VSTU no Unity versão 5.2 ou posterior.  
  
-   Para o Visual Studio 2015 Community, Visual Studio 2015 Professional ou Visual Studio 2015 Enterprise:  
  
     [Baixe as Ferramentas do Visual Studio 2015 para Unity](https://visualstudiogallery.msdn.microsoft.com/8d26236e-4a64-4d64-8486-7df95156aba9)  
  
-   Para o Visual Studio 2013 Community, Visual Studio 2013 Professional ou Visual Studio 2013 Premium:  
  
     [Baixe as Ferramentas do Visual Studio 2013 para Unity](https://visualstudiogallery.msdn.microsoft.com/20b80b8c-659b-45ef-96c1-437828fe7cf2)  
  
-   Para o Visual Studio 2012 Professional ou Visual Studio 2012 Premium:  
  
     [Baixe as Ferramentas do Visual Studio 2012 para Unity](https://visualstudiogallery.msdn.microsoft.com/7ab11d2a-f413-4ed6-b3de-ff1d05157714)  
  
-   Para o Visual Studio 2010 Professional ou Visual Studio 2010 Premium:  
  
     [Baixe as Ferramentas do Visual Studio 2010 para Unity](https://visualstudiogallery.msdn.microsoft.com/6e536faa-ce73-494a-a746-6a14753015f1)  
  
> [!NOTE]
>  Versões Express do Visual Studio não dão suporte a extensões como as Ferramentas do Visual Studio para Unity. O Visual Studio Community é uma versão gratuita do Visual Studio que dá suporte às Ferramentas do Visual Studio para Unity e a outras extensões. Para a maioria dos usuários, o Visual Studio Community é uma opção melhor que o Express.  
  
## <a name="your-first-unity-project-with-visual-studio-tools-for-unity"></a>Seu primeiro projeto do Unity com as Ferramentas do Visual Studio para Unity  
 Agora que tem tudo de que precisa, você está pronto para seu primeiro projeto do Unity com o Visual Studio. Configurar seu projeto do Unity é diferente dependendo de quais versões do Unity e das Ferramentas do Visual Studio para Unity estão instaladas. Siga as etapas abaixo para a versão do Unity e das Ferramentas do Visual Studio para Unity que você instalou.  
  
### <a name="unity-52-and-higher-requires-vstu-21-or-higher"></a>Unity 5.2 e posterior (requer o VSTU para Unity 2.1 ou posterior)  
 A partir do Unity 5.2, você não precisa mais importar o unitypackage das Ferramentas do Visual Studio para seus projetos. Se seu projeto importar esse unitypackage, o Unity 5.2 o ignorará e carregará as Ferramentas do Visual Studio para Unity diretamente do local de instalação.  
  
#### <a name="1---create-a-unity-project"></a>1 – Criar um projeto do Unity  
 Se já estiver familiarizado com o Unity, você pode criar um novo projeto ou carregar um de seus próprios projetos. Se você estiver carregando um projeto que importou o unitypackage das Ferramentas do Visual Studio para usar as Ferramentas do Visual Studio para Unity com uma versão anterior do Unity, recomendamos que o remova excluindo o diretório UnityVS.  
  
 Caso contrário, se estiver apenas começando a usar o Unity, comece com um tutorial básico. Visite a página Aprender do Unity para encontrar tutoriais sobre projetos de exemplo com que você pode começar e lições com que você pode aprender para criar seu próprio jogo com o Unity. A página Aprenda do Unity tem tutoriais fáceis de seguir para vários jogos diferentes.  
  
 [Tutoriais – Página Aprenda do Unity](http://unity3d.com/learn/tutorials/modules)  
  
#### <a name="2---configure-unity-editor-to-use-visual-studio-tools-for-unity"></a>2 – Configurar o Editor do Unity para usar as Ferramentas do Visual Studio para Unity  
 Para habilitar seu projeto a usar as Ferramentas do Visual Studio para Unity, basta definir o Visual Studio como seu editor de script externo. No Editor do Unity, no menu principal, escolha **Editar, Preferências**; em seguida, na caixa de diálogo **Preferências do Unity**, escolha **Ferramentas Externas**. Em seguida, defina a propriedade **Editor de Script Externo** como a versão do Visual Studio que deseja usar (as Ferramentas do Visual Studio para Unity devem ser instaladas para esta versão do Visual Studio) e verifique se a propriedade **Editor Anexando** está definida.  
  
 Para garantir que o suporte interno para as Ferramentas do Visual Studio para Unity esteja habilitado, consulte a caixa de diálogo **Sobre o Unity**. No editor do Unity, no menu principal, escolha **Ajuda, Sobre o Unity.** Se as Ferramentas do Visual Studio para Unity estiverem instaladas e configuradas corretamente, você verá uma mensagem no canto inferior esquerdo da caixa de diálogo **Sobre o Unity**.  
  
 Por fim, verifique se você definiu um destino de build na página **Configurações de Build** e se **Depuração de Script** está habilitado.  
  
 ![Defina as configurações de build do Unity para depuração. ](../cross-platform/media/vstu-debugging-build-settings.png "vstu_debugging_build_settings")  
  
#### <a name="3---launch-visual-studio-from-the-unity-editor"></a>3 – Inicialize o Visual Studio no Editor do Unity  
 A partir do Unity 5.2, o menu da extensão **Ferramentas do Visual Studio** não é mais necessário para inicializar o Visual Studio ou para configurar as Ferramentas do Visual Studio para Unity. Em vez disso, quando o Visual Studio estiver configurado como o editor de script externo, basta escolher o arquivo de script do editor do Unity e seu código será aberto no Visual Studio.  
  
### <a name="previous-versions-of-unity-pre-52"></a>Versões anteriores do Unity (anteriores à 5.2)  
 Antes do Unity 5.2, não havia nenhum suporte interno para as Ferramentas do Visual Studio para Unity. Em vez disso, cada projeto precisava importar o unitypackage das Ferramentas do Visual Studio e definir outras configurações do projeto para usar as Ferramentas do Visual Studio para Unity.  
  
#### <a name="1---create-a-unity-project"></a>1 – Criar um projeto do Unity  
 Se já estiver familiarizado com o Unity, você pode criar um novo projeto ou carregar um de seus próprios projetos. Se estiver iniciando um novo projeto, importe o unitypackage das Ferramentas do Visual Studio quando criá-lo.  
  
 Caso contrário, se estiver apenas começando a usar o Unity, comece com um tutorial básico. Visite a página Aprender do Unity para encontrar tutoriais sobre projetos de exemplo com que você pode começar e lições com que você pode aprender para criar seu próprio jogo com o Unity. A página Aprenda do Unity tem tutoriais fáceis de seguir para vários jogos diferentes.  
  
 [Tutoriais – Página Aprenda do Unity](http://unity3d.com/learn/tutorials/modules)  
  
#### <a name="2---configure-unity-editor-to-use-visual-studio-tools-for-unity"></a>2 – Configurar o Editor do Unity para usar as Ferramentas do Visual Studio para Unity  
 Se estiver começando de um projeto existente do Unity ou se não tiver importado o unitypackage das Ferramentas do Visual Studio quando criou o projeto, você precisará importar o unitypackage agora. No editor do Unity, no menu principal, escolha **Ativos, Importar Pacote, Ferramentas do Visual Studio 2015** (você verá uma opção para a versão do Visual Studio que tiver instalado).  
  
 ![Importe o pacote do VSTU para seu projeto do Unity.](../cross-platform/media/vstu-configure-unity-import-vstu.png "vstu_configure_unity_import_vstu")  
  
 Por fim, verifique se você definiu um destino de build na página **Configurações de Build** e se **Depuração de Script** está habilitado.  
  
 ![Defina as configurações de build do Unity para depuração. ](../cross-platform/media/vstu-debugging-build-settings.png "vstu_debugging_build_settings")  
  
#### <a name="3---launch-visual-studio-from-unity-editor"></a>3 – Inicializar o Visual Studio no Editor do Unity  
 A etapa final é iniciar o Visual Studio no Unity. Isso cria uma solução do Visual Studio para seu projeto e a abre no Visual Studio.  
  
 No Editor do Unity, no menu principal, escolha **Ferramentas do Visual Studio, Abrir no Visual Studio**.  
  
 ![Abra seu projeto do Unity no Visual Studio.](../cross-platform/media/vstu-configure-open-in-visual-studio.png "vstu_configure_open_in_visual_studio")  
  
## <a name="next-steps"></a>Próximas etapas  
 Para saber como trabalhar e como depurar seu projeto do Unity no Visual Studio, consulte [Usando as Ferramentas do Visual Studio para Unity](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md).  
  
## <a name="see-also"></a>Consulte também  
 [Home page do Unity](http://unity3d.com)

