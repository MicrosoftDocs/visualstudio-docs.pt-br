---
title: Desenvolver soluções do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.ProjectProperties
- VS.SharePointTools.Project.ProjectItemProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, overview
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 25a7402a8d0464152e9b1bdd9d2edcdc66824914
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295898"
---
# <a name="develop-sharepoint-solutions"></a>Desenvolver soluções do SharePoint
  Vários modelos de tipo de projeto do SharePoint estão disponíveis no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] para a criação de sites do SharePoint e os elementos do site. Para obter uma lista dos tipos de projeto disponíveis, consulte [SharePoint modelos de item de projeto e projeto](../sharepoint/sharepoint-project-and-project-item-templates.md). Veja a seguir uma descrição dos elementos e propriedades de um projeto do SharePoint.  
  
 Para obter informações sobre os suplementos do SharePoint e SharePoint 2013, consulte [SharePoint 2013](https://msdn.microsoft.com/library/jj162979.aspx) e [suplementos do SharePoint compilar](/sharepoint/dev/sp-add-ins/sharepoint-add-ins).  
  
## <a name="elements-of-a-sharepoint-project"></a>Elementos de um projeto do SharePoint
 Os nós em um projeto do SharePoint são conhecidos como *itens do SharePoint*. Itens do SharePoint também podem conter um ou mais subarquivos, conhecidos como *arquivos de item do SharePoint*, como [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivos de configuração, os formulários. aspx e muito mais.  
  
 Em vez de criar projetos usando modelos de projeto que já estão preenchidos com arquivos de item de projeto, você pode usar o **projeto vazio** modelo para criar um projeto vazio do SharePoint e, em seguida, adicionar itens de projeto manualmente. Projetos do SharePoint também podem conter um ou mais arquivos de recurso (para ativação no SharePoint) e um arquivo de pacote para distribuir o projeto.  
  
### <a name="special-nodes"></a>Nós especiais
 Cada projeto do SharePoint contém dois nós que não podem ser renomeados, excluídos, recortar, copiados ou arrastados do projeto. Esses nós são da seguinte maneira:  
  
- Recursos    
- Pacote  
  
  Ambos os nós sempre aparecem em todos os projetos do SharePoint, mesmo se nenhum recurso ou os pacotes são definidos para o projeto.  
  
#### <a name="features-node"></a>Nó de recursos
 O **recursos** nó contém um ou mais recursos de projeto do SharePoint. Um recurso é um contêiner de extensões para o SharePoint. Depois que um recurso é implantado no servidor do SharePoint, pode ser incluído em definições de site ou ativado individualmente por administradores do SharePoint nos sites do SharePoint. Para obter mais informações, consulte [trabalhando com recursos](http://go.microsoft.com/fwlink/?LinkID=147704).  
  
 Quando você adiciona um item, como um tipo de conteúdo ou uma instância de lista, para um projeto do SharePoint, ele é adicionado a um recurso nas **recursos** nó. O escopo do item determina se ele é adicionado a um recurso novo ou existente. Se o novo item tem o mesmo escopo como um recurso existente, em seguida, ele é adicionado a esse recurso. Caso contrário, o item é adicionado a um novo recurso.  
  
 Para adicionar manualmente um recurso, execute as **adicionar recurso** comando no menu de atalho do nó de recurso. Você pode exibir ou alterar o conteúdo de um recurso usando o Designer de recursos. Para obter mais informações, consulte [como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md).  
  
 Quando um recurso é adicionado a um projeto do SharePoint, ele aparece no **Gerenciador de soluções** recurso de nome como um nó com o padrão*x*Feature, onde *x* é um número exclusivo. Depois que um recurso é implantado para o servidor do SharePoint, um administrador do SharePoint pode ativá--lo, tornando-o disponível aos usuários do site do SharePoint.  
  
#### <a name="package-node"></a>No nó do pacote
 O **pacote** nó contém um único arquivo que serve como o mecanismo de distribuição para o projeto do SharePoint. Esse arquivo, conhecido como um *pacote de solução*, é. Com base no CAB com um. Extensão do WSP. Um pacote de solução é um arquivo implantável e reutilizável que contém um conjunto de recursos, definições de site e assemblies que se aplicam a sites do SharePoint e que você pode habilitar ou desabilitar individualmente. O **pacote** nó também sempre contém um arquivo chamado wspdef, um [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivo de definição de pacote. Depois que um pacote é implantado para o servidor que está executando o SharePoint, o administrador do SharePoint pode instalá-lo e ativar seus recursos.  
  
 Você pode exibir ou alterar o conteúdo do pacote no Designer de pacote, clicando duas vezes no nó do pacote ou abrindo o menu de atalho e, em seguida, escolhendo **aberto**. Para obter mais informações, consulte [pacotes de soluções do SharePoint criar](../sharepoint/creating-sharepoint-solution-packages.md).  
  
## <a name="sharepoint-project-and-project-item-properties"></a>Projeto do SharePoint e as propriedades de item de projeto
 Projetos do SharePoint, como qualquer outro [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos, exibir as propriedades na janela Propriedades e a página de propriedades. As propriedades que são exibidas dependem do nó que está selecionado.  
  
 Quando um projeto do SharePoint, item de projeto ou nó de arquivo do item de projeto for selecionado no **Gerenciador de soluções**, as seguintes propriedades aparecerão na janela de propriedades ou a página de propriedades:  
  
### <a name="project-properties"></a>Propriedades de projeto
  
|Nome da Propriedade|Descrição|  
|-------------------|-----------------|  
|Configuração de implantação ativa|Especifica a série de etapas executadas durante a implantação. Para obter mais informações, consulte [como: editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md).|  
|Destino de implantação do assembly|Determina onde *assemblies de aplicativo do SharePoint* estão localizados. Os valores de local de assembly válidos são *GlobalAssemblyCache* (padrão), ou *WebApplication*.<br /><br /> Se o *solução de área restrita* estiver definida como **true**, em seguida, essa propriedade está desabilitada.|  
|Retração automática após a depuração|Especifica se a solução implantada retrai automaticamente do SharePoint depois de executar o aplicativo no modo de depuração no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Quando selecionada, a solução retrai quando o IDE volta para criar o modo de exibição após a depuração. Quando desmarcada, a solução não retrai. Para obter mais informações, consulte [cancelamento de uma solução](http://go.microsoft.com/fwlink/?LinkId=183819).|  
|Editar configurações|Especifica a configuração de implantação a ser usado para o projeto. Para obter mais informações, consulte [como: editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md) e [implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md).|  
|Habilitar a depuração do Silverlight (em vez de depuração de Script)|Quando selecionada, o depurador do Silverlight anexa ao processo de depuração. Quando desmarcada, o depurador de Script anexa ao processo de depuração. Para obter mais informações, consulte [visão geral de depuração do Silverlight](http://go.microsoft.com/fwlink/?LinkId=179826).|  
|Incluir Assembly no pacote|Especifica se o assembly do projeto é empacotado em tempo de compilação ou não.|  
|Linha de comando de pós-implantação|Especifica os comandos a serem executados depois de implantar a solução do SharePoint. Essa linha dá suporte a qualquer comando em lote, bem como a resolução de variáveis do MSBuild. Para obter mais informações, consulte [como: definir comandos de implantação do SharePoint](../sharepoint/how-to-set-sharepoint-deployment-commands.md).|  
|Linha de comando de pré-implantação|Especifica os comandos para executar antes de implantar a solução do SharePoint. Essa linha dá suporte a qualquer comando em lote, bem como a resolução de variáveis do MSBuild. Para obter mais informações, consulte [como: definir comandos de implantação do SharePoint](../sharepoint/how-to-set-sharepoint-deployment-commands.md).|  
|Arquivo de Projeto|O nome do arquivo contendo compilação, configuração e outras informações sobre o projeto.|  
|Pasta do projeto|O local do arquivo de projeto no sistema. (Somente leitura.)|  
|Solução de área restrita|Especifica se o projeto deve ser implantado como um *solução de área restrita*, também conhecido como um *solução criada pelo usuário*. Soluções em área restrita não são necessariamente confiáveis. Um valor de **verdadeira** significa que o projeto é implantado como uma solução em área restrita, um valor de **falso** significa que o projeto é implantado como uma solução de farm. Para obter mais informações, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md) e [diferenças entre em modo seguro e soluções de Farm](../sharepoint/differences-between-sandboxed-and-farm-solutions.md).|  
|URL do site|Especifica o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] do site de destino para este projeto.|  
|Item de inicialização|Especifica o primeiro item no projeto a ser executado.|  
  
 Quando você escolhe um arquivo de item do SharePoint (como um fluxo de trabalho ou um recurso no nó recursos), as seguintes propriedades aparecerão na janela Propriedades:  
  
### <a name="project-item-properties"></a>Propriedades de item de projeto
  
|Nome da Propriedade|Descrição|  
|-------------------|-----------------|  
|Resolução do Conflito de Implantação|Especifica a ação a ser tomada ao implantar um item de projeto cujas propriedades são idênticas às de um item existente no servidor. Para obter mais informações, consulte [implantação e solução de problemas de empacotamento de SharePoint](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md).|  
|Propriedades do recurso|Especifica um conjunto de valores (armazenados como pares chave/valor) que está incluído com um recurso quando ele é implantado no SharePoint. Depois que o recurso é implantado, você pode acessar os valores de propriedade em seu código. Para obter mais informações, consulte [fornecendo informações de pacote e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|  
|Receptor de recurso|Fornece código que é executado quando determinados eventos ocorrem em um item de projeto que contém recursos. Para obter mais informações, consulte [fornecendo informações de pacote e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|  
|Nome da Pasta|O nome da pasta de item de projeto do SharePoint.|  
|Referências de saída do projeto|Especifica uma dependência, como um assembly, o que o item de projeto precisa ser executada. Para obter mais informações, consulte [fornecendo informações de pacote e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|  
|Entradas de controle seguro|Especifica controles que são seguros para usuários não confiáveis editar. Para obter mais informações, consulte [fornecendo informações de pacote e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|  
  
### <a name="project-item-file-properties"></a>Propriedades do arquivo de item de projeto
  
|Nome da Propriedade|Descrição|  
|-------------------|-----------------|  
|Ação de build|Especifica como o arquivo se relaciona aos processos de compilação e implantação. Para obter mais informações, consulte [propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|  
|Copiar para diretório de saída|Especifica se os arquivos de origem serão copiados para o diretório de saída. pode ser um dos seguintes valores:<br /><br /> -   *Não copiar*<br />-   *Sempre copiar*<br />-   *Copiar se mais recente*<br /><br /> Para obter mais informações, consulte [propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|  
|Ferramenta personalizada|Especifica o nome de uma ferramenta, se houver, que transforma o arquivo em tempo de design e coloca a saída da transformação em outro arquivo. Por exemplo, um conjunto de dados (.[!INCLUDE[TLA2#tla_xsd](../sharepoint/includes/tla2sharptla-xsd-md.md)]) arquivo tem uma ferramenta personalizada padrão. Para obter mais informações, consulte [propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|  
|Namespace de ferramenta personalizada|O namespace no qual a saída da ferramenta personalizada é copiada. Para obter mais informações, consulte [propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|  
|Local de implantação|O caminho totalmente qualificado do arquivo no servidor do SharePoint. Esse caminho é composto de raiz de implantação e caminho de implantação de subpropriedades.|  
|Caminho de implantação|O caminho relativo do arquivo no arquivo do SharePoint Server, como Workflow1\\. O caminho totalmente qualificado para o arquivo é criado concatenando as *caminho de implantação* valor ao final da *raiz de implantação* valor.<br /><br /> Selecionando um valor de *RootFile* para o *tipo de implantação* alterações de propriedade a *raiz de implantação* propriedade \<SharePointRoot >\\, resultando em um caminho totalmente qualificado \<SharePointRoot > \Workflow1\\. Para obter mais informações, consulte [empacotamento e implantação de soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md).|  
|Raiz de implantação|Cadeia. A pasta raiz onde o arquivo é implantado no servidor do SharePoint. Por exemplo, \<SharePointRoot > \Template\Features\\\<FeatureName >\\.<br /><br /> O valor da *raiz de implantação* propriedade é determinada pelo *tipo de implantação* configuração.|  
|Tipo de implantação|Tipo de implantação do arquivo, que determina sua *raiz de implantação* valor. pode ser um dos seguintes valores:<br /><br /> NoDeployment:  *\<nenhum valor >*<br /><br /> ElementManifest:  *\<SharePointRoot > \Template\Features\\\<FeatureName >*\\<br /><br /> ElementFile:  *\<SharePointRoot > \Template\Features\\\<FeatureName >\\*<br /><br /> TemplateFile:  *\<SharePointRoot > \Template\\*<br /><br /> RootFile:  *\<SharePointRoot >\\*<br /><br /> GlobalResource:  *\<SharePointRoot > \Resources\\*<br /><br /> ClassResource:  *\<ClassResourcePath >\\*<br /><br /> Para obter mais informações, consulte <xref:Microsoft.VisualStudio.SharePoint.DeploymentType>.|  
|Nome do Arquivo|O nome do arquivo ou pasta para o arquivo do item.|  
|Caminho completo|O local do arquivo para o item. (Somente leitura.)|  
  
## <a name="related-topics"></a>Tópicos relacionados
  
|Título|Descrição|  
|-----------|-----------------|  
|[Projeto do SharePoint e Modelos de Item de Projeto](../sharepoint/sharepoint-project-and-project-item-templates.md)|Descreve o projeto do SharePoint e modelos de item de projeto disponíveis para você no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].|  
|[Como adicionar itens a um Projeto do SharePoint](../sharepoint/how-to-add-items-to-a-sharepoint-project.md)|Descreve como adicionar itens novos ou existentes para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.|  
|[Passo a passo: Criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)|Orienta você passo a passo na criação de um cliente campo, tipo de conteúdo, definição de lista e instância de lista.|  
|[Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)|Descreve como adicionar um receptor de eventos para o projeto criado no [instruções passo a passo: criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md).|  
|[Criar soluções de fluxo de trabalho do SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)|Descreve como criar projetos de fluxo de trabalho que inclui formulários de associação de fluxo de trabalho e formulários de iniciação do fluxo de trabalho.|  
|[Criar páginas do SharePoint](../sharepoint/creating-pages-for-sharepoint.md)|Descreve como você pode criar páginas como páginas de aplicativos, páginas do site, páginas mestras e layouts de página para o SharePoint.|  
|[Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)|Descreve como adicionar controles que permitem aos usuários modificar diretamente o conteúdo, aparência e comportamento das páginas do site do SharePoint usando um navegador.|  
|[Criar controles reutilizáveis para web parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|Descreve como criar controles de usuário que podem ser consumidos por páginas de aplicativos e Web Parts executadas no SharePoint.|  
|[Integre dados corporativos no SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)|Descreve como integrar dados de serviços da Web e aplicativos de servidor back-end em um aplicativo do SharePoint.|  
|[Criar definições de site do SharePoint](../sharepoint/creating-site-definitions-for-sharepoint.md)|Descreve como criar definições de site: modelos que são usados para criar sites do SharePoint.|  
|[Importando itens de um site existente do SharePoint](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)|Descreve como importar itens como módulos e tipos de conteúdo de um site do SharePoint existente para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.|  
|[Usando módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md)|Descreve como usar módulos para implantar arquivos de seu [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto para o site do SharePoint.|  
|[Procurar conexões do SharePoint usando o Gerenciador de servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)|Descreve como procurar sites locais do SharePoint usando o Gerenciador de servidores.|  
|[Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)|Descreve como usar propriedades de item de projeto para fornecer informações de empacotamento e implantação de projetos, como entradas de controle seguro, referências de saída do projeto e as propriedades do recurso.|  
|[Como: adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md)|Descreve como as pastas mapeadas podem ser adicionados ao seu projeto para facilitar o acesso aos recursos do SharePoint.|  
|[Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md)|Descreve os problemas associados às soluções em área restrita.|  
|[Segurança das soluções do SharePoint](../sharepoint/security-for-sharepoint-solutions.md)|Descreve as considerações de segurança para desenvolver soluções do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].|  
|[Caixa de diálogo do seletor de URL &#40;desenvolvimento do SharePoint no Visual Studio&#41;](../sharepoint/url-picker-dialog-box-sharepoint-development-in-visual-studio.md)|Descreve uma caixa de diálogo que você pode usar para adicionar referências de caminho a recursos em seu projeto ou no servidor do SharePoint local.|  
  
## <a name="see-also"></a>Consulte também
 [Introdução ao &#40;desenvolvimento do SharePoint no Visual Studio&#41;](../sharepoint/getting-started-sharepoint-development-in-visual-studio.md)   
 [Procurar conexões do SharePoint usando o Gerenciador de servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)   
 [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)   
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
  
