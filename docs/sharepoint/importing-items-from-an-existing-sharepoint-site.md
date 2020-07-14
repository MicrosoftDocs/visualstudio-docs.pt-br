---
title: Importando itens de um site existente do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- VS.SharePointTools.WSPImport.SelectionDependency
- VS.SharepointTools.WSPImport.SpecifyProjectSource
- VS.SharePointTools.WSPImport.SelectionItemsToImport
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- SharePoint development in Visual Studio, importing .wsp files
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 9c2703bfdd4f47281a1fc19060cb69f8b312e7d2
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017029"
---
# <a name="import-items-from-an-existing-sharepoint-site"></a>Importar itens de um site existente do SharePoint
  O modelo de projeto importar pacote de solução do SharePoint permite reutilizar elementos como tipos de conteúdo e campos de sites existentes do SharePoint em uma nova [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] solução do SharePoint. Embora você possa executar a maioria das soluções importadas sem modificação, há certas restrições e problemas a serem considerados, especialmente se você modificar os itens depois de importá-los.

> [!NOTE]
> Para importar fluxos de trabalho reutilizáveis, use o modelo de projeto importar fluxo de trabalho reutilizável. [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][Diretrizes para importar fluxos de trabalho reutilizáveis](../sharepoint/guidelines-for-importing-reusable-workflows.md).

## <a name="supported-sharepoint-solutions"></a>Soluções do SharePoint com suporte
 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]dá suporte total à importação de soluções criadas no [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] e no [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] .

 [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)]o não oferece suporte à importação de soluções criadas nos seguintes aplicativos:

- [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)]

- [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)]

- [!INCLUDE[vs_orcas_long](../sharepoint/includes/vs-orcas-long-md.md)]

- Microsoft SharePoint Designer 2007

- [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)]

  Embora muitas vezes você possa importar soluções criadas por esses aplicativos com êxito, essa funcionalidade não é testada e não tem suporte.

## <a name="item-import-restrictions"></a>Restrições de importação de item
 Embora a maioria dos itens do SharePoint possa ser importada de um arquivo *. wsp* existente, os itens a seguir não têm suporte e podem exigir modificações para funcionar corretamente:

- Entidades do BDC

- Elementos de associação do fluxo de trabalho de código

- Fluxos de trabalho de código

- Web Parts visuais (. ascx)

- Serviços Web (*. asmx*)

- Associações de tipo de conteúdo

- Receptores de eventos

- Definições de lista (modelos)

- Definições de site

  Quando você exporta uma solução do [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou do [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] , esses itens são excluídos automaticamente do arquivo *. wsp* . No entanto, outros arquivos *. wsp* gerados por meio de ferramentas sem suporte podem conter esses itens. (Consulte "soluções do SharePoint com suporte" anteriormente neste tópico.)

## <a name="what-happens-when-you-import-a-solution"></a>O que acontece quando você importa uma solução
 Quando você importa uma solução com o modelo importar pacote de solução do SharePoint, o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] copia todo o conteúdo do arquivo *. wsp* e tenta reconciliar e reter quantas associações e referências entre elementos importados e seus arquivos forem possíveis.

 Todos os itens importados são copiados para pastas correspondentes no **Gerenciador de soluções**. Por exemplo, os tipos de conteúdo aparecem sob a pasta **tipos de conteúdo** e instâncias de lista aparecem em **instâncias de lista**. Os arquivos associados a um item importado também são copiados para a pasta do item. Por exemplo, uma instância de lista importada inclui seus módulos, formulários e páginas ASPX.

### <a name="dependent-items"></a>Itens dependentes
 Se você selecionar um item no Assistente para importar pacote de solução do SharePoint, mas não seus itens dependentes, uma caixa de mensagem informará que os itens dependentes também devem ser selecionados antes da importação.

### <a name="what-are-features"></a>O que são recursos?
 Os usuários do SharePoint Designer podem ver arquivos inesperados, chamados *recursos*, exibidos em suas soluções importadas no **Gerenciador de soluções.** Embora os recursos existiam na solução do SharePoint Designer, eles estavam ocultos na exibição. Agora, os recursos estão visíveis no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

 Os recursos são contêineres para itens do SharePoint. Cada recurso mantém uma referência a cada item, como tipos de conteúdo e definições de lista, que ele contém. Quando você importa sua solução, o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] configura os recursos para todos os elementos importados e tenta manter as relações entre recursos e elementos para os arquivos. Todos os arquivos cujas referências não puderam ser resolvidas são colocados na pasta **outros arquivos importados** .

 Para obter mais informações sobre recursos, consulte [desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md) e [trabalhar com recursos](/previous-versions/office/developer/sharepoint-2010/ms460318(v=office.14)).

### <a name="handle-special-cases"></a>Lidar com casos especiais
 Em alguns casos, o Visual Studio não pode reconciliar um item com seus arquivos dependentes. Todos os arquivos que [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] não puderam ser resolvidos aparecem na pasta **outros arquivos importados**. Além disso, suas propriedades **DeploymentType** são definidas como **NoDeployment** para que não sejam implantadas com a solução.

 Por exemplo, se você importar a definição de lista ExpenseForms, uma definição de lista com esse nome aparecerá na pasta de **definições de lista** em **Gerenciador de soluções** junto com seus *Elements.xml* e *Schema.xml* arquivos. No entanto, seus formulários ASPX e HTML associados podem ser colocados em uma pasta chamada **ExpenseForms** na pasta **outros arquivos importados** . Para concluir a importação, mova esses arquivos na definição de lista ExpenseForms em **Gerenciador de soluções** e altere a propriedade **DeploymentType** para cada arquivo de **NoDeployment** para **ElementFile**.

 Ao importar receptores de eventos, o arquivo de *Elements.xml* é copiado para o local correto, mas você deve incluir manualmente o assembly no pacote de solução para que ele seja implantado com a solução. [!INCLUDE[crabout](../sharepoint/includes/crabout-md.md)]como fazer isso, consulte [como: Adicionar e remover assemblies adicionais](../sharepoint/how-to-add-and-remove-additional-assemblies.md).

 Ao importar fluxos de trabalho, os formulários do InfoPath são copiados para a pasta **arquivos importados** . Se o arquivo *. wsp* contiver um modelo da Web, ele será definido como a página de inicialização no **Gerenciador de soluções**.

## <a name="import-fields-and-property-bags"></a>Importar campos e pacotes de propriedades
 Quando você importa uma solução que tem vários campos, todas as definições de campo separadas são mescladas em um único arquivo de *Elements.xml* em um nó **Solution Explorer** em Gerenciador de soluções **campos**chamados. Da mesma forma, todas as entradas do recipiente de propriedades são mescladas em um arquivo de *Elements.xml* em um nó chamado **PropertyBags**.

 Os campos no SharePoint são colunas de um tipo de dados especificado, como um texto, booliano ou pesquisa. Para obter mais informações, consulte [bloco de construção: colunas e tipos de campo](/previous-versions/office/developer/sharepoint-2010/ee535893(v=office.14)). Os pacotes de propriedades permitem que você adicione Propriedades a objetos no SharePoint, tudo de um farm a uma lista em um site do SharePoint. Os pacotes de propriedade são implementados como uma tabela de hash de valores e nomes de propriedade. Para obter mais informações, consulte [Gerenciando a configuração do SharePoint](/previous-versions/msp-n-p/ff647766(v=pandp.10)) ou [configurações do recipiente de propriedades do SharePoint](https://archive.codeplex.com/?p=pbs).

## <a name="delete-items-in-the-project"></a>Excluir itens do projeto
 A maioria dos itens em soluções do SharePoint tem um ou mais itens dependentes. Por exemplo, instâncias de lista dependem de tipos de conteúdo e tipos de conteúdo dependem de campos. Depois de importar uma solução do SharePoint, o não o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] notificará sobre problemas de referência se você excluir um item da solução, mas não seus itens dependentes, até tentar implantar a solução. Por exemplo, se uma solução importada tiver uma instância de lista que dependa de um tipo de conteúdo e você excluir esse tipo de conteúdo, poderá ocorrer um erro na implantação. O erro ocorrerá se o item dependente não estiver presente no servidor do SharePoint. Da mesma forma, se um item excluído também tiver um recipiente de propriedades relacionado, exclua as entradas do recipiente de propriedades do arquivo **PropertyBags** *Elements.xml* . Portanto, se você excluir todos os itens de uma solução importada e receber erros de implantação, verifique se os itens dependentes precisam também ser excluídos.

## <a name="restore-missing-feature-attributes"></a>Restaurar atributos de recurso ausentes
 Ao importar soluções, alguns atributos de recurso opcionais são omitidos do manifesto de recurso importado. Se você quiser restaurar esses atributos no novo arquivo de recurso, identifique os atributos ausentes comparando o arquivo de recurso original com o novo manifesto de recurso e siga as instruções no tópico [como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md).

## <a name="deployment-conflict-detection-is-not-performed-on-built-in-list-instances"></a>A detecção de conflito de implantação não é executada em instâncias de lista internas
 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]não executa a detecção de conflito de implantação em instâncias de lista internas (ou seja, instâncias de lista padrão que acompanham o SharePoint). A detecção de conflitos não é feita para evitar a substituição das instâncias de lista internas no SharePoint. As instâncias de lista internas ainda são implantadas ou atualizadas, mas nunca são excluídas ou substituídas. [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][Solucionar problemas de implantação e empacotamento do SharePoint](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md).

## <a name="import-sharepoint-server-2010-workflows"></a>Importar fluxos de trabalho do SharePoint Server 2010
 Se você importar um fluxo de trabalho criado no [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] , ele não será executado corretamente depois que você implantá-lo. O fluxo de trabalho não é executado corretamente porque determinados assemblies estão ausentes e [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] os fluxos de trabalho contêm formulários do InfoPath que não têm suporte no momento em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] soluções de fluxo de trabalho. No entanto, os fluxos de trabalho importados [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] podem ser feitos para funcionar corretamente após a correção de alguns itens, como a adição de referências aos [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] assemblies e a reconexão dos formulários do InfoPath. [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][Importando fluxos de trabalho do SharePoint Server 2010](/sharepoint/dev/).

## <a name="item-name-character-limit"></a>Limite de caracteres do nome do item
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]tem um limite de 260 caracteres no total para nomes de item de projeto e projeto, incluindo o caminho. Ao importar uma solução, se um nome de item exceder esse limite, você receberá o erro:

 **O caminho especificado, o nome do arquivo ou ambos são muito longos. O nome de arquivo totalmente qualificado deve ter menos de 260 caracteres e o nome do diretório deve ter menos de 248 caracteres.**

 Quando você receber esse erro, o item não será criado. Esse problema ocorre com mais frequência com módulos importados. Para evitar esse problema, faça o seguinte:

- Use nomes curtos para seu projeto ao inseri-los na caixa de diálogo **Adicionar novo projeto** .

- Crie o projeto em um local o mais próximo possível da pasta raiz, para reduzir o caminho.

## <a name="the-sharepointproductversion-attribute"></a>O atributo SharePointProductVersion
 Se você importar uma solução criada em uma versão anterior do SharePoint, como [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] ou [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] , altere o valor do atributo SharePointProductVersion no manifesto do pacote para 12,0 ou insira um controle de Gerenciador de script em todas as páginas da Web importadas e deixe SharePointProductVersion definido como 14,0. Caso contrário, os Web Forms importados não serão exibidos no SharePoint.

### <a name="background"></a>Segundo plano
 Soluções no [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] e [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] inclua um atributo chamado SharePointProductVersion. O SharePoint usa esse atributo em seus manifestos de pacote para determinar a versão do SharePoint para a qual a solução foi projetada. Os dois valores válidos são 12,0 e 14,0. Um valor de 12,0 indica que o item foi projetado para [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] ou [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] ; um valor de 14,0 indica que o item foi projetado para [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] .

 Para aumentar a segurança ao renderizar páginas ASPX [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] e [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] exigir que todas as páginas aspx ou mestras contenham um controle Gerenciador de scripts. Para obter mais informações sobre o Gerenciador de scripts, consulte [visão geral do controle ScriptManager](/previous-versions/bb398863(v=vs.140)). Como o controle do Gerenciador de scripts não estava disponível em [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] e [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] , um deve ser adicionado a qualquer [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] página ou que seja atualizada para [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] . As páginas ASPX que usam uma página mestra padrão não exigem um controle de Gerenciador de script porque já existe uma adicionada à página mestra padrão. No entanto, as páginas ASPX que não usam uma página mestra ou que usam uma página mestra personalizada devem adicionar um controle de script para trabalhar no [!INCLUDE[wss_14_short](../sharepoint/includes/wss-14-short-md.md)] ou no [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] .

 A ausência de um controle do Gerenciador de scripts pode ser um problema quando você importa um [!INCLUDE[winshare3](../sharepoint/includes/winshare3-md.md)] projeto do ou do [!INCLUDE[offshare7](../sharepoint/includes/offshare7-md.md)] no [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] , porque o atributo SharePointProductVersion de todos os novos projetos está definido como 14,0. Se você implantar um projeto atualizado que tenha um formulário da Web sem um Gerenciador de scripts, o formulário não será exibido no SharePoint.

## <a name="see-also"></a>Consulte também
- [Walkthrough: importar itens de um site existente do SharePoint](../sharepoint/walkthrough-import-items-from-an-existing-sharepoint-site.md)
- [Diretrizes para importar fluxos de trabalho reutilizáveis](../sharepoint/guidelines-for-importing-reusable-workflows.md)
- [Walkthrough: importar um fluxo de trabalho reutilizável do SharePoint Designer para o Visual Studio](../sharepoint/walkthrough-import-a-sharepoint-designer-reusable-workflow-into-visual-studio.md)
- [Como: adicionar um arquivo de modelo BDC existente a um projeto do SharePoint](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
