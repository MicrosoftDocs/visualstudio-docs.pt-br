---
title: Criação de Item modelos e modelos de projeto para itens de projeto do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- .spdata files
- projects [SharePoint development in Visual Studio], creating custom templates
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, creating custom project and item templates
- project items [SharePoint development in Visual Studio], creating custom templates
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d181891fb36645e4f246aa0c2238c12ea1dc4903
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296002"
---
# <a name="create-item-templates-and-project-templates-for-sharepoint-project-items"></a>Criar modelos de projeto do SharePoint para itens de projeto e modelos de item
  Quando você define um tipo de item de projeto personalizado do SharePoint, você pode associá-lo com um modelo de item ou um modelo de projeto. Essa associação permite que outros desenvolvedores a usar o item de projeto no Visual Studio. Você também pode criar um Assistente para o modelo.

 Por exemplo, o Visual Studio não inclui um modelo de projeto ou o modelo de item para adicionar um campo a um site do SharePoint. Você pode definir um tipo de item de projeto do SharePoint que representa um campo e, em seguida, criar um modelo de item que outros desenvolvedores podem usar para adicionar o item de campo para um projeto do SharePoint. Ou, você pode construir um modelo de projeto para que os desenvolvedores podem criar um novo projeto do SharePoint que tem o item de campo. Em ambos os casos, você também pode fornecer um assistente que aparece quando os desenvolvedores usam seu modelo. Este assistente pode coletar informações de desenvolvedores para configurar o novo item ou projeto.

 Modelos de item e projeto são *. zip* arquivos que contêm arquivos que são usados pelo Visual Studio para criar um item de projeto ou o projeto. Para obter mais informações sobre os conceitos básicos de modelos de item e projeto, consulte [criar modelos de projeto e item](../ide/creating-project-and-item-templates.md).

## <a name="create-item-templates"></a>Criar modelos de item
 Quando você cria um modelo de item para um item de projeto do SharePoint, há alguns arquivos que sempre são necessários e arquivos opcionais que podem ser usados por determinados tipos de itens de projeto. Para um passo a passo que demonstra como definir um tipo de item de projeto do SharePoint e criar um modelo de item para ele, consulte [instruções passo a passo: criar o item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md).

 A tabela a seguir lista os arquivos necessários para criar um modelo de item para um item de projeto do SharePoint.

|Arquivo necessário|Descrição|
|-------------------|-----------------|
|Uma *. spdata* arquivo|Esse arquivo XML Especifica o conteúdo e o comportamento padrão do item de projeto. Esse arquivo deve ser incluído no modelo de item. Para obter mais informações sobre o conteúdo do *. spdata* arquivos, consulte [referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md).|
|Um *. vstemplate* arquivo.|Esse arquivo fornece o Visual Studio com as informações necessárias para exibir o modelo na **Adicionar Novo Item** caixa de diálogo e criar um item de projeto do modelo. Esse arquivo deve ser incluído no modelo de item. Para obter mais informações, consulte [arquivos de metadados de modelo do Visual Studio](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\)).|
|Um assembly de extensão do Visual Studio que implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface.|Esse assembly define o comportamento de tempo de execução do item de projeto. Esse assembly deve ser incluído no pacote VSIX com o modelo de item. Para obter mais informações, consulte [definir tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md) e [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).|

 A tabela a seguir lista alguns dos arquivos opcionais mais comuns que podem ser incluídos no modelo de item. Alguns tipos de itens de projeto podem exigir outros arquivos não listados aqui.


| Arquivo opcional | Descrição |
|----------------------| - |
| *Elements. XML* | Um *elemento Feature* arquivo. Esse arquivo define a interface do usuário e o comportamento da personalização que criou o item de projeto. Cada tipo de personalização, como instâncias de lista, tipos de conteúdo ou ações personalizadas, tem um esquema diferente que define o conteúdo desse arquivo. Para obter mais informações, consulte [bloco de construção: recursos](http://go.microsoft.com/fwlink/?LinkId=169183) e [esquemas de recurso](http://go.microsoft.com/fwlink/?LinkId=169192). |
| *Schema. XML* | O arquivo de esquema para definições de lista. Para obter mais informações, consulte [bloco de construção: listas e bibliotecas de documentos](http://go.microsoft.com/fwlink/?LinkId=177792) e [Schema. XML](http://go.microsoft.com/fwlink/?LinkId=177793). |
| *. WebPart* | Um *definição de Web Part* arquivo. Esse arquivo contém as configurações de propriedade para uma Web Part. Para obter mais informações, consulte [bloco de construção: Web Parts](http://go.microsoft.com/fwlink/?LinkId=177791). |
| *. ascx* | Um arquivo de controle de usuário ASP.NET. Esse arquivo define a interface do usuário de uma Web Part Visual. |
| *. aspx* | Um arquivo de página ASP.NET. Esse arquivo contém a marcação XML que define uma página de aplicativo. |
| *. CS* ou *VB* arquivos | Esses arquivos de código definem o comportamento das personalizações do SharePoint que têm um modelo de programação que pode ser acessado do Visual c# ou código do Visual Basic, como páginas de aplicativos, Web parts e fluxos de trabalho. |

## <a name="create-project-templates"></a>Criar modelos de projeto
 Quando você cria um modelo de projeto do SharePoint, há alguns arquivos que são sempre arquivos obrigatórios e opcionais que podem ser usados por determinados tipos de projetos. Normalmente, os projetos do SharePoint incluem pelo menos um item de projeto do SharePoint. No entanto, isso não é necessário. Por exemplo, você pode definir um modelo de projeto do SharePoint que se destina a ser usado apenas para implantar soluções do SharePoint criadas em outros projetos.

 Para um passo a passo que demonstra como definir um tipo de item de projeto do SharePoint e criar um modelo de projeto para ele, consulte [instruções passo a passo: criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md).

 A tabela a seguir lista os arquivos que devem ser incluídos em um modelo de projeto do SharePoint.

|Arquivo necessário|Descrição|
|-------------------|-----------------|
|Um *. vstemplate* arquivo|Esse arquivo fornece o Visual Studio com as informações necessárias para exibir o modelo na **novo projeto** caixa de diálogo e criar um projeto do modelo. Para obter mais informações, consulte [arquivos de metadados de modelo do Visual Studio](/previous-versions/visualstudio/visual-studio-2010/xsxc3ete\(v\=vs.100\)).|
|Um *. csproj* ou *. vbproj* arquivo|Esse é o arquivo de projeto. Ele define o conteúdo e definições de configuração do projeto.|
|*Pacote*|Esse arquivo define o pacote de implantação para o projeto. Quando você usa o Designer de pacote para personalizar o pacote de solução para seu projeto, o Visual Studio armazena dados sobre o pacote de solução nesse arquivo.<br /><br /> Quando você cria um modelo de projeto personalizado do SharePoint, é recomendável que você inclua somente o conteúdo mínimo necessário na *pacote* arquivo e que você configure o pacote de solução usando as APIs no <xref:Microsoft.VisualStudio.SharePoint.Packages> namespace em uma extensão que está associado com o modelo de projeto. Se você fizer isso, o modelo de projeto está protegido contra alterações futuras para a estrutura do *pacote* arquivo. Para obter um exemplo que demonstra como criar uma *pacote* conteúdo do arquivo com apenas o mínimo necessário, consulte [passo a passo: criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md).<br /><br /> Se você quiser modificar a *pacote* diretamente do arquivo, você poderá verificar o conteúdo usando o esquema em *% arquivos de programas (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\PackageModelSchema.xsd* .|
|*Package.Template.xml*|Esse arquivo fornece a base para o arquivo de manifesto da solução (*manifest. XML*) para o pacote de solução do SharePoint (*wsp*) que é gerado a partir do projeto. Você pode adicionar conteúdo a esse arquivo, se você quiser especificar um comportamento que não se destina a ser alterado pelos usuários do seu tipo de projeto. Para obter mais informações, consulte [bloco de construção: soluções](http://go.microsoft.com/fwlink/?LinkId=169186) e [solução esquema](http://go.microsoft.com/fwlink/?LinkId=177794).<br /><br /> Quando você compila um pacote de solução do projeto, o Visual Studio mescla o conteúdo do *pacote* e o *Package.Template.xml* arquivo de manifesto de arquivos na solução. Para obter mais informações sobre a criação de pacotes de soluções, consulte [como: criar um pacote de solução do SharePoint usando tarefas do MSBuild](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md).|

 A tabela a seguir lista os arquivos opcionais que podem ser incluídos no modelo de projeto.

|Arquivo opcional|Descrição|
|-------------------|-----------------|
|itens de projeto do SharePoint|Você pode incluir um ou mais arquivos. spdata que definem tipos de item de projeto do SharePoint. Cada *. spdata* arquivo deve ter uma correspondência <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> implementação em um assembly de extensão que está incluído no pacote VSIX com o modelo de projeto. Para obter mais informações, consulte [criando modelos de Item](#creatingitemtemplates).<br /><br /> Normalmente, os projetos do SharePoint incluem pelo menos um item de projeto do SharePoint. No entanto, isso não é necessário.|
|*\<featureName > Feature*|Esse arquivo define um recurso do SharePoint que é usado para agrupar vários itens de projeto para a implantação. Quando você usa o Designer de recursos para personalizar um recurso em seu projeto, o Visual Studio armazena dados sobre o recurso neste arquivo. Se você quiser agrupar os itens de projeto em diferentes recursos, você pode incluir vários *Feature* arquivos.<br /><br /> Quando você cria um modelo de projeto personalizado do SharePoint, é recomendável que você inclua o conteúdo mínimo necessário em cada *Feature* arquivo e que você configure os recursos usando as APIs no <xref:Microsoft.VisualStudio.SharePoint.Features> namespace em um extensão que está associado com o modelo de projeto. Se você fizer isso, o modelo de projeto está protegido contra alterações futuras para a estrutura do *Feature* arquivo. Para obter um exemplo que demonstra como criar uma *Feature* conteúdo do arquivo com apenas o mínimo necessário, consulte [passo a passo: criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md).<br /><br /> Se você quiser modificar uma *Feature* diretamente do arquivo, você poderá verificar o conteúdo usando o esquema em *% arquivos de programas (x86)%\Microsoft Visual Studio 11.0\Xml\Schemas\FeatureModelSchema.xsd*.|
|*\<featureName >. Template*|Esse arquivo fornece a base para o arquivo de manifesto de recurso (*Feature*) para cada recurso que é gerado a partir do projeto. Você pode adicionar conteúdo a esse arquivo, se você quiser especificar um comportamento que não se destina a ser alterado pelos usuários do seu tipo de projeto. Para obter mais informações, consulte [bloco de construção: recursos](http://go.microsoft.com/fwlink/?LinkId=169183) e [Feature](http://go.microsoft.com/fwlink/?LinkId=177795) arquivos.<br /><br /> Quando você compila um pacote de solução do projeto, o Visual Studio mescla o conteúdo de cada par de  *\<featureName > Feature* arquivo e  *\<featureName >. Template* arquivos em um recurso de arquivo de manifesto. Para obter mais informações sobre a criação de pacotes de soluções, consulte [como: criar um pacote de solução do SharePoint usando tarefas do MSBuild](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md).|

## <a name="create-wizards-for-item-templates-and-project-templates"></a>Criar assistentes para modelos de item e projeto
 Depois de definir um tipo de item de projeto do SharePoint e associá-la com um modelo de item ou projeto, você também pode criar um assistente. O assistente exibe quando um desenvolvedor usa o modelo de item para adicionar o item de projeto do SharePoint a um projeto, ou quando um desenvolvedor usa o modelo de projeto para criar um novo projeto que contém o item de projeto do SharePoint. O assistente pode ser usado para coletar informações de desenvolvedores e para inicializar o novo item de projeto do SharePoint.

 Para instruções passo a passo que demonstre como criar assistentes para modelos de item e projeto, consulte [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md) e [passo a passo: criar um site item de projeto de coluna com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md).

## <a name="see-also"></a>Consulte também

- [Definir tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [Passo a passo: Criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [Passo a passo: Criar um item de projeto da coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
