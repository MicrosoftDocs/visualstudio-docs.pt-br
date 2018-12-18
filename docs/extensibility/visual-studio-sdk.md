---
title: SDK do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b5701044e20f2122199d9d0ca5558e453e6e5f72
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906020"
---
# <a name="visual-studio-sdk"></a>SDK do Visual Studio
O SDK do Visual Studio ajuda você a estender os recursos do Visual Studio ou integrar novos recursos no Visual Studio. Você pode distribuir suas extensões para outros usuários, bem como o Visual Studio Marketplace. Seguem algumas das maneiras em que você pode estender o Visual Studio:  
  
- Adicionar comandos, botões, menus e outros elementos de interface do usuário para o IDE  
  
- Adicionar janelas de ferramentas para a nova funcionalidade  
  
- Estender o IntelliSense para um determinado idioma, ou fornecer o IntelliSense para novas linguagens de programação  
  
- Usar as lâmpadas para fornecer dicas e sugestões para ajudam os desenvolvedores escrevam códigos melhores  
  
- Habilitar o suporte para um novo idioma  
  
- Adicionar um tipo de projeto personalizado  
  
- Alcance milhões de desenvolvedores por meio do Visual Studio Marketplace  
  
  Se você nunca escreveu uma extensão do Visual Studio antes, você deve encontrar mais informações sobre esses recursos e no [começando a desenvolver extensões do Visual Studio](../extensibility/starting-to-develop-visual-studio-extensions.md).  
  
## <a name="install-the-visual-studio-sdk"></a>Instalar o SDK do Visual Studio  
 O SDK do Visual Studio é um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="whats-new-in-the-visual-studio-2017-sdk"></a>O que há de novo no SDK do Visual Studio 2017  
 O SDK do Visual Studio tem alguns recursos novos, como o formato do VSIX v3, bem como alterações da falha, que pode exigir que você atualize sua extensão. Para obter mais informações, consulte [o que há de novo no SDK do Visual Studio 2017](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md).  
  
## <a name="visual-studio-user-experience-guidelines"></a>Diretrizes de experiência de usuário do Visual Studio  
 Obtenha ótimas dicas para projetar a interface do usuário para a sua extensão em [diretrizes de experiência de usuário do Visual Studio](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).  
  
 Você também pode aprender como fazer sua extensão combinam bem com dispositivos de DPI alto com o [endereço DPI emite](../extensibility/addressing-dpi-issues2.md) artigo.  
  
 Aproveitar o [service e o catálogo de imagens](../extensibility/image-service-and-catalog.md) para gerenciamento de imagem grande e suporte para DPI alto e temas.  
  
## <a name="find-and-install-existing-visual-studio-extensions"></a>Localizar e instalar extensões do Visual Studio existentes  
 Você pode encontrar extensões do Visual Studio na **extensões e atualizações** caixa de diálogo na **ferramentas** menu. Para obter mais informações, consulte [localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md). Você também pode encontrar extensões no [Visual Studio marketplace](https://marketplace.visualstudio.com/)  
  
## <a name="visual-studio-sdk-reference"></a>Referência do Visual Studio SDK  
 Você pode encontrar a referência da API do SDK do Visual Studio em [referência de SDK do Visual Studio](../extensibility/visual-studio-sdk-reference.md).  
  
## <a name="visual-studio-sdk-samples"></a>Exemplos do Visual Studio SDK  
 Você pode encontrar exemplos de código-fonte aberto de extensões do SDK do VS no GitHub em [exemplos do Visual Studio](https://aka.ms/vs2015sdksamples). Este repositório GitHub contém exemplos que ilustram diversos recursos extensíveis no Visual Studio.  
  
## <a name="other-visual-studio-sdk-resources"></a>Outros recursos do SDK do Visual Studio  
 Se você tiver dúvidas sobre VSSDK ou deseja compartilhar suas experiências de desenvolvimento de extensões, você pode usar o [Visual Studio Extensibility Forum](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx) ou o [ExtendVS Gitter Chatroom](https://gitter.im/Microsoft/extendvs).  
  
 Você pode encontrar mais informações na [no blog do VSX Arcana](https://blogs.msdn.microsoft.com/vsx/) e uma série de blogs escritos por MVPs da Microsoft:  
  
-   [Extensões do Visual Studio favoritas](http://geekswithblogs.net/sdorman/archive/2014/10/05/favorite-visual-studio-extensions.aspx)  
  
-   [Extensibilidade do Visual Studio](http://www.visualstudioextensibility.com/overview/vs/)  
  
-   [Estendendo o Visual Studio](http://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)   
 [Como: migrar projetos de extensibilidade para o Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)   
 [Perguntas Frequentes: Convertendo suplementos em extensões VSPackage](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md)   
 [Gerenciar vários threads em código gerenciado](../extensibility/managing-multiple-threads-in-managed-code.md)   
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)   
 [Adicionar comandos em barras de ferramentas](../extensibility/adding-commands-to-toolbars.md)   
 [Estender e personalizar janelas de ferramentas](../extensibility/extending-and-customizing-tool-windows.md)   
 [Extensões de serviços do Editor e linguagem](../extensibility/editor-and-language-service-extensions.md)   
 [Estender projetos](../extensibility/extending-projects.md)   
 [Estender opções e configurações de usuário](../extensibility/extending-user-settings-and-options.md)   
 [Criar modelos personalizados de projeto e de item](../extensibility/creating-custom-project-and-item-templates.md)   
 [Estender propriedades e a janela de propriedade](../extensibility/extending-properties-and-the-property-window.md)   
 [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)   
 [Uso e o fornecimento de serviços](../extensibility/using-and-providing-services.md)   
 [Gerenciar VSPackages](../extensibility/managing-vspackages.md)   
 [Shell do Visual Studio isolado](../extensibility/visual-studio-isolated-shell.md)   
 [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)   
 [Dentro do SDK do Visual Studio](../extensibility/internals/inside-the-visual-studio-sdk.md)   
 [Suporte para o SDK do Visual Studio](../extensibility/support-for-the-visual-studio-sdk.md)   
 [Arquivo morto](../extensibility/archive.md)   
 [Referência do Visual Studio SDK](../extensibility/visual-studio-sdk-reference.md)
