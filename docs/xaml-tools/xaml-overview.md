---
title: Visão geral do XAML
ms.date: 06/23/2020
ms.topic: overview
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: e14e23f9820301374bd435484ba784edf50294bb
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331942"
---
# <a name="overview-of-xaml"></a>Visão geral do XAML

XAML (Extensible Application Markup Language) é uma linguagem declarativa baseada em XML. O XAML é usado extensivamente nos seguintes tipos de aplicativos para criar interfaces do usuário:

- [Aplicativos WPF (Windows Presentation Foundation)](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [Aplicativos Plataforma Universal do Windows (UWP)](/windows/uwp/xaml-platform/xaml-overview)
- [Aplicativos do Xamarin.Forms](/xamarin/xamarin-forms/xaml/)

O código XAML a seguir define um controle de botão simples.

```xaml
<Button Click="ButtonClick">Show updates</Button>
```

O XAML também é usado para definir fluxos de trabalho em [aplicativos do WF (Windows Workflow Foundation)](/dotnet/framework/windows-workflow-foundation/serializing-workflows-and-activities-to-and-from-xaml).

## <a name="xaml-code-editor"></a>Editor de código XAML

O [Editor de código XAML](xaml-code-editor.md) no IDE do Visual Studio inclui todas as ferramentas necessárias para criar aplicativos WPF e UWP para a plataforma Windows e para Xamarin. Forms. E, embora o IDE (ambiente de desenvolvimento integrado) no Visual Studio tenha muitos recursos que você pode usar para desenvolver aplicativos para outras plataformas, ele também tem alguns recursos que são exclusivos do XAML.

## <a name="xaml-designer"></a>XAML Designer

O Visual Studio e o Blend para Visual Studio fornecem um [Designer XAML](creating-a-ui-by-using-xaml-designer-in-visual-studio.md) que ajuda a criar interfaces de usuário (IU) para aplicativos WPF, UWP e Xamarin. Forms. Você pode arrastar controles das janelas Caixa de ferramentas ou Ativos e definir propriedades na janela Propriedades. Quando você faz isso, o Visual Studio e o Blend para Visual Studio criam o código XAML correspondente. Se você preferir, também poderá editar diretamente o código XAML.

## <a name="whats-new"></a>Novidades

Para obter as informações mais recentes, consulte os seguintes recursos:

- As **[melhorias nas ferramentas XAML na postagem no blog do Visual Studio 2019 versão 16,7 Preview 1](https://devblogs.microsoft.com/visualstudio/improvements-to-xaml-tooling-in-visual-studio-2019-version-16-7-preview-1/)**
- A postagem **[novidades nas ferramentas de desenvolvedor XAML na publicação do blog do Visual Studio 2019](https://devblogs.microsoft.com/visualstudio/whats-new-in-xaml-developer-tools-in-visual-studio-2019-for-wpf-uwp/)**
- Os **[novos recursos XAML no vídeo do Visual Studio](https://youtu.be/yI9OyA4ZM2E)** sobre o YouTube

## <a name="see-also"></a>Veja também

- [XAML em aplicativos WPF](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [XAML em aplicativos UWP](/windows/uwp/xaml-platform/xaml-overview)
- [XAML em aplicativos do Xamarin.Forms](/xamarin/xamarin-forms/xaml/)
