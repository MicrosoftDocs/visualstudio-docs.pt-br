---
title: Criando Web Parts do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
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
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, Web Parts
- Web Parts [SharePoint development in Visual Studio], designing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0cbc26a198cace58a957f3d3aaf25457cf457256
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906033"
---
# <a name="create-web-parts-for-sharepoint"></a>Criar web parts para SharePoint
  Usando web parts, você pode modificar o conteúdo, aparência e comportamento de páginas de um site do SharePoint usando um navegador. Web parts são controles de servidor que são executados dentro de uma página de web part: são os blocos de construção de páginas que aparecem em um site do SharePoint. Ver [bloco de construção: Web Parts](http://go.microsoft.com/fwlink/?LinkID=182097).  
  
 Você pode criar e depurar o web parts em um site do SharePoint usando modelos do Visual Studio.  
  
## <a name="create-a-web-part-in-visual-studio"></a>Criar uma web part no Visual Studio
 Criar uma web part, adicionando um **Web Part** item para qualquer projeto do SharePoint. Você pode usar um **Web Part** item em uma solução em área restrita ou uma solução de farm.  
  
 Se você quiser criar uma web part visualmente usando um designer, crie uma **Web Part Visual** do projeto ou adicione **Web Part Visual** item para qualquer projeto do SharePoint. Você pode usar um **Web Part Visual** item em uma solução de farm.  
  
### <a name="web-part-item"></a>Item da Web part
 Um **Web Part** item fornece os arquivos que você pode usar para criar uma web part para um site do SharePoint. Quando você adiciona uma **Web Part** item, o Visual Studio cria uma pasta em seu projeto e, em seguida, adiciona vários arquivos para a pasta. A tabela a seguir descreve cada arquivo.  
  
|Arquivo|Descrição|  
|----------|-----------------|  
|*Elements. XML*|Contém informações que o arquivo de definição de recurso em seu projeto usa para implantar a web part.|  
|arquivo. WebPart|Fornece informações que precisa para exibir sua web part em uma galeria de web parts de SharePoint.|  
|Arquivo de código|Contém métodos que adicionam controles à web part e que geram conteúdo personalizado na web part.|  
  
 Para obter mais informações, consulte [como: criar uma web part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md).  
  
### <a name="visual-web-part-item"></a>Item do Visual web part
 Uma web part visual é uma web part que você cria usando o designer do Visual Web Developer no Visual Studio. Uma web part visual funciona como qualquer outra web part. Para adicionar controles, como botões e caixas de texto, a uma web part, você pode adicionar código para um arquivo XML. No entanto, você adicionar controles a uma web part visual arrastando ou copiando-os para a web part do Visual Studio **caixa de ferramentas**. O designer, em seguida, gera o código necessário no arquivo XML. Ver [como: criar SharePoint web parts usando um designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md).  
  
## <a name="sharepoint-controls"></a>Controles do SharePoint
 Visual Studio fornece alguns controles para a criação de páginas do SharePoint, como páginas de aplicativo. Esses controles aparecem na **caixa de ferramentas** sob **controles do SharePoint**. A funcionalidade desses controles deriva de [WebControls](http://go.microsoft.com/fwlink/?LinkId=235315) namespace, que contém os controles de servidor ASP.NET que são usados nas páginas de site e a lista do SharePoint.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|[AspMenu](http://go.microsoft.com/fwlink/?LinkId=235307)|Insere um menu ASP. Para obter mais informações, consulte [visão geral do controle de Menu](http://go.microsoft.com/fwlink/?LinkId=235316).|  
|[CssLink](http://go.microsoft.com/fwlink/?LinkId=235308)|Insere um **LINK** elemento para o *. aspx* da página e aplica um ou mais folhas de estilos externas definidas pelo **CssRegistration**.|  
|[DateTimeControl](http://go.microsoft.com/fwlink/?LinkId=235306)|Insere um controle de DateTime para o *. aspx* página.|  
|[FormDigest](http://go.microsoft.com/fwlink/?LinkId=235309)|Insere uma validação de segurança para o *. aspx* página|  
|[ListProperty](http://go.microsoft.com/fwlink/?LinkId=235310)|Retorna uma propriedade de uma lista especificada.|  
|[ProjectProperty](http://go.microsoft.com/fwlink/?LinkId=235311)|Retorna uma propriedade global do site da Web atual.|  
|[RssLink](http://go.microsoft.com/fwlink/?LinkId=235312)|Insere um link para um RSS feed para o *. aspx* página.|  
|[ScriptLink](http://go.microsoft.com/fwlink/?LinkId=235313)|Fornece propriedades e métodos para registrar recursos, como scripts, em uma página, de modo que eles possam ser solicitados quando a página é renderizada.|  
|[Tema](http://go.microsoft.com/fwlink/?LinkId=235314)|Aplica um tema para o *. aspx* página.|  
  
## <a name="debug-a-web-part"></a>Depurar uma web part
 Você pode depurar um projeto do SharePoint que contém uma web part exatamente como você faria para depurar outros projetos do Visual Studio. Quando você inicia o depurador do Visual Studio, o Visual Studio abre o site do SharePoint.  
  
 Para começar a depurar seu código, adicione a web part a uma página de web part no SharePoint.  
  
 Para obter mais informações sobre como depurar projetos do SharePoint, consulte [soluções do SharePoint solucionar](../sharepoint/troubleshooting-sharepoint-solutions.md).  
  
## <a name="visual-web-part-limitations"></a>Limitações do Visual web part
 A partir do Visual Studio, você pode adicionar web parts visuais para soluções em área restrita do SharePoint e soluções de farm. No entanto, as web parts visuais têm as seguintes limitações:  
  
- Web parts visuais não dão suporte a parâmetros substituíveis. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).  
  
- Controles de usuário ou partes visuais da web não podem ser arrastados e descartados ou copiados para a web part visual. Essa ação faz com que um erro de compilação.  
  
- Web parts visuais diretamente não dão suporte a tokens de servidor do SharePoint como $SPUrl. Para obter mais informações, consulte "Token restrições em área restrita e Web Parts visuais" no tópico [soluções do SharePoint solucionar](../sharepoint/troubleshooting-sharepoint-solutions.md).  
  
- Web part Visual em uma solução em área restrita, ocasionalmente, obter o erro, "a solicitação de execução de código em modo seguro foi recusada porque o serviço de Host do código em área restrita estava muito ocupado para tratar a solicitação". Para obter mais informações sobre esse erro, consulte esta postagem na [blog da equipe do SharePoint Developer](http://go.microsoft.com/fwlink/?LinkId=225932).  
  
- Depuração de JavaScript do lado do servidor não tem suporte no Visual Studio, mas há suporte para depuração de JavaScript do lado do cliente.  
  
   Embora você possa adicionar JavaScript embutido para um arquivo de marcação do lado do servidor, depuração não tem suporte para pontos de interrupção adicionados à marcação. Para depurar o JavaScript, fazer referência a um arquivo JavaScript externo no arquivo de marcação e, em seguida, defina os pontos de interrupção no arquivo JavaScript.  
  
- Depuração de embutido [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] código deve ser feito no arquivo de código gerado, em vez de no arquivo de marcação.  
  
- Web parts visuais não suportam o uso da `<@ Assembly Src=` diretiva.  
  
- SharePoint controles da web e alguns [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] controles não têm suporte no ambiente de área restrita e do SharePoint. Se não há suporte para controles são usados em uma web part visual em uma solução em área restrita, o erro "O nome do namespace ou tipo 'Tema' não existe no namespace 'WebControls'" será exibida.  
  
  Para obter mais informações sobre as soluções em área restrita, consulte [diferenças entre a área restrita e soluções em farm](../sharepoint/differences-between-sandboxed-and-farm-solutions.md).  
  
## <a name="create-older-style-sharepoint-based-web-parts"></a>Criar estilo antigo baseado no SharePoint web parts
 Você pode usar os modelos no Visual Studio para criar um personalizado [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] as web parts para SharePoint. [!INCLUDE[vstecasplong](../sharepoint/includes/vstecasplong-md.md)] partes da Web são criados sobre o [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] infra-estrutura de web part e o tipo recomendado para novos projetos.  
  
 Em poucos casos, você talvez precise criar uma web part usando o estilo mais antigo de web part baseada no SharePoint. Você pode usar o Visual Studio para criar esses tipos de web parts, mas o Visual Studio não fornece quaisquer modelos que são projetados especificamente para ajudar a criá-los.  
  
 Para obter mais informações sobre quando você talvez queira criar um estilo mais antigo de web part baseada no SharePoint, consulte [infraestrutura de Web Parts no Windows SharePoint Services](http://go.microsoft.com/fwlink/?LinkId=169290). Para obter mais informações sobre como criar uma web part usando o estilo mais antigo de web part baseada no SharePoint, consulte [instruções passo a passo Criando uma Web Part do SharePoint básico](http://go.microsoft.com/fwlink/?LinkId=169288).  
  
## <a name="related-topics"></a>Tópicos relacionados
  
|Título|Descrição|  
|-----------|-----------------|  
|[Como: criar uma web part do SharePoint](../sharepoint/how-to-create-a-sharepoint-web-part.md)|Mostra como criar web parts páginas do SharePoint.|  
|[Como: criar uma web part do SharePoint usando um designer](../sharepoint/how-to-create-a-sharepoint-web-part-by-using-a-designer.md)|Mostra como criar web parts para SharePoint usando uma superfície de design visual.|  
|[Como: criar um controle de usuário para uma página ou web part de aplicativo do SharePoint](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|Mostra como criar controles reutilizáveis personalizados que podem ser consumidos por páginas de aplicativos e web parts executadas no SharePoint.|  
|[Passo a passo: Criar uma web part do SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)|Descreve como criar uma web part para SharePoint.|  
|[Passo a passo: Criar uma web part para SharePoint usando um designer](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint-by-using-a-designer.md)|Descreve como criar uma web part para o SharePoint arrastando controles a uma superfície de design visual.|  
|[Passo a passo: Criar a web part do Silverlight que exiba OData para o SharePoint](../sharepoint/walkthrough-creating-a-silverlight-web-part-that-displays-odata-for-sharepoint.md)|Descreve como criar uma web part do SharePoint que hospeda um aplicativo do Silverlight e exibe dados de listas do SharePoint.|  
  
