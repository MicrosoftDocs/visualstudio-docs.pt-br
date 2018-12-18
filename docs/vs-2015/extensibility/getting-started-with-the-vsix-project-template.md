---
title: Introdução ao modelo de projeto do VSIX | Microsoft Docs
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
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
caps.latest.revision: 26
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1f7230bce49342ad8e31baeb3f46c72f1c45d776
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787725"
---
# <a name="getting-started-with-the-vsix-project-template"></a>Introdução ao modelo de projeto do VSIX
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o modelo de projeto de VSIX para criar uma extensão ou para uma extensão existente para a implantação do pacote. O modelo de projeto do VSIX tem versões de Visual Basic e Visual c# e é instalado como parte do SDK do Visual Studio.  
  
 O modelo de projeto do VSIX apenas consiste em um arquivo de vsixmanifest, que contém informações sobre a extensão e os ativos de que enviá-lo.  
  
 Para localizar o modelo de projeto do VSIX, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
## <a name="deploying-a-custom-project-template-using-the-vsix-project-template"></a>Implantar um modelo de projeto personalizado usando o modelo de projeto do VSIX  
 As etapas a seguir mostram como usar o projeto do VSIX para empacotar um modelo de projeto que você pode compartilhar com outros desenvolvedores ou carregar a Galeria do Visual Studio.  
  
1.  Crie um modelo de projeto.  
  
    1.  Abra o projeto do qual criar um modelo. Este projeto pode ser de qualquer tipo de projeto.  
  
    2.  No menu **Arquivo**, clique em **Exportar Modelo**. Conclua as etapas do assistente.  
  
         Um arquivo. zip é criado no %USERPROFILE%\My Documents\Visual Studio  *\<versão >* \My Exported Templates\\.  
  
2.  Crie um projeto vazio do VSIX.  
  
     Sobre o **arquivo** menu, clique em **New** e, em seguida, clique em **projeto**. Selecione a **Visual Basic** ou **Visual c#**. Sob o nó selecionado, selecione **extensibilidade**e, em seguida, selecione **projeto VSIX**.  
  
3.  Adicione o arquivo. zip para o projeto. Defina suas **Copy to Output Directory** propriedade `Copy Always`.  
  
4.  No **Gerenciador de soluções**, clique duas vezes o `source.extension.vsixmanifest` arquivo para abri-lo no **Designer de manifesto do VSIX**e, em seguida, faça as seguintes alterações:  
  
    -   Defina as **nome do produto** campo **meu modelo de projeto**.  
  
    -   Defina as **ID do produto** campo **MyProjectTemplate - 1**.  
  
    -   Defina as **autor** campo **Fabrikam**.  
  
    -   Defina as **descrição** campo **meu modelo de projeto**.  
  
    -   No **ativos** seção, adicione um **Microsoft.VisualStudio.ProjectTemplate** digite e defina seu caminho para o nome do arquivo. zip.  
  
5.  Salve e feche o arquivo vsixmanifest.  
  
6.  Compile o projeto.  
  
7.  No diretório de saída, clique duas vezes no arquivo. VSIX.  
  
8.  Um **instalador do VSIX** caixa de mensagem é exibida. Siga as instruções para instalar a extensão.  
  
9. Feche o Visual Studio e, em seguida, abra-o novamente.  
  
10. Selecione **extensões e atualizações** (sobre o **ferramentas** menu) e selecione o **modelos** categoria. Uma das extensões disponíveis deve ser **meu modelo de projeto**.  
  
11. O novo modelo de projeto aparece na **novo projeto** caixa de diálogo no mesmo local que o modelo de projeto original. Por exemplo, se você tiver criado um modelo chamado **VB Console** de um aplicativo de console do Visual Basic **Console VB** aparece no painel do mesmo como o Visual Basic **o aplicativo de Console**modelo.  
  
#### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>Para especificar o local do modelo na caixa de diálogo Novo projeto  
  
1.  Pastas de modelos estão localizadas na *caminho de instalação do Visual Studio*\Common7\IDE\ProjectTemplates e *caminho de instalação do Visual Studio*\Common7\IDE\ItemTemplates diretórios. Os nomes das seções de nível superior na caixa de diálogo Novo projeto exatamente não coincidem com os nomes das pastas de modelo. Em que eles forem diferentes, use o nome da pasta do modelo.  
  
     Altere a extensão de arquivo. VSIX para. zip e, em seguida, abra o arquivo.  
  
2.  Crie uma nova pasta com o mesmo nome que a seção da caixa de diálogo Novo projeto em que de modelo deve aparecer.  
  
3.  Se o modelo deve aparecer em uma subseção, crie uma subpasta de mesmo nome.  
  
4.  Mova o arquivo. zip de modelo para a nova pasta.  
  
5.  Altere a extensão. zip para. VSIX.  
  
6.  Abra o manifesto do VSIX.  
  
7.  No manifesto do VSIX, atualize o **ativo** caminho do modelo para que ele aponte para a raiz da árvore de diretório que contém o arquivo de modelo. Por exemplo, se o modelo estiver em \CSharp\Windows, a referência deve apontar para \CSharp.

