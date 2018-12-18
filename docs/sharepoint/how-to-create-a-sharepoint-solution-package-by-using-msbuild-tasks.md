---
title: 'Como: criar um pacote de solução do SharePoint usando tarefas do MSBuild | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5a95eb80b860a1447fe6e958edb9c98b66805a90
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118340"
---
# <a name="how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks"></a>Como: criar um pacote de solução do SharePoint usando tarefas do MSBuild
  Você pode compilar, limpar e validar um pacote do SharePoint (*. wsp*) usando as tarefas de linha de comando do MSBuild em um computador de desenvolvimento. Você também pode usar esses comandos para automatizar o processo de compilação usando o Team Foundation Server em um computador de compilação.  
  
## <a name="build-a-sharepoint-package"></a>Criar um pacote do SharePoint  
  
#### <a name="to-build-a-sharepoint-package"></a>Para criar um pacote do SharePoint  
  
1.  Sobre o Windows **inicie** menu, escolha **todos os programas** > **Acessórios** > **Prompt de comando**.  
  
2.  Altere para o diretório onde se encontra o projeto do SharePoint.  
  
3.  Digite o seguinte comando para criar um pacote para o projeto. Substitua *ProjectFileName* com o nome do projeto.  
  
    ```cmd  
    msbuild /t:Package ProjectFileName  
    ```  
  
     Por exemplo, você pode executar um dos comandos a seguir para empacotar um projeto do SharePoint chamado ListDefinition1.  
  
    ```cmd  
    msbuild /t:Package ListDefinition1.vbproj  
    msbuild /t:Package ListDefinition1.csproj  
    ```  
  
## <a name="clean-a-sharepoint-package"></a>Limpar um pacote do SharePoint  
  
#### <a name="to-clean-a-sharepoint-package"></a>Para limpar um pacote do SharePoint  
  
1.  Abra uma janela do prompt de comando.  
  
2.  Altere para o diretório onde se encontra o projeto do SharePoint.  
  
3.  Insira o seguinte comando para limpar um pacote para o projeto. Substitua *ProjectFileName* com o nome do projeto.  
  
    ```cmd  
    msbuild /t:CleanPackage ProjectFileName  
    ```  
  
     Por exemplo, você pode executar um dos comandos a seguir para limpar um projeto do SharePoint chamado ListDefinition1.  
  
    ```cmd  
    msbuild /t:CleanPackage ListDefinition1.vbproj  
    msbuild /t:CleanPackage ListDefinition1.csproj  
    ```  
  
## <a name="validate-a-sharepoint-package"></a>Validar um pacote do SharePoint  
  
#### <a name="to-validate-a-sharepoint-package"></a>Para validar um pacote do SharePoint  
  
1.  Abra uma janela do prompt de comando.  
  
2.  Altere para o diretório onde se encontra o projeto do SharePoint.  
  
3.  Insira o comando a seguir para validar um pacote para o projeto. Substitua *ProjectFileName* com o nome do projeto.  
  
    ```cmd  
    msbuild /t:ValidatePackage ProjectFileName  
    ```  
  
     Por exemplo, você pode executar um dos comandos a seguir para validar um projeto do SharePoint chamado ListDefinition1.  
  
    ```cmd  
    msbuild /t:ValidatePackage ListDefinition1.vbproj  
    msbuild /t:ValidatePackage ListDefinition1.csproj  
    ```  
  
## <a name="set-properties-in-a-sharepoint-package"></a>Definir propriedades em um pacote do SharePoint  
  
#### <a name="to-set-a-property-in-a-sharepoint-package"></a>Para definir uma propriedade em um pacote do SharePoint  
  
1.  Abra uma janela do prompt de comando.  
  
2.  Altere para o diretório onde se encontra o projeto do SharePoint.  
  
3.  Digite o seguinte comando para definir uma propriedade em um pacote para o projeto. Substitua *PropertyName* com a propriedade que você deseja definir.  
  
    ```cmd  
    msbuild /property:PropertyName=Value  
    ```  
  
     Por exemplo, você pode executar o comando a seguir para definir o nível de aviso.  
  
    ```cmd  
    msbuild /property:WarningLevel = 2  
    ```  
  
## <a name="see-also"></a>Consulte também
 [Criar recursos do SharePoint](../sharepoint/creating-sharepoint-features.md)   
 [Como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md)   
 [Como: adicionar e remover itens de recursos do SharePoint](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)  
