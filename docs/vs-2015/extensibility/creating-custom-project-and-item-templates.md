---
title: Criando modelos de Item e projeto personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3229eb90dad59269d81bfd34b7eb5fa15bdab6d7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794602"
---
# <a name="creating-custom-project-and-item-templates"></a>Criando modelos de item e de projeto personalizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O SDK do Visual Studio inclui modelos de projeto que cria um modelo de projeto personalizado e um modelo de item personalizado. Esses modelos incluem algumas substituições de parâmetro comuns e de build como arquivos zip. Eles não são implantados automaticamente e eles não estão disponíveis na instância experimental. Você deve copiar o zip arquivos para o local  
  
 Os modelos de criação de modelo permitem que você incluir modelos em extensões maiores. Isso permite implementar o controle de versão nos arquivos de origem e criar um grupo de projetos de modelo em um pacote VSIX.  
  
 Para cenários de criação do modelo básico, você deve usar o **exportar modelo** assistente, o que é gerada para um arquivo compactado. Para obter mais informações sobre a criação do modelo básico, consulte [criando modelos de projeto e Item](../ide/creating-project-and-item-templates.md).  
  
 A partir do Visual Studio "15" visualização 4, verificação de modelos de item e projeto personalizados não serão executadas. Em vez disso, a extensão deve fornecer os arquivos de manifesto de modelo que descrevem o local de instalação desses modelos. Você pode usar a instalação de visualização 2 para atualizar as extensões VSIX. Se você implantar sua extensão usando um MSI, você deve gerar os arquivos de manifesto do modelo manualmente. Para obter mais informações, consulte [atualizando personalizados de projeto e modelos de Item para Visual Studio "15"](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md). O esquema de modelo de manifesto está documentado em [modelo de manifesto do esquema de referência do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).  
  
## <a name="creating-a-project-template"></a>Criando um modelo de projeto  
  
1.  Crie um projeto de modelo de projeto. Você pode encontrar o modelo de projeto na **novo projeto** caixa de diálogo, no Visual Basic ou Visual c# **extensibilidade** pasta.  
  
     O modelo gera um arquivo de classe, um ícone, um arquivo. vstemplate, um arquivo de projeto editável chamado ProjectTemplate.vbproj ou ProjectTemplate.csproj e alguns arquivos que normalmente são gerados por outros tipos de projeto, esse arquivo resx, um AssemblyInfo arquivo e um arquivo. Settings. Cada arquivo de código contém substituições de parâmetro comuns onde for apropriado.  
  
2.  Adicionar e remover itens do projeto conforme necessário para seu projeto. Não remova o arquivo de projeto editável, o arquivo AssemblyInfo ou o arquivo. vstemplate.  
  
3.  Atualize o arquivo. vstemplate para refletir quaisquer adições e exclusões. O [Project](../extensibility/project-element-visual-studio-templates.md) elemento deve conter um [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) elemento para cada arquivo a ser incluído no modelo.  
  
4.  Modificar os arquivos de código e outros tipos de conteúdo voltado para o usuário e adicione substituições de parâmetro apropriado.  
  
5.  Modifica o conteúdo gerado conforme necessário.  
  
6.  Compile o projeto.  
  
     Visual Studio cria um arquivo. zip que contém o modelo. Não está implantado, e ele não está disponível na instância experimental.  
  
## <a name="creating-an-item-template"></a>Criando um modelo de Item  
  
1.  Crie um projeto de modelo de Item.  
  
     O modelo gera um arquivo de classe, um ícone, um arquivo. vstemplate e um arquivo AssemblyInfo. O arquivo de classe contém algumas substituições de parâmetro comuns.  
  
2.  Adicionar e remover itens do projeto conforme necessário para seu projeto.  
  
3.  Atualize o arquivo. vstemplate para refletir quaisquer adições e exclusões. O [Project](../extensibility/project-element-visual-studio-templates.md) elemento deve conter um [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) elemento para cada arquivo a ser incluído no modelo.  
  
4.  Modificar os arquivos de código e outros tipos de conteúdo voltado para o usuário e adicione substituições de parâmetro apropriado.  
  
5.  Modifica o conteúdo gerado conforme necessário.  
  
6.  Compile o projeto.  
  
     Visual Studio cria um arquivo compactado que contém o modelo. Não está implantado, e ele não está disponível na instância experimental.  
  
## <a name="deployment"></a>Implantação  
  
#### <a name="to-deploy-the-project-or-item-template"></a>Para implantar o modelo de projeto ou item  
  
1.  Crie um projeto VSIX. Para obter mais informações, consulte [modelo de projeto do VSIX](../extensibility/vsix-project-template.md).  
  
2.  Defina o projeto VSIX como o projeto de inicialização. No **Gerenciador de soluções**, selecione o nó do projeto VSIX, clique com botão direito e selecione **definir como projeto de inicialização**.  
  
3.  Defina o projeto de modelo de projeto como um ativo do projeto VSIX. Abra o arquivo .vsixmanifest. Vá para o **ativos** guia e clique em **New**.  
  
    1.  Defina as **tipo** campo **Microsoft.VisualStudio.ProjectTemplate** ou **Microsoft.VisualStudio.ItemTemplate**.  
  
    2.  Para o código-fonte, selecione a **um projeto na solução atual** opção e, em seguida, selecione o projeto que contém o modelo.  
  
4.  Compile a solução e, em seguida, pressione F5. A instância experimental é exibida.  
  
5.  Para um projeto de modelo de projeto, você deve ver o modelo de projeto listado na **novo projeto** caixa de diálogo (**arquivo / novo / projeto**), no Visual c# ou no nó Visual Basic. Para um projeto de modelo de item, você deve ver o modelo de item listado na caixa de diálogo Add New Item (na **Gerenciador de soluções**, selecione o nó do projeto e clique em **Add / Novo Item**).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de modelo do Visual Studio](../ide/visual-studio-template-reference.md)

