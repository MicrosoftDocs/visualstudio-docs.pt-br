---
title: Depurando soluções do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.WebConfigModificationDialog
- VS.SharePointTools.Project.DebuggingNotEnabled
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6f53ca7f1a5e449d47a30a32967072f7220c159a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49903147"
---
# <a name="debug-sharepoint-solutions"></a>Depurar soluções do SharePoint
  Você pode depurar soluções do SharePoint usando o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] depurador. Quando você inicia a depuração, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] implanta os arquivos de projeto para o servidor do SharePoint e, em seguida, abre uma instância do site do SharePoint no navegador da Web. As seções a seguir explicam como depurar aplicativos do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
-   [Habilitando a depuração](#EnableDebug)  
  
-   [Processo de implantação e depuração F5](#Deployment)  
  
-   [Recursos de projeto do SharePoint](#Features)  
  
-   [Depurando fluxos de trabalho](#Workflow)  
  
-   [Receptores de evento de depuração](#FeatureEvents)  
  
-   [Habilitar informações de depuração aprimoradas](#EnhancedDebug)  
  
## <a name="enable-debugging"></a>Habilitar a depuração
 Quando você depura uma solução do SharePoint no primeiro [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], uma caixa de diálogo alerta você que o arquivo Web. config não está configurado para habilitar a depuração. (O arquivo Web. config é criado quando você instala o SharePoint server. Para obter mais informações, consulte [trabalhando com arquivos Web. config](http://go.microsoft.com/fwlink/?LinkID=149266).) A caixa de diálogo lhe dá a opção de execução do projeto sem depuração ou modificando o arquivo Web. config para habilitar a depuração. Se você escolher a primeira opção, o projeto é executado normalmente. Se você escolher a segunda opção, o arquivo Web. config está configurado para:  
  
- Ativar a pilha de chamadas (`CallStack="true"`)  
  
- Desabilitar erros personalizados no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] (`<customErrors mode="Off" />`)  
  
- Habilitar a depuração de compilação (`<compilation debug="true">`)  
  
  O arquivo Web. config resultante é:  
  
```xml  
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <configuration>  
        ...  
        <SharePoint>  
            <SafeMode MaxControls="200"  
                CallStack="true"  
                DirectFileDependencies="10"  
                TotalFileDependencies="50"  
                AllowPageLevelTrace="false">  
                ...  
            </SafeMode>  
        ...  
        </SharePoint>  
        <system.web>  
            ...  
            <customErrors mode="Off" />  
            ...  
            <compilation debug="true">  
            ...  
            </compilation>  
            ...  
        </system.web>  
        ...  
    </configuration>  
```  
  
 Para reverter as alterações e desabilitar a depuração, altere o seguinte [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] no arquivo Web. config:  
  
-   Desativar a pilha de chamadas (`CallStack="false"`)  
  
-   Habilitar erros personalizados em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] (`<customErrors mode="On" />`)  
  
-   Desabilitar a depuração de compilação (`<compilation debug="false">`)  
  
## <a name="f5-debug-and-deployment-process"></a>Processo de implantação e depuração F5
 Quando você executa seu projeto do SharePoint no modo de depuração, o processo de implantação do SharePoint executa as seguintes tarefas:  
  
1. Executa os comandos de pré-implantação personalizáveis.  
  
2. Cria um arquivo de pacote (. wsp) da solução de Web usando [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] comandos. O arquivo. wsp inclui todos os arquivos necessários e os recursos. Para obter mais informações, consulte [visão geral das soluções](http://go.microsoft.com/fwlink/?LinkID=128154).  
  
3. Se a solução do SharePoint é uma solução de farm, recicla o [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] pool de aplicativos para o site especificado [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]. Esta etapa libera arquivos bloqueados pelo [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] processo de trabalho.  
  
4. Se já existir uma versão anterior do pacote, cancela a versão anterior dos recursos e arquivos no arquivo. wsp. Esta etapa desativa os recursos, desinstala o pacote de solução e, em seguida, exclui o pacote da solução no servidor do SharePoint.  
  
5. Instala a versão atual dos recursos e arquivos no arquivo. wsp. Esta etapa adiciona e instala a solução no servidor do SharePoint.  
  
6. Para fluxos de trabalho, instala o assembly de fluxo de trabalho. Você pode alterar seu local usando o *local do Assembly* propriedade.  
  
7. Ativa o recurso do projeto no SharePoint se o escopo é o Site ou Web. Recursos em escopos WebApplication e Farm não são ativados.  
  
8. Para fluxos de trabalho, associa o fluxo de trabalho com a biblioteca do SharePoint, lista ou site que você selecionou na **Assistente para personalização do SharePoint**.  
  
   > [!NOTE]  
   >  Essa associação ocorre somente se você selecionou **fluxo de trabalho associado automaticamente** no assistente.  
  
9. Executa os comandos de pós-implantação personalizáveis.  
  
10. Anexa a [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] do depurador para o [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] processo (*w3wp.exe*). Se o tipo de projeto permite que você altere a *solução de área restrita* propriedade e seu valor é definido como **verdadeiro**, em seguida, o depurador é anexado a um processo diferente (*SPUCWorkerProcess.exe*). Para obter mais informações, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
11. Inicia o depurador do JavaScript se a solução do SharePoint é uma solução de farm.  
  
12. Exibe a página do site, lista ou biblioteca apropriada no navegador da Web.  
  
    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Exibe uma mensagem de status na janela de saída após a conclusão de cada tarefa. Se uma tarefa não pode ser concluída, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] exibe uma mensagem de erro na janela lista de erros.  
  
## <a name="sharepoint-project-features"></a>Recursos de projeto do SharePoint
 Um recurso é uma unidade portátil e modular de funcionalidades que simplificam a modificação de sites usando definições de site. Também é um pacote de [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] elementos (WSS) que podem ser ativados para um escopo específico e que ajuda os usuários a realizar uma tarefa ou uma meta específica. Modelos são implantados como recursos.  
  
 Quando você executa um projeto no modo de depuração, o processo de implantação cria uma pasta na *recurso* diretório no *%COMMONPROGRAMFILES%\Microsoft Shared\web server extensions\14\TEMPLATE\FEATURES*. Nomes de recurso têm o formato *nome do projeto*recurso*x*, como TestProject_Feature1.  
  
 A pasta da solução no diretório do recurso contém um *da definição de recurso* arquivo e um *definição de fluxo de trabalho* arquivo. O arquivo de definição de recurso (Feature. xml) descreve os arquivos no arquivo de definição de projeto de processos do projeto (*Elements. XML*) descreve o modelo de projeto. *Elements. XML* pode ser encontrado no **Gerenciador de soluções**, mas Feature. XML é gerado quando o pacote de solução é criado. Para obter mais informações sobre esses arquivos, consulte [SharePoint modelos de item de projeto e projeto](../sharepoint/sharepoint-project-and-project-item-templates.md).  
  
## <a name="debug-workflows"></a>Depurar fluxos de trabalho
 Quando você depurar projetos de fluxo de trabalho, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] adiciona o modelo de fluxo de trabalho (dependendo do tipo) para uma biblioteca ou uma lista. Em seguida, você pode iniciar o modelo de fluxo de trabalho manualmente ou por adicionar ou atualizar um item. Você pode usar [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] para depurar o fluxo de trabalho.  
  
> [!NOTE]
>  Se você adicionar referências a outros assemblies, certifique-se de que esses assemblies são instalados no cache de assembly global ( [!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)]). Caso contrário, a solução de fluxo de trabalho falhará. Para obter informações sobre como instalar assemblies, consulte [iniciar manualmente um fluxo de trabalho em um documento ou item](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963).  
  
 No entanto, o processo de implantação não inicia o fluxo de trabalho. Você deve iniciar o fluxo de trabalho do site do SharePoint. Você também pode iniciar o fluxo de trabalho usando um aplicativo cliente como o Microsoft Office Word 2010 ou usando o código do lado do servidor separado. Use uma das abordagens especificadas na **Assistente para personalização do SharePoint**.  
  
 Por exemplo, se você tiver especificado o fluxo de trabalho pode ser iniciado manualmente, inicie o fluxo de trabalho diretamente do item na lista ou biblioteca. Para obter mais informações sobre como iniciar um fluxo de trabalho manualmente, consulte [iniciar manualmente um fluxo de trabalho em um item do documento](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963).  
  
## <a name="debug-feature-event-receivers"></a>Receptores de evento de depuração
 Por padrão, quando você executa um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] aplicativo do SharePoint, seus recursos serão ativados automaticamente para você no servidor do SharePoint. No entanto, isso causa problemas quando você depura receptores de evento, porque quando um recurso é ativado por [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], ele é executado em um processo diferente que o depurador. Isso significa que algumas funcionalidades de depuração, como pontos de interrupção, não funcionará corretamente.  
  
 Para desabilitar a ativação automática do recurso no SharePoint e permitir a depuração adequada de receptores de evento, defina o valor do projeto **configuração de implantação ativa** propriedade **sem ativação** antes de depurar. Em seguida, depois de começar a depurar seu aplicativo do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], manualmente ativar o recurso no SharePoint. Para ativar o recurso, abra o **ações do Site** menu no SharePoint, escolha **configurações de Site**, escolha o **gerenciar recursos de Site** vincular e, em seguida, escolha o **Activate** botão ao lado do recurso, para continuar a depuração como de costume.  
  
## <a name="enable-enhanced-debug-information"></a>Habilitar informações de depuração avançada
 Devido a interações complexas, às vezes, entre o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] processo (devenv.exe), o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] processo de host do SharePoint (*vssphost4.exe*), SharePoint e a camada do WCF, diagnóstico de erros que ocorrem enquanto Compilando, implantando e assim por diante podem ser um desafio. Para ajudá-lo a resolver esses erros, você pode habilitar as informações de depuração aprimoradas. Para fazer isso, vá para a seguinte chave do registro no registro do Windows:  
  
 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools**  
  
 Se o "EnableDiagnostics" **REG_DWORD** valor ainda não existir, crie-o manualmente. Defina o valor de "EnableDiagnostics" como "1".  
  
 Definir esse valor de chave para a pilha de 1 faz com que informações aparecem no rastreamento de **saída** janela sempre que os erros de sistema do projeto ocorrerem enquanto você estiver executando em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para desabilitar as informações de depuração aprimoradas, defina EnableDiagnostics para 0 ou exclua o valor.  
  
 Para obter mais informações sobre outras chaves do registro do SharePoint, consulte [depurar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Solucionar problemas de soluções do SharePoint](../sharepoint/troubleshooting-sharepoint-solutions.md)  
  
