---
title: Introdução ao serviço de linguagem e às extensões do editor
description: Saiba como adicionar recursos de serviço de linguagem a qualquer tipo de conteúdo e personalizar a aparência e o comportamento do editor do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 6b151891-c06d-40b1-9867-42298caa8492
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1afec04882d5d52bffac509dd1d1202ccf9ea449
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057605"
---
# <a name="get-started-with-language-service-and-editor-extensions"></a>Introdução ao serviço de linguagem e às extensões do editor

Você pode usar extensões do editor para adicionar recursos de serviço de linguagem, como estrutura de tópicos, correspondência de chaves, IntelliSense e lâmpadas de iluminação à sua própria linguagem de programação ou a qualquer tipo de conteúdo. Você também pode personalizar a aparência e o comportamento do editor do Visual Studio, por exemplo, coloração de texto, margens, adornos e outros elementos visuais. Você também pode definir seu próprio tipo de conteúdo e especificar a aparência e o comportamento das exibições de texto nas quais seu conteúdo é exibido.

 Para começar a escrever extensões do editor, use os modelos de projeto do editor instalados como parte do SDK do Visual Studio. O SDK do Visual Studio é um conjunto de ferramentas para download que facilita o desenvolvimento de extensões do Visual Studio, usando VSPackages ou usando o Managed Extensibility Framework (MEF).

> [!NOTE]
> Para obter mais informações sobre o SDK do Visual Studio, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).

 Recomendamos que você conheça os conceitos e as tecnologias a seguir antes de escrever suas próprias extensões de editor.

## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>As extensões do Windows Presentation Foundation (WPF) e do editor

 A interface do usuário (IU) do editor do Visual Studio é implementada usando o Windows Presentation Foundation (WPF). O WPF fornece uma rica experiência visual e um modelo de programação consistente que separa os aspectos visuais do código da lógica de negócios. Você pode usar muitos elementos e recursos do WPF ao criar extensões de editor. Para obter mais informações, consulte [Windows Presentation Foundation](/dotnet/framework/wpf/index).

## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>As extensões Managed Extensibility Framework (MEF) e editor

 O editor do Visual Studio usa o Managed Extensibility Framework (MEF) para gerenciar seus componentes e extensões. O MEF também permite que os desenvolvedores criem extensões com mais facilidade para um aplicativo host como o Visual Studio. Nessa estrutura, você define uma extensão de acordo com um contrato de MEF e a exporta como uma parte de componente do MEF. O aplicativo host gerencia as partes do componente encontrando-as, registrando-as e garantindo que elas sejam aplicadas ao contexto correto.

> [!NOTE]
> Para obter mais informações sobre o MEF no editor, consulte [Managed Extensibility Framework no editor](../extensibility/managed-extensibility-framework-in-the-editor.md).

## <a name="visual-studio-editor-extension-points-and-extensions"></a>Pontos e extensões de extensão do editor do Visual Studio

 Os pontos de extensão do editor são partes de componentes do MEF que você pode personalizar e estender. Em alguns casos, você estende o ponto de extensão implementando uma interface e exportando-a junto com os metadados corretos. Em outros casos, basta declarar uma extensão e exportá-la como um tipo específico.

 A seguir estão alguns dos tipos básicos de extensões do editor:

- Margens e barras de rolagem

- Marcações

- Adornos

- Opções

- IntelliSense

  Para obter mais informações sobre pontos de extensão do editor, consulte [serviço de linguagem e pontos de extensão do editor](../extensibility/language-service-and-editor-extension-points.md).

## <a name="deploying-editor-extensions"></a>Implantando extensões do editor

 No Visual Studio, você implanta extensões do editor adicionando um arquivo de metadados chamado *Source. Extension. vsixmanifest* à solução, compilando a solução e, em seguida, adicionando uma cópia dos arquivos binários e o manifesto em uma pasta conhecida pelo Visual Studio. O arquivo de manifesto define os fatos básicos sobre a extensão (por exemplo, nome, autor, versão e tipo de conteúdo). Para obter mais informações sobre o arquivo de manifesto do VSIX e como implantar extensões, consulte [Enviar extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md).

 Quando você instala uma extensão em um computador, inclui os binários e o manifesto em uma subpasta da pasta que é conhecida pelo Visual Studio.

> [!WARNING]
> Você não precisa se preocupar com os detalhes de manifestos e locais de implantação se usar um dos modelos de extensibilidade do editor que estão incluídos no Visual Studio. Os modelos contêm tudo o que é necessário para registrar e implantar uma extensão.

## <a name="run-extensions-in-the-experimental-instance"></a>Executar extensões na instância experimental

 Você pode isolar sua versão de trabalho do Visual Studio enquanto estiver desenvolvendo uma extensão, implantando-a na seguinte pasta experimental (no Windows Vista e no Windows 7):

 *{% LOCALAPPDATA%} \VisualStudio\10.0Exp\Extensions \\ {empresa} \\ {ExtensionId}*

 onde *% LocalAppData%* é o nome do usuário conectado, *empresa* é o nome da empresa que possui a extensão e *ExtensionId* é a ID da extensão.

 Quando você implanta uma extensão para o local experimental, ela é executada no modo de depuração. Uma segunda instância do Visual Studio é iniciada e é nomeada **Microsoft Visual Studio instância experimental**.

## <a name="manage-extensions"></a>Gerenciar extensões

 As extensões para o Visual Studio são listadas em **extensões e atualizações** (no menu **ferramentas** ). Se você estiver testando uma extensão na instância experimental, ela será listada em **extensões e atualizações** na instância experimental, mas não será listada na instância de desenvolvimento.

 Para obter mais informações, consulte [Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md).

## <a name="use-templates-to-create-editor-extensions"></a>Usar modelos para criar extensões do editor

 Você pode usar modelos do editor para criar extensões de MEF que personalizem classificadores, adornos e margens. Há modelos para projetos em C# e Visual Basic. Para obter mais informações, consulte [criar uma extensão com um modelo de item do editor](../extensibility/creating-an-extension-with-an-editor-item-template.md).

 Você também pode usar o modelo de projeto VSIX para criar extensões. Esse modelo fornece apenas os elementos necessários para implantar qualquer tipo de extensão e inclui o arquivo *Source. Extension. vsixmanifest* , as referências de assembly necessárias e um arquivo de projeto que inclui as tarefas de compilação que permitem que você implante a extensão. Para obter mais informações, consulte [modelo de projeto VSIX](../extensibility/vsix-project-template.md).

 Você também pode criar componentes do MEF do editor de uma extensão de pacote do Visual Studio. Consulte as instruções a seguir para obter detalhes:

- [Walkthrough: usando um comando do shell com uma extensão do editor](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)

- [Walkthrough: usando uma tecla de atalho com uma extensão do editor](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)

## <a name="see-also"></a>Confira também

- [Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)
