---
title: Importando itens de um Site existente do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.WSPImport.SelectionDependency
- VS.SharepointTools.WSPImport.SpecifyProjectSource
- VS.SharePointTools.WSPImport.SelectionItemsToImport
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- SharePoint development in Visual Studio, importing .wsp files
- importing items [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 7435d6c7ad210554031994f4a366812f9799ffb2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832091"
---
# <a name="import-items-from-an-existing-sharepoint-site"></a>Importar itens de um site do SharePoint existente
  O modelo de projeto Importar pacote de solução do SharePoint permite a reutilização elementos como tipos de conteúdo e campos de sites do SharePoint existentes em uma nova [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] solução do SharePoint. Embora seja possível executar a maioria das soluções importadas sem modificação, há certas restrições e problemas a serem considerados, especialmente se você modificar todos os itens após importá-los.  
  
> [!NOTE]  
>  Para importar fluxos de trabalho reutilizáveis, use o modelo de projeto importar fluxo de trabalho reutilizável. [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)] [Diretrizes para importar fluxos de trabalho reutilizáveis](../sharepoint/guidelines-for-importing-reusable-workflows.md).  
  
## <a name="supported-sharepoint-solutions"></a>Soluções do SharePoint com suporte
 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] totalmente compatível com a importação de soluções criadas no [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] e [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)].  
  
 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] não oferece suporte à importação de soluções criadas nos seguintes aplicativos:  
  
- [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)]  
  
- [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)]  
  
- [!INCLUDE[vs_orcas_long](../sharepoint/includes/vs-orcas-long-md.md)]  
  
- Microsoft SharePoint Designer 2007  
  
- [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)]  
  
  Embora muitas vezes com êxito, você pode importar soluções criadas por esses aplicativos, essa funcionalidade não testada e não tem suporte.  
  
## <a name="item-import-restrictions"></a>Restrições de importação de item
 Embora a maioria dos itens do SharePoint podem ser importados de uma já existente *. wsp* arquivo, os itens a seguir não têm suporte e podem exigir modificações para funcionar corretamente:  
  
- Entidades de BDC  
  
- Elementos de associação de fluxo de trabalho de código  
  
- Fluxos de trabalho de código  
  
- Web parts visuais (. ascx)  
  
- Serviços Web (*asmx*)  
  
- Associações de tipo de conteúdo  
  
- Receptores de evento  
  
- Definições de lista (modelos)  
  
- Definições de site  
  
  Quando você exportar uma solução a partir [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)], esses itens são excluídos automaticamente das *. wsp* arquivo. No entanto, outras *. wsp* gerados a partir de ferramentas sem suporte de arquivos podem conter esses itens. (Consulte "Suporte para soluções do SharePoint" neste tópico.)  
  
## <a name="what-happens-when-you-import-a-solution"></a>O que acontece quando você importa uma solução
 Quando você importa uma solução com o modelo de Import SharePoint Solution Package [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] copia todo o conteúdo do *. wsp* importados do arquivo e tentar reconciliar e manter o maior número de associações e referências entre elementos e seus arquivos quanto possível.  
  
 Copiar de todos os itens importados para pastas correspondentes em **Gerenciador de soluções**. Por exemplo, tipos de conteúdo são exibidos na pasta **tipos de conteúdo** e instâncias de lista aparecem sob **listar instâncias**. Arquivos associados a um item importado também são copiados para a pasta do item. Por exemplo, uma instância de lista importada inclui módulos, formulários e páginas ASPX.  
  
### <a name="dependent-items"></a>Itens dependentes
 Se você selecionar um item no Assistente Importar pacote de solução do SharePoint, mas não seus itens dependentes, uma caixa de mensagem informa que os itens dependentes também devem ser selecionados antes da importação.  
  
### <a name="what-are-features"></a>Quais são os recursos?
 Os usuários do SharePoint Designer podem ver arquivos inesperados, chamados *recursos*, são exibidos em suas soluções importadas em **Gerenciador de soluções.** Embora os recursos existiam na solução do SharePoint Designer, eles estavam ocultas na exibição. Recursos agora são visíveis no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
 Recursos são contêineres para itens do SharePoint. Cada recurso mantém uma referência para cada item, como tipos de conteúdo e definições de lista, o que ele contém. Quando você importar sua solução, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] configura recursos para todos os elementos importados e tenta manter as relações de elemento de recurso para os arquivos. Todos os arquivos cujas referências não puderam ser resolvidas são colocados na **outros arquivos importados** pasta.  
  
 Para obter mais informações sobre recursos, consulte [soluções do SharePoint desenvolver](../sharepoint/developing-sharepoint-solutions.md) e [trabalhando com recursos](http://go.microsoft.com/fwlink/?LinkID=147704).  
  
### <a name="handle-special-cases"></a>Lidar com casos especiais
 Em alguns casos, o Visual Studio não é possível reconciliar um item com seus arquivos dependentes. Os arquivos que [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] não foi possível resolver aparecem sob a pasta **outros arquivos importados**. Além disso, seus **DeploymentType** propriedades são definidas como **NoDeployment** para que eles não são implantados com a solução.  
  
 Por exemplo, se você importar a definição de lista ExpenseForms, uma definição de lista com esse nome aparece sob o **definições de listas** pasta no **Gerenciador de soluções** juntamente com seu  *Elements. XML* e *Schema. XML* arquivos. No entanto, seus formulários ASPX e HTML associados podem ser colocados em uma pasta chamada **ExpenseForms** sob o **outros arquivos importados** pasta. Para concluir a importação, mova esses arquivos sob a definição de lista no ExpenseForms **Gerenciador de soluções** e altere o **DeploymentType** propriedade para cada arquivo de **NoDeployment** ao **ElementFile**.  
  
 Durante a importação de receptores de evento, o *Elements. XML* arquivo é copiado para o local correto, mas você deverá incluir manualmente o assembly no pacote de solução para que ele seja implantado com a solução. [!INCLUDE[crabout](../sharepoint/includes/crabout-md.md)] como fazer isso, consulte [como: adicionar e remover assemblies adicionais](../sharepoint/how-to-add-and-remove-additional-assemblies.md).  
  
 Ao importar fluxos de trabalho, formulários do InfoPath são copiados para o **outros arquivos importados** pasta. Se o *. wsp* arquivo contém um modelo da Web, ele será definido como a página de inicialização na **Gerenciador de soluções**.  
  
## <a name="import-fields-and-property-bags"></a>Os recipientes de propriedades e campos de importação
 Quando você importa uma solução que tem vários campos, todas as definições de campo separados são mescladas em um único *Elements. XML* arquivo sob um nó no **Gerenciador de soluções** chamado **campos** . Da mesma forma, todas as entradas de recipiente de propriedade são mescladas em um *Elements. XML* arquivo em um nó chamado **PropertyBags**.  
  
 Campos no SharePoint são colunas de um tipo de dados especificado, como um texto, booliano ou pesquisa. Para obter mais informações, consulte [bloco de construção: colunas e tipos de campo](http://go.microsoft.com/fwlink/?LinkId=182304). Recipientes de propriedade permitem adicionar propriedades aos objetos no SharePoint, tudo de um farm em uma lista em um site do SharePoint. Os recipientes de propriedades são implementados como uma tabela de hash de valores e nomes de propriedade. Para obter mais informações, consulte [gerenciamento de configuração do SharePoint](http://go.microsoft.com/fwlink/?LinkId=182296) ou [configurações de recipiente de propriedades do SharePoint](http://go.microsoft.com/fwlink/?LinkId=182297).  
  
## <a name="delete-items-in-the-project"></a>Excluir itens no projeto
 A maioria dos itens em soluções do SharePoint tem um ou mais itens dependentes. Por exemplo, instâncias de lista dependem de tipos de conteúdo e tipos de conteúdo dependem de campos. Depois de importar uma solução do SharePoint, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] não notifica você de quaisquer problemas de referência se você excluir um item na solução, mas não seus itens dependentes, até você tentar implantar a solução. Por exemplo, se uma solução importada tiver uma instância de lista que depende de um tipo de conteúdo e excluir o tipo de conteúdo, um erro pode ocorrer na implantação. O erro ocorre se o item dependente não está presente no servidor do SharePoint. Da mesma forma, se um item excluído também tiver um conjunto de propriedades relacionadas, em seguida, exclua essas entradas de recipiente da propriedade do **PropertyBags** *Elements. XML* arquivo. Portanto, se você excluir todos os itens de uma solução importada e você obtiver erros de implantação, verifique se todos os itens dependentes precisam também ser excluídas.  
  
## <a name="restore-missing-feature-attributes"></a>Restaurar os atributos de recurso ausentes
 Ao importar soluções, alguns atributos do recurso opcional são omitidos do manifesto de recurso importada. Se você desejar restaurar esses atributos no novo arquivo de recurso, identificar os atributos ausentes, comparando o arquivo de recurso original para o novo manifesto de recurso e siga as instruções no tópico [como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md).  
  
## <a name="deployment-conflict-detection-is-not-performed-on-built-in-list-instances"></a>Detecção de conflitos de implantação não será executada em instâncias de lista internas
 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] não executar a detecção de conflitos de implantação em instâncias de lista interna (ou seja, lista instâncias padrão que vêm com o SharePoint). Não executar a detecção de conflito é feito para evitar sobrescrever as instâncias de lista interno no SharePoint. A lista interna instâncias ainda são implantados ou atualizados, mas é nunca excluída ou substituída. [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)] [Solucionar problemas de implantação e empacotamento do SharePoint](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md).  
  
## <a name="import-sharepoint-server-2010-workflows"></a>Importar fluxos de trabalho do SharePoint Server 2010
 Se você importar um fluxo de trabalho criado no [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)], ele não será executado corretamente após a implantação. O fluxo de trabalho não é executado corretamente porque faltam determinados assemblies e [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] fluxos de trabalho contêm os formulários do InfoPath que atualmente não têm suporte no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] soluções de fluxo de trabalho. No entanto, importados [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] fluxos de trabalho podem ser feitos para funcionar corretamente depois de corrigir alguns itens, como a adição de referências para o [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] assemblies e reconectar-se os formulários do InfoPath. [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)] [Importando fluxos de trabalho do SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=182226).  
  
## <a name="item-name-character-limit"></a>Limite de caracteres de nome do item
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] tem um limite de 260 caracteres total para o projeto e nomes de item de projeto, incluindo o caminho. Ao importar uma solução, se um nome de item exceder esse limite, você obterá o erro:  
  
 **O caminho especificado, o nome do arquivo ou ambos são muito longos. O nome de arquivo totalmente qualificado deve ter menos de 260 caracteres e o nome do diretório, menos de 248 caracteres.**  
  
 Quando você receber esse erro, o item não é criado. Esse problema geralmente ocorre com os módulos importados. Para evitar esse problema, faça o seguinte:  
  
-   Use nomes curtos para seu projeto quando você inseri-los a **adicionar novo projeto** caixa de diálogo.  
  
-   Crie o projeto em um local como próximo a pasta raiz quanto possível, para encurtar o caminho.  
  
## <a name="the-sharepointproductversion-attribute"></a>O atributo SharePointProductVersion
 Se você importar uma solução criada em uma versão anterior do SharePoint, como [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] ou [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)], altere o valor do atributo SharePointProductVersion no manifesto do pacote para a versão 12.0, ou inserir um controle de Gerenciador de script em todos os Web importada páginas e deixe SharePointProductVersion definido como 14.0. Caso contrário, Web forms importados não exibirá no SharePoint.  
  
### <a name="background"></a>Informações preliminares  
 Soluções no [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] e [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] incluem um atributo chamado SharePointProductVersion. O SharePoint usa esse atributo em seus manifestos de pacote para determinar a versão do SharePoint, a solução foi projetada para. Os dois valores válidos são 12.0 e 14.0. Um valor de 12.0 indica se o item foi projetado para [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] ou [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)]; um valor de 14.0 indica se o item foi projetado para [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)].  
  
 Para aumentar a segurança durante a renderização de páginas do ASPX [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] e [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] exigem que todos os ASPX ou páginas mestras contenham um controle do Gerenciador de script. Para obter mais informações sobre o Gerenciador de script, consulte [visão geral do controle ScriptManager](http://go.microsoft.com/fwlink/?LinkID=169399). Porque o controle do Gerenciador de script não estava disponível no [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] e [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)], um deve ser adicionado a qualquer [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] ou [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] página é atualizada para o [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]. Páginas ASPX que usem uma página mestra padrão não exigem um controle do Gerenciador de script porque um já foi adicionado à página mestra padrão. No entanto, as páginas ASPX que não use uma página mestra ou que usam uma página mestra personalizada devem adicionar um controle de script para funcionar [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)].  
  
 A ausência de um controle do Gerenciador de script pode ser um problema quando você importa uma [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] ou [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] projetar em [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)], porque o atributo SharePointProductVersion de todos os novos projetos é definido como 14.0. Se você implantar um projeto atualizado que tem um formulário da Web sem um Gerenciador de script, o formulário não será exibido no SharePoint.  
  
## <a name="see-also"></a>Consulte também
 [Passo a passo: Importar itens de um site do SharePoint existente](../sharepoint/walkthrough-import-items-from-an-existing-sharepoint-site.md)   
 [Diretrizes para importar fluxos de trabalho reutilizáveis](../sharepoint/guidelines-for-importing-reusable-workflows.md)   
 [Passo a passo: Importar um fluxo de trabalho reutilizável do SharePoint Designer no Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)   
 [Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)  
