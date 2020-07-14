---
title: Criando modelos personalizados de projeto e item | Microsoft Docs
ms.date: 3/16/2019
ms.topic: overview
ms.assetid: 586da5dc-f678-402b-afd0-0332959fd7a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c702aaaa51d86e2b8aac18a6b55201be03a635f
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903326"
---
# <a name="create-custom-project-and-item-templates"></a>Criar modelos de item e projeto personalizados

O SDK do Visual Studio inclui modelos de projeto que criam um modelo de projeto personalizado e um modelo de item personalizado. Esses modelos incluem algumas substituições de parâmetro comuns e compilam como arquivos zip. Eles não são implantados automaticamente e não estão disponíveis na instância experimental. Você deve copiar o arquivo zip gerado para o diretório de modelos do usuário.

Os modelos de criação de modelo permitem que você inclua modelos em extensões maiores. Isso permite que você implemente o controle de versão nos arquivos de origem e crie um grupo de projetos de modelo em um pacote VSIX.

Você também pode configurar um modelo para instalar pacotes NuGet. Para obter mais informações, consulte [pacotes NuGet em modelos do Visual Studio](/nuget/visual-studio-extensibility/visual-studio-templates).

Para cenários de criação de modelo básico, você deve usar o assistente para **Exportar modelo** , que gera um arquivo compactado. Para obter mais informações sobre a criação de modelo básico, consulte [criando modelos de projeto e item](../ide/creating-project-and-item-templates.md).

> [!NOTE]
> A partir do Visual Studio 2017, a verificação de modelos de projeto e item personalizados não será mais executada. Em vez disso, a extensão deve fornecer arquivos de manifesto de modelo que descrevem o local de instalação desses modelos. Você pode usar o Visual Studio 2017 para atualizar suas extensões VSIX. Se você implantar sua extensão usando um MSI, deverá gerar os arquivos de manifesto de modelo manualmente. Para obter mais informações, consulte [upgrading Custom Project and item templates for Visual Studio 2017](../extensibility/upgrading-custom-project-and-item-templates-for-visual-studio-2017.md). O esquema de manifesto de modelo está documentado na [referência de esquema de manifesto de modelo do Visual Studio](../extensibility/visual-studio-template-manifest-schema-reference.md).

## <a name="create-a-project-template"></a>Criar um modelo de projeto

1. Crie um projeto de modelo de projeto. Você pode encontrar o modelo de projeto na caixa de diálogo **novo projeto** , pesquisando "modelo de projeto" e selecionando a versão em C# ou Visual Basic.

     O modelo gera um arquivo de classe, um ícone, um arquivo *. vstemplate* , um arquivo de projeto editável chamado *ProjectTemplate. vbproj* ou *ProjectTemplate. csproj*e alguns arquivos que normalmente são gerados por outros tipos de projeto, como um arquivo *. resx de recursos* , um arquivo *AssemblyInfo* e um arquivo *. Settings* . Cada arquivo de código contém substituições de parâmetro comuns, quando apropriado.

![seleção de projeto de modelo de projeto](media/project-template-selection.png)

2. Adicione e remova itens do projeto conforme necessário para seu projeto. Não remova o arquivo de projeto editável, o arquivo *AssemblyInfo* ou o arquivo *. vstemplate* .

3. Atualize o arquivo *. vstemplate* para refletir quaisquer inclusões e exclusões. O elemento [Project](../extensibility/project-element-visual-studio-templates.md) deve conter um elemento [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) para cada arquivo a ser incluído no modelo.

4. Modifique seus arquivos de código e outros conteúdos voltados para o usuário e adicione substituições de parâmetro apropriadas.

5. Modifique o conteúdo gerado conforme necessário.

6. Compile o projeto.

     O Visual Studio cria um arquivo *. zip* que contém o modelo. Ele não é implantado e não está disponível na instância experimental.

## <a name="create-an-item-template"></a>Criar um modelo de item

1. Crie um projeto de modelo de item.

     O modelo gera um arquivo de classe, um ícone, um arquivo *. vstemplate* e um arquivo *AssemblyInfo* . O arquivo de classe contém algumas substituições de parâmetro comuns.

2. Adicione e remova itens do projeto conforme necessário para seu projeto.

3. Atualize o arquivo *. vstemplate* para refletir quaisquer inclusões e exclusões. O elemento [Project](../extensibility/project-element-visual-studio-templates.md) deve conter um elemento [ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md) para cada arquivo a ser incluído no modelo.

4. Modifique seus arquivos de código e outros conteúdos voltados para o usuário e adicione substituições de parâmetro apropriadas.

5. Modifique o conteúdo gerado conforme necessário.

6. Compile o projeto.

     O Visual Studio cria um arquivo compactado que contém o modelo. Ele não é implantado e não está disponível na instância experimental.

## <a name="deployment"></a>Implantação

### <a name="to-deploy-the-project-or-item-template"></a>Para implantar o modelo de projeto ou item

1. Crie um projeto VSIX. Para obter mais informações, consulte [modelo de projeto VSIX](../extensibility/vsix-project-template.md).

2. Defina o projeto VSIX como o projeto de inicialização. Na **Gerenciador de soluções**, selecione o nó do projeto VSIX, clique com o botão direito do mouse e selecione **definir como projeto de inicialização**.

3. Defina o projeto de modelo de projeto como um ativo do projeto VSIX. Abra o arquivo *. vsixmanifest* . Vá para a guia **ativos** e clique em **novo**.

    1. Defina o campo de **tipo** para **Microsoft. VisualStudio. ProjectTemplate** ou **Microsoft. VisualStudio. ItemTemplate**.

    2. Para origem, selecione a opção **um projeto na solução atual** e, em seguida, selecione o projeto que contém o modelo.

4. Compile a solução e pressione **F5**. A instância experimental é exibida.

5. Para um projeto de modelo de projeto, você deve ver o modelo de projeto listado na caixa de diálogo **novo projeto** (**arquivo**  >  **novo**  >  **projeto**), no nó Visual C# ou Visual Basic. Para um projeto de modelo de item, você deve ver o modelo de item listado na caixa de diálogo **Adicionar novo item** . Para exibir a caixa de diálogo **Adicionar novo item** , na **Gerenciador de soluções**, selecione o nó do projeto e clique em **Adicionar**  >  **novo item**).

## <a name="see-also"></a>Confira também

- [Referência de modelo do Visual Studio](../ide/creating-project-and-item-templates.md)
- [Pacotes NuGet em modelos do Visual Studio](/nuget/visual-studio-extensibility/visual-studio-templates)
