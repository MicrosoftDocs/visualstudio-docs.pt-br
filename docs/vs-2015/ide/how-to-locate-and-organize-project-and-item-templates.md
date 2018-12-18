---
title: Como localizar e organizar modelos de projeto e de item | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- project templates [Visual Studio], locations
- custom template locations [Visual Studio]
- item templates, locations
- Visual Studio templates, locations
- project templates [Visual Studio], displaying
- templates [Visual Studio], locations
ms.assetid: 71f9ed52-c9c9-4818-9bce-c279ffaa0438
caps.latest.revision: 28
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 2a3954e5d18db6585c8dbda017773969f96b33de
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830971"
---
# <a name="how-to-locate-and-organize-project-and-item-templates"></a>Como localizar e organizar projeto e modelos de item
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Arquivos de modelo devem ser colocados em um local reconhecido pelo Visual Studio, de modo que os modelos apareçam nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item**. É possível criar subcategorias personalizadas para os modelos, para que as subcategorias também apareçam na interface do usuário.  
  
## <a name="locating-templates"></a>Localizando modelos  
 Por padrão, o Visual Studio pesquisa dois locais em busca de modelos de item e projeto. Se houver um arquivo compactado que inclui um arquivo .vstemplate nesses locais, um modelo será exibido nas caixas de diálogo **Novo Projeto** ou **Adicionar Novo Item**.  
  
### <a name="installed-templates"></a>Modelos instalados  
 Por padrão, modelos instalados com o produto ficam localizados em:  
  
- \\*VisualStudioInstallationDirectory*\Common7\IDE\ItemTemplates\\*Idioma*\\*Localidade*\  
  
- \\*VisualStudioInstallationDirectory*\Common7\IDE\ProjectTemplates\\*Idioma*\\*Localidade\\*  
  
  Por exemplo, o diretório a seguir contém o modelos de projeto [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para o inglês:  
  
  C:\\*VisualStudioInstallationDirectory*\Common7\IDE\ItemTemplates\VisualBasic\1033\  
  
### <a name="custom-templates"></a>Modelos personalizados  
 Por padrão, modelos personalizados ficam localizados em:  
  
- \Meus Documentos\Visual Studio *Versão*\Templates\ProjectTemplates\\*Idioma*\  
  
- \Meus Documentos\Visual Studio *Versão*\Templates\ItemTemplates\\*Idioma*\  
  
  Por exemplo, o diretório a seguir contém modelos de projeto [!INCLUDE[csprcs](../includes/csprcs-md.md)] personalizados:  
  
  C:\Documents and Settings\UserName\Meus Documentos\\<versão do Visual Studio\>\Templates\ProjectTemplates\Visual C#\  
  
  Modelos personalizados não incluem um subdiretório para modelos localizados. É possível alterar o diretório padrão para modelos personalizados na caixa de diálogo **Opções**, em **Ambiente\Projetos e Soluções**.  
  
## <a name="organizing-templates"></a>Organizando modelos  
 As categorias nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item** refletem as estruturas de diretório que existem nos locais dos modelos instalados e personalizados. É possível modificar essas estruturas de diretório para organizar seus modelos de forma que faça sentido para você.  
  
> [!NOTE]
>  Você não pode criar uma nova categoria no nível da linguagem de programação. Novas categorias podem ser criadas apenas dentro de cada linguagem.  
  
 Se as estruturas de diretório dos modelos instalados e personalizados de uma determinada linguagem não tiverem a mesma estrutura (ou seja, se houver diretórios dentro de uma pasta que não existem em outra), o conjunto de categorias que aparecem na caixa de diálogo **Novo Projeto** será a fusão de todas as categorias.  
  
### <a name="organizing-installed-templates"></a>Organizando modelos instalados  
 É possível organizar modelos instalados criando subdiretórios na pasta da linguagem de programação. Esses subdiretórios aparecem nas caixas de diálogo **Novo Projeto** e **Adicionar Novo Item** como pastas virtuais dentro de cada linguagem.  
  
##### <a name="to-create-new-installed-project-template-categories"></a>Para criar novas categorias de modelo de projeto instalado  
  
1. Crie uma pasta na pasta da linguagem do diretório do modelo instalado. Por exemplo, para criar uma categoria Office para modelos de projeto de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], você criaria o diretório a seguir:  
  
    \\*VisualStudioInstallationDirectory*\Common7\IDE\ProjectTemplates\VisualBasic\1033\Office\  
  
2. Coloque todos os modelos dessa categoria na nova pasta.  
  
3. Feche todas as instâncias de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
4. No menu **Iniciar**, clique em **Executar**, digite **cmd** e clique em **OK**.  
  
5. No prompt de comando, localize o diretório que contém devenv.exe e digite **devenv /installvstemplates**.  
  
6. Execute [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
7. No menu **Arquivo**, clique em **Novo** e clique em **Projeto**.  
  
8. Verifique se a categoria Office aparece na caixa de diálogo **Novo Projeto**, no painel **Tipos de projeto**, em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)].  
  
   Você também pode agrupar um subconjunto de modelos de item do projeto em uma pasta personalizada.  
  
##### <a name="to-create-new-installed-item-template-categories"></a>Para criar novas categorias do modelo de item instalado  
  
1.  Crie uma pasta na pasta da linguagem do diretório do modelo instalado. Por exemplo, para criar uma categoria Web para modelos de item de [!INCLUDE[csprcs](../includes/csprcs-md.md)], você criaria o diretório a seguir:  
  
     \\*VisualStudioInstallationDirectory*\Common7\IDE\ItemTemplates\CSharp\1033\Web\  
  
2.  Coloque todos os modelos dessa categoria na nova pasta.  
  
3.  Feche todas as instâncias de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
4.  No menu **Iniciar**, clique em **Executar**, digite **cmd** e clique em **OK**.  
  
5.  No prompt de comando, localize o diretório que contém devenv.exe e digite **devenv /setup**.  
  
6.  Execute [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
7.  Crie um projeto ou abra um projeto existente.  
  
8.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
9. Verifique se a categoria Web aparece na caixa de diálogo **Adicionar Novo Item**, no painel **Tipos de projeto**.  
  
### <a name="organizing-custom-templates"></a>Organizando modelos personalizados  
 Modelos personalizados podem ser organizados em suas próprias categorias adicionando novas pastas ao local do modelo personalizado. A caixa de diálogo **Novo Projeto** reflete alterações feitas nas categorias de modelo.  
  
##### <a name="to-create-new-custom-project-template-categories"></a>Para criar novas categorias de modelo de projeto personalizado  
  
1. Crie uma pasta na pasta da linguagem no diretório do modelo de projeto personalizado. Por exemplo, para criar uma categoria HelloWorld para modelos de [!INCLUDE[csprcs](../includes/csprcs-md.md)], você criaria o diretório a seguir:  
  
    \Meus Documentos\\<versão do Visual Studio\>\Templates\ProjectTemplates\CSharp\HelloWorld\  
  
2. Coloque todos os modelos dessa categoria na nova pasta.  
  
3. No menu **Arquivo**, clique em **Novo** e clique em **Projeto**.  
  
4. Verifique se a categoria HelloWorld aparece na caixa de diálogo **Novo Projeto**, no painel **Tipos de projeto**, em [!INCLUDE[csprcs](../includes/csprcs-md.md)].  
  
   Você também pode agrupar um subconjunto de modelos de item personalizado em uma pasta personalizada.  
  
##### <a name="to-create-new-custom-item-template-categories"></a>Para criar novas categorias de modelo de item personalizado  
  
1.  Crie uma pasta na pasta da linguagem no diretório do modelo de item personalizado. Por exemplo, para criar uma categoria HelloWorld para modelos de [!INCLUDE[csprcs](../includes/csprcs-md.md)], você criaria o diretório a seguir:  
  
     \Meus Documentos\\<versão do Visual Studio\>\Templates\ItemTemplates\CSharp\HelloWorld\  
  
2.  Coloque todos os modelos dessa categoria na nova pasta.  
  
3.  Crie um projeto ou abra um projeto existente.  
  
4.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
5.  Verifique se a categoria HelloWorld aparece na caixa de diálogo **Adicionar Novo Item**, no painel **Tipos de projeto**.  
  
### <a name="displaying-templates-in-parent-categories"></a>Exibindo modelos em categorias pai  
 Você pode habilitar modelos em subcategorias a serem exibidos em suas categorias pai usando o elemento `NumberOfParentCategoriesToRollUp` no arquivo .vstemplate. Estas etapas são idênticas para modelos de projeto e modelos de item.  
  
##### <a name="to-display-templates-in-parent-categories"></a>Para exibir modelos em categorias pai  
  
1.  Localize o arquivo .zip que contém o modelo.  
  
2.  Extraia o arquivo .zip.  
  
3.  Abra o arquivo .vstemplate em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
4.  No elemento `TemplateData`, adicione um elemento `NumberOfParentCategoriesToRollUp`. Por exemplo, o código a seguir torna o modelo visível na categoria pai, mas não superior.  
  
    ```  
    <TemplateData>  
        ...  
        <NumberOfParentCategoriesToRollUp>  
            1  
        </NumberOfParentCategoriesToRollUp>  
        ...  
    </TemplateData>  
    ```  
  
5.  Salve e feche o arquivo .vstemplate.  
  
6.  Selecione os arquivos em seu modelo, clique com o botão direito do mouse na seleção, clique em **Enviar Para** e, em seguida, em **Pasta Compactada (zipada)**. Os arquivos são compactados em um arquivo .zip.  
  
7.  Exclua os arquivos de modelo extraídos e o arquivo .zip de modelo antigo.  
  
8.  Coloque o novo arquivo .zip no diretório que tinha o arquivo .zip excluído.  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando modelos](../ide/customizing-project-and-item-templates.md)   
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [NumberOfParentCategoriesToRollUp (modelos do Visual Studio)](../extensibility/numberofparentcategoriestorollup-visual-studio-templates.md)   
 [Como criar modelos de projeto](../ide/how-to-create-project-templates.md)   
 [Como criar modelos de item](../ide/how-to-create-item-templates.md)



