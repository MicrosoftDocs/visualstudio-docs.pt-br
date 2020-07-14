---
title: Desenvolvendo soluções do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.Project.ProjectProperties
- VS.SharePointTools.Project.ProjectItemProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, overview
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 36823637c530d65776c149ff576bf5e7e0ca545f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016793"
---
# <a name="develop-sharepoint-solutions"></a>Desenvolver soluções do SharePoint
  Vários modelos de tipo de projeto do SharePoint estão disponíveis no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] para criar sites e elementos do site do SharePoint. Para obter uma lista dos tipos de projeto disponíveis, consulte [projeto do SharePoint e modelos de item de projeto](../sharepoint/sharepoint-project-and-project-item-templates.md). Veja a seguir uma descrição dos elementos e das propriedades de um projeto do SharePoint.

 Para obter informações sobre os suplementos do SharePoint 2013 e do SharePoint, consulte [sharepoint 2013](https://www.microsoft.com/microsoft-365/previous-versions/microsoft-sharepoint-2013) e [Compilar suplementos do SharePoint](/sharepoint/dev/sp-add-ins/sharepoint-add-ins).

## <a name="elements-of-a-sharepoint-project"></a>Elementos de um projeto do SharePoint
 Os nós em um projeto do SharePoint são conhecidos como *itens do SharePoint*. Os itens do SharePoint também podem conter um ou mais subarquivos, conhecidos como *arquivos de item do SharePoint*, como [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivos de configuração, formulários. aspx e muito mais.

 Em vez de criar projetos usando modelos de projeto que já estão preenchidos com arquivos de item de projeto, você pode usar o modelo de **projeto vazio** para criar um projeto do SharePoint vazio e, em seguida, adicionar itens de projeto manualmente. Os projetos do SharePoint também podem conter um ou mais arquivos de recursos (para ativação no SharePoint) e um arquivo de pacote no qual distribuir o projeto.

### <a name="special-nodes"></a>Nós especiais
 Cada projeto do SharePoint contém dois nós que não podem ser renomeados, excluídos, recortados, copiados ou arrastados do projeto. Esses nós são os seguintes:

- Recursos
- Pacote

  Ambos os nós sempre aparecem em todos os projetos do SharePoint, mesmo que nenhum recurso ou pacote seja definido para o projeto.

#### <a name="features-node"></a>Nó de recursos
 O nó **recursos** contém um ou mais recursos de projeto do SharePoint. Um recurso é um contêiner de extensões para o SharePoint. Depois que um recurso é implantado no SharePoint Server, ele pode ser incluído em definições de site ou ativado individualmente por administradores do SharePoint em sites do SharePoint. Para obter mais informações, consulte [trabalhando com recursos](/previous-versions/office/developer/sharepoint-2010/ms460318(v=office.14)).

 Quando você adiciona um item, como um tipo de conteúdo ou uma instância de lista, a um projeto do SharePoint, ele é adicionado a um recurso no nó **recursos** . O escopo do item determina se ele é adicionado a um recurso novo ou existente. Se o novo item tiver o mesmo escopo de um recurso existente, ele será adicionado a esse recurso. Caso contrário, o item será adicionado a um novo recurso.

 Para adicionar um recurso manualmente, execute o comando **Adicionar recurso** no menu de atalho do nó de recurso. Você pode exibir ou alterar o conteúdo de um recurso usando o designer de recursos. Para obter mais informações, consulte [como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md).

 Quando um recurso é adicionado a um projeto do SharePoint, ele aparece em **Gerenciador de soluções** como um nó com o recurso de nome padrão*x*. Feature, em que *x* é um número exclusivo. Depois que um recurso é implantado no servidor do SharePoint, um administrador do SharePoint pode ativá-lo, disponibilizando-o para os usuários do site do SharePoint.

#### <a name="package-node"></a>Nó do pacote
 O nó do **pacote** contém um único arquivo que serve como o mecanismo de distribuição para o projeto do SharePoint. Esse arquivo, conhecido como um *pacote de solução*, é. Baseado em CAB com um. Extensão WSP. Um pacote de solução é um arquivo implantável e reutilizável que contém um conjunto de recursos, definições de site e assemblies que se aplicam a sites do SharePoint e que você pode habilitar ou desabilitar individualmente. O nó do **pacote** também contém sempre um arquivo chamado Package. wspdef, um [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivo de definição para o pacote. Depois que um pacote é implantado no servidor que está executando o SharePoint, o administrador do SharePoint pode instalá-lo e ativar seus recursos.

 Você pode exibir ou alterar o conteúdo do pacote no designer de pacote clicando duas vezes no nó do pacote ou abrindo o menu de atalho e, em seguida, escolhendo **abrir**. Para obter mais informações, consulte [criar pacotes de solução do SharePoint](../sharepoint/creating-sharepoint-solution-packages.md).

## <a name="sharepoint-project-and-project-item-properties"></a>Projeto do SharePoint e propriedades de item do projeto
 Projetos do SharePoint, assim como outros [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos, exibem propriedades no janela Propriedades e na página Propriedades. As propriedades exibidas dependem do nó selecionado.

 Quando um projeto do SharePoint, item de projeto ou nó de arquivo de item de projeto é selecionado em **Gerenciador de soluções**, as propriedades a seguir aparecem na janela Propriedades ou na página de propriedades:

### <a name="project-properties"></a>Propriedades do projeto

|Nome da propriedade|Descrição|
|-------------------|-----------------|
|Configuração de implantação ativa|Especifica a série de etapas executadas durante a implantação. Para obter mais informações, consulte [como: editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md).|
|Destino de implantação de assembly|Determina onde os *assemblies de aplicativo do SharePoint* estão localizados. Os valores válidos de localização do assembly são *GlobalAssemblyCache* (padrão) ou *WebApplication*.<br /><br /> Se a propriedade da *solução em área restrita* estiver definida como **true**, essa propriedade será desabilitada.|
|Cancelar automaticamente após a depuração|Especifica se a solução implantada automaticamente cancela do SharePoint após a execução do aplicativo no modo de depuração no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Quando selecionada, a solução cancela quando o IDE volta para o modo de exibição de design após a depuração. Quando desmarcada, a solução não é removida. Para obter mais informações, consulte [cancelando uma solução](/previous-versions/office/developer/sharepoint-2010/aa543958(v=office.14)).|
|Editar configurações|Especifica a configuração de implantação a ser usada para o projeto. Para obter mais informações, consulte [como: editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md) e [implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md).|
|Habilitar depuração do Silverlight (em vez de depuração de script)|Quando selecionado, o depurador do Silverlight é anexado ao processo de depuração. Quando desmarcada, o depurador de script é anexado ao processo de depuração. Para obter mais informações, consulte [visão geral de depuração do Silverlight](/previous-versions/windows/).|
|Incluir assembly no pacote|Especifica se o assembly do projeto é empacotado no momento da compilação ou não.|
|Linha de comando pós-implantação|Especifica os comandos a serem executados após a implantação da solução do SharePoint. Essa linha dá suporte a qualquer comando do lote, bem como à resolução de variáveis do MSBuild. Para obter mais informações, consulte [como: definir comandos de implantação do SharePoint](../sharepoint/how-to-set-sharepoint-deployment-commands.md).|
|Linha de comando de pré-implantação|Especifica os comandos a serem executados antes da implantação da solução do SharePoint. Essa linha dá suporte a qualquer comando do lote, bem como à resolução de variáveis do MSBuild. Para obter mais informações, consulte [como: definir comandos de implantação do SharePoint](../sharepoint/how-to-set-sharepoint-deployment-commands.md).|
|Arquivo de Projeto|O nome do arquivo que contém a compilação, a configuração e outras informações sobre o projeto.|
|Pasta de projeto|O local do arquivo de projeto no sistema. (Somente leitura.)|
|Solução em área restrita|Especifica se o projeto deve ser implantado como uma *solução de área restrita*, também conhecida como *solução criada pelo usuário*. As soluções de área restrita não são necessariamente confiáveis. Um valor **true** significa que o projeto é implantado como uma solução de área restrita, um valor **false** significa que o projeto é implantado como uma solução de farm. Para obter mais informações, consulte [considerações de solução em área restrita](../sharepoint/sandboxed-solution-considerations.md) e [diferenças entre as soluções de área restrita e de farm](../sharepoint/differences-between-sandboxed-and-farm-solutions.md).|
|URL do site|Especifica o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] do site de destino para este projeto.|
|Item de inicialização|Especifica o primeiro item no projeto a ser executado.|

 Quando você escolhe um arquivo de item do SharePoint (como um fluxo de trabalho ou um recurso no nó recursos), as seguintes propriedades aparecem no janela Propriedades:

### <a name="project-item-properties"></a>Propriedades do item de projeto

|Nome da propriedade|Descrição|
|-------------------|-----------------|
|Resolução do Conflito de Implantação|Especifica a ação a ser tomada ao implantar um item de projeto cujas propriedades são idênticas às de um item que já está no servidor. Para obter mais informações, consulte [solução de problemas de empacotamento e implantação do SharePoint](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md).|
|Propriedades de recurso|Especifica um conjunto de valores (armazenados como pares de chave/valor) que é incluído com um recurso quando ele é implantado no SharePoint. Depois que o recurso for implantado, você poderá acessar os valores de propriedade em seu código. Para obter mais informações, consulte [fornecendo informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|
|Receptor de recursos|Fornece o código que é executado quando determinados eventos ocorrem para um recurso que contém um item de projeto. Para obter mais informações, consulte [fornecendo informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|
|Nome da Pasta|O nome da pasta do item de projeto do SharePoint.|
|Referências de saída do projeto|Especifica uma dependência, como um assembly, que seu item de projeto precisa executar. Para obter mais informações, consulte [fornecendo informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|
|Entradas de controle seguro|Especifica os controles que são seguros para usuários não confiáveis editarem. Para obter mais informações, consulte [fornecendo informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md).|

### <a name="project-item-file-properties"></a>Propriedades do arquivo de item do projeto

|Nome da propriedade|Descrição|
|-------------------|-----------------|
|Criar ação|Especifica como o arquivo está relacionado aos processos de compilação e implantação. Para obter mais informações, consulte [Propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|
|Copiar para o diretório de saída|Especifica se os arquivos de origem serão copiados para o diretório de saída. Pode ser um dos seguintes valores:<br /><br /> -   *Não copiar*<br />-   *Copiar sempre*<br />-   *Copiar se mais recente*<br /><br /> Para obter mais informações, consulte [Propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|
|Ferramenta personalizada|Especifica o nome de uma ferramenta, se houver, que transforma o arquivo em tempo de design e coloca a saída da transformação em outro arquivo. Por exemplo, um arquivo de conjunto de um (. [!INCLUDE[TLA2#tla_xsd](../sharepoint/includes/tla2sharptla-xsd-md.md)] ) tem uma ferramenta personalizada padrão. Para obter mais informações, consulte [Propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|
|Namespace de ferramenta personalizada|O namespace no qual a saída da ferramenta personalizada é copiada. Para obter mais informações, consulte [Propriedades do arquivo](/previous-versions/visualstudio/visual-studio-2010/0c6xyb66\(v\=vs.100\)).|
|Local da implantação|O caminho totalmente qualificado do arquivo no servidor do SharePoint. Esse caminho é composto pelas subpropriedades raiz de implantação e caminho de implantação.|
|Caminho de implantação|O caminho relativo do arquivo no arquivo do SharePoint Server, como Workflow1 \\ . O caminho totalmente qualificado para o arquivo é criado concatenando o valor do *caminho de implantação* no final do valor *raiz da implantação* .<br /><br /> A seleção de um valor de *RootFile* para a propriedade de *tipo de implantação* altera a propriedade *raiz de implantação* para \<SharePointRoot> \\ , resultando em um caminho totalmente qualificado de \<SharePointRoot> \Workflow1 \\ . Para obter mais informações, consulte [empacotando e implantando soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md).|
|Raiz da implantação|Cadeia de caracteres. A pasta raiz onde o arquivo é implantado no servidor do SharePoint. Por exemplo, \<SharePointRoot> \Template\Features \\ \<FeatureName> \\ .<br /><br /> O valor da propriedade *raiz da implantação* é determinado pela configuração do *tipo de implantação* .|
|Tipo de implantação|O tipo de implantação do arquivo, que determina seu valor de *raiz de implantação* . Pode ser um dos seguintes valores:<br /><br /> NoDeployment:*\<no value>*<br /><br /> ElementManifest: * \<SharePointRoot> \Template\Features \\ \<FeatureName> *\\<br /><br /> Elementofile: * \<SharePointRoot> \Template\Features \\ \<FeatureName> \\ *<br /><br /> Modelo: * \<SharePointRoot> \Template \\ *<br /><br /> RootFile*\<SharePointRoot>\\*<br /><br /> GlobalResource: * \<SharePointRoot> \Resources \\ *<br /><br /> ClassResource:*\<ClassResourcePath>\\*<br /><br /> Para obter mais informações, consulte <xref:Microsoft.VisualStudio.SharePoint.DeploymentType>.|
|Nome do Arquivo|O nome do arquivo ou da pasta do arquivo de item.|
|Caminho completo|O local do arquivo para o item. (Somente leitura.)|

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[SharePoint Modelos de projeto e de item de projeto](../sharepoint/sharepoint-project-and-project-item-templates.md)|Descreve o projeto do SharePoint e os modelos de item de projeto disponíveis no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .|
|[Como adicionar itens a um Projeto do SharePoint](../sharepoint/how-to-add-items-to-a-sharepoint-project.md)|Descreve como adicionar itens novos ou existentes a um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.|
|[Walkthrough: criar uma coluna de site, um tipo de conteúdo e uma lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)|O leva você passo a passo na criação de um campo de cliente, tipo de conteúdo, definição de lista e instância de lista.|
|[Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)|Descreve como adicionar um receptor de eventos para o projeto criado em [passo a passos: criar uma coluna de site, tipo de conteúdo e lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md).|
|[Criar soluções de fluxo de trabalho do SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)|Descreve como criar projetos de fluxo de trabalho que incluem formulários de associação de fluxo de trabalho e formulários de inicialização de fluxo de trabalho.|
|[Criar páginas para o SharePoint](../sharepoint/creating-pages-for-sharepoint.md)|Descreve como você pode criar páginas como páginas de aplicativo, páginas de site, páginas mestras e layouts de página para o SharePoint.|
|[Criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md)|Descreve como adicionar controles que permitem que os usuários modifiquem diretamente o conteúdo, a aparência e o comportamento das páginas do site do SharePoint usando um navegador.|
|[Criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)|Descreve como criar controles de usuário que podem ser consumidos por páginas de aplicativo e Web Parts que são executados no SharePoint.|
|[Integre dados corporativos ao SharePoint](../sharepoint/integrating-business-data-into-sharepoint.md)|Descreve como integrar dados de serviços Web e aplicativos de servidor back-end em um aplicativo do SharePoint.|
|[Criar definições de site para o SharePoint](../sharepoint/creating-site-definitions-for-sharepoint.md)|Descreve como criar definições de site: modelos que são usados para criar sites do SharePoint.|
|[Importando itens de um local do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)|Descreve como importar itens como tipos de conteúdo e módulos de um site do SharePoint existente para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.|
|[Usando módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md)|Descreve como usar módulos para implantar arquivos do seu [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto no site do SharePoint.|
|[Procurar conexões do SharePoint usando Gerenciador de Servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)|Descreve como procurar sites locais do SharePoint usando Gerenciador de Servidores.|
|[Fornecer informações de empacotamento e implantação em itens de projeto](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)|Descreve como usar as propriedades do item de projeto para fornecer informações de empacotamento e implantação para projetos, como entradas de controle seguro, referências de saída de projeto e propriedades de recurso.|
|[Como: Adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md)|Descreve como as pastas mapeadas podem ser adicionadas ao seu projeto para fornecer acesso mais fácil aos recursos do SharePoint.|
|[Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md)|Descreve os problemas associados a soluções em área restrita.|
|[Segurança das soluções do SharePoint](../sharepoint/security-for-sharepoint-solutions.md)|Descreve as considerações de segurança para o desenvolvimento de soluções do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .|
|[Caixa de diálogo Seletor de URL &#40;desenvolvimento do SharePoint no Visual Studio&#41;](../sharepoint/url-picker-dialog-box-sharepoint-development-in-visual-studio.md)|Descreve uma caixa de diálogo que você pode usar para adicionar referências de caminho a recursos em seu projeto ou no servidor do SharePoint local.|

## <a name="see-also"></a>Consulte também
- [Introdução &#40;desenvolvimento do SharePoint no Visual Studio&#41;](../sharepoint/getting-started-sharepoint-development-in-visual-studio.md)
- [Procurar conexões do SharePoint usando Gerenciador de Servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
