---
title: Modelos de Item de projeto do SharePoint e Project | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.SPE.FirstWizardPage
- VS.SharePointTools.SPE.ListInstance
- VS.SharePointTools.SPE.ListDefinition
- VS.SharePointTools.SPE.ListDefFromContentType
- VS.SharePointTools.SPE.ContentType
- SPE.Wizard
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, project and project item templates
- SharePoint development in Visual Studio, templates
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6e38a3e709a8d49d29d598e7eabd55e7be154836
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49896435"
---
# <a name="sharepoint-project-and-project-item-templates"></a>Projeto do SharePoint e modelos de item de projeto
  As seções a seguir descrevem o projeto do SharePoint disponível e de item de projeto modelos e como eles são usados. 
  
## <a name="project-and-project-item-templates-overview"></a>Visão geral de modelos de item de projeto e de projeto
 Quando você cria um novo projeto do SharePoint no Visual Studio, um projeto do SharePoint é adicionado à solução junto com todos os itens de projeto necessários para esse tipo de projeto. Por exemplo, se você criar um projeto de Web Part do Silverlight, o Visual Studio cria uma solução que contém um item de projeto de Web Part Visual e um item de projeto de aplicativo do Silverlight juntamente com todos os arquivos necessários por esses itens de projeto. Modelos de item de projeto são usados para adicionar itens de projeto a um projeto existente do SharePoint, como a adição de um receptor de eventos, uma coluna de site ou uma lista.  
  
 Para obter informações sobre conceitos básicos do SharePoint, consulte [blocos de construção do SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=179404). Usuários avançados podem criar modelos de item de projeto e projeto personalizados. Para obter mais informações, consulte [estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).  
  
## <a name="project-templates"></a>Modelos de projeto
 A seguir está uma lista de modelos de projeto do SharePoint. Para exibir os modelos de projeto do SharePoint no Visual Studio, nos **novo projeto** diálogo caixa, expanda o **SharePoint** nó em um **Visual c#** ou  **Visual Basic**e, em seguida, escolha **2010**.  
  
### <a name="sharepoint-2010-project"></a>Projeto do SharePoint 2010
 O conteúdo de um *projeto do SharePoint 2010* estão incluídos em cada modelo de projeto do SharePoint. Contém um projeto do SharePoint 2010:  
  
-   Um arquivo de projeto.  
  
-   Uma página de propriedades do projeto.  
  
-   Um **referências** pasta listando todas as referências de assembly no projeto.  
  
-   Um **recursos** pasta que contém uma *Feature* arquivo de configuração, usado para implantar recursos no servidor do SharePoint.  
  
-   Um **pacote** pasta que contém uma *pacote* arquivo, usado para implantar a solução do SharePoint.  
  
-   Um arquivo de snk (chave de nome forte) que é usado para assinar o assembly com um nome forte, para segurança aprimorada.  
  
### <a name="sharepoint-2010-silverlight-web-part"></a>Web part do Silverlight do SharePoint 2010
 *Web Part do SharePoint 2010 Silverlight* projetos permitem que você a criar web parts para SharePoint que exibem os aplicativos do Silverlight. Quando você cria este projeto, você pode especificar se deseja adicionar um novo aplicativo Silverlight para ele ou fazer referência a um existente. Para obter mais informações, consulte [criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) e [passo a passo: criar uma web part do Silverlight que exiba OData para o SharePoint](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md).  
  
### <a name="sharepoint-2010-visual-web-part"></a>SharePoint 2010 web part visual
 Um *Visual Web Part do SharePoint 2010* projeto inclui um *Elements. XML* arquivo de definição, um **Web Part** item e um **controle de usuário** item . Você pode criar a aparência da web part visual arrastando ou copiando os controles de ferramentas do Visual Studio para a superfície do controle de usuário. Para obter mais informações, consulte [como: criar uma web part do SharePoint usando um Designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) e [bloco de construção: Web Parts](http://go.microsoft.com/fwlink/?LinkId=179438).  
  
### <a name="import-sharepoint-2010-solution-package"></a>Importar pacote de solução do SharePoint 2010
 *Importar o pacote de solução do SharePoint 2010* projetos permitem que você importe todo ou parte de um site existente do SharePoint 2010, exportado para uma solução do SharePoint (*wsp*) o arquivo, no Visual Studio. Depois de importados para o Visual Studio, você pode personalizar seus itens e reimplantá-los. Para obter mais informações, consulte [importar itens de um site do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md).  
  
### <a name="import-reusable-sharepoint-2010-workflow"></a>Importar fluxo de trabalho reutilizável do SharePoint 2010
 *Importar fluxo de trabalho reutilizável do SharePoint 2010* projetos permitem que você importe um fluxo de trabalho reutilizável e declarativo criado no SharePoint Designer 2010 no Visual Studio. O fluxo de trabalho é exportado do site do SharePoint como uma *. wsp* arquivo. Quando importado para o Visual Studio, pode personalizá-lo, adicione o código a ele e, em seguida, implantá-lo em um site do SharePoint. Para obter mais informações, consulte [instruções passo a passo: importar um fluxo de trabalho reutilizável do SharePoint Designer no Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md).  
  
## <a name="project-item-templates"></a>Modelos de item de projeto
 A seguir está uma lista de modelos de item de projeto do SharePoint. Modelos de item de projeto adicionam arquivos à solução do SharePoint para dar suporte à funcionalidade do SharePoint como colunas de site, listas e tipos de conteúdo. Por exemplo, a adição de uma coluna de site para sua solução adiciona um projeto de coluna de site que contém um *Elements. XML* arquivo de definição. Adicionar uma web part visual adiciona um projeto do visual web part à sua solução que contém um *Elements. XML* arquivo, um item de controle de usuário e um item do visual web part.  
  
 Para exibir os modelos de item de projeto do SharePoint, no **Gerenciador de soluções**, abra o menu de atalho para um projeto do SharePoint e, em seguida, escolha **Add**, **Novo Item**. Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha **2010**.  
  
### <a name="application-page-farm-solution-only"></a>Página de aplicativo (somente solução de farm)
 Uma **página do aplicativo (somente solução de Farm)** item permite que você projete um [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] página da web para um site do SharePoint. Páginas de aplicativos podem ser usadas somente em soluções de farm. Você pode adicionar esse item de projeto somente a soluções de farm. Para obter mais informações, consulte [como: criar uma página de aplicativo](../sharepoint/how-to-create-an-application-page.md) e [tipo de página layouts do aplicativo](http://go.microsoft.com/fwlink/?LinkId=179434).  
  
### <a name="business-data-connectivity-model-farm-solution-only"></a>Modelo de conectividade de dados corporativos (somente solução de farm)
 Um **modelo de conectividade de dados corporativos (somente solução de Farm)** item permite que você integrar dados de negócios no SharePoint. Dados de negócios podem vir de aplicativos de servidor back-end, como [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)], Siebel e o protocolo de anúncios de serviço (SAP). Modelos de conectividade de dados de negócios podem ser usados somente em soluções de farm. Você pode adicionar esse item de projeto somente a soluções de farm. Para obter mais informações, consulte [como: criar um modelo BDC](../sharepoint/how-to-create-a-bdc-model.md), [como: usar um arquivo de recurso para especificar nomes localizados, propriedades e permissões](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md), e [que há de novo: conectividade de negócios Serviços](http://go.microsoft.com/fwlink/?LinkId=179411).  
  
### <a name="content-type"></a>Tipo de conteúdo
 *Tipo de conteúdo* itens permitem que você crie tipos de conteúdo personalizados com base em um tipo de conteúdo (base) existente como um documento, anúncio ou uma tarefa. Um tipo de conteúdo personalizado fornece os mesmos atributos e campos como o tipo de conteúdo base junto com quaisquer colunas de site (campos) que você definir. Por exemplo, você pode criar um tipo de conteúdo de contato personalizado com base no tipo de base entre em contato com conteúdo que vem no SharePoint. Você pode personalizar o tipo de conteúdo alterando as colunas de site existente ou adicionando mais colunas de site para aqueles que já está incluídos no tipo de conteúdo base.  
  
> [!NOTE]  
>  Devido a uma limitação do SharePoint, você não pode criar um tipo de conteúdo de solução do farm com base em um tipo de conteúdo de solução de área restrita.  
  
 Para obter mais informações, consulte [instruções passo a passo: criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) e [bloco de construção: tipo de conteúdo](http://go.microsoft.com/fwlink/?LinkId=179413).  
  
### <a name="empty-element"></a>Elemento vazio
 *Elementos vazios* geralmente são usadas para definir os itens de projeto do SharePoint que não têm um projeto ou o modelo de item de projeto no Visual Studio. Quando você adiciona um elemento vazio ao seu projeto, um nó denominado EmptyElement [x](where [x] is a unique number\) is created. EmptyElement [x] contém um arquivo único que é nomeado *Elements. XML.* Use [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] instruções para definir os elementos desejados no *Elements. XML*.  
  
### <a name="event-receiver"></a>Receptor de eventos
 *Receptores de evento* manipular eventos para itens no site do SharePoint, como quando um item é adicionado a uma lista, quando um item da web for excluído ou quando um fluxo de trabalho foi iniciado. O modelo de item de projeto de receptor de evento permite que você manipule  
  
- Lista de eventos  
  
- Eventos de item de lista  
  
- Listar eventos de email  
  
- Eventos da Web  
  
- Eventos de fluxo de trabalho de lista  
  
  O item de projeto do receptor de eventos cria uma **receptor de evento** pasta com um arquivo de classe única que contém os manipuladores de eventos para todos os eventos você especificou quando criou o projeto na **personalização do SharePoint Assistente**. A classe do receptor de eventos pode manipular eventos que ocorrem no site do SharePoint quando itens como arquivos, campos, itens, listas, anexos, web parts e fluxos de trabalho são adicionados, atualizados, excluídos ou removidos. Para obter mais informações, consulte [como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md) e [bloco de construção: manipulação de eventos](http://go.microsoft.com/fwlink/?LinkId=179416).  
  
### <a name="list"></a>Lista  
 Uma lista é uma instância de uma base do SharePoint lista definição reutilizável, como um calendário ou uma lista de tarefas. Depois de adicionar uma lista para sua solução, o Designer de lista permite que você adicione colunas de site à lista e criar colunas de lista personalizada. Isso inclui colunas de tipos de conteúdo de site. Você pode especificar o *exibição* para a lista, que determina as colunas que aparecerão na lista. Para obter mais informações, consulte [instruções passo a passo: criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) e [bloco de construção: listas e bibliotecas de documentos](http://go.microsoft.com/fwlink/?LinkId=179421).  
  
### <a name="module"></a>Módulo  
 *Módulos* (não deve ser confundido com [!include[vbprvb](../sharepoint/includes/vbprvb-md.md)] módulos) contêm todos os arquivos que você deseja implantar para o servidor do SharePoint, como imagens ou notas. O item de projeto de módulo contém um **módulo** nó. O nó do módulo contém dois modelos de item de projeto: um arquivo de definição XML, que atua como um manifesto para o módulo, e um *txt* arquivo, um arquivo de espaço reservado. Para obter mais informações, consulte [uso de módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md) e [módulos](http://go.microsoft.com/fwlink/?LinkId=179425).  
  
### <a name="sequential-workflow-farm-solution-only"></a>O fluxo de trabalho sequencial (somente solução de farm)
 Um *fluxo de trabalho sequencial* é uma série de etapas de lógica de negócios, executadas em sequência, até que a última etapa é concluída. Fluxos de trabalho sequenciais são usados para gerenciar os processos que envolvem itens como listas e documentos do SharePoint. Você pode criar fluxos de trabalho de nível de site (globais) ou (locais) no nível da lista de fluxos de trabalho, e você pode selecionar se um fluxo de trabalho é iniciado automaticamente ou manualmente. Esse item de projeto pode ser usado somente em soluções de farm. Você pode adicionar esse item de projeto somente a soluções de farm. Para obter mais informações, consulte [soluções de fluxo de trabalho do SharePoint crie](../sharepoint/creating-sharepoint-workflow-solutions.md), [fluxos de trabalho no SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=260555), e [Novidades: aprimoramentos de fluxo de trabalho](http://go.microsoft.com/fwlink/?LinkId=179418).  
  
### <a name="silverlight-web-part"></a>Web part do Silverlight
 *Web part do Silverlight* itens de projeto permitem que você a criar web parts para SharePoint que exibem os aplicativos do Silverlight. Quando você adiciona esse item de projeto à sua solução, você pode escolher se deseja adicionar um novo aplicativo do Silverlight ou fazer referência a um existente mais tarde. Para obter mais informações, consulte [criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) e [passo a passo: criar uma web part do Silverlight que exiba OData para o SharePoint](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md).  
  
### <a name="site-column"></a>Coluna de site
 Um *coluna de site*, também conhecido como um *campo*, é um dos elementos mais básicos que você pode adicionar a um projeto do SharePoint. Uma coluna de site representa um tipo de dados, como um número de telefone, um comentário de texto ou o nome da cidade de um contato em uma lista de contatos. Para obter mais informações, consulte [criar colunas de site, tipos de conteúdo e listas para o SharePoint](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md) e [colunas](http://go.microsoft.com/fwlink/?LinkId=226840).  
  
### <a name="site-definition-farm-solution-only"></a>Definição de site (somente solução de farm)
 *Definição de site* itens de projeto contém uma pasta de definição de site que inclui os seguintes arquivos:  
  
- Uma padrão página. aspx, usada como a página da web padrão para o site.  
  
- Uma *onet* arquivo que define os componentes do site.  
  
- Um arquivo xml webtemp que especifica as configurações de definição de site que aparecem na **seleção de modelo** seção o **novo Site do SharePoint** página.  
  
  Depois de adicionar uma definição de site, você deve adicionar código e arquivos para apresentar a funcionalidade. Esse item de projeto pode ser usado somente em soluções de farm. Você pode adicionar esse item de projeto somente a soluções de farm. Para obter mais informações, consulte [criar definições de site do SharePoint](../sharepoint/creating-site-definitions-for-sharepoint.md) e [definições de Site e configurações](http://go.microsoft.com/fwlink/?LinkId=260554).  
  
### <a name="state-machine-workflow-farm-solution-only"></a>Fluxo de trabalho de máquina de estado (somente solução de farm)
 Um *fluxo de trabalho de máquina de estado* é um conjunto de estados de lógica de negócios, transições e ações. As etapas em um fluxo de trabalho de máquina de estado não são executadas em sequência. em vez disso, eles são disparados por ações e os estados. Como um fluxo de trabalho sequencial, fluxos de trabalho de máquina de estado são associados a itens como listas e documentos do SharePoint. Mais uma vez, você pode criar fluxos de trabalho de nível de site (globais) ou (locais) no nível da lista de fluxos de trabalho. Você também pode selecionar se um fluxo de trabalho é iniciado automaticamente ou manualmente. Esse item de projeto pode ser usado somente em soluções de farm. Você pode adicionar esse item de projeto somente a soluções de farm. Para obter mais informações, consulte [soluções de fluxo de trabalho do SharePoint crie](../sharepoint/creating-sharepoint-workflow-solutions.md), [fluxos de trabalho no SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=260555), e [Novidades: aprimoramentos de fluxo de trabalho](http://go.microsoft.com/fwlink/?LinkId=179418).  
  
### <a name="user-control-farm-solution-only"></a>Controle de usuário (somente solução de farm)
 Um *controle de usuário* é um controle personalizado, reutilizável para o qual você pode adicionar outros controles do ASP.NET e controles do SharePoint. O controle de usuário pode ser adicionado a páginas de aplicativos e web parts executadas no SharePoint. Esse item de projeto pode ser usado somente em soluções de farm. Você pode adicionar esse item de projeto somente a soluções de farm. Para obter mais informações, consulte [criação de controles de reutilizáveis para Web Parts ou páginas de aplicativo](http://go.microsoft.com/fwlink/?LinkId=226841).  
  
### <a name="visual-web-part"></a>Web part Visual
 Um *web part visual* item de projeto inclui um *Elements. XML* arquivo de definição, um **Web Part** item e um **controle de usuário** item. Você pode criar a aparência da web part visual arrastando ou copiando os controles de ferramentas do Visual Studio para a superfície do controle de usuário. Para obter mais informações, consulte [como: criar uma web part do SharePoint usando um Designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md) e [bloco de construção: Web Parts](http://go.microsoft.com/fwlink/?LinkId=179438).  
  
### <a name="web-part"></a>Web Part
 Um *da web part* é um controle de servidor que é executado dentro de um tipo especial de página chamado de uma página de Web Parts. Eles são os blocos de construção de páginas que aparecem em um site do SharePoint. O item da web part fornece os arquivos que permitem que você criar uma web part para um site do SharePoint. Para obter mais informações, consulte [como: criar uma web part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md) e [bloco de construção: Web Parts](http://go.microsoft.com/fwlink/?LinkId=179438).  
  
## <a name="see-also"></a>Consulte também
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)   
 [Produtos e tecnologias SharePoint](http://go.microsoft.com/fwlink/?LinkId=178818)  
  
  
