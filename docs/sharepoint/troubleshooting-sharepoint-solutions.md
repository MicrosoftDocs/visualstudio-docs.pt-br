---
title: Solução de problemas de soluções do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Tools.SharePoint.Errors.Debugging
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, troubleshooting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f68f6e50be569df6130f7e6c6f3aa4bc7c107214
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296041"
---
# <a name="troubleshoot-sharepoint-solutions"></a>Solucionar problemas de soluções do SharePoint
  Os seguintes problemas ou alertas que podem ocorrer quando você depura soluções do SharePoint usando o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depurador. Para obter mais informações, consulte [depuração de soluções de fluxo de trabalho do SharePoint 2007](https://msdn.microsoft.com/3a5392f3-66f3-48be-956e-02de23fa6247).
  
## <a name="token-restrictions-in-sandboxed-visual-web-parts"></a>Restrições de token em área restrita e web parts visuais
 Web part Visual em soluções em área restrita não é possível processar tokens padrão, como $SPUrl, que dá suporte ao tempo de execução do SharePoint. Como resultado, a URL não é resolvida, e você não é possível visualizar o conteúdo no modo de exibição de Design no designer visual web part se você fizer referência a ele diretamente em um elemento de script, como no exemplo a seguir:  
  
```xml  
<script src="<% $SPUrl:~site/SiteAssets/ListOperations.js %>"></script>  
```  
  
 Para contornar essa limitação e resolver o token, fazer referência a ele usando literais:  
  
```xml  
<asp:literal ID="Literal1" runat="server" Text="<script src='" />  
<asp:literal ID="Literal2" runat="server" Text="<% $SPUrl:~site/SiteAssets/ListOperations.js %>" />  
<asp:literal ID="Literal3" runat="server" Text="' type='text/javascript' ></script>" />  
```  
  
## <a name="character-restrictions-in-names-of-projects-and-project-items"></a>Restrições de caracteres em nomes de projetos e itens de projeto
 Nomes de projetos e itens de projeto podem conter apenas caracteres válidos em um caminho de implantação no SharePoint 2010. Não há outros caracteres são permitidos.  
  
### <a name="error-message"></a>mensagem de erro
 Mensagem de erro de "Caracteres inválido".  
  
### <a name="resolution"></a>Resolução  
 Para nomes de projetos do SharePoint e itens de projeto, use somente os seguintes caracteres:  
  
- Caracteres ASCII alfanuméricos  
  
- Espaço  
  
- Ponto final (.)  
  
- Vírgula (,)  
  
- Caractere de sublinhado (_)  
  
- Traço (-)  
  
- Barra invertida (\\)  
  
  Quando um projeto é empacotado, uma regra de validação verifica se a propriedade de caminho de implantação para cada arquivo que você está implantando contém apenas esses caracteres válidos.  
  
## <a name="errors-when-creating-custom-fields"></a>Erros ao criar campos personalizados
 No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], campos personalizados são definidos no XML. Erros podem ocorrer se um campo não estiver definido ou referenciado usando um formato específico.  
  
### <a name="error-message"></a>mensagem de erro
 Mensagem de erro de "Caracteres inválidos" no tempo de empacotamento.  
  
### <a name="resolution"></a>Resolução  
 A ID de uma definição de campo deve ser um GUID entre chaves, como mostra o exemplo a seguir:  
  
```xml  
<Field ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"   
    Type="Note"   
    Name="PatientName"   
    DisplayName="Patient Name"   
    Group="A Custom Group">  
</Field>.  
```  
  
 Como mostra o exemplo a seguir, uma referência de campo em um tipo de conteúdo deve ser definida usando o formato de elemento vazio (\<FieldRef / >), não pelo uso de elementos de início/término (\<FieldRef >\</FieldRef >):  
  
```xml  
<FieldRef ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"   
    Name="PatientName"   
    DisplayName="Patient Name"   
    Required="TRUE"/>  
```  
  
 Se o XML de origem para o campo está malformado, não é um arquivo XML válido ou apresenta algum outro problema, o erro "não é possível analisar o arquivo" ocorre.  
  
## <a name="new-non-english-site-definitions-do-not-appear-in-site-creation-page-after-deployment"></a>Novas definições de site diferente do inglês não aparecem na página de criação de site após a implantação
 Depois de criar e implantar uma definição de site, usando uma versão diferente do inglês do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] (ou seja, uma versão com uma localidade [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] diferente de 1033), o **personalizações do SharePoint** guia não aparece no **Seleção de modelo** caixa e o novo modelo de site não aparecer na **novo Site do SharePoint** página.  
  
### <a name="error-message"></a>mensagem de erro
 nenhuma.  
  
### <a name="resolution"></a>Resolução  
 Esse problema ocorre devido a um valor incorreto na **caminho** arquivo, como de propriedade para a configuração de definição de site webtemp *webtemp_SiteDefinitionProject1.xml*. No **caminho** propriedade para o arquivo webtemp, localizado sob a **local de implantação**, altere 1033 para a localidade apropriada [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]. Por exemplo, para usar uma localidade japonês altere o valor para 1041. Para obter mais informações, consulte [IDs de localidade atribuídas pela Microsoft](http://go.microsoft.com/fwlink/?LinkID=165561).  
  
## <a name="error-appears-when-a-workflow-project-is-deployed-on-a-clean-system"></a>Erro aparece quando um projeto de fluxo de trabalho é implantado em um sistema limpo
 Esse problema ocorre se você implantar um projeto de fluxo de trabalho no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] em um sistema limpo. Um sistema limpo é um computador que tenha uma instalação nova do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e SharePoint, mas não há projetos de fluxo de trabalho implantados.  
  
### <a name="error-message"></a>mensagem de erro
 Não é possível encontrar a lista do SharePoint: histórico de fluxo de trabalho.  
  
### <a name="resolution"></a>Resolução  
 Esse erro ocorre devido a uma lista do histórico de fluxo de trabalho ausente. Como o ambiente de desenvolvimento é um sistema limpo, não há fluxos de trabalho são implantados e a lista de histórico de fluxo de trabalho ainda não existir. Para resolver esse problema, abra novamente o Assistente de fluxo de trabalho, o que faz com que a lista de histórico de fluxo de trabalho a ser criado.  
  
##### <a name="to-reenter-the-workflow-wizard"></a>Insira novamente o Assistente de fluxo de trabalho  
  
1.  Na **Gerenciador de soluções**, escolha o nó do fluxo de trabalho.  
  
2.  No **propriedades** janela, escolha o botão de reticências (...) em qualquer propriedade que tem um botão de reticências.  
  
## <a name="user-must-refresh-application-page-in-browser-while-debugging-to-view-updated-image"></a>Usuário deve atualizar a página de aplicativo no navegador durante a depuração para exibir a imagem atualizada
 Se você estiver depurando uma solução do SharePoint que contém uma página de aplicativo com um controle que exibe uma imagem, como um [!INCLUDE[TLA2#tla_html](../sharepoint/includes/tla2sharptla-html-md.md)] controle de imagem, você deve atualizar a página no navegador para exibir todas as alterações foram feitas para a imagem.  
  
## <a name="error-the-site-location-is-not-valid"></a>Erro: O local do site não é válido
 Esse problema pode ocorrer se [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)] não está instalado. Ele também pode ocorrer se você não tiver acesso de administrador para o site do SharePoint que é especificado na **Assistente para personalização do SharePoint**.  
  
### <a name="error-message"></a>mensagem de erro
  
-   Local do site do SharePoint não é válido.  
  
### <a name="resolution"></a>Resolução  
  
-   Instale o [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)].  
  
-   Certifique-se de que você tem acesso de administrador para o site do SharePoint. Para obter mais informações, consulte o [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] artigo Online [atribuir ou remover administradores de aplicativos de serviço no SharePoint Server](https://docs.microsoft.com/sharepoint/administration/assign-or-remove-administrators-of-service-applications).  
  
## <a name="site-deletion-web-event-does-not-occur-in-event-receiver-project"></a>Evento de web de exclusão do site não ocorre no projeto de receptor de evento
 Quando você cria um projeto de receptor de evento e selecionar determinados eventos da Web, como "um site está sendo excluído", ocorre o evento nunca.  
  
### <a name="error-message"></a>mensagem de erro
 nenhuma.  
  
### <a name="resolution"></a>Resolução  
 Esse problema ocorre porque o escopo do recurso deve ser "Site" para manipular eventos de nível de site, mas o escopo do recurso padrão para projetos de receptor de evento é "Web". Os eventos da Web afetados são:  
  
- Um site está sendo excluída (WebDeleting)  
  
- Um site foi excluído (WebDeleted)  
  
- Um site está sendo movido (WebMoving)  
  
- Um site foi movido (WebMoved)  
  
  Para corrigir o problema, altere o escopo do recurso do receptor do evento, da seguinte maneira.  
  
##### <a name="to-change-the-feature-scope-of-the-event-receiver"></a>Para alterar o escopo do recurso do receptor do evento  
  
1.  Na **Gerenciador de soluções**, abra o receptor de evento *Feature* de arquivo no **Designer de recursos** por duas vezes no arquivo ou abrindo o menu de atalho e, em seguida, escolhendo **aberto**.  
  
2.  Escolha a seta ao lado **escopo**e, em seguida, escolha **Site** na lista que aparece.  
  
## <a name="deployment-error-appears-after-the-name-of-an-identifier-in-a-business-data-connectivity-model-project-is-changed"></a>Erro de implantação é exibida depois que o nome de um identificador em um projeto de modelo de conectividade de dados de negócios é alterado
 Esse problema ocorre se você alterar o nome do identificador de uma entidade em um modelo de conectividade de dados comerciais (BDC) e, em seguida, tente implantar a solução.  
  
### <a name="error-messages"></a>Mensagens de erro
  
-   \<*nome do modelo*> tem os seguintes erros de ativação de tipo de conteúdo externo...  
  
-   O IMetadataObject com nome '\<*nome do modelo*>' tem um valor no campo 'name' duplicado...  
  
### <a name="resolution"></a>Resolução  
 Para resolver esse problema, exclua manualmente o modelo e, em seguida, implante a solução novamente.  Você pode excluir o modelo usando qualquer uma das seguintes ferramentas:  
  
-   Administração Central do SharePoint 2010. Para obter mais informações, consulte [gerenciamento de modelos de BDC](http://go.microsoft.com/fwlink/?LinkID=181472) no site da Web do Microsoft TechNet.  
  
-   Windows PowerShell. Você pode excluir o modelo digitando o seguinte comando no prompt de comando: **SPBusinessDataCatalogModel remover**. Para obter mais informações, consulte [geral de cmdlets (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkID=182375) no site da Web do Microsoft TechNet.  
  
## <a name="an-error-appears-when-you-try-to-view-a-visual-web-part-in-sharepoint"></a>Um erro será exibido quando você tenta exibir uma web part visual no SharePoint
 Esse problema ocorre quando o **caminho** propriedade do controle de usuário não começa com a cadeia de caracteres "CONTROLTEMPLATES\\".  
  
### <a name="error-messages"></a>Mensagens de erro
  
-   O arquivo ' /_CONTROLTEMPLATES/*\<nome do projeto >*/*\<nome da Web Part >*/*\<controle de usuário nome >*. ascx ' não existe.  
  
-   Erro de servidor no aplicativo '/'.  
  
### <a name="resolution"></a>Resolução  
  
##### <a name="to-resolve-this-issue"></a>Para resolver esse problema  
  
1.  Na **Gerenciador de soluções**, escolha o arquivo de controle de usuário, cuja extensão de nome de arquivo é *. ascx*.  
  
2.  Na barra de menus, escolha **modo de exibição** > **janela propriedades**.  
  
3.  No **propriedades** janela, expanda o **local de implantação** nó.  
  
4.  Certifique-se de que o valor de **caminho** propriedade começa com a cadeia de caracteres "CONTROLTEMPLATES\\".  
  
## <a name="error-appears-when-an-imported-reusable-workflow-that-contains-a-task-form-field-is-run"></a>Erro aparece quando um fluxo de trabalho importado reutilizável que contém um campo de formulário de tarefa é executado
 Esse problema ocorre se você importar um fluxo de trabalho que contém um formulário de tarefa que tem um campo e, em seguida, execute o novo fluxo de trabalho no mesmo sistema do qual você importou.  
  
### <a name="error-message"></a>mensagem de erro
 Ocorreu um erro na etapa de implantação 'Ativar recursos': O campo com a Id [*Guid*] definido recurso [*Guid*] foi encontrado no conjunto de sites atual ou em um subsite.  
  
### <a name="resolution"></a>Resolução  
 Esse erro é o resultado de colisões de ID de campo que ocorrem porque o projeto de fluxo de trabalho reutilizável de importação no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] não altera o campo de formulário de tarefa IDs. Se você implantar um fluxo de trabalho importado no mesmo servidor que contém o fluxo de trabalho original, ocorrerem conflitos de ID de campo.  
  
 Para resolver esse problema, use o recurso Localizar e substituir para alterar o valor do atributo ID do campo em todos os arquivos de fluxo de trabalho importados.  
  
## <a name="error-appears-when-a-renamed-imported-list-instance-is-run"></a>Erro aparece quando um renomeado importado é executar a instância de lista
 Esse problema ocorre se você renomear uma instância de lista importados e, em seguida, executá-lo em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
### <a name="error-message"></a>mensagem de erro
 Erro de build: Ocorreu um erro na etapa de implantação 'Ativar recursos': O arquivo Template\Features\\[*Importar projeto*<em>recurso</em>*nome*] \Files\Lists \\[*antigo*<em>nome da lista</em>] \Schema.xml não existe.  
  
### <a name="resolution"></a>Resolução  
 Quando você importa uma instância de lista, um atributo chamado CustomSchema é adicionado ao arquivo Elements. XML da instância de lista. Elements. XML inclui o caminho de um Schema. XML personalizado para a instância de lista. Quando você renomeia a instância de lista no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], altera o caminho de implantação para o Schema. XML personalizado, mas o valor do caminho do atributo CustomSchema não é atualizado. Como resultado, a instância de lista não é possível localizar o *Schema. XML* arquivo no caminho antigo que é especificado pelo atributo CustomSchema quando o recurso é ativado.  
  
 Para resolver esse problema, atualize o caminho do local de implantação do *Schema. XML* arquivo no atributo CustomSchema.  
  
## <a name="sharepoint-debugging-session-terminated-by-iis"></a>Encerrado pelo IIS de sessão de depuração do SharePoint
 Esse problema ocorre se você definir um ponto de interrupção em uma [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] solução do SharePoint, escolha o **F5** chave executá-lo e, em seguida, permanecem em um ponto de interrupção mais de 90 segundos.  
  
### <a name="error-message"></a>mensagem de erro
 O processo do servidor Web que estava sendo depurado foi encerrado pelo Internet Information Services (IIS). Você pode evitar esse problema ao configurar as configurações de ping do Pool de aplicativos no IIS. Consulte a Ajuda para obter mais detalhes.  
  
### <a name="resolution"></a>Resolução  
 Por padrão, o pool de aplicativos IIS aguardará 90 segundos para um aplicativo responder antes que ele fecha o aplicativo. Esse processo é conhecido como "ping" o aplicativo. Para resolver esse problema, você pode aumentar o tempo de espera ou desabilitar aplicativo ping inteiramente.  
  
##### <a name="to-access-the-iis-app-pool-settings"></a>Para acessar as configurações de pool do aplicativo IIS  
  
1.  Abra o Gerenciador do IIS.  
  
2.  No **conexões** painel, expanda o nó de servidor do SharePoint e, em seguida, escolha o **Pools de aplicativos** nó.  
  
3.  No **Pools de aplicativos** , escolha o pool de aplicativos do SharePoint (normalmente "SharePoint - 80") e, em seguida, no **ações** painel, escolha o **configurações avançadas** link.  
  
4.  Para aumentar o tempo de espera antes do tempo limite do IIS, altere o valor de **tempo de resposta máximo de Ping (segundos)** para um valor maior que 90 segundos.  
  
5.  Para desabilitar a execução de ping do IIS, defina **Ping habilitado** à **falso**.  
  
## <a name="auto-retract-leaves-orphaned-list-instance-in-sharepoint"></a>Retração automática deixa a instância de lista órfãos no SharePoint
 Esse problema ocorre se você executar as etapas a seguir.  
  
1.  Criar uma definição de lista que tenha uma instância de lista no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Escolha o **F5** chave para executar a solução.  
  
3.  Parar a depuração ou fechar o site do SharePoint.  
  
4.  Abra o site do SharePoint e abra a instância de lista.  
  
### <a name="error-message"></a>mensagem de erro
 Erro de servidor no aplicativo '/'.  
  
### <a name="resolution"></a>Resolução  
 Isso acontece porque, após você fechar uma sessão de depuração de uma solução do SharePoint, a retração automática recurso cancela a solução. O cancelamento exclui a definição de lista do SharePoint, mas não exclui a instância da lista. A definição de lista subjacente é necessária para a instância de lista.  
  
 Para resolver esse problema, implante a solução, na barra de menus, escolhendo **construir** > **implantar**. (Não depurar a solução escolhendo os **F5** chave.) Em seguida, exclua a instância de lista no SharePoint.  
  
## <a name="original-sharepoint-solution-is-replaced-by-an-exported-version"></a>Solução do SharePoint original é substituída por uma versão exportada
 Se você exportar uma solução do SharePoint, importar a solução em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]e, em seguida, implantar a solução de volta para o mesmo site do qual ele foi exportado, a solução do SharePoint original será substituída. Esse problema não ocorre se você implantar a solução em um servidor que não tem a solução original ativada nele.  
  
### <a name="error-message"></a>mensagem de erro
 nenhuma.  
  
### <a name="resolution"></a>Resolução  
 Para evitar a substituição de uma solução no site do qual ele foi exportado, alterar os GUIDs do SolutionID e as IDs de recurso de todos os recursos importados no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto.  
  
## <a name="error-appears-when-debugging-starts"></a>Erro aparece quando a depuração iniciar
 Quando você inicia a depuração de uma solução do SharePoint no Visual Studio, um erro indica que o Visual Studio não foi possível carregar o arquivo Web. config porque não foi determinada chave no dicionário.  
  
### <a name="error-message"></a>mensagem de erro
 Não foi possível carregar o arquivo de configuração Web. config. Verifique o arquivo para elementos XML malformados e tente novamente. Ocorreu o seguinte erro: A chave fornecida não estava presente no dicionário.  
  
### <a name="resolution"></a>Resolução  
 Para resolver esse problema, certifique-se de que o valor da propriedade URL do Site do projeto do SharePoint no Visual Studio corresponde à URL que é atribuído para a região padrão para os mapeamentos alternativos de acesso do aplicativo web. Você não pode resolver o erro usando outra zona, como a Intranet, para a URL. O site de URL para o projeto e a URL na zona padrão devem corresponder. Para acessar os mapeamentos alternativos de acesso, abra o utilitário de Administração Central do SharePoint 2010, escolha o **gerenciamento de aplicativos** link e, em **aplicativos da Web**, escolha o  **Configurar mapeamentos alternativos de acesso** link. Para obter mais informações, consulte [criar zonas para aplicativos Web](http://go.microsoft.com/fwlink/?LinkId=192274).  
  
## <a name="see-also"></a>Consulte também
 [Solucionar problemas de implantação e empacotamento do SharePoint](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)   
 [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)   
 [Depurando no Visual Studio](/visualstudio/debugger/debugging-in-visual-studio)  
  
  
