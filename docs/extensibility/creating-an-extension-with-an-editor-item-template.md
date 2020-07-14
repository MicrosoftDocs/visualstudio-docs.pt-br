---
title: Criando uma extensão com um modelo de item do editor | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 91daa7e195435f33b93e6286cb19d820b4418d48
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903839"
---
# <a name="create-an-extension-with-an-editor-item-template"></a>Criar uma extensão com um modelo de item do editor
Você pode usar modelos de item que estão incluídos no SDK do Visual Studio para criar extensões básicas do editor que adicionam classificadores, adornos e margens ao editor. Os modelos de item do editor estão disponíveis para projetos VSIX do Visual C# ou Visual Basic.

## <a name="prerequisites"></a>Pré-requisitos
 A partir do Visual Studio 2015, você não instala o SDK do Visual Studio a partir do centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-classifier-extension"></a>Criar uma extensão de classificador
 O modelo de item classificador de editor cria um classificador de editor que colore o texto apropriado (nesse caso, tudo) em qualquer arquivo de texto.

1. Na caixa de diálogo **novo projeto** , expanda **Visual C#** ou **Visual Basic** e clique em **extensibilidade**. No painel **modelos** , selecione **projeto VSIX**. Na caixa **Nome**, digite `TestClassifier`. Clique em **OK**.

2. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Vá para o nó **extensibilidade** do Visual C# e selecione **classificador de editor**. Deixe o nome de arquivo padrão (*EditorClassifier1.cs*).

3. Há quatro arquivos de código, da seguinte maneira:

    - *EditorClassifier1.cs* contém a `EditorClassifier1` classe.

    - *EditorClassifier1ClassificationDefinition.cs* contém a `EditorClassifier1ClassificationDefinition` classe.

    - *EditorClassifier1Format.cs* contém a `EditorClassifier1Format` classe.

    - *EditorClassifier1Provider.cs* contém a `EditorClassifier1Provider` classe.

4. Compile o projeto e comece a depuração. A instância experimental do Visual Studio é exibida.

     Se você abrir um arquivo de texto, todo o texto será sublinhado em relação a um plano de fundo violeta.

## <a name="create-a-text-relative-adornment-extension"></a>Criar uma extensão Adornment relativa a texto
 O modelo de texto Adornment do editor cria um Adornment relativo a texto que decora todas as instâncias do caractere de texto ' a ' usando uma caixa que tem um contorno vermelho e um plano de fundo azul. Ele é relativo a texto porque a caixa sempre sobrepõe os caracteres ' a ', mesmo quando eles são movidos ou reformatados.

1. Na caixa de diálogo **novo projeto** , expanda **Visual C#** ou **Visual Basic** e clique em **extensibilidade**. No painel **modelos** , selecione **projeto VSIX**. Na caixa **Nome**, digite `TestAdornment`. Clique em **OK**.

2. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Vá para o nó **extensibilidade** do Visual C# e selecione **texto do editor Adornment**. Deixe o nome de arquivo padrão (*TextAdornment1.cs/vb*).

3. Há dois arquivos de código, da seguinte maneira:

    - *TextAdornment1.cs* contém a `TextAdornment1` classe.

    - *TextAdornment1TextViewCreationListener.cs* contém a `TextAdornment1TextViewCreationListener` classe.

4. Compile o projeto e comece a depuração. A instância experimental é exibida. Se você abrir um arquivo de texto, todos os caracteres ' a ' no texto serão contornados em vermelho em relação a um plano de fundo azul.

## <a name="create-a-viewport-relative-adornment-extension"></a>Criar uma extensão Adornment relativa ao visor
 O modelo visor Adornment do editor cria um Adornment relativo ao visor que adiciona uma caixa violeta que tem um contorno vermelho no canto superior direito do visor.

> [!NOTE]
> O **visor** é a área da exibição de texto exibida no momento.

### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>Para criar uma extensão Adornment do visor usando o modelo Adornment do visor do editor

1. Na caixa de diálogo **novo projeto** , expanda **Visual C#** ou **Visual Basic** e clique em **extensibilidade**. No painel **modelos** , selecione **projeto VSIX**. Na caixa **Nome**, digite `ViewportAdornment`. Clique em **OK**.

2. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Vá para o nó **extensibilidade** do Visual C# e selecione **Editor visor Adornment**. Deixe o nome de arquivo padrão (*ViewportAdornment1.cs/vb*).

3. Há dois arquivos de código, da seguinte maneira:

    - *ViewportAdornment1.cs* contém a `ViewportAdornment1` classe.

    - *ViewportAdornment1TextViewCreationListener.cs* contém a `ViewportAdornment1TextViewCreationListener` classe

4. Compile o projeto e comece a depuração. A instância experimental é exibida. Se você criar um novo arquivo de texto, uma caixa violeta que tem um contorno vermelho será exibida no canto superior direito do visor.

## <a name="create-a-margin-extension"></a>Criar uma extensão de margem
 O modelo de margem do editor cria uma margem verde que aparece junto com as palavras **Olá, mundo!* abaixo da barra de rolagem horizontal.

### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>Para criar uma extensão de margem usando o modelo de margem do editor

1. Na caixa de diálogo **novo projeto** , expanda **Visual C#** ou **Visual Basic** e clique em **extensibilidade**. No painel **modelos** , selecione **projeto VSIX**. Na caixa **Nome**, digite `MarginExtension`. Clique em **OK**.

2. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Vá para o nó **extensibilidade** do Visual C# e selecione **margem do editor**. Deixe o nome de arquivo padrão (EditorMargin1.cs/vb).

3. Há dois arquivos de código, da seguinte maneira:

    - *EditorMargin1.cs* contém a `EditorMargin1` classe.

    - *EditorMargin1Factory.cs* contém a `EditorMargin1Factory` classe.

4. Compile este projeto e inicie a depuração. A instância experimental é exibida. Se você abrir um arquivo de texto, uma margem verde com as palavras **Hello EditorMargin1** será exibida abaixo da barra de rolagem horizontal.

## <a name="see-also"></a>Confira também
- [Pontos de extensão do serviço de linguagem e do editor](../extensibility/language-service-and-editor-extension-points.md)
