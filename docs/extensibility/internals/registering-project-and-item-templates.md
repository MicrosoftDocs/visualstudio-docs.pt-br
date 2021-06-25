---
title: Registrando modelos de projeto e item | Microsoft Docs
description: Saiba como o Visual Studio usa informações de registro para seus tipos de projeto para determinar o que mostrar nas caixas de diálogo Adicionar novo projeto e adicionar novo item.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], adding items
- registry, Add New Item dialog box
- Add New Item dialog box
- Add New Project dialog box
- registry, Add New Project dialog box
ms.assetid: 6b909f93-d7f5-4aec-81c6-ee9ff0f31638
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8b60022c6adf65d0b0d60d32b4ad7ae72067726d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905625"
---
# <a name="registering-project-and-item-templates"></a>Registrando modelos de projeto e item
Os tipos de projeto devem registrar os diretórios em que os modelos de projeto e de item de projeto estão localizados. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usa as informações de registro associadas aos tipos de projeto para determinar o que mostrar nas caixas de diálogo **Adicionar novo projeto** e **Adicionar novo item** .

 Para obter mais informações sobre modelos, consulte [adicionando projeto e modelos de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md).

## <a name="registry-entries-for-projects"></a>Entradas de registro para projetos
 Os exemplos a seguir mostram entradas de registro em HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ < *versão*>. As tabelas que as acompanham explicam os elementos usados nos exemplos.

```
[Projects\{ProjectGUID}]
@="MyProjectType"
"DisplayName"="#2"
"Package"="{VSPackageGUID}"
"ProjectTemplatesDir"="C:\\MyProduct\\MyProjectTemplates"
```

|Nome|Tipo|Descrição|
|----------|----------|-----------------|
|@|REG_SZ|Nome padrão dos projetos deste tipo.|
|DisplayName|REG_SZ|ID de recurso do nome a ser recuperado da DLL satélite registrada em pacotes.|
|Pacote|REG_SZ|ID de classe do pacote registrado em pacotes.|
|ProjectTemplatesDir|REG_SZ|Caminho padrão dos arquivos de modelo de projeto. Os arquivos de modelo de projeto são exibidos pelo novo modelo de **projeto** .|

### <a name="registering-item-templates"></a>Registrando modelos de item
 Você deve registrar o diretório onde você armazena os modelos de item.

```
[Projects\{ProjectGUID}\AddItemTemplates\TemplateDirs\{VSPackageGUID}\1]
@="#7"
"TemplatesDir"="C:\\MyProduct\\MyProjectItemTemplates "
"TemplatesLocalizedSubDir"="#10"
"SortPriority"=dword:00000064
```

| Nome | Tipo | Descrição |
|--------------------------|-----------| - |
| @ | REG_SZ | ID do recurso para adicionar modelos de item. |
| TemplatesDir | REG_SZ | Caminho dos itens de projeto exibidos na caixa de diálogo para o assistente **Adicionar novo item** . |
| TemplatesLocalizedSubDir | REG_SZ | ID de recurso de uma cadeia de caracteres que nomeia o subdiretório de TemplatesDir que contém modelos localizados. Como [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o carrega o recurso de cadeia de caracteres de DLLs satélite, se você os tiver, cada DLL satélite poderá conter um nome de subdiretório localizado diferente. |
| SortPriority | REG_DWORD | Defina SortPriority para controlar a ordem na qual os modelos são exibidos na caixa de diálogo **Adicionar novo item** . Valores SortPriority maiores aparecem anteriormente na lista de modelos. |

### <a name="registering-file-filters"></a>Registrando filtros de arquivo
 Opcionalmente, você pode registrar filtros que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usa quando ele solicita nomes de arquivo. Por exemplo, o [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] filtro para a caixa de diálogo **Abrir arquivo** é:

 **Arquivos do Visual C# ( \* . cs, \* . resx, \* . Settings, \* . xsd, \* . WSDL); \* . CS, \* . resx, \* . Settings, \* . xsd, \* . WSDL)**

 Para dar suporte ao registro de vários filtros, cada filtro é registrado em sua própria subchave em HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ < *versão*> \\ subchave do \projects { \<*ProjectGUID*> } \Filters \\ < >. O nome da subchave é arbitrário; [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ignora o nome da subchave e usa apenas seus valores.

 Você pode controlar os contextos nos quais um filtro é usado definindo sinalizadores, mostrados na tabela a seguir. Se um filtro não tiver nenhum sinalizador definido, ele será listado após os filtros comuns na caixa de diálogo **Adicionar item existente** e na caixa de diálogo **Abrir arquivo** , mas não será usado na caixa de diálogo **localizar nos arquivos** .

```
[Projects\{ProjectGUID}\Filters\MyLanguageFilter]
@="#3"
"CommonOpenFilesFilter"=dword:00000000
"CommonFindFilesFilter"=dword:00000000
"FindInFilesFilter"=dword:00000000
"NotOpenFileFilter"=dword:00000000
"NotAddExistingItemFilter"=dword:00000000
"SortPriority"=dword:00000064
```

|Nome|Tipo|Descrição|
|----------|----------|-----------------|
|CommonFindFilesFilter|REG_DWORD|Torna o filtro um dos filtros comuns na caixa de diálogo **localizar nos arquivos** . Os filtros comuns são listados na lista filtro antes dos filtros não marcados como comuns.|
|CommonOpenFilesFilter|REG_DWORD|Torna o filtro um dos filtros comuns na caixa de diálogo **Abrir arquivo** . Os filtros comuns são listados na lista filtro antes dos filtros não marcados como comuns.|
|FindInFilesFilter|REG_DWORD|Lista o filtro após os filtros comuns na caixa de diálogo **localizar nos arquivos** .|
|NotOpenFileFilter|REG_DWORD|Indica que o filtro não é usado na caixa de diálogo **Abrir arquivo** .|
|NotAddExistingItemFilter|REG_DWORD|Indica que o filtro não é usado na caixa de diálogo **Adicionar item existente** .|
|SortPriority|REG_DWORD|Defina SortPriority para controlar a ordem na qual os filtros são exibidos. Valores SortPriority maiores aparecem anteriormente na lista de filtros.|

## <a name="directory-structure"></a>Estrutura de diretórios
 O VSPackages pode colocar arquivos de modelo e pastas em qualquer lugar em um disco local ou remoto, desde que o local seja registrado por meio do IDE (ambiente de desenvolvimento integrado). No entanto, para facilitar a organização, recomendamos a seguinte estrutura de diretório no caminho de instalação do seu produto.

 \Templates

 \Projects (contém os modelos de projeto)

 \Applications

 \Components

 \ ...

 \ProjectItems (contém os itens de projeto)

 \Class

 \Form

 Página \Servidor

 \HelperFiles (contém os arquivos usados em itens de projeto de vários arquivos)

 \WizardFiles

## <a name="see-also"></a>Confira também

- [Adicionando o projeto e os modelos de item do projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [Assistentes](../../extensibility/internals/wizards.md)
- [Localizando aplicativos](../../ide/globalizing-and-localizing-applications.md)
- [CATIDs para objetos que normalmente são usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
