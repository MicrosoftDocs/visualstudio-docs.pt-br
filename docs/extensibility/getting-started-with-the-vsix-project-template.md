---
title: Introdução ao modelo de projeto do VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 829ee38e5d22fbc38e47bdf9a2b9e7e9342957cd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49817048"
---
# <a name="get-started-with-the-vsix-project-template"></a>Comece com o modelo de projeto do VSIX
Você pode usar o modelo de projeto de VSIX para criar uma extensão ou para uma extensão existente para a implantação do pacote. O modelo de projeto do VSIX tem versões de Visual Basic e Visual c# e é instalado como parte do SDK do Visual Studio.  

 O modelo de projeto do VSIX consiste apenas em uma *vsixmanifest* arquivo, que contém informações sobre a extensão e os ativos de enviá-lo.  

 Para localizar o modelo de projeto do VSIX, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  

## <a name="deploy-a-custom-project-template-using-the-vsix-project-template"></a>Implantar um modelo de projeto personalizado usando o modelo de projeto do VSIX  
 As etapas a seguir mostram como usar o projeto do VSIX para empacotar um modelo de projeto que você pode compartilhar com outros desenvolvedores ou carregar a Galeria do Visual Studio.  

1.  Crie um modelo de projeto.  

    1.  Abra o projeto do qual criar um modelo. Este projeto pode ser de qualquer tipo de projeto.  

    2.  No menu **Projeto**, clique em **Exportar Modelo**. Conclua as etapas do assistente.  

         Um *. zip* arquivo é criado na *%USERPROFILE%\My Documents\Visual Studio \<versão > \My Exported Templates\\*.  

2.  Crie um projeto vazio do VSIX.  

     Sobre o **arquivo** menu, clique em **New** e, em seguida, clique em **projeto**. Selecione a **Visual Basic** ou **Visual c#**. Sob o nó selecionado, selecione **extensibilidade**e, em seguida, selecione **projeto VSIX**.  

3.  Adicione a *. zip* arquivo ao projeto. Defina suas **Copy to Output Directory** propriedade `Copy Always`.  

4.  No **Gerenciador de soluções**, clique duas vezes o *vsixmanifest* arquivo para abri-lo no **Designer de manifesto do VSIX**e, em seguida, faça as seguintes alterações:  

    -   Defina as **nome do produto** campo **meu modelo de projeto**.  

    -   Defina as **ID do produto** campo **MyProjectTemplate - 1**.  

    -   Defina as **autor** campo **Fabrikam**.  

    -   Defina as **descrição** campo **meu modelo de projeto**.  

    -   No **ativos** seção, adicione um **Microsoft.VisualStudio.ProjectTemplate** digite e defina seu caminho para o nome da *. zip* arquivo.  

5.  Salve e feche o *vsixmanifest* arquivo.  

6.  Compile o projeto.  

7.  No diretório de saída, clique duas vezes o *VSIX* arquivo.  

8.  Um **instalador do VSIX** caixa de mensagem é exibida. Siga as instruções para instalar a extensão.  

9. Feche o Visual Studio e, em seguida, abra-o novamente.  

10. Selecione **extensões e atualizações** (sobre o **ferramentas** menu) e selecione o **modelos** categoria. Uma das extensões disponíveis deve ser **meu modelo de projeto**.  

11. O novo modelo de projeto aparece na **novo projeto** caixa de diálogo no mesmo local que o modelo de projeto original. Por exemplo, se você tiver criado um modelo chamado **VB Console** de um aplicativo de console do Visual Basic **Console VB** aparece no painel do mesmo como o Visual Basic **o aplicativo de Console**modelo.  

### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>Para especificar o local do modelo na caixa de diálogo Novo projeto  

1. Pastas de modelos estão localizadas na *{caminho de instalação do Visual Studio} \Common7\IDE\ProjectTemplates* e <em>\Common7\IDE\ItemTemplates {caminho de instalação do Visual Studio}} diretórios. Os nomes dos principais seções de nível de **novo projeto</em>*  caixa de diálogo não correspondem exatamente os nomes das pastas de modelo. Em que eles forem diferentes, use o nome da pasta do modelo.  

    Alterar o *. VSIX* extensão de arquivo *. zip*e, em seguida, abra o arquivo.  

2. Crie uma nova pasta com o mesmo nome que a seção do **novo projeto** o modelo deve aparecer de caixa de diálogo.  

3. Se o modelo deve aparecer em uma subseção, crie uma subpasta de mesmo nome.  

4. Mover o modelo *. zip* arquivo para a nova pasta.  

5. Alterar o *. zip* extensão *VSIX*.  

6. Abra o manifesto do VSIX.  

7. No manifesto do VSIX, atualize o **ativo** caminho do modelo para que ele aponte para a raiz da árvore de diretório que contém o arquivo de modelo. Por exemplo, se o modelo está na *\CSharp\Windows*, a referência deve apontar para *\CSharp*.
