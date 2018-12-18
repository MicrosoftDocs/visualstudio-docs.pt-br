---
title: Considerações sobre a solução em área restrita | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SandboxedSolutions
- VS.SharePointTools.Security.SandboxedSolutions
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2f9a5d0c439d619864cc6e9559608e3c3891fc7e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49890030"
---
# <a name="sandboxed-solution-considerations"></a>Considerações sobre a solução em área restrita
  *Soluções em área restrita* são um recurso do Microsoft SharePoint 2010 que permite que os usuários da coleção de site carregar suas próprias soluções de código personalizado. Uma solução em área restrita comum é carregar suas próprias Web Parts de usuários.  
  
 Um aplicativo em área restrita do SharePoint é executado em um processo seguro e monitorado que tem acesso a uma parte limitada do Web farm. Microsoft SharePoint 2010 usa uma combinação de recursos, galerias de solução, solução de monitoramento e uma estrutura de validação para habilitar soluções em área restrita.  
  
## <a name="specify-project-trust-level"></a>Especifique o nível de confiança do projeto
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] oferece suporte a soluções em área restrita por meio de uma propriedade de projeto booleano chamadas *solução de área restrita*. Essa propriedade pode ser definida a qualquer momento no projeto, ou pode ser especificado quando você cria o projeto na **Assistente para personalização do SharePoint**.  
  
> [!NOTE]  
>  Alterando a *solução de área restrita* propriedade de um projeto após sua criação pode causar erros de validação.  
  
 A solução é considerada uma solução com escopo de farm se o *solução de área restrita* estiver definida como **falso** ou escolher o **implantar como uma solução de farm** opção. No entanto, a solução é tratada Diferentemente de uma solução de farm se o *solução de área restrita* estiver definida como **verdadeiro** ou escolher o **implantar como solução em área restrita** opção no assistente.  
  
## <a name="sharepoint-site-hierarchy"></a>Hierarquia do site do SharePoint
 Para entender as soluções em área restrita como trabalho, é útil para saber que os sites do SharePoint são hierárquicos no escopo. O elemento superior é conhecido como farm da Web e outros elementos são subordinados a ele:  
  
 Web Farm  
  
 Aplicativo Web  
  
 A1 da coleção de site  
  
 Site A1a  
  
 Aplicativo Web B  
  
 B1 de coleção do site  
  
 Site B1a  
  
 Site B1b  
  
 B2 de coleção do site  
  
 Site B2a  
  
 Como você pode ver, os farms da Web podem conter um ou mais aplicativos Web, que por sua vez, podem conter um ou mais coleções de site, que podem ter subsites e assim por diante. Alterações feitas em um afetam de coleção de site apenas que o conjunto de sites e nenhum outro. No entanto, as alterações feitas no nível do farm da Web afetam todos os conjuntos de sites no farm.  
  
 Windows SharePoint Services (WSS) 3.0 permite que você implante soluções somente para o nível de farm, mas [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] permite que você implante no nível do farm (solução de farm) ou o nível de conjunto de sites (solução de área restrita).  
  
## <a name="why-sandboxed-solutions"></a>Por que soluções em área restrita?
 O WSS 3.0, soluções poderiam ser implantadas somente para o nível de farm. Isso significava que potencialmente perigosas ou desestabilizadoras soluções pode ser implantadas que que afetava o farm da Web inteiro e todos os outros conjuntos de sites e aplicativos que são executados sob ele. No entanto, usando as soluções em área restrita, você pode implantar suas soluções para uma subárea do farm, um conjunto de sites específico. Para fornecer proteção adicional, o assembly da solução não é carregado no principal [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] processo (*w3wp.exe*). Em vez disso, ele é carregado em um processo separado (*SPUCWorkerProcess.exe*). Esse processo é monitorado e implementa cotas e limitação para proteger o farm de soluções em área restrita que executam atividades prejudiciais, como a execução de loops rígidos que consomem ciclos de CPU.  
  
## <a name="site-collection-solution-gallery"></a>Galeria de soluções de coleta de site
 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 2010 tem um recurso que é conhecido como a "Galeria de soluções de coleta de site". Você pode acessar esse recurso na página Administração Central do SharePoint 2010 ou abrindo o **ações do Site** menu, escolhendo **configurações de Site**e, em seguida, escolhendo o **soluções** vincular sob **galerias** no site do SharePoint. Galerias de solução são repositórios de soluções que permitem que os administradores de coleção de site gerenciar soluções em suas coleções de sites.  
  
 A Galeria de soluções é uma biblioteca de documentos armazenada na raiz da Web do site do SharePoint. A Galeria de soluções substitui os modelos de site e dá suporte a pacotes de solução. Quando um pacote de solução do SharePoint (*. wsp*) arquivo é carregado, ele é processado como uma solução em área restrita.  
  
## <a name="sandboxed-solution-limitations"></a>Limitações de solução de área restrita
 Quando uma solução em área restrita é implantada, a matriz de funcionalidade do SharePoint disponível para ele é limitada para ajudar a reduzir as vulnerabilidades de segurança pode ter. Algumas dessas limitações incluem o seguinte:  
  
- Soluções em área restrita têm um subconjunto restrito de elementos da solução implantável disponíveis para eles. Modelos de projeto do SharePoint potencialmente vulneráveis, como definições de site e fluxos de trabalho, não estão disponíveis.  
  
- SharePoint executa o código da solução em área restrita em um processo (*SPUCWorkerProcess.exe*) separado do principal [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] pool de aplicativos (*w3wp.exe*) processo.  
  
- Pastas mapeadas não podem ser adicionadas ao projeto.  
  
- Tipos no [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] assembly Microsoft.Office.Server não pode ser usado em soluções em área restrita. Além disso, somente tipos no [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] assembly Microsoft. SharePoint podem ser usados em soluções em área restrita.  
  
  É importante observar que especificar uma solução do SharePoint como uma solução em área restrita não tem nenhum efeito no servidor do SharePoint; apenas determina como o projeto do SharePoint é implantado no SharePoint de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e quais assemblies ele se vincula. Não afeta o gerado *. wsp* arquivo e o *. wsp* arquivo não tem dados que correlaciona diretamente para o *solução em área restrita* propriedade.  
  
## <a name="capabilities-and-elements-in-sandboxed-solutions"></a>Elementos soluções em área restrita e recursos
 Soluções em área restrita dão suporte a elementos e os recursos a seguir:  
  
- Tipos de conteúdo/campos  
  
- Ações personalizadas  
  
- Fluxos de trabalho declarativos  
  
- Receptores de evento  
  
- Textos explicativos do recurso  
  
- Definições de lista  
  
- Instâncias de lista  
  
- Arquivos do módulo  
  
- Navegação  
  
- *onet*  
  
- SPItemEventReceiver  
  
- SPListEventReceiver  
  
- SPWebEventReceiver  
  
- Suporte para todas as Web Parts que derivam de `System.Web.UI.WebControls.WebParts.WebPart`  
  
- Web Parts  
  
- Elementos de recurso WebTemplate (em vez de *webtemp*)  
  
- Web Parts visuais  
  
  Soluções em área restrita não dão suporte a elementos e os recursos a seguir:  
  
- Páginas de aplicativo  
  
- Grupo de ação personalizado  
  
- Recursos de escopo de farm  
  
- Elemento `HideCustomAction`  
  
- Recursos de escopo do aplicativo Web  
  
- Fluxos de trabalho com código  
  
## <a name="see-also"></a>Consulte também
 [Diferenças entre a área restrita e soluções em farm](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)   
 [Desenvolvendo soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  