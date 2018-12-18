---
title: Criando modelos de Item e projeto personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: eeea0f92fc846b6ed51673d22450b22e01b348eb
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497856"
---
# <a name="create-custom-project-and-item-templates"></a>Criar modelos personalizados de projeto e de item

O SDK do Visual Studio inclui modelos de projeto que cria um modelo de projeto personalizado e um modelo de item personalizado. Esses modelos incluem algumas substituições de parâmetro comuns e de build como arquivos zip. Eles não são implantados automaticamente e eles não estão disponíveis na instância experimental. Você deve copiar o arquivo zip gerado no diretório de modelo de usuário.
  
Os modelos de criação de modelo permitem que você incluir modelos em extensões maiores. Isso permite implementar o controle de versão nos arquivos de origem e criar um grupo de projetos de modelo em um pacote VSIX.  
  
Você também pode configurar um modelo para instalar pacotes do NuGet. Para obter mais informações, consulte [pacotes do NuGet em modelos do Visual Studio](/nuget/visual-studio-extensibility/visual-studio-templates).

Para cenários de criação do modelo básico, você deve usar o **exportar modelo** assistente, o que é gerada para um arquivo compactado. Para obter mais informações sobre a criação do modelo básico, consulte [criando modelos de projeto e item](../ide/creating-project-and-item-templates.md).  

> [!NOTE]
> A partir do Visual Studio 2017, verificação de modelos de item e projeto personalizados será não é mais executada. Em vez disso, a extensão deve fornecer os arquivos de manifesto de modelo que descrevem o local de instalação desses modelos. Você pode usar o Visual Studio 2017 para atualizar as extensões VSIX. Se você implantar sua extensão usando um MSI, você deve gerar os arquivos de manifesto do modelo manualmente. Para obter mais informações, consulte [da atualização projeto e item modelos personalizados para o Visual Studio 2017](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md). O esquema de modelo de manifesto está documentado em [referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).

## <a name="create-a-project-template"></a>Criar um modelo de projeto  
  
1.  Crie um projeto de modelo de projeto. Você pode encontrar o modelo de projeto na **novo projeto** caixa de diálogo, no Visual Basic ou Visual c# *extensibilidade* pasta.  
  
     O modelo gera um arquivo de classe, um ícone, um *. vstemplate* do arquivo, um arquivo de projeto editável denominado *ProjectTemplate.vbproj* ou *ProjectTemplate.csproj*e alguns arquivos que normalmente são gerados por outros tipos de projeto, tal uma *Resources* arquivo, um *AssemblyInfo* arquivo e um *Settings* arquivo. Cada arquivo de código contém substituições de parâmetro comuns onde for apropriado.  
  
2.  Adicionar e remover itens do projeto conforme necessário para seu projeto. Não remova o arquivo de projeto editável, a *AssemblyInfo* arquivo, ou o *. vstemplate* arquivo.  
  
3.  Atualizar o *. vstemplate* arquivo para refletir quaisquer adições e exclusões. O [Project](../extensibility/project-element-visual-studio-templates.md) elemento deve conter um [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) elemento para cada arquivo a ser incluído no modelo.  
  
4.  Modificar os arquivos de código e outros tipos de conteúdo voltado para o usuário e adicione substituições de parâmetro apropriado.  
  
5.  Modifica o conteúdo gerado conforme necessário.  
  
6.  Compile o projeto.  
  
     O Visual Studio cria uma *. zip* arquivo que contém o modelo. Não está implantado, e ele não está disponível na instância experimental.  
  
## <a name="create-an-item-template"></a>Criar um modelo de item  
  
1.  Crie um projeto de modelo de Item.  
  
     O modelo gera um arquivo de classe, um ícone, um *. vstemplate* arquivo e um *AssemblyInfo* arquivo. O arquivo de classe contém algumas substituições de parâmetro comuns.  
  
2.  Adicionar e remover itens do projeto conforme necessário para seu projeto.  
  
3.  Atualizar o *. vstemplate* arquivo para refletir quaisquer adições e exclusões. O [Project](../extensibility/project-element-visual-studio-templates.md) elemento deve conter um [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) elemento para cada arquivo a ser incluído no modelo.  
  
4.  Modificar os arquivos de código e outros tipos de conteúdo voltado para o usuário e adicione substituições de parâmetro apropriado.  
  
5.  Modifica o conteúdo gerado conforme necessário.  
  
6.  Compile o projeto.  
  
     Visual Studio cria um arquivo compactado que contém o modelo. Não está implantado, e ele não está disponível na instância experimental.  
  
## <a name="deployment"></a>Implantação  
  
### <a name="to-deploy-the-project-or-item-template"></a>Para implantar o modelo de projeto ou item  
  
1.  Crie um projeto VSIX. Para obter mais informações, consulte [modelo de projeto do VSIX](../extensibility/vsix-project-template.md).  
  
2.  Defina o projeto VSIX como o projeto de inicialização. No **Gerenciador de soluções**, selecione o nó do projeto VSIX, clique com botão direito e selecione **definir como projeto de inicialização**.  
  
3.  Defina o projeto de modelo de projeto como um ativo do projeto VSIX. Abra o *.vsixmanifest* arquivo. Vá para o **ativos** guia e clique em **New**.  
  
    1.  Defina as **tipo** campo **Microsoft.VisualStudio.ProjectTemplate** ou **Microsoft.VisualStudio.ItemTemplate**.  
  
    2.  Para o código-fonte, selecione a **um projeto na solução atual** opção e, em seguida, selecione o projeto que contém o modelo.  
  
4.  Compilar a solução e pressione **F5**. A instância experimental é exibida.  
  
5.  Para um projeto de modelo de projeto, você deve ver o modelo de projeto listado na **novo projeto** caixa de diálogo (**arquivo** > **novo**  >  **Projeto**), no Visual c# ou no nó Visual Basic. Para um projeto de modelo de item, você deve ver o modelo de item listado na **Adicionar Novo Item** caixa de diálogo. Para exibir o **Adicionar Novo Item** caixa de diálogo, da **Gerenciador de soluções**, selecione o nó do projeto e clique em **Add** > **Novo Item**).  
  
## <a name="see-also"></a>Consulte também

[Referência de modelo do Visual Studio](../ide/visual-studio-template-reference.md)  
[Pacotes do NuGet em modelos do Visual Studio](/nuget/visual-studio-extensibility/visual-studio-templates)