---
title: Criando Web Parts para SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
f1_keywords:
- Microsoft.SharePoint.WebControls.DateTimeControl
- Microsoft.SharePoint.WebControls.CssLink
- Microsoft.SharePoint.WebControls.RssLink
- Microsoft.SharePoint.WebControls.Theme
- Microsoft.SharePoint.WebControls.AspMenu
- Microsoft.SharePoint.WebControls.ListProperty
- Microsoft.SharePoint.WebControls.ProjectProperty
- Microsoft.SharePoint.WebControls.FormsDigest
- Microsoft.SharePoint.WebControls.ScriptLink
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web Parts
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3825ef7d2c1c90f63a90f5028063c74332543841
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015048"
---
# <a name="create-web-parts-for-sharepoint"></a>Criar Web Parts para SharePoint
  Usando Web Parts, você pode modificar o conteúdo, a aparência e o comportamento de páginas de um site do SharePoint usando um navegador. As Web Parts são controles do lado do servidor que são executados dentro de uma página de Web Part: são os blocos de construção de páginas que aparecem em um site do SharePoint. Consulte [bloco de construção: Web Parts](/previous-versions/office/developer/sharepoint-2010/ee535520(v=office.14)).

 Você pode criar e depurar Web Parts em um site do SharePoint usando modelos do Visual Studio.

## <a name="create-a-web-part-in-visual-studio"></a>Criar uma Web Part no Visual Studio
 Crie uma Web Part adicionando um item de **Web Part** a qualquer projeto do SharePoint. Você pode usar um item de **Web Part** em uma solução em área restrita ou em uma solução de farm.

 Se você quiser criar uma Web Part visualmente usando um designer, crie um projeto de **Web Part Visual** ou adicione um item de **Web Part Visual** a qualquer projeto do SharePoint. Você pode usar um item de **Web Part Visual** somente em uma solução de farm.

### <a name="web-part-item"></a>Item de Web Part
 Um item de **Web Part** fornece arquivos que você pode usar para criar uma Web Part para um site do SharePoint. Quando você adiciona um item de **Web Part** , o Visual Studio cria uma pasta em seu projeto e, em seguida, adiciona vários arquivos à pasta. A tabela a seguir descreve cada arquivo.

|Arquivo|Descrição|
|----------|-----------------|
|*Elements.xml*|Contém informações que o arquivo de definição de recurso em seu projeto usa para implantar a Web Part.|
|arquivo. WebPart|Fornece informações que o SharePoint precisa para exibir sua Web Part em uma galeria de Web Parts.|
|Arquivo de código|Contém métodos que adicionam controles à Web Part e que geram conteúdo personalizado dentro da Web Part.|

 Para obter mais informações, consulte [como: criar uma Web Part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md).

### <a name="visual-web-part-item"></a>Item de Web Part Visual
 Uma Web Part Visual é uma Web Part que você cria usando o Visual Web Developer designer no Visual Studio. Uma Web Part Visual funciona da mesma forma que qualquer outra Web Part. Para adicionar controles, como botões e caixas de texto, a uma Web Part, você adiciona código a um arquivo XML. No entanto, você adiciona controles a uma Web Part Visual arrastando-os ou copiando-os para a Web Part da **caixa de ferramentas**do Visual Studio. Em seguida, o designer gera o código necessário no arquivo XML. Consulte [como: criar uma Web Part do SharePoint usando um designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md).

## <a name="sharepoint-controls"></a>Controles do SharePoint
 O Visual Studio fornece alguns controles para criar páginas do SharePoint, como páginas de aplicativo. Esses controles aparecem na **caixa de ferramentas** em **controles do SharePoint**. A funcionalidade para esses controles deriva do namespace [Microsoft. SharePoint. WebControls](/previous-versions/office/sharepoint-server/ms413880(v=office.15)) , que contém os controles de servidor ASP.NET que são usados nas páginas de site e de lista do SharePoint.

|Nome do controle|Descrição|
|------------------|-----------------|
|[AspMenu](/previous-versions/office/sharepoint-server/ms454108(v=office.15))|Insere um menu ASP. Para obter mais informações, consulte [visão geral do controle de menu](/previous-versions/ecs0x9w5(v=vs.140)).|
|[CssLink](/previous-versions/office/sharepoint-server/ms439048(v=office.15))|Insere um elemento **link** na página *. aspx* e aplica uma ou mais folhas de estilo externas definidas por **CssRegistration**.|
|[DateTimeControl](/previous-versions/office/sharepoint-server/ms414993(v=office.15))|Insere um controle DateTime na página *. aspx* .|
|[FormDigest](/previous-versions/office/sharepoint-server/ms416616(v=office.15))|Insere uma validação de segurança na página *. aspx*|
|[Lista de](/previous-versions/office/sharepoint-server/ms455032(v=office.15))|Retorna uma propriedade de uma lista especificada.|
|[ProjectProperty](/previous-versions/office/sharepoint-server/ms478990(v=office.15))|Retorna uma propriedade global do site atual.|
|[RssLink](/previous-versions/office/sharepoint-server/ms457574(v=office.15))|Insere um link para um RSS feed na página *. aspx* .|
|[ScriptLink](/previous-versions/office/sharepoint-server/ms411959(v=office.15))|Fornece propriedades e métodos para registrar recursos, como scripts, em uma página para que eles possam ser solicitados quando a página é renderizada.|
|[Tema](/previous-versions/office/sharepoint-server/ms460735(v=office.15))|Aplica um tema à página *. aspx* .|

## <a name="debug-a-web-part"></a>Depurar uma Web Part
 Você pode depurar um projeto do SharePoint que contém uma Web Part da mesma forma que depuraria outros projetos do Visual Studio. Quando você inicia o depurador do Visual Studio, o Visual Studio abre o site do SharePoint.

 Para começar a depurar seu código, adicione a Web Part a uma página de Web Part no SharePoint.

 Para obter mais informações sobre como depurar projetos do SharePoint, consulte [solução de problemas de soluções do SharePoint](../sharepoint/troubleshooting-sharepoint-solutions.md).

## <a name="visual-web-part-limitations"></a>Limitações da Web Part Visual
 A partir do Visual Studio, você pode adicionar Web Parts visuais para soluções do SharePoint em área restrita e soluções de farm. No entanto, as Web Parts visuais têm as seguintes limitações:

- Web Parts visuais não dão suporte a parâmetros substituíveis. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).

- Os controles de usuário ou Web Parts visuais não podem ser arrastados e descartados ou copiados em Web Parts visuais. Essa ação causa um erro de compilação.

- As Web Parts visuais não oferecem suporte direto a tokens do SharePoint Server, como $SPUrl. Para obter mais informações, consulte "restrições de token no Visual de área restrita Web Parts" no tópico [solucionar problemas de soluções do SharePoint](../sharepoint/troubleshooting-sharepoint-solutions.md).

- As Web Parts visuais em uma solução em área restrita eventualmente recebem o erro "a solicitação de execução de código em área restrita foi recusada porque o serviço de host de código em área restrita estava muito ocupado para lidar com a solicitação". Para obter mais informações sobre esse erro, consulte esta postagem no [blog da equipe de desenvolvedores do SharePoint](https://blogs.msdn.microsoft.com/sharepointdev/2011/02/08/error-the-sandboxed-code-execution-request-was-refused-because-the-sandboxed-code-host-service-was-too-busy-to-handle-the-request-ricky-kirkham/#10149157).

- A depuração de JavaScript do lado do servidor não tem suporte no Visual Studio, mas há suporte para a depuração de JavaScript do lado do cliente.

   Embora você possa adicionar JavaScript embutido a um arquivo de marcação do lado do servidor, a depuração não tem suporte para pontos de interrupção adicionados à marcação. Para depurar o JavaScript, faça referência a um arquivo JavaScript externo no arquivo de marcação e, em seguida, defina os pontos de interrupção no arquivo JavaScript.

- A depuração de [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] código embutido deve ser feita no arquivo de código gerado em vez de no arquivo de marcação.

- Web Parts visuais não dão suporte ao uso da `<@ Assembly Src=` diretiva.

- Não há suporte para controles da Web do SharePoint e alguns [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] controles no ambiente de área restrita do SharePoint. Se controles sem suporte forem usados em uma Web Part Visual em uma solução de área restrita, o erro "o tipo ou o nome do namespace ' Theme ' não existirá no namespace ' Microsoft. SharePoint. WebControls '" será exibido.

  Para obter mais informações sobre soluções em área restrita, consulte [diferenças entre as soluções de área restrita e de farm](../sharepoint/differences-between-sandboxed-and-farm-solutions.md).

## <a name="create-older-style-sharepoint-based-web-parts"></a>Criar Web Parts baseadas no SharePoint com estilo antigo
 Você pode usar os modelos no Visual Studio para criar [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] Web Parts personalizadas para o SharePoint. [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)]as Web Parts são criadas sobre a [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] infraestrutura da Web Part e são o tipo recomendado para novos projetos.

 Em poucos casos, talvez seja necessário criar uma Web Part usando a Web Part com estilo mais antigo do SharePoint. Você pode usar o Visual Studio para criar esses tipos de Web Parts, mas o Visual Studio não fornece modelos projetados especificamente para ajudá-lo a criá-los.

 Para obter mais informações sobre quando você pode querer criar uma Web Part baseada no SharePoint com estilo antigo, consulte [infraestrutura de Web Part no Windows SharePoint Services](/previous-versions/office/developer/sharepoint-2010/ms415560(v=office.14)). Para obter mais informações sobre como criar uma Web Part usando o estilo antigo da Web Part baseada no SharePoint, consulte [passo a passos criando uma Web Part básica do SharePoint](/previous-versions/office/ms452873(v=office.14)).

## <a name="related-topics"></a>Tópicos relacionados

|Title|Descrição|
|-----------|-----------------|
|[Como: criar uma Web Part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md)|Mostra como criar Web Parts para páginas do SharePoint.|
|[Como: criar uma Web Part do SharePoint usando um designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)|Mostra como criar Web Parts para o SharePoint usando uma superfície de Design Visual.|
|[Como: criar um controle de usuário para uma página de aplicativo do SharePoint ou Web Part](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|Mostra como criar controles personalizados e reutilizáveis que podem ser consumidos por páginas de aplicativo e Web Parts que são executados no SharePoint.|
|[Walkthrough: criar uma Web Part para o SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)|Descreve como criar uma Web Part para o SharePoint.|
|[Walkthrough: criar uma Web Part para o SharePoint usando um designer](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)|Descreve como criar uma Web Part para o SharePoint arrastando controles para uma superfície de Design Visual.|
|[Walkthrough: criar Web Part do Silverlight que exibe o OData para SharePoint](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)|Descreve como criar uma Web Part para o SharePoint que hospeda um aplicativo do Silverlight e exibe dados de listas do SharePoint.|
