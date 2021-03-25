---
title: Registrando um tipo de projeto | Microsoft Docs
description: Saiba mais sobre como criar entradas de registro que permitem que o Visual Studio reconheça e trabalhe com o novo tipo de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], new project registry entries
- registry, new project types
- registration, new project types
ms.assetid: dfc0e231-6b4e-447d-9d64-0e66dea3394a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e54f62a90ece61fc2dd8f3cc2b242957f249ed33
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062766"
---
# <a name="registering-a-project-type"></a>Registrando um tipo de projeto
Ao criar um novo tipo de projeto, você deve criar entradas de registro que habilitam [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o para reconhecer e trabalhar com o tipo de projeto. Normalmente, você cria essas entradas de registro usando um arquivo de script do registro (. rgs).

 No exemplo a seguir, as instruções do registro fornecem caminhos e dados padrão quando aplicável, seguidos por uma tabela que contém entradas do script de registro para cada instrução. As tabelas fornecem as entradas de script e informações adicionais sobre as instruções.

> [!NOTE]
> As informações de registro a seguir devem ser um exemplo do tipo e da finalidade das entradas nos scripts de registro que você estará escrevendo para registrar o tipo de projeto. Suas entradas reais e seus usos podem variar com base nos requisitos específicos do seu tipo de projeto. Você deve examinar os exemplos disponíveis para encontrar um que seja parecido com o tipo de projeto que você está desenvolvendo e, em seguida, examinar o script do registro para esse exemplo.

 Os exemplos a seguir são de HKEY_CLASSES_ROOT.

## <a name="example-1"></a>Exemplo 1

```
\.figp
   @="FigPrjFile"
   "Content Type"="text/plain"
\.figp\ShellNew
   "NullFile"=""
\FigPrjFile
   @="Figure Project File"
\DefaultIcon
   @="<Visual Studio SDK installation path>\\9.0VSIntegration\\SomeFolder\\FigPkgs\\FigPrj\\Debug\\FigPrj.dll,-206"
\shell\open
   @="&Open in Visual Studio"
\shell\open\command
   @="devenv.exe \"%1\""
```

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrjFile`|Nome e descrição dos arquivos de tipo de projeto que têm a extensão. figp.|
|`Content Type`|REG_SZ|`Text/plain`|Tipo de conteúdo para os arquivos de projeto.|
|`NullFile`|REG_SZ|`Null`||
|`@`|REG_SZ|`%MODULE%,-206`|Ícone padrão usado para o projeto deste tipo. A instrução% MODULE% foi concluída no registro para o local padrão do tipo de projeto DLL.|
|`@`|REG_SZ|`&Open in Visual Studio`|Aplicativo padrão no qual este tipo de projeto será aberto.|
|`@`|REG_SZ|`devenv.exe "%1"`|Comando padrão que será executado quando um projeto desse tipo for aberto.|

 Os exemplos a seguir são de HKEY_LOCAL_MACHINE e estão localizados no registro na chave [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\99.0Exp\Packages].

## <a name="example-2"></a>Exemplo 2

```
\{ACEF4EB2-57CF-11D2-96F4-000000000000} (The CLSID for the VSPackage)
   @="FigPrj Project Package"
   "InprocServer32"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\                      Debug\\FigPrj.dll"
   "CompanyName"="Microsoft"
   "ProductName"="Figure Project Sample"
   "ProductVersion"="9.0"
   "MinEdition"="professional"
   "ID"=dword:00000001
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\SatelliteDLL
   "DllName"="FigPrjUI.dll"
   "Path"="9.0<Visual Studio SDK installation path>\\VSIntegration\\Archive\\FigPkgs\\FigPrj\\Debug\\"
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\Automation
   "FigProjects"=""
\{ACEF4EB2-57CF-11D2-96F4-000000000000}\AutomationEvents
   "FigProjectsEvents"="Returns the FigProjectsEvents Object"
   "FigProjectItemsEvents"="Returns the FigProjectItemsEvents Object"
```

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|`@` (Padrão)|REG_SZ|`FigPrj Project VSPackage`|Nome localizável deste VSPackage registrado (tipo de projeto).|
|`InprocServer32`|REG_SZ|`%MODULE%`|Caminho do tipo de projeto DLL. O IDE carrega essa DLL e passa o CLSID VSPackage para `DllGetClassObject` para <xref:Microsoft.VisualStudio.OLE.Interop.IClassFactory> construir o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> objeto.|
|`CompanyName`|REG_SZ|`Microsoft`|Nome da empresa que desenvolveu o tipo de projeto.|
|`ProductName`|REG_SZ|`Figure Project Sample`|Nome para o tipo de projeto.|
|`ProductVersion`|REG_SZ|`9.0`|Número de versão da versão do tipo de projeto.|
|`MinEdition`|REG_SZ|`professional`|Edição do VSPackage que está sendo registrado.|
|`ID`|REG_DWORD|`%IDS_PACKAGE_LOAD_KEY%`|A chave de carregamento do pacote para o projeto VSPackage. A chave é validada quando um projeto é carregado depois que o ambiente é iniciado.|
|`DllName`|REG_SZ|`%RESOURCE_DLL%`|Nome do arquivo da DLL satélite que contém recursos localizados para o tipo de projeto.|
|`Path`|REG_SZ|`%RESOURCE_PATH%`|Caminho da DLL satélite.|
|`FigProjectsEvents`|REG_SZ|Consulte a instrução para obter o valor.|Determina a cadeia de texto retornada para este evento de automação.|
|`FigProjectItemsEvents`|REG_SZ|Consulte a instrução para obter o valor.|Determina a cadeia de texto retornada para este evento de automação.|

 Todos os exemplos a seguir estão localizados no registro na chave [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects].

## <a name="example-3"></a>Exemplo 3

```
\{C061DB26-5833-11D2-96F5-000000000000} (The CLSID for projects of this type)
   @="FigPrj Project"
   "DisplayName"="#2"
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "ProjectTemplatesDir"="C:\\Program Files\\VSIP 9.0\\EnvSDK\\FigPkgs\\                           FigPrj\\FigPrjProjects"
   "ItemTemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                           FigPrjProjectItems"
   "DisplayProjectFileExtensions"="#3"
   "PossibleProjectExtensions"="figp"
   "DefaultProjectExtension"=".figp"
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\1       (Folder 1 contains settings for Open Files filters.)
   @="#4"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000000
   "FindInFilesFilter"=dword:00000000
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\Filters\2
      (Folder 2 contains settings for Find in Files filters.)
   @="#5"
   "CommonOpenFilesFilter"=dword:00000000
   "CommonFindFilesFilter"=dword:00000000
   "NotAddExistingItemFilter"=dword:00000001
   "FindInFilesFilter"=dword:00000001
   "NotOpenFileFilter"=dword:00000000
   "SortPriority"=dword:000003e8
\{C061DB26-5833-11D2-96F5-000000000000}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (Second GUID indicates the registered project type for the Add Items templates.)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`FigPrj Project`|Nome padrão dos projetos deste tipo.|
|`DisplayName`|REG_SZ|`#%IDS_PROJECT_TYPE%`|ID de recurso do nome a ser recuperado da DLL satélite registrada em pacotes.|
|`Package`|REG_SZ|`%CLSID_Package%`|ID de classe do VSPackage registrado em pacotes.|
|`ProjectTemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|Caminho padrão dos arquivos de modelo de projeto. Esses são os arquivos exibidos pelo novo modelo de projeto.|
|`ItemTemplatesDir`|REG_SZ|`%TEMPLATE_PATH% \FigPrjProjectItems`|Caminho padrão dos arquivos de modelo de item de projeto. Esses são os arquivos exibidos pelo novo modelo de adição de item.|
|`DisplayProjectFileExtensions`|REG_SZ|`#%IDS_DISPLAY_PROJ_FILE_EXT%`|Permite que o IDE implemente a caixa de diálogo **abrir** .|
|`PossibleProjectExtensions`|REG_SZ|`figp`|Usado pelo IDE para determinar se o projeto que está sendo aberto é tratado por esse tipo de projeto (fábrica de projetos). O formato de mais de uma entrada é uma lista delimitada por ponto e vírgula. Por exemplo, "vdproj; VDP".|
|`DefaultProjectExtension`|REG_SZ|`.figp`|Usado pelo IDE como a extensão de nome de arquivo padrão para a operação salvar como.|
|`Filter Settings`|REG_DWORD|Vários, consulte as instruções e comentários após a tabela.|Essas configurações são usadas para definir os vários filtros para exibir arquivos em caixas de diálogo da interface do usuário.|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|ID do recurso para adicionar modelos de item.|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|Caminho dos itens de projeto exibidos na caixa de diálogo para o modelo **Adicionar novo item** .|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|Determina a ordem de classificação no nó de árvore dos arquivos exibidos na caixa de diálogo **Adicionar novo item** .|

 A tabela a seguir mostra as opções de filtros disponíveis no segmento de código anterior.

|Opção de filtro|Descrição|
|-------------------|-----------------|
|`CommonFindFilesFilter`|Indica que o filtro é um dos filtros comuns na caixa de diálogo **localizar nos arquivos** . Os filtros comuns são listados na lista de filtros antes que os filtros não sejam marcados como comuns.|
|`CommonOpenFilesFilter`|Indica que o filtro é um dos filtros comuns na caixa de diálogo **Abrir arquivo** . Os filtros comuns são listados na lista de filtros antes que os filtros não sejam marcados como comuns.|
|`FindInFilesFilter`|Indica que o filtro será um dos filtros na caixa de diálogo **localizar nos arquivos** e será listado após os filtros comuns.|
|`NotOpenFileFilter`|Indica que o filtro não será usado na caixa de diálogo **Abrir arquivo** .|
|`NotAddExistingItemFilter`|Indica que o filtro não será usado na caixa de diálogo Adicionar **Item existente** .|

 Por padrão, se um filtro não tiver um ou mais desses sinalizadores definidos, o filtro será usado na caixa de diálogo **Adicionar item existente** e na caixa de diálogo **Abrir arquivo** depois que os filtros comuns forem listados. O filtro não é usado na caixa de diálogo **localizar nos arquivos** .

 Todos os exemplos a seguir estão localizados no registro na chave [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects].

## <a name="example-4"></a>Exemplo 4

```
{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4} (The CLSID for Enterprise Projects)
\{FE3BBBB6-72D5-11d2-9ACE-00C04F79A2A4}\AddItemTemplates\TemplateDirs\ {ACEF4EB2-57CF-11D2-96F4-000000000000}\1 (CLSID for projects of this type)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_ TEMPLATES_ENTRY%`|ID do recurso para novos modelos de projeto.|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|Caminho padrão para projetos do tipo de projeto registrado.|
|`SortPriority`|REG_DWORD|`41 (x29)`|Define a ordem de classificação dos projetos exibidos na caixa de diálogo Assistente de novos projetos.|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 indica que os projetos desse tipo são exibidos apenas na caixa de diálogo novo projeto.|

 Todos os exemplos a seguir estão localizados no registro na chave [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Projects].

## <a name="example-5"></a>Exemplo 5

```
\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3} (CLSID for Miscellaneous Files projects)
   @="Miscellaneous Files Project"
\AddItemTemplates\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1
                                 (CLSID for Figures Project projects)
   @="#6"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\                    FigPrjProjectItems"
   "SortPriority"=dword:00000064
```

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|Nenhum|Valor padrão que indica que as entradas a seguir são para as entradas de projetos de arquivos diversos.|
|`@`|REG_SZ|`#%IDS_ADDITEM_TEMPLATES_ENTRY%`|Valor da ID do recurso para adicionar novos itens de modelo arquivos.|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjectItems`|Caminho padrão dos itens que serão exibidos na caixa de diálogo **Adicionar novo item** .|
|`SortPriority`|REG_DWORD|`100 (vcprx64)`|Estabelece a ordem de classificação para exibição no nó de árvore da caixa de diálogo **Adicionar novo item** .|

 O exemplo a seguir está localizado no registro na chave [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\Menus].

## <a name="example-6"></a>Exemplo 6

```
"{ACEF4EB2-57CF-11D2-96F4-000000000000}"=",1000,1"
```

 A entrada de menu aponta o IDE para o recurso usado para recuperar as informações do menu. Quando esses dados tiverem sido mesclados no banco de dado de menu, a mesma chave será adicionada na seção MenusMerged do registro. O VSPackage não deve modificar nada na seção MenusMerged diretamente. No campo de dados na tabela a seguir, há três campos separados por vírgulas. O primeiro campo identifica um caminho completo de um arquivo de recurso de menu:

- Se o primeiro campo for omitido, o recurso de menu será carregado a partir da DLL satélite identificada pelo GUID VSPackage.

  O segundo campo identifica uma ID de recurso de menu do tipo CTMENU:

- Se a ID do recurso for especificada e o caminho do arquivo for fornecido pelo primeiro parâmetro, um recurso de menu será carregado a partir do caminho de arquivo completo.

- Se a ID do recurso for fornecida, mas o caminho do arquivo não for, o recurso de menu será carregado a partir da DLL satélite.

- Se o caminho completo do arquivo for fornecido e a ID do recurso for omitida, espera-se que o arquivo a ser carregado seja um arquivo do CTO.

  O último campo identifica o número de versão do recurso CTMENU. Você pode mesclar o menu novamente alterando o número de versão.

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|% CLSID_Package%|REG_SZ|`,1000,1`|O recurso para recuperar as informações do menu.|

 Todos os exemplos a seguir estão localizados no registro na chave [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\NewProjectTemplates].

```
\TemplateDirs\{ACEF4EB2-57CF-11D2-96F4-000000000000}\1                (CLSID for Figures Project projects)
   @="#7"
   "TemplatesDir"="<Visual Studio SDK installation path>\\VSIntegration\\Archive9.0\\FigPkgs\\FigPrj\\FigPrjProjects"
   "SortPriority"=dword:00000029
   "NewProjectDialogOnly"=dword:00000000
```

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|`@`|REG_SZ|`#%IDS_NEWPROJ_TEMPLATES_ENTRY%`|Valor da ID do recurso para o projeto de figuras novos modelos de projeto.|
|`TemplatesDir`|REG_SZ|`%TEMPLATE_PATH%\FigPrjProjects`|Caminho padrão do novo diretório de projetos. Os itens neste diretório serão exibidos na caixa de diálogo **Assistente de novo projeto** .|
|`SortPriority`|REG_DWORD|`41 (x29)`|Estabelece a ordem na qual os projetos serão exibidos no nó de árvore da caixa de diálogo **novo projeto** .|
|`NewProjectDialogOnly`|REG_DWORD|`0`|0 indica que os projetos desse tipo são exibidos apenas na caixa de diálogo **novo projeto** .|

 O exemplo a seguir está localizado no registro na chave [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0Exp\InstalledProducts].

```
\FiguresProductSample
   "Package"="{ACEF4EB2-57CF-11D2-96F4-000000000000}"
   "UseInterface"=dword:00000001
```

|Nome|Type|Dados|Descrição|
|----------|----------|----------|-----------------|
|`Package`|REG_SZ|`%CLSID_Package%`|ID de classe do VSPackage registrado.|
|`UseInterface`|REG_DWORD|`1`|1 indica que a interface do usuário será usada para interagir com este projeto. 0 indica que não há interface de interface do usuário.|

 Os arquivos. vsz que controlam os novos tipos de projeto com frequência contêm uma entrada de RELATIVE_PATH. Esse caminho é relativo ao caminho especificado na entrada \ProductDir do tipo de projeto na seguinte chave de instalação:

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup

 Por exemplo, os modelos de projeto do Enterprise Frameworks adicionam as seguintes entradas de registro:

 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\7.0Exp\Setup\EF\ProductDir = C:\Program Files\Microsoft Visual Studio\EnterpriseFrameworks\

 Isso significa que se você incluir uma entrada PROJECT_TYPE = EF no arquivo. vsz, o ambiente localizará os arquivos. vsz no diretório ProductDir especificado anteriormente.

## <a name="see-also"></a>Confira também
- [Lista de verificação: Criando tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Elementos de um modelo de projeto](../../extensibility/internals/elements-of-a-project-model.md)
- [Criando instâncias de projeto por meio de fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
