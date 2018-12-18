---
title: Criar uma extensão com um modelo de Item do Editor | Microsoft Docs
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
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ab22549550c0564f7e27b88adae4627f24ab9acc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51772736"
---
# <a name="creating-an-extension-with-an-editor-item-template"></a>Criando uma extensão com um modelo de item do editor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar modelos de item que estão incluídos no SDK do Visual Studio para criar extensões de editor básico que adicionar classificadores, adornos e margens no Editor. Os modelos de item editor estão disponíveis para projetos do Visual c# ou Visual Basic VSIX.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ele é incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="creating-a-classifier-extension"></a>Criando uma extensão do classificador  
 O modelo de item do classificador de Editor cria um classificador de editor que o texto apropriado de cores (nesse caso, tudo) em qualquer arquivo de texto.  
  
1.  No **novo projeto** diálogo caixa, expanda **Visual c#** ou **Visual Basic** e, em seguida, clique em **extensibilidade**. No **modelos** painel, selecione **projeto VSIX**. Na caixa **Nome**, digite `TestClassifier`. Clique em **OK**.  
  
2.  No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. Vá para o Visual c# **extensibilidade** nó e selecione **Editor de classificador**. Deixe o nome de arquivo padrão (EditorClassifier1.cs).  
  
3.  Há três arquivos de código, da seguinte maneira:  
  
    -   EditorClassifier1.cs contém o `EditorClassifier1` classe.  
  
    -   EditorClassifier1ClassificationDefinition.cs contém o `OEditorClassifier1ClassificationDefinition` classe.  
  
    -   EditorClassifier1Format.cs contém o `EditorClassifier1Format` classe.  
  
    -   EditorClassifier1Provider.cs contém o `EditorClassifier1Provider` classe.  
  
4.  Compile o projeto e comece a depuração. A instância experimental do Visual Studio é exibida.  
  
     Se você abrir um arquivo de texto, todo o texto está sublinhado em relação a um plano de fundo violeta.  
  
## <a name="creating-a-text-relative-adornment-extension"></a>Criando uma extensão do adorno relativo do texto  
 O modelo de adornos de texto do Editor cria um adorno de texto relativo que decora todas as instâncias do caractere de texto 'a' por meio de uma caixa com um contorno vermelho e um plano de fundo azul. Ele é relativo ao texto porque a caixa sempre sobrepõe as 'a' caracteres, mesmo quando eles são movidos ou reformatados.  
  
1.  No **novo projeto** diálogo caixa, expanda **Visual c#** ou **Visual Basic** e, em seguida, clique em **extensibilidade**. No **modelos** painel, selecione **projeto VSIX**. Na caixa **Nome**, digite `TestAdornment`. Clique em **OK**.  
  
2.  No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. Vá para o Visual c# **extensibilidade** nó e selecione **Editor de texto adorno**. Deixe o nome de arquivo padrão (TextAdornment1.cs/vb).  
  
3.  Há dois arquivos de código, da seguinte maneira:  
  
    -   TextAdornment1.cs contém o `TextAdornment1` classe.  
  
    -   extAdornment1TextViewCreationListener.cs contém o `TextAdornment1TextViewCreationListener` classe.  
  
4.  Compile o projeto e comece a depuração. A instância experimental é exibida. Se você abrir um arquivo de texto, todos os 'a' caracteres no texto são realçados em vermelho em relação a um plano de fundo azul.  
  
## <a name="creating-a-viewport-relative-adornment-extension"></a>Criando uma extensão do adorno relativo ao visor  
 O modelo do adorno de visor Editor cria um adorno de visor relativo que adiciona uma caixa violeta que tem um contorno vermelho para o canto superior direito do visor.  
  
> [!NOTE]
>  O *visor* é a área do modo de exibição de texto que está sendo exibida.  
  
#### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>Para criar uma extensão de adorno do visor, usando o modelo do adorno de visor do Editor  
  
1.  No **novo projeto** diálogo caixa, expanda **Visual c#** ou **Visual Basic** e, em seguida, clique em **extensibilidade**. No **modelos** painel, selecione **projeto VSIX**. Na caixa **Nome**, digite `ViewportAdornment`. Clique em **OK**.  
  
2.  No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. Vá para o Visual c# **extensibilidade** nó e selecione **Editor de visor adorno**. Deixe o nome de arquivo padrão (ViewportAdornment1.cs/vb).  
  
3.  Há dois arquivos de código, da seguinte maneira:  
  
    -   ViewportAdornment1.cs contém o `ViewportAdornment1` classe.  
  
    -   ViewportAdornment1TextViewCreationListener.cs contém o `ViewportAdornment1TextViewCreationListener` classe  
  
4.  Compile o projeto e comece a depuração. A instância experimental é exibida. Se você criar um novo arquivo de texto, uma caixa violeta que tem um contorno vermelho é exibida no canto superior direito do visor.  
  
## <a name="creating-a-margin-extension"></a>Criando uma extensão de margem  
 O modelo de margem do Editor cria uma margem de verde é exibida junto com as palavras "Hello world!" abaixo da barra de rolagem horizontal.  
  
#### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>Para criar uma extensão de margem, usando o modelo de margem do Editor  
  
1.  No **novo projeto** diálogo caixa, expanda **Visual c#** ou **Visual Basic** e, em seguida, clique em **extensibilidade**. No **modelos** painel, selecione **projeto VSIX**. Na caixa **Nome**, digite `MarginExtension`. Clique em **OK**.  
  
2.  No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **Add / Novo Item**. Vá para o Visual c# **extensibilidade** nó e selecione **Editor de visor adorno**. Deixe o nome de arquivo padrão (EditorMargin1.cs/vb).  
  
3.  Há dois arquivos de código, da seguinte maneira:  
  
    -   EditorMargin1.cs contém o `EditorMargin1` classe.  
  
    -   EditorMargin1Factory.cs contém o `EditorMargin1Factory` classe.  
  
4.  Compilar esse projeto e iniciar a depuração. A instância experimental é exibida. Se você abrir um arquivo de texto, uma margem verde que tem as palavras "Olá, EditorMargin1" é exibida abaixo de barra de rolagem horizontal.  
  
## <a name="see-also"></a>Consulte também  
 [Serviço de linguagem e pontos de extensão do editor](../extensibility/language-service-and-editor-extension-points.md)

