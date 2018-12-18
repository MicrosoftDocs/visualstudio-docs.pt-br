---
title: Modelos de suporte do Site da Web | Microsoft Docs
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
- we site projects, templates
ms.assetid: 37173c97-486b-4b3c-8ed3-cf5890c4de23
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: eebacb3006826a90320cbc61edf7d56467e688ce
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760226"
---
# <a name="web-site-support-templates"></a>Modelos de suporte a site
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Modelos de projeto e item do site da Web fornecem stubs de item e projeto de site reutilizáveis e personalizáveis que aceleram o processo de desenvolvimento, eliminando a necessidade de criar novos projetos de site da Web e itens do zero. Para obter mais informações sobre [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] modelos, consulte [criando modelos de projeto e Item](../../ide/creating-project-and-item-templates.md).  
  
## <a name="project-template-folder"></a>Pasta de modelos de projeto  
 Modelos de modelo de projeto Web normalmente são instalados em [*caminho de instalação do Visual Studio*] \Common7\IDE\ProjectTemplates\Web\\, cada um em uma subpasta nomeada com base na linguagem de programação de web.  
  
## <a name="project-file"></a>Arquivo de Projeto  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE) requer uma extensão de arquivo de projeto como uma maneira de mapear um modelo para o tipo de projeto correto. Como projetos da Web não têm um arquivo de projeto, a extensão de arquivo de projeto fictício. webproj está registrada para dar suporte a isso.  
  
 Opcionalmente, uma cadeia de caracteres de nome de idioma pode ser adicionada ao modelo para permitir que o sistema de projeto da Web definir o idioma padrão no **Adicionar Novo Item** caixa de diálogo para itens com base no modelo. A cadeia de caracteres deve ser a primeira linha do arquivo e deve coincidir com o nome registrado sob AddItemLanguageName no registro do mecanismo do Intellisense e o nome registrado sob Subtype(VsTemplate) do projeto. Para obter mais informações, consulte [tributos de suporte do Site da Web](../../extensibility/internals/web-site-support-attributes.md).  
  
 Se a cadeia de caracteres não estiver presente, o sistema de projeto Web tentará determinar o idioma padrão com base nas extensões de atributo e o arquivo de linguagem das páginas adicionadas ao projeto da Web pelo modelo de projeto de modelo.  
  
## <a name="project-templates"></a>Modelos de projeto  
 Modelos de projeto de site da Web são usados para criar novos sites da Web em resposta à **New Web Site** comando as **arquivo** menu. Atualmente, há suporte para três tipos de projeto de site da Web:  
  
-   Projetos de site da Web vazio  
  
-   Projetos de site  
  
-   Projetos de serviço da Web  
  
### <a name="empty-web-site-projects"></a>Projetos de Site da Web vazio  
 Esses arquivos de criam um novo site vazio em resposta à **Site da Web vazio** comando, que está disponível após a apontando para **New Web Site** no **arquivo** menu:  
  
-   EmptyWeb.vstemplate  
  
     O arquivo de modelo que orienta a criação do novo site da Web vazio.  
  
-   EmptyWeb.webproj  
  
     Esse arquivo é um artefato do sistema de modelo de projeto. Ele atende a referência de arquivo de projeto no arquivo EmptyWeb.vstemplate.  
  
### <a name="web-site-projects"></a>Projetos de Site  
 Esses arquivos de criam um novo site em resposta à **Site da Web ASP.NET** comando, que está disponível após a apontando para **New Web Site** no **arquivo** menu:  
  
-   Default.aspx  
  
     A home page padrão para o novo site da Web. O atributo Language Especifica a linguagem de code-behind e o atributo CodeFile Especifica o arquivo dependente que contém o código de code-behind associado a esta página.  
  
-   Default.aspx.*extension*  
  
     O arquivo dependente que contém o código de code-behind para a página inicial padrão. Determina o idioma de code-behind a *extensão* desse arquivo.  
  
-   web.config  
  
     O arquivo de configuração de web.site raiz.  
  
-   WebApplication.vstemplate  
  
     O arquivo de modelo que determina o conteúdo da solução de site da Web e força a criação da pasta App_Data.  
  
-   WebApplication.webproj  
  
     Esse arquivo é um artefato do sistema de modelo de projeto. Ele atende a referência de arquivo de projeto no arquivo WebApplication.vstemplate.  
  
### <a name="web-service-projects"></a>Projetos de serviço da Web  
 Esses arquivos de criam um novo site em resposta à **serviço Web ASP.NET** comando que está disponível após apontando para **New Web Site** no **arquivo** menu:  
  
-   Service.asmx  
  
     A página HTML para o novo serviço Web. O atributo Language Especifica a linguagem de code-behind e o atributo CodeBehind Especifica o arquivo dependente que contém o código de code-behind associado a esse serviço.  
  
-   Serviço. *extension*  
  
     O arquivo dependente que implementa a classe de serviço. Determina o idioma de code-behind a *extensão* desse arquivo.  
  
-   web.config  
  
-   O arquivo de configuração de web.site raiz.  
  
-   WebService.vstemplate  
  
     O arquivo de modelo que determina o conteúdo da solução de site da Web e força a criação das pastas App_Data e App_Code. O serviço. *extensão* arquivo é copiado para a pasta App_Code.  
  
-   WebService.webproj  
  
     Esse arquivo é um artefato do sistema de modelo de projeto. Ele atende a referência de arquivo de projeto no arquivo WebService.vstemplate.  
  
## <a name="project-item-template-folder"></a>Pasta de modelos de Item de projeto  
 Modelos de modelo de item de projeto da Web normalmente são instalados em [*caminho de instalação do Visual Studio*] \Common7\IDE\ItemTemplates\Web\\, cada um em uma subpasta que é nomeada após sua linguagem de programação da web.  
  
## <a name="project-item-templates"></a>Modelos de Item de projeto  
 Modelos de item de projeto de site da Web são usados para adicionar novas páginas da Web para um site da Web em resposta à **Add Existing Item** comando. Atualmente, há suporte para esses tipos de páginas da Web:  
  
-   Nova classe  
  
-   Nova página HTML  
  
-   Novo formulário da Web  
  
-   Nova página mestra  
  
### <a name="new-class"></a>Nova classe  
 Este modelo cria um novo arquivo de origem que define uma classe vazia na resposta para o **Add New Class** comando.  
  
-   Classe. *extension*  
  
     O arquivo de origem que implementa a classe vazia. Determina o idioma de code-behind a *extensão* desse arquivo.  
  
-   Class.vstemplate  
  
     O arquivo de modelo que cria o arquivo de origem e determina seu conteúdo.  
  
### <a name="new-html-page"></a>Nova página HTML  
 Este modelo cria uma nova página da Web em resposta à **adicionar nova página HTML** comando.  
  
-   HTMLPage.htm  
  
     O conteúdo inicial da página da Web. Esta página da Web geralmente não tem nenhum arquivo de code-behind associado dependente. Para criar uma página inteligente com um arquivo code-behind associado, use o modelo de formulário da Web.  
  
-   HTMLPage.vstemplate  
  
     O arquivo de modelo que cria a página da Web e determina seu conteúdo.  
  
### <a name="new-webform"></a>Novo formulário da Web  
 Este modelo cria uma nova página da Web inteligente na resposta para o **adicionar novo Web Form** comando.  
  
 Para criar um arquivo de origem code-behind dependentes, selecione **colocar código em arquivo separado**. Caso contrário, uma única página da Web é criada que tem um bloco de script vazio e nenhum \<% Page % > diretivas para ligar a um arquivo dependente.  
  
 Para criar uma página de conteúdo para uma página mestra selecionada, selecione **página mestra selecione**.  
  
-   WebForm.aspx  
  
     O conteúdo inicial da página da Web. Esta página da Web não tem nenhum arquivo de code-behind associado dependente.  
  
-   WebForm_cb.aspx  
  
     O conteúdo inicial da página da Web. Esta página da Web tem um arquivo dependente do code-behind associado.  
  
-   Code-behind. *extension*  
  
     O arquivo dependente que implementa a classe de formulário da Web. Determina o idioma de code-behind a *extensão* desse arquivo.  
  
-   ContentPage.aspx  
  
     O conteúdo inicial da página da Web como uma página de conteúdo. Esta página da Web não tem nenhum arquivo de code-behind associado dependente.  
  
-   ContentPage_cb.aspx  
  
     O conteúdo inicial da página da Web como uma página de conteúdo. Esta página da Web tem um arquivo dependente do code-behind associado.  
  
-   WebForm.vstemplate  
  
     O arquivo de modelo que determina o conteúdo da página da web novo e seu arquivo dependente, se houver.  
  
### <a name="new-master-page"></a>Nova página mestra  
 Este modelo cria uma nova página mestra em resposta à **adicionar nova página mestra** comando.  
  
 Para criar um arquivo de origem code-behind dependentes, selecione **colocar código em arquivo separado**. Caso contrário, uma única página da Web é criada que tem um bloco de script vazio e nenhum \<% Page % > diretivas para ligar a um arquivo dependente.  
  
-   MasterPage.master  
  
     O conteúdo inicial da página mestra. Essa página mestra não tem nenhum arquivo de code-behind associado dependente.  
  
-   MasterPage_cb.master  
  
     O conteúdo inicial da página mestra. Essa página mestra tem um arquivo dependente do code-behind associado.  
  
-   Code-behind. *extensão*  
  
     O arquivo dependente que implementa a classe de página mestra. Determina o idioma de code-behind a *extensão* desse arquivo.  
  
-   MasterPage.vstemplate  
  
     O arquivo de modelo que determina o conteúdo da nova página mestra e seu arquivo dependente, se houver.  
  
## <a name="see-also"></a>Consulte também  
 [Suporte ao site](../../extensibility/internals/web-site-support.md)

