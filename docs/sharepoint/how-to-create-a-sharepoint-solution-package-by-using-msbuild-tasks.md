---
title: Criar pacote de solução do SharePoint usando tarefas do MSBuild
description: Saiba como criar, limpar e validar um pacote de solução do SharePoint (. wsp) usando tarefas de linha de comando do MSBuild em um computador de desenvolvimento.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f4c1d2e986b6a810cc568efd9577be87a38fdefb
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99873535"
---
# <a name="how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks"></a>Como: criar um pacote de solução do SharePoint usando tarefas do MSBuild
  Você pode criar, limpar e validar um pacote do SharePoint (*. wsp*) usando tarefas de linha de comando do MSBuild em um computador de desenvolvimento. Você também pode usar esses comandos para automatizar o processo de compilação usando Team Foundation Server em um computador de compilação.

## <a name="build-a-sharepoint-package"></a>Criar um pacote do SharePoint

#### <a name="to-build-a-sharepoint-package"></a>Para criar um pacote do SharePoint

1. No menu **Iniciar** do Windows, escolha **todos os programas**  >  **acessórios**  >  **prompt de comando**.

2. Altere para o diretório em que o projeto do SharePoint está localizado.

3. Digite o comando a seguir para criar um pacote para o projeto. Substitua *ProjectFileName* pelo nome do projeto.

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

1. Abra una janela de prompt de comando.

2. Altere para o diretório em que o projeto do SharePoint está localizado.

3. Digite o comando a seguir para limpar um pacote para o projeto. Substitua *ProjectFileName* pelo nome do projeto.

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

1. Abra una janela de prompt de comando.

2. Altere para o diretório em que o projeto do SharePoint está localizado.

3. Digite o comando a seguir para validar um pacote para o projeto. Substitua *ProjectFileName* pelo nome do projeto.

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

1. Abra una janela de prompt de comando.

2. Altere para o diretório em que o projeto do SharePoint está localizado.

3. Digite o comando a seguir para definir uma propriedade em um pacote para o projeto. Substitua *PropertyName* pela propriedade que você deseja definir.

    ```cmd
    msbuild /property:PropertyName=Value
    ```

     Por exemplo, você pode executar o comando a seguir para definir o nível de aviso.

    ```cmd
    msbuild /property:WarningLevel = 2
    ```

## <a name="see-also"></a>Confira também
- [Criar recursos do SharePoint](../sharepoint/creating-sharepoint-features.md)
- [Como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [Como: Adicionar e remover itens para recursos do SharePoint](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
