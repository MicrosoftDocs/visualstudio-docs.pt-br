---
title: SDK do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
caps.latest.revision: 57
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e64506ca544dd3811864358f9c928f6893dc8448
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758979"
---
# <a name="visual-studio-sdk"></a>SDK do Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O SDK do Visual Studio ajuda você a estender os recursos do Visual Studio ou integrar novos recursos no Visual Studio. Você pode distribuir suas extensões para outros usuários, bem como a Galeria do Visual Studio. Seguem algumas das maneiras em que você pode estender o Visual Studio:  
  
- Adicionar comandos, botões, menus e outros elementos de interface do usuário para o IDE  
  
- Adicionar janelas de ferramentas para a nova funcionalidade  
  
- Estender o IntelliSense para um determinado idioma, ou fornecer o IntelliSense para novas linguagens de programação  
  
- Usar as lâmpadas para fornecer dicas e sugestões para ajudam os desenvolvedores escrevam códigos melhores  
  
- Habilitar o suporte para um novo idioma  
  
- Adicionar um tipo de projeto personalizado  
  
- Alcance milhões de desenvolvedores por meio da Galeria do Visual Studio  
  
  Se você nunca escreveu uma extensão do Visual Studio antes, você deve encontrar mais informações sobre esses recursos e no [começando a desenvolver extensões do Visual Studio](../extensibility/starting-to-develop-visual-studio-extensions.md).  
  
## <a name="installing-the-visual-studio-sdk"></a>Instalar o SDK do Visual Studio  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="whats-new-in-the-visual-studio-2015-sdk"></a>O que há de novo no SDK do Visual Studio 2015  
 O SDK do Visual Studio tem alguns recursos novos, incluindo as lâmpadas e novos itens de projeto que permitem que você crie comandos de menu, janelas de ferramentas e extensões de editor usando um pacote VSIX. Para obter mais informações, consulte [o que há de novo no SDK do Visual Studio 2015](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md).  
  
## <a name="visual-studio-user-experience-guidelines"></a>Diretrizes da experiência do usuário do Visual Studio  
 Obtenha ótimas dicas para projetar a interface do usuário para a sua extensão em [diretrizes de experiência de usuário do Visual Studio](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).  
  
 Você também pode aprender como fazer sua extensão combinam bem com dispositivos de DPI alto com nossos [abordar questões de DPI](../extensibility/addressing-dpi-issues2.md) tópico.  
  
 Aproveitar o [serviço de imagem e catálogo](../extensibility/image-service-and-catalog.md) para gerenciamento de imagem grande e suporte para DPI alto e temas.  
  
## <a name="finding-and-installing-existing-visual-studio-extensions"></a>Localizando e instalando extensões existentes do Visual Studio  
 Você pode encontrar extensões do Visual Studio na **extensões e atualizações** caixa de diálogo na **ferramentas** menu. Para obter mais informações, consulte [Localizando e usando extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md). Você também pode encontrar extensões no [Galeria do Visual Studio](https://visualstudiogallery.msdn.microsoft.com/)  
  
## <a name="visual-studio-sdk-reference"></a>Referência ao SDK do Visual Studio  
 Você pode encontrar a referência da API do SDK do Visual Studio em [referência de SDK do Visual Studio](../extensibility/visual-studio-sdk-reference.md).  
  
## <a name="visual-studio-sdk-samples"></a>Exemplos SDK do Visual Studio  
 Você pode encontrar exemplos de código-fonte aberto de extensões do SDK do VS no GitHub em [exemplos do Visual Studio](https://aka.ms/vs2015sdksamples). Este repositório GitHub contém exemplos que ilustram diversos recursos extensíveis no Visual Studio.  
  
## <a name="other-visual-studio-sdk-resources"></a>Outros recursos SDK do Visual Studio  
 Se você tiver dúvidas sobre VSSDK ou deseja compartilhar suas experiências de desenvolvimento de extensões, você pode usar o [Visual Studio Extensibility Forum](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx) ou o [Chat de grupo ExtendVS](https://gitter.im/Microsoft/extendvs).  
  
 Você pode encontrar mais informações na [no blog do VSX Arcana](http://blogs.msdn.com/b/vsx/) e um número de blogs escritos por MVPs da Microsoft:  
  
-   [Extensões do Visual Studio favoritas](http://geekswithblogs.net/sdorman/archive/2014/10/05/favorite-visual-studio-extensions.aspx)  
  
-   [Extensibilidade do Visual Studio](http://www.visualstudioextensibility.com/overview/vs/)  
  
-   [Estendendo o Visual Studio](http://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md)   
 [Como: migrar projetos de extensibilidade para o Visual Studio 2015](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md)   
 [Perguntas Frequentes: Convertendo suplementos em extensões VSPackage](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md)   
 [Gerenciar vários Threads em código gerenciado](../extensibility/managing-multiple-threads-in-managed-code.md)   
 [Ampliar Menus e comandos](../extensibility/extending-menus-and-commands.md)   
 [Adicionando comandos em barras de ferramentas](../extensibility/adding-commands-to-toolbars.md)   
 [Estendendo e personalizando o Windows de ferramenta](../extensibility/extending-and-customizing-tool-windows.md)   
 [Editor e extensões do serviço de linguagem](../extensibility/editor-and-language-service-extensions.md)   
 [Estendendo projetos](../extensibility/extending-projects.md)   
 [Opções e configurações de usuário de extensão](../extensibility/extending-user-settings-and-options.md)   
 [Criando modelos de Item e projeto personalizados](../extensibility/creating-custom-project-and-item-templates.md)   
 [Estendendo propriedades e a janela de propriedade](../extensibility/extending-properties-and-the-property-window.md)   
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)   
 [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)   
 [Estendendo os serviços conectados](../extensibility/extending-connected-services.md)   
 [Gerenciar VSPackages](../extensibility/managing-vspackages.md)   
 [Shell isolado do Visual Studio](../extensibility/visual-studio-isolated-shell.md)   
 [Envio de extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)   
 [Dentro do SDK do Visual Studio](../extensibility/internals/inside-the-visual-studio-sdk.md)   
 [Suporte para o SDK do Visual Studio](../extensibility/support-for-the-visual-studio-sdk.md)   
 [Arquivo morto](../extensibility/archive.md)   
 [Referência do SDK do Visual Studio](../extensibility/visual-studio-sdk-reference.md)

