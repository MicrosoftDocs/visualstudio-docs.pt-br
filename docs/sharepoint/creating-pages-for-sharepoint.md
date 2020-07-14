---
title: Criando páginas para o SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, master pages
- SharePoint development in Visual Studio, page layouts
- SharePoint development in Visual Studio, content pages
- master pages[SharePoint development in Visual Studio], designing
- content pages[SharePoint development in Visual Studio], designing
- page layouts[SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 942891bc9281c07966160ea9df065408fcbfd5ff
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015169"
---
# <a name="create-pages-for-sharepoint"></a>Criar páginas para o SharePoint
  Você pode criar páginas de aplicativo, páginas de site, páginas mestras e layouts de página para um site do SharePoint.

 Você pode criar páginas de aplicativo usando um modelo no Visual Studio. Crie páginas de site, páginas mestras e layouts de página usando o SharePoint Designer. Em seguida, você pode importar essas páginas para o Visual Studio para usá-las em um projeto do SharePoint.

 Você também pode modificar a aparência e o comportamento das páginas usando folhas de estilo em cascata, ECMAScript e temas.

## <a name="types-of-sharepoint-pages"></a>Tipos de páginas do SharePoint
 A tabela a seguir descreve os quatro tipos principais de páginas que um site do SharePoint contém.

|Tipo de página|Descrição|
|---------------|-----------------|
|Páginas do aplicativo|Crie uma página de aplicativo se desejar que a página contenha código personalizado ou que você queira que a página seja compartilhada entre vários sites. Caso contrário, uma página do site pode ser a melhor opção.|
|Páginas do site|Crie uma página do site se desejar executar qualquer uma das seguintes tarefas:<br /><br /> -Adicione a página a uma biblioteca do SharePoint.<br />– Habilite a página para hospedar recursos como Web Parts dinâmicos e zonas de Web Part.<br />– Permitir que os usuários personalizem a página usando o SharePoint Designer.<br /><br /> Não crie uma página do site se desejar que a página contenha código personalizado. Embora você possa adicionar código personalizado a uma página do site, o código parará de ser executado quando o usuário personalizar a página usando o SharePoint Designer.|
|Páginas mestras|Crie uma página mestra se desejar definir uma estrutura comum para páginas do site e páginas do aplicativo.|
|Layouts de página|Os layouts de página são específicos para [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] o e permitem que você defina ainda mais uma estrutura comum para páginas do site e páginas do aplicativo.|

 Para obter uma visão geral de cada tipo de página, consulte [bloco de construção: páginas e a interface do usuário](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14)), [layouts de página e páginas mestras](/previous-versions/office/developer/sharepoint-2010/ms543497(v=office.14)).

## <a name="create-application-pages"></a>Criar páginas de aplicativo
 Você pode criar páginas de aplicativo no Visual Studio adicionando um item de **página de aplicativo** a um projeto do SharePoint. Você pode adicionar controles à página e manipular eventos de controle adicionando código.

 Você pode definir pontos de interrupção no arquivo de código da página, iniciar o depurador e testar a página em um site local do SharePoint sem executar nenhuma etapa de configuração adicional. Para obter mais informações, consulte [criando páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

## <a name="create-site-pages-master-pages-and-page-layouts"></a>Criar páginas do site, páginas mestras e layouts de página
 Você pode criar páginas de site, páginas mestras e layouts de página usando o SharePoint Designer. Em seguida, você pode importar essas páginas para o Visual Studio. Importe suas páginas se desejar aproveitar os recursos de implantação ou controle do código-fonte que estão disponíveis no Visual Studio. Para obter mais informações, consulte [Importando itens de um site existente do SharePoint](../sharepoint/importing-items-from-an-existing-sharepoint-site.md).

 Como é difícil modificar essas páginas depois de importá-las, você deve criar essas páginas antes de importá-las.

## <a name="create-cascading-style-sheets-ecmascript-and-themes"></a>Criar folhas de estilo em cascata, ECMAScript e temas
 O Visual Studio não fornece modelos para desenvolvimento de folhas de estilos em cascata (CSS), ECMAScript (JavaScript, JScript) ou arquivos de tema para sites do SharePoint. Você pode criar esses arquivos usando as diretrizes disponíveis no SDK do SharePoint ou usando ferramentas como o SharePoint Designer.

 Você pode adicionar esses arquivos à sua solução diretamente ou pode importá-los. Em ambos os casos, você deve criar as pastas mapeadas apropriadas para cada item que adicionar. Para obter mais informações sobre como criar uma pasta mapeada, consulte [como adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).

 Para obter mais informações sobre como criar folhas de estilos em cascata, consulte [folhas de estilos em cascata uso de classe no SharePoint Foundation](/previous-versions/office/developer/sharepoint-2010/ms438349(v=office.14)). Para obter mais informações sobre como criar arquivos JavaScript e JScript para uma solução do SharePoint, consulte [Configurando uma página aspx básica para ECMAScript](/previous-versions/office/developer/sharepoint-2010/ee535709(v=office.14)). Para obter mais informações sobre temas, consulte [bloco de construção: páginas e a interface do usuário](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14)).

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md)|Descreve como adicionar páginas de aplicativos: conteúdo *. aspx* que é mesclado com uma página mestra do SharePoint.|
|[Como: criar uma página de aplicativo](../sharepoint/how-to-create-an-application-page.md)|Mostra como criar páginas do ASP.NET que são executadas em um site do SharePoint.|
|[Walkthrough: criar uma página de aplicativo do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-application-page.md)|Mostra como projetar e depurar uma página da Web do ASP.NET para um site do SharePoint.|
