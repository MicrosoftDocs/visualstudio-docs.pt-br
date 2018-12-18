---
title: Shell (isolado ou integrado) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio shell
- Visual Studio, Shell
- Shell [Visual Studio]
- Visual Studio shell, shell-based applications
- Shell [Visual Studio], shell-based applications
ms.assetid: c64a9bf0-9bf8-45c3-8fa2-306fa6cab66a
caps.latest.revision: 26
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 856e32d4569e5dcb73e783d0a6b66e186fbb1848
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755875"
---
# <a name="shell-isolated-or-integrated"></a>Shell (isolado ou integrado)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode criar seu próprio aplicativo com base no Visual Studio no modo integrado ou isolado. No modo integrado, muitos recursos do Visual Studio estão disponíveis, além de seu aplicativo. No modo isolado, você deve escolher um subconjunto de recursos do Visual Studio que você deseja distribuir juntamente com sua própria extensão.  
  
## <a name="integrated-mode"></a>Modo integrado  
 Modo integrado permite que os usuários usem os recursos padrão do Visual Studio juntamente com suas ferramentas personalizadas. O shell integrado destina-se principalmente para hospedar linguagens de programação e ferramentas de desenvolvimento de software.  
  
 Ferramentas personalizadas que são criadas automaticamente no shell integrado de mesclagem com qualquer outra edição do Visual Studio está instalado no mesmo computador. Se o Visual Studio não estiver instalado, você pode fornecer uma versão redistribuível do shell do Visual Studio integrado.  
  
 A versão redistribuível do shell integrado do Visual Studio não inclui os recursos que dão suporte a seus respectivos sistemas de projeto e linguagens de programação.  
  
> [!NOTE]
>  O modo integrado do Visual Studio shell pode ser instalado junto com todas as edições do Visual Studio, exceto as edições Express.  
  
 Para obter mais informações, consulte [Visual Studio Shell (integrado)](../extensibility/visual-studio-shell-integrated.md).  
  
## <a name="isolated-mode"></a>Modo isolado  
 Modo isolado permite que você crie ferramentas personalizadas que são executados lado a lado com outras versões do Visual Studio. Ele destina-se principalmente para as ferramentas que podem acessar os serviços do Visual Studio sem dependendo de todos os recursos padrão do Visual Studio. Você pode personalizar a aparência dos aplicativos criados no shell isolado do Visual Studio. Você pode desativar facilmente os recursos e grupos de comando de menu que você não deseja aparecer junto com seu aplicativo.  
  
 Para obter mais informações, consulte [Shell isolado do Visual Studio](../extensibility/visual-studio-isolated-shell.md).  
  
## <a name="distributing-your-integrated-or-isolated-shell-application"></a>Distribuir seu aplicativo de Shell integrado ou isolado  
 Para distribuir seu aplicativo de shell integrado ou isolado, você precisa incluir seu aplicativo, um shell de integrado ou isolado especial redistribuível e um programa de instalação. Para obter mais informações sobre a distribuição e a instalação, consulte [distribuição de aplicativos de Shell isolado](../extensibility/distributing-isolated-shell-applications.md).  
  
> [!IMPORTANT]
>  O [contrato de licença de usuário final (EULA)](https://www.visualstudio.com/en-us/support/legal/mt171552) para o Visual Studio integrado e isolado shells inclui uma seção sobre a coleta de dados (**seção 3. Dados**).  Ele descreve os dados de uso do cliente que podem ser coletados pela Microsoft de usuários do que o software shell integrado ou isolado que você cria em seu aplicativo. Para obter mais informações, consulte [Microsoft Visual Studio produto privacidade da família](https://www.visualstudio.com/en-us/dn948229).  
> 
>  Se você coletar dados de uso separados de seus clientes por meio de seu aplicativo, você deve fornecer o aviso apropriado para usuários do seu aplicativo do qual você coleta.  Quando você distribui o software de shell isolado ou integrado como parte do seu aplicativo, de acordo com a licença do Visual Studio Software Development Kit, você deve incluir um dos seguintes:  
> 
> - o contrato de licença de usuário final como parte da sua licença do aplicativo  
>   -   seus próprios termos de licença que exige que os clientes aceitem termos que protegem o Visual Studio integrado ou isolado shell pelo menos a quantidade como os termos de licença de usuário final Microsoft para o software de shell  
  
## <a name="additional-resources"></a>Recursos adicionais  
 Para obter mais informações sobre os pacotes redistribuíveis, consulte o [Downloads do Visual Studio Extensibility](http://go.microsoft.com/fwlink/?LinkID=119298) site da Web.  
  
## <a name="see-also"></a>Consulte também  
 [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)

