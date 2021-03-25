---
title: SDK do Visual Studio | Microsoft Docs
description: O SDK do Visual Studio ajuda a estender recursos ou adicionar novos recursos ao Visual Studio. Saiba mais sobre algumas das maneiras pelas quais você pode estender o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 91411ec183e6c51abd825af1080c4330ca46fc90
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062519"
---
# <a name="visual-studio-sdk"></a>SDK do Visual Studio
O SDK do Visual Studio ajuda você a estender recursos do Visual Studio ou integrar novos recursos ao Visual Studio. Você pode distribuir suas extensões para outros usuários, bem como para a Visual Studio Marketplace. A seguir estão algumas das maneiras pelas quais você pode estender o Visual Studio:

- Adicionar comandos, botões, menus e outros elementos da interface do usuário ao IDE

- Adicionar janelas de ferramentas para nova funcionalidade

- Estender o IntelliSense para um determinado idioma ou fornecer IntelliSense para novas linguagens de programação

- Use lâmpadas leves para fornecer dicas e sugestões que ajudem os desenvolvedores a escrever código melhor

- Habilitar o suporte para uma nova linguagem

- Adicionar um tipo de projeto personalizado

- Alcance milhões de desenvolvedores por meio do Visual Studio Marketplace

  Se você nunca escreveu uma extensão do Visual Studio antes, você deve encontrar mais informações sobre esses recursos e em [iniciando o desenvolvimento de extensões do Visual Studio](../extensibility/starting-to-develop-visual-studio-extensions.md).

## <a name="install-the-visual-studio-sdk"></a>Instalar o SDK do Visual Studio
 O SDK do Visual Studio é um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="whats-new-in-the-visual-studio-sdk"></a>O que há de novo no SDK do Visual Studio
 O SDK do Visual Studio tem alguns recursos novos, como o formato de as extensões autocarregadas e os formatos VSIX v3, bem como alterações significativas, que podem exigir que você atualize sua extensão. Para obter mais informações, consulte [What ' s New in the visual studio 2019 SDK](../extensibility/whats-new-visual-studio-2019-sdk.md) e [What ' s New in the Visual Studio 2017 SDK](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md).

## <a name="visual-studio-user-experience-guidelines"></a>Diretrizes de experiência do usuário do Visual Studio
 Obtenha ótimas dicas para criar a interface do usuário para sua extensão nas [diretrizes de experiência do usuário do Visual Studio](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).

 Você também pode aprender a fazer com que sua extensão fique ótima em dispositivos DPI altos com o artigo [problemas de dpi de endereço](../extensibility/addressing-dpi-issues2.md) .

 Aproveite o [catálogo e o serviço de imagem](../extensibility/image-service-and-catalog.md) para um excelente gerenciamento de imagens e suporte para DPI alto e temas.

## <a name="find-and-install-existing-visual-studio-extensions"></a>Localizar e instalar as extensões existentes do Visual Studio
 Você pode encontrar extensões do Visual Studio na caixa de diálogo **extensões e atualizações** no menu **ferramentas** . Para obter mais informações, consulte [Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md). Você também pode encontrar extensões no [Visual Studio Marketplace](https://marketplace.visualstudio.com/)

## <a name="visual-studio-sdk-reference"></a>Referência do SDK do Visual Studio
 Você pode encontrar a referência de API do SDK do Visual Studio na [referência do SDK do Visual Studio](../extensibility/visual-studio-sdk-reference.md).

## <a name="visual-studio-sdk-samples"></a>Exemplos do SDK do Visual Studio
 Você pode encontrar exemplos de software livre de extensões do SDK do VS no GitHub em [exemplos do Visual Studio](https://github.com/Microsoft/VSSDK-Extensibility-Samples). Este repositório do GitHub contém exemplos que ilustram vários recursos extensíveis no Visual Studio.

## <a name="other-visual-studio-sdk-resources"></a>Outros recursos do SDK do Visual Studio
 Se você tiver dúvidas sobre o VSSDK ou quiser compartilhar suas experiências desenvolvendo extensões, poderá usar o fórum de [extensibilidade do Visual Studio](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx) ou o [ExtendVS Gitter chatroom](https://gitter.im/Microsoft/extendvs).

 Você pode encontrar mais informações no [blog do VSX Arcana](/archive/blogs/vsx/) e vários Blogs escritos por MVPs da Microsoft:

- [Extensões do Visual Studio favoritas](https://scottdorman.blog/2014/10/05/favorite-visual-studio-extensions/)

- [Extensibilidade do Visual Studio](http://www.visualstudioextensibility.com/overview/vs/)

- [Estendendo o Visual Studio](https://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)

## <a name="see-also"></a>Confira também

- [Criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)
- [Como migrar projetos de extensibilidade para o Visual Studio 2017](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)
- [Perguntas frequentes: convertendo suplementos em extensões VSPackage](/previous-versions/visualstudio/visual-studio-2015/extensibility/faq-converting-add-ins-to-vspackage-extensions?preserve-view=true&view=vs-2015)
- [Gerenciar vários threads em código gerenciado](../extensibility/managing-multiple-threads-in-managed-code.md)
- [Estender menus e comandos](../extensibility/extending-menus-and-commands.md)
- [Adicionar comandos a barras de ferramentas](../extensibility/adding-commands-to-toolbars.md)
- [Estender e personalizar janelas de ferramentas](../extensibility/extending-and-customizing-tool-windows.md)
- [Extensões do editor e do serviço de linguagem](../extensibility/editor-and-language-service-extensions.md)
- [Estender projetos](../extensibility/extending-projects.md)
- [Estender as configurações e opções de usuário](../extensibility/extending-user-settings-and-options.md)
- [Criar modelos de item e projeto personalizados](../extensibility/creating-custom-project-and-item-templates.md)
- [Estender Propriedades e a janela de propriedades](../extensibility/extending-properties-and-the-property-window.md)
- [Estender outras partes do Visual Studio](../extensibility/extending-other-parts-of-visual-studio.md)
- [Usar e fornecer serviços](../extensibility/using-and-providing-services.md)
- [Gerenciar VSPackages](../extensibility/managing-vspackages.md)
- [Shell isolado do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
- [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md)
- [Por dentro do SDK do Visual Studio](../extensibility/internals/inside-the-visual-studio-sdk.md)
- [Suporte para o SDK do Visual Studio](../extensibility/support-for-the-visual-studio-sdk.md)
- [Referência do SDK do Visual Studio](../extensibility/visual-studio-sdk-reference.md)