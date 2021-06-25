---
title: Modelos de suporte de site | Microsoft Docs
description: Saiba mais sobre modelos de suporte de site. Visual Studio modelo de item e projeto de site da Web fornecem stubs de item e projeto de site da Web reutilizáveis e personalizáveis.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- we site projects, templates
ms.assetid: 37173c97-486b-4b3c-8ed3-cf5890c4de23
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a1bd391d13a6d650cb4d23ce78789a66ef50c2e3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898882"
---
# <a name="web-site-support-templates"></a>Modelos de suporte a site
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Modelos de item e projeto de site da Web fornecem stubs de item e projeto de site reutilizáveis e personalizáveis que aceleram o processo de desenvolvimento removendo a necessidade de criar novos projetos e itens de site do zero. Para obter mais informações [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] sobre modelos, consulte [Criando modelos de projeto e item](../../ide/creating-project-and-item-templates.md).

## <a name="project-template-folder"></a>Pasta do modelo de projeto
 Os modelos de projeto Web normalmente são instalados em [ caminho de instalação do Visual Studio ]\Common7\IDE\ProjectTemplates\Web , cada um em uma subpasta que é nomeada após *a* linguagem de programação da \\ Web.

## <a name="project-file"></a>Arquivo de Projeto
 O IDE (ambiente de desenvolvimento integrado) requer uma extensão de arquivo de projeto como uma maneira de mapear [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] um modelo para o tipo de projeto correto. Como os projetos Web não têm um arquivo de projeto, a extensão de arquivo de projeto fictício .webproj é registrada para mapear o modelo para o tipo de projeto.

 Opcionalmente, uma cadeia de caracteres de nome de idioma pode ser adicionada ao modelo para habilitar o sistema de projeto Web a definir o padrão de idioma na caixa de diálogo Adicionar Novo **Item** para itens com base no modelo. A cadeia de caracteres deve ser a primeira linha do arquivo. Ele deve corresponder ao nome registrado em AddItemLanguageName no registro do mecanismo do IntelliSense e ao nome registrado em Subtipo de Projeto(VsTemplate). Para obter mais informações, consulte [Atributos de suporte do site](../../extensibility/internals/web-site-support-attributes.md).

 Se a cadeia de caracteres não estiver presente, o sistema de projeto Web tentará determinar o idioma padrão com base no atributo Language e nas extensões de arquivo das páginas adicionadas ao projeto Web pelo Modelo de Projeto.

## <a name="project-templates"></a>Modelos de projeto
 Os modelos de projeto do site são usados para criar novos sites em resposta ao comando **Novo Site** no menu **Arquivo.** No momento, há suporte para três tipos de projeto de site:

- Projetos de site vazios

- Projetos de site da Web

- Projetos de serviço Web

### <a name="empty-web-site-projects"></a>Projetos de site vazios
 Esses arquivos criam um novo site vazio em resposta ao comando **Site** Vazio, que está disponível depois de escolher Arquivo   >  **Novo Site**:

- EmptyWeb.vstemplate

     O arquivo de modelo que orienta a criação do novo site vazio.

- EmptyWeb.webproj

     Esse arquivo é um artefato do sistema de modelo de projeto. Ele satisfaz a referência de arquivo de projeto no arquivo EmptyWeb.vstemplate.

### <a name="web-site-projects"></a>Projetos de site da Web
 Esses arquivos criam um novo site em resposta ao comando **ASP.NET Site** da Web, que está disponível depois de escolher Arquivo  >  **Novo Site**:

- Default.aspx

     O padrão home page para o novo site. O atributo Language especifica a linguagem codebehind e o atributo CodeFile especifica o arquivo dependente que contém o código codebehind associado a esta página.

- Default.aspx. *extensão*

     O arquivo dependente que contém o código codebehind para o arquivo padrão home page. A linguagem codebehind determina a *extensão* desse arquivo.

- web.config

     O arquivo de web.site raiz.

- WebApplication.vstemplate

     O arquivo de modelo que determina o conteúdo da solução de site da Web e força a criação da pasta App_Data dados.

- WebApplication.webproj

     Esse arquivo é um artefato do sistema de modelo de projeto. Ele satisfaz a referência de arquivo de projeto no arquivo WebApplication.vstemplate.

### <a name="web-service-projects"></a>Projetos de serviço Web
 Esses arquivos criam um novo site em resposta ao comando **ASP.NET Web Service,** que está disponível depois de escolher Arquivo   >  **Novo Site**:

- Service.asmx

     A página HTML do novo serviço Web. O atributo Language especifica a linguagem codebehind e o atributo CodeBehind especifica o arquivo dependente que contém o código codebehind associado a esse serviço.

- Serviço. *extension*

     O arquivo dependente que implementa a classe de serviço. A linguagem codebehind determina a *extensão* desse arquivo.

- web.config

- O arquivo de web.site raiz.

- WebService.vstemplate

     O arquivo de modelo que determina o conteúdo da solução de site da Web e força a criação das pastas App_Data e App_Code web. O serviço. *O* arquivo de extensão é copiado para a pasta App_Code dados.

- WebService.webproj

     Esse arquivo é um artefato do sistema de modelo de projeto. Ele satisfaz a referência de arquivo de projeto no arquivo WebService.vstemplate.

## <a name="project-item-template-folder"></a>Pasta de modelo de item de projeto
 Os modelos de item de projeto Web normalmente são instalados em [ caminho de instalação do *Visual Studio*]\Common7\IDE\ItemTemplates\Web , cada um em uma subpasta que é nomeada após sua linguagem de programação da \\ Web.

## <a name="project-item-templates"></a>Modelos de item de projeto
 Os modelos de item de projeto do site são usados para adicionar novas páginas da Web a um site em resposta ao comando **Adicionar Item** Existente. Atualmente, há suporte para esses tipos de páginas da Web:

- Nova classe

- Nova página HTML

- Novo formulário da Web

- Nova página mestra

### <a name="new-class"></a>Nova Classe
 Esse modelo cria um novo arquivo de origem que define uma classe vazia em resposta ao **comando Adicionar Nova** Classe.

- Classe. *extension*

     O arquivo de origem que implementa a classe vazia. A linguagem codebehind determina a *extensão* desse arquivo.

- Class.vstemplate

     O arquivo de modelo que cria o arquivo de origem e determina seu conteúdo.

### <a name="new-html-page"></a>Nova página HTML
 Esse modelo cria uma nova página da Web em resposta ao **comando Adicionar Nova Página HTML.**

- HTMLPage.htm

     O conteúdo inicial da página da Web. Essa página da Web normalmente não tem nenhum arquivo dependente codebehind associado. Para criar uma página inteligente com um arquivo codebehind associado, use o modelo de Formulário da Web.

- HTMLPage.vstemplate

     O arquivo de modelo que cria a página da Web e determina seu conteúdo.

### <a name="new-webform"></a>Novo WebForm
 Esse modelo cria uma nova página da Web inteligente em resposta ao **comando Adicionar Novo Formulário da Web.**

 Para criar um arquivo de origem codebehind dependente, selecione **Colocar código no arquivo separado**. Caso contrário, uma única página da Web será criada com um bloco de script vazio e nenhuma \<% Page %> diretiva para conectar um arquivo dependente.

 Para criar uma página de conteúdo para uma página mestra selecionada, **selecione Selecionar página mestra**.

- WebForm.aspx

     O conteúdo inicial da página da Web. Esta página da Web não tem nenhum arquivo dependente codebehind associado.

- WebForm_cb.aspx

     O conteúdo inicial da página da Web. Esta página da Web tem um arquivo dependente codebehind associado.

- Codebehind. *extension*

     O arquivo dependente que implementa a classe webform. A linguagem codebehind determina a *extensão* desse arquivo.

- ContentPage.aspx

     O conteúdo inicial da página da Web como uma página de conteúdo. Esta página da Web não tem nenhum arquivo dependente codebehind associado.

- ContentPage_cb.aspx

     O conteúdo inicial da página da Web como uma página de conteúdo. Esta página da Web tem um arquivo dependente codebehind associado.

- WebForm.vstemplate

     O arquivo de modelo que determina o conteúdo da nova página da Web e seu arquivo dependente, se for o caso.

### <a name="new-master-page"></a>Nova página mestra
 Esse modelo cria uma nova página mestra em resposta ao **comando Adicionar Nova Página Mestra.**

 Para criar um arquivo de origem codebehind dependente, selecione **Colocar código no arquivo separado**. Caso contrário, uma única página da Web será criada com um bloco de script vazio e nenhuma \<% Page %> diretiva para conectar um arquivo dependente.

- MasterPage.master

     O conteúdo inicial da página mestra. Esta página mestra não tem nenhum arquivo dependente codebehind associado.

- MasterPage_cb.master

     O conteúdo inicial da página mestra. Esta página mestra tem um arquivo dependente codebehind associado.

- Codebehind. *extensão*

     O arquivo dependente que implementa a classe de página mestra. A linguagem codebehind determina a *extensão* desse arquivo.

- MasterPage.vstemplate

     O arquivo de modelo que determina o conteúdo da nova página mestra e seu arquivo dependente, se for o caso.

## <a name="see-also"></a>Confira também
- [Suporte a site](../../extensibility/internals/web-site-support.md)
