---
title: Solução de problemas de implantação e empacotamento do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VSTO.WorkflowDeployment.Troubleshooting
- VS.SharePointTools.Project.PackageRetraction
- VS.SharePointTools.Deployment.Troubleshooting
- VS.SharePointTools.Deploying.Troubleshooting
- VS.SharePointTools.Project.DeploymentTroubleshooting
- VS.SharePointTools.Project.SharePointNotInstalled
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
- SharePoint development in Visual Studio, troubleshooting
- SharePoint development in Visual Studio, deployment conflict resolution
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ba6f0a1aff0c263534c17256b7f5cf49ff9c9533
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49898051"
---
# <a name="troubleshoot-sharepoint-packaging-and-deployment"></a>Solucionar problemas de implantação e empacotamento do SharePoint
  Este tópico aborda diversos problemas que você pode encontrar ao empacotar e implantar soluções do SharePoint.

## <a name="enable-enhanced-debugging"></a>Habilitar a depuração aprimorada
 Para diagnosticar entre o Visual Studio, SharePoint e outras camadas, você pode usar a chave do registro EnableDiagnostics para exibir o rastreamento de pilha. Para obter mais informações, consulte [soluções do SharePoint depurar](../sharepoint/debugging-sharepoint-solutions.md).

## <a name="add-project-output-to-the-solution-package"></a>Adicionar a saída do projeto ao pacote de solução
 Você pode adicionar a saída do projeto para um pacote por meio do Designer de pacote. No entanto, quando você adiciona a saída do projeto, certifique-se de que a plataforma do projeto corresponda à plataforma da solução do SharePoint. É recomendável que você use o **qualquer CPU** destino da plataforma para os assemblies que você deseja implantar em um servidor do SharePoint. Para obter mais informações, consulte [compilar página, Designer de projeto &#40;Visual Basic&#41; ](/visualstudio/ide/reference/compile-page-project-designer-visual-basic) e [caixa de diálogo de configurações de compilador avançadas &#40;Visual Basic&#41;](/visualstudio/ide/reference/advanced-compiler-settings-dialog-box-visual-basic).

## <a name="validation-warnings-and-errors"></a>Erros e avisos de validação
 As ferramentas de desenvolvimento do SharePoint no Visual Studio executam etapas de validação para verificar se o pacote de solução está formado corretamente. Você também pode criar etapas de validação personalizada para os recursos e pacotes. Para obter mais informações, consulte [como: criar o recurso personalizado e o pacote de regras de validação para soluções do SharePoint](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md).

## <a name="deployment-conflict-resolution"></a>Resolução de conflitos de implantação
 Quando você implanta uma solução do SharePoint, você pode encontrar conflitos quando um item no servidor tem o mesmo nome, URL ou ID como um item em seu pacote de solução. Você pode alterar o **resolução de conflitos de implantação** propriedade para resolver, relatar ou evitar conflitos para os módulos, partes da Web, instâncias de lista e tipos de conteúdo.

 A tabela a seguir demonstra as configurações para o **resolução de conflitos de implantação** propriedade.

|Valor|Descrição|
|-----------|-----------------|
|Automático|Detecta conflitos e resolve os conflitos automaticamente.|
|Solicitar|Detecta conflitos e relata-os para o desenvolvedor antes de resolver os conflitos.|
|Nenhum|Não detecta conflitos.|

## <a name="differences-between-f5-deployment"></a>Diferenças entre a implantação de F5
 Quando você usa [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] para implantar seu projeto do SharePoint para o servidor do SharePoint local para testar e depurar, há algumas etapas adicionais que são executadas pelo [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

1. Redefina o serviço de informações da Internet (IIS) durante a etapa de implantação.

2. Associe automaticamente fluxos de trabalho.

3. Defina a ordem de ativação de recurso acordo com a hierarquia no Designer de pacote.

   Você pode adicionar etapas de implantação personalizado a alteração ainda mais a **F5** comportamento. Para obter mais informações, consulte [instruções passo a passo: criar uma etapa de implantação para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md).

## <a name="delay-displaying-sharepoint-page-when-deploy-visual-web-part"></a>Atraso exibindo a página do SharePoint quando implantar a web part visual
 A página do SharePoint leva muito tempo para aparecer durante a implantação de uma Web part Visual para a pasta Bin em [!INCLUDE[wiprlhext](../sharepoint/includes/wiprlhext-md.md)], [!INCLUDE[win7](../sharepoint/includes/win7-md.md)], ou [!INCLUDE[winsvr08](../sharepoint/includes/winsvr08-md.md)]. Se você alterar todos os arquivos em um nível superior [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] recompilações do diretório, como o diretório Bin, todo o aplicativo Web. Isso pode causar um atraso de até 25 segundos para a página do SharePoint para renderizar.

### <a name="error-message"></a>mensagem de erro
 nenhuma.

### <a name="resolution"></a>Resolução
 Para contornar esse problema, execute as seguintes etapas:

1.  Instale a atualização KB967535 conforme descrito no artigo da Microsoft Support [corrigir: um hotfix está disponível para corrigir dois problemas no ASP.NET no IIS 7.0 para Windows Vista e Windows Server 2008](http://go.microsoft.com/fwlink/?LinkId=179055).

2.  Adicione a seguinte linha ao arquivo Web. config:

    ```xml
    <compilation batch="false" optimizeCompilations="true">
    ```

## <a name="sharepoint-project-deployment-fails-with-error-failed-to-extract-the-cab-file-in-the-solution"></a>Falha de implantação de projeto do SharePoint com o erro "Falha ao extrair o arquivo de gabinete na solução"
 Se o nome de qualquer item de projeto do SharePoint contiver parênteses, sua solução falhará na implantação com um erro.

### <a name="error-message"></a>mensagem de erro
 Ocorreu um erro na etapa de implantação adicionar solução: Falha ao extrair o arquivo de gabinete na solução.

### <a name="resolution"></a>Resolução
 Para contornar esse problema, remova todos os parênteses nos nomes de itens de projeto do SharePoint.

## <a name="error-appears-when-deploying-a-visual-web-part-to-a-site-on-a-different-web-application"></a>Erro aparece ao implantar uma web part visual em um site em um aplicativo web diferente
 Na primeira vez que você implante uma Web part visual em um site em um aplicativo Web diferente no qual está implementada atualmente (alterando a propriedade SiteUrl da parte Web visual), você obterá um erro.

### <a name="error-message"></a>mensagem de erro
 Ocorreu um erro na etapa de implantação adicionar solução: um recurso com a ID [#] já foi instalado neste farm. Use o atributo de força para reinstalar explicitamente o recurso.

### <a name="resolution"></a>Resolução
 Esse erro ocorre devido à maneira como recursos de Web part visual são retraídos no SharePoint. Para implantar com êxito a Web part visual, implante a solução novamente escolhendo a **F5** chave.

## <a name="warning-appears-when-deploying-nested-user-controls"></a>Aviso é exibido ao implantar controles de usuário aninhados
 Este aviso ocorre quando você implanta uma solução do SharePoint que tem controles de usuário aninhados, como uma Web part visual que contém um controle de usuário ou um controle de usuário que contém uma Web part visual ou outro controle de usuário. Este aviso ocorre se você adicionar um controle a um designer arrastando-o na caixa de ferramentas ou usando o @Register diretiva na exibição da fonte.

### <a name="error-message"></a>mensagem de erro
 Aviso 1 elemento ' [*nome do controle*]' não é um elemento conhecido. Isso pode ocorrer se houver um erro de compilação no site da Web ou o arquivo Web. config está ausente.

### <a name="resolution"></a>Resolução
 Se o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] sistema de projeto não está ciente de um controle de usuário aninhados, ele não pode fornecer o IntelliSense e ele emitirá o aviso. O sistema de projeto não fica ciente de um controle de usuário aninhado se o projeto não é compilado e o designer não é fechado e reaberto, ou se a retração automática opção estiver habilitada, que faz com que o controle de usuário seja retraído da seção o hive do SharePoint após a depuração.

 Para remover este aviso, compile o projeto e, em seguida, feche e, em seguida, reabra o designer ou desabilite a opção para o projeto de retração automática. Para fazer isso, desmarque a **retração automática após a depuração** caixa de seleção a **SharePoint** guia da caixa de diálogo de propriedades do projeto.

## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)

