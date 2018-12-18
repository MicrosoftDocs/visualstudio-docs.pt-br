---
title: O que&#39;novo no SDK do Visual Studio 2015 | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c64aac80-a411-463f-b7bd-8b7607a52ece
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9ea99585913c5bf997d54a11f428fb168633b6e7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51797462"
---
# <a name="what39s-new-in-the-visual-studio-2015-sdk"></a>O que&#39;novo no SDK do Visual Studio 2015
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O SDK do Visual Studio tem os seguintes recursos novos e atualizados para o Visual Studio 2015, o Visual Studio 2015 atualizado e o Visual Studio "15".  
  
## <a name="visual-studio-15-preview-2"></a>Visual Studio "15" Preview 2  
 A partir do Visual Studio "15" visualização 4, verificação de modelos de item e projeto personalizados não serão executadas. Em vez disso, a extensão deve fornecer os arquivos de manifesto de modelo que descrevem o local de instalação desses modelos. Você pode usar a instalação de visualização 2 para atualizar as extensões VSIX. Se você implantar sua extensão usando um MSI, você deve gerar os arquivos de manifesto do modelo manualmente. Para obter mais informações, consulte [atualizando personalizados de projeto e modelos de Item para Visual Studio "15"](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md). O esquema de modelo de manifesto está documentado em [modelo de manifesto do esquema de referência do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).  
  
## <a name="vs-2015-sdk-update-1"></a>Atualização do SDK do VS 2015 1  
 A atualização 1 inclui ferramentas para ajudar a sua extensão funcionam bem com temas de cores e o serviço de imagem do Visual Studio.  
  
 Esses tópicos estão sob o [utilitários VSSDK](../extensibility/internals/vssdk-utilities.md) seção:  
  
-   O [ferramentas de temas de cores](../extensibility/internals/color-theming-tools.md) ajudá-lo a criar e editar cores personalizadas para o Visual Studio.  
  
-   O [ferramentas de serviço de imagem](../extensibility/internals/image-service-tools.md) permitem trabalhar com arquivos de manifesto de imagem do Visual Studio.  
  
## <a name="new-way-to-add-the-visual-studio-sdk-to-visual-studio"></a>Nova maneira de adicionar o SDK do Visual Studio para o Visual Studio  
 A partir do Visual Studio 2015, você não precisará baixar o SDK do Visual Studio separadamente. Em vez disso, você pode instalá-lo como parte do processo de instalação normal, ou você pode optar por instalá-lo mais tarde. Quando você abre ou cria uma solução VSIX, o Visual Studio solicitará que você instale as ferramentas de extensibilidade do Visual Studio. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="new-ways-of-creating-extensions"></a>Novas maneiras de criação de extensões  
 A partir do SDK do Visual Studio 2015, você tem opções diferentes para criar extensões, dependendo da linguagem de programação que você está usando.  
  
### <a name="visual-c-and-visual-basic"></a>Visual C# e Visual Basic  
 Para c# e Visual Basic, há uma ampla gama de modelos de item de projeto que permitem que você crie os VSPackages, comandos de menu, janelas de ferramentas, classificadores de editor, editor adornos e as extensões de margem do editor. Você pode adicionar qualquer ou todos eles ao projeto do VSIX standard. Para obter mais informações, consulte:  
  
-   [Criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
-   [Criar uma extensão com uma janela de ferramentas](../extensibility/creating-an-extension-with-a-tool-window.md)  
  
-   [Criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md)  
  
-   [Criar uma extensão com um VSPackage](../extensibility/creating-an-extension-with-a-vspackage.md)  
  
     O Assistente de VSPackage não cria mais extensões em c# ou Visual Basic.  
  
### <a name="c"></a>C++  
 Para C++, o Assistente de VSPackage dar suporte a editores personalizados, as janelas de ferramentas e comandos de menu. Procure-na **novo projeto** caixa de diálogo no **Visual C++ / extensibilidade**.  
  
## <a name="vs-sdk-reference-assemblies-via-nuget"></a>Assemblies de referência SDK do VS por meio do NuGet  
 Para maior portabilidade e compartilhamento de projetos de extensibilidade, você pode usar as versões do NuGet dos assemblies de referência do SDK do VS.  Eles estão disponíveis no [nuget.org](http://www.nuget.org) publicado pela [VisualStudioExtensibility](http://www.nuget.org/profiles/VisualStudioExtensibility) e pode ser facilmente adicionado ao seu projeto ou solução por meio do Visual Studio **referencia / gerenciar NuGet Pacotes** caixa de diálogo. Você pode adicionar individuais referências aos assemblies de extensibilidade específicos ou adicionar o SDK do VS faz referência a assemblies ao mesmo tempo usando o SDK do VS [metapacote](http://www.nuget.org/packages/VSSDK_Reference_Assemblies). Para saber mais sobre o NuGet, consulte [visão geral do NuGet](http://docs.nuget.org/) e [gerenciar pacotes de NuGet usando a caixa de diálogo](http://docs.nuget.org/Consume/Package-Manager-Dialog).  
  
 Quando você usa as versões do NuGet dos assemblies de referência do SDK do VS, outro usuário não precisa instalar o SDK do VS para abrir e compilar seu projeto.  Os assemblies de referência do NuGet e ferramentas de build do SDK do VS serão instaladas automaticamente em seu computador para o projeto.  
  
 Os modelos de item do SDK do VS usam NuGet para suas referências e ferramentas de compilação para que você obtenha os benefícios do NuGet por padrão.  
  
> [!NOTE]
>  Você pode continuar a usar os assemblies de referência do SDK do VS instalado com seus projetos (localizado em \<local de instalação do Visual Studio > \ VSSDK\VisualStudioIntegration\Common\Assemblies) e projetos de extensibilidade existentes não precisam ser atualizado para usar pacotes NuGet.  O projeto **referencia / adicionar referência** diálogo continua a usar os assemblies de referência do SDK do VS instalado.  
>   
>  Se você quiser modificar seus projetos existentes para usar o NuGet, consulte [como: migrar VSPackages ao Visual Studio 2015](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2015.md) que tem uma seção sobre como atualizar projetos de extensibilidade para pacotes do NuGet.  
  
## <a name="light-bulbs"></a>Lâmpadas  
 Uma das maneiras de novo mais interessantes de escrever código de extensão é fornecida pelo projeto Roslyn. Para obter mais informações, consulte [Roslyn](https://github.com/dotnet/Roslyn).  
  
 As lâmpadas são um novo recurso que é fornecido com VSSDK. Eles são ícones usados no editor do Visual Studio que expandem para exibir um conjunto de ações de refatoração de código ou correções para problemas identificados pelos analisadores de código internos. Para obter mais informações, consulte [instruções passo a passo: Exibir sugestões de lâmpada](../extensibility/walkthrough-displaying-light-bulb-suggestions.md).  
  
## <a name="updated-user-experience-guidelines"></a>Diretrizes da experiência do usuário atualizada  
 Criando recursos ou novas extensões para Visual Studio? Fazer check-out atualizado e expandida [diretrizes de experiência de usuário do Visual Studio](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md).  Você encontrará a [tokens de cor](../extensibility/ux-guidelines/shared-colors-for-visual-studio.md), [tamanhos de fonte](../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md), [especificações de layout de caixa de diálogo](../extensibility/ux-guidelines/layout-for-visual-studio.md)e outras diretrizes necessárias para integrar sua nova interface do usuário com o Visual Studio.

