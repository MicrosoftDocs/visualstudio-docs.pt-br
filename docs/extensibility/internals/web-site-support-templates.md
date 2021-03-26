---
title: Modelos de suporte do site | Microsoft Docs
description: Saiba mais sobre modelos de suporte de site. Os modelos de projeto e item de site do Visual Studio fornecem projeto de site e stubs de item reutilizáveis e personalizáveis.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- we site projects, templates
ms.assetid: 37173c97-486b-4b3c-8ed3-cf5890c4de23
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c39e900bbdddd1d558bd0604f16924d2536cb98
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069083"
---
# <a name="web-site-support-templates"></a>Modelos de suporte a site
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Os modelos de projeto e item de site fornecem um projeto de site e stubs de item reutilizáveis e personalizáveis que aceleram o processo de desenvolvimento removendo a necessidade de criar novos projetos de site e itens do zero. Para obter mais informações sobre [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] modelos, consulte [Creating Project and item templates](../../ide/creating-project-and-item-templates.md).

## <a name="project-template-folder"></a>Pasta de modelos de projeto
 Os modelos de projeto Web normalmente são instalados no [*caminho de instalação do Visual Studio*] \Common7\IDE\ProjectTemplates\Web \\ , cada um em uma subpasta que é nomeada após a linguagem de programação da Web.

## <a name="project-file"></a>Arquivo de Projeto
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado) requer uma extensão de arquivo de projeto como uma maneira de mapear um modelo para o tipo de projeto correto. Como os projetos da Web não têm um arquivo de projeto, a extensão de arquivo de projeto fictício. o webproj é registrado para mapear o modelo para o tipo de projeto.

 Opcionalmente, uma cadeia de caracteres de nome de idioma pode ser adicionada ao modelo para habilitar o sistema de projeto da Web para definir o padrão de idioma na caixa de diálogo **Adicionar novo item** para itens com base no modelo. A cadeia de caracteres deve ser a primeira linha do arquivo. Ele deve corresponder tanto ao nome registrado em AddItemLanguageName no registro do mecanismo do IntelliSense quanto ao nome registrado em VsTemplate (subtipo do projeto). Para obter mais informações, consulte [atributos de suporte do site](../../extensibility/internals/web-site-support-attributes.md).

 Se a cadeia de caracteres não estiver presente, o sistema de projeto da Web tentará determinar o idioma padrão com base no atributo de idioma e nas extensões de arquivo das páginas adicionadas ao projeto Web pelo modelo de projeto.

## <a name="project-templates"></a>Modelos de projeto
 Os modelos de projeto de site são usados para criar novos sites da Web em resposta ao comando **novo site** no menu **arquivo** . No momento, há suporte para três tipos de projeto de site:

- Projetos de sites da Web vazios

- Projetos de site

- Projetos de serviço Web

### <a name="empty-web-site-projects"></a>Projetos de sites da Web vazios
 Esses arquivos criam um novo site vazio em resposta ao comando de **site vazio** , que está disponível depois de escolher **arquivo**  >  **novo site**:

- EmptyWeb. vstemplate

     O arquivo de modelo que orienta a criação do novo site da Web vazio.

- EmptyWeb. webproj

     Esse arquivo é um artefato do sistema de modelo de projeto. Ele satisfaz a referência de arquivo de projeto no arquivo EmptyWeb. vstemplate.

### <a name="web-site-projects"></a>Projetos de site
 Esses arquivos criam um novo site em resposta ao comando **site da ASP.net** , que está disponível depois de escolher **arquivo**  >  **novo site**:

- Default.aspx

     O home page padrão para o novo site. O atributo language especifica a linguagem codebehind e o atributo CodeFile especifica o arquivo dependente que contém o código code-behind associado a essa página.

- Default. aspx. *extensão* do

     O arquivo dependente que contém o código code-behind para o home page padrão. A linguagem codebehind determina a *extensão* desse arquivo.

- web.config

     O arquivo de configuração web.site raiz.

- WebApplication. vstemplate

     O arquivo de modelo que determina o conteúdo da solução de site e força a criação da pasta App_Data.

- WebApplication. webproj

     Esse arquivo é um artefato do sistema de modelo de projeto. Ele satisfaz a referência de arquivo de projeto no arquivo WebApplication. vstemplate.

### <a name="web-service-projects"></a>Projetos de serviço Web
 Esses arquivos criam um novo site em resposta ao comando **ASP.NET Web Service** , que está disponível depois de escolher **arquivo**  >  **novo site**:

- Service. asmx

     A página HTML para o novo serviço Web. O atributo language especifica a linguagem codebehind e o atributo CodeBehind especifica o arquivo dependente que contém o código code-behind associado a esse serviço.

- Serviço. *extension*

     O arquivo dependente que implementa a classe de serviço. A linguagem codebehind determina a *extensão* desse arquivo.

- web.config

- O arquivo de configuração web.site raiz.

- WebService. vstemplate

     O arquivo de modelo que determina o conteúdo da solução de site e força a criação das pastas App_Data e App_Code. O serviço. o arquivo de *extensão* é copiado para a pasta App_Code.

- WebService. webproj

     Esse arquivo é um artefato do sistema de modelo de projeto. Ele satisfaz a referência de arquivo de projeto no arquivo WebService. vstemplate.

## <a name="project-item-template-folder"></a>Pasta de modelo de item do projeto
 Projeto Web-os modelos de item normalmente são instalados no [*caminho de instalação do Visual Studio*] \Common7\IDE\ItemTemplates\Web \\ , cada um em uma subpasta que é nomeada após sua linguagem de programação da Web.

## <a name="project-item-templates"></a>Modelos de item de projeto
 Os modelos de item de projeto de site são usados para adicionar novas páginas da Web a um site em resposta ao comando **Adicionar item existente** . Atualmente, há suporte para esses tipos de páginas da Web:

- Nova classe

- Nova página HTML

- Novo formulário da Web

- Nova página mestra

### <a name="new-class"></a>Nova classe
 Este modelo cria um novo arquivo de origem que define uma classe vazia em resposta ao comando **Adicionar nova classe** .

- Classe. *extension*

     O arquivo de origem que implementa a classe vazia. A linguagem codebehind determina a *extensão* desse arquivo.

- Classe. vstemplate

     O arquivo de modelo que cria o arquivo de origem e determina seu conteúdo.

### <a name="new-html-page"></a>Nova página HTML
 Este modelo cria uma nova página da Web em resposta ao comando **Adicionar nova página HTML** .

- HTMLPage.htm

     O conteúdo inicial da página da Web. Essa página da Web normalmente não tem nenhum arquivo dependente de codebehind associado. Para criar uma página inteligente com um arquivo code-behind associado, use o modelo de formulário da Web em vez disso.

- HTMLPage. vstemplate

     O arquivo de modelo que cria a página da Web e determina seu conteúdo.

### <a name="new-webform"></a>Novo formulário da
 Este modelo cria uma nova página da Web inteligente em resposta ao comando **Adicionar novo formulário da Web** .

 Para criar um arquivo de origem code-behind dependente, selecione **posicionar código em arquivo separado**. Caso contrário, uma única página da Web é criada e tem um bloco de script vazio e nenhuma \<% Page %> diretivas para conectar um arquivo dependente.

 Para criar uma página de conteúdo para uma página mestra selecionada, selecione **selecionar página mestra**.

- WebForms. aspx

     O conteúdo inicial da página da Web. Esta página da Web não tem nenhum arquivo dependente de codebehind associado.

- WebForm_cb. aspx

     O conteúdo inicial da página da Web. Esta página da Web tem um arquivo dependente de codebehind associado.

- Behind. *extension*

     O arquivo dependente que implementa a classe webform. A linguagem codebehind determina a *extensão* desse arquivo.

- ContentPage. aspx

     O conteúdo inicial da página da Web como uma página de conteúdo. Esta página da Web não tem nenhum arquivo dependente de codebehind associado.

- ContentPage_cb. aspx

     O conteúdo inicial da página da Web como uma página de conteúdo. Esta página da Web tem um arquivo dependente de codebehind associado.

- WebForms. vstemplate

     O arquivo de modelo que determina o conteúdo da nova página da Web e seu arquivo dependente, se houver.

### <a name="new-master-page"></a>Nova página mestra
 Este modelo cria uma nova página mestra em resposta ao comando **Adicionar nova página mestra** .

 Para criar um arquivo de origem code-behind dependente, selecione **posicionar código em arquivo separado**. Caso contrário, uma única página da Web é criada e tem um bloco de script vazio e nenhuma \<% Page %> diretivas para conectar um arquivo dependente.

- MasterPage. Master

     O conteúdo inicial da página mestra. Esta página mestra não tem nenhum arquivo dependente de codebehind associado.

- MasterPage_cb. Master

     O conteúdo inicial da página mestra. Esta página mestra tem um arquivo dependente de codebehind associado.

- Behind. *extensão* do

     O arquivo dependente que implementa a classe da página mestra. A linguagem codebehind determina a *extensão* desse arquivo.

- MasterPage. vstemplate

     O arquivo de modelo que determina o conteúdo da nova página mestra e seu arquivo dependente, se houver.

## <a name="see-also"></a>Confira também
- [Suporte a site](../../extensibility/internals/web-site-support.md)
