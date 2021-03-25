---
title: Registrando verbos para extensões de nome de arquivo | Microsoft Docs
description: Saiba como registrar um verbo associado a um identificador programático para uma extensão de nome de arquivo usando uma chave de Shell.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, registering
ms.assetid: 81a58e40-7cd0-4ef4-a475-c4e1e84d6e06
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9936efc2e01c0d82d5cc9fce140d543eb95247ad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068473"
---
# <a name="register-verbs-for-file-name-extensions"></a>Registrar verbos para extensões de nome de arquivo
A associação de uma extensão de nome de arquivo com um aplicativo geralmente tem uma ação preferida que ocorre quando um usuário clica duas vezes em um arquivo. Essa ação preferencial é vinculada a um verbo, por exemplo, abrir, que corresponde à ação.

 Você pode registrar os verbos associados a um identificador programático (ProgID) para uma extensão usando a chave do Shell localizada em **HKEY_CLASSES_ROOT \{ ProgID} \Shell**. Para obter mais informações, consulte [tipos de arquivo](/windows/desktop/shell/fa-file-types).

## <a name="register-standard-verbs"></a>Registrar verbos padrão
 O sistema operacional reconhece os seguintes verbos padrão:

- Aberto

- Editar

- Reproduzir

- Imprimir

- Visualização

  Sempre que possível, registre um verbo padrão. A escolha mais comum é o verbo Open. Use o verbo editar somente se houver uma diferença clara entre abrir o arquivo e editar o arquivo. Por exemplo, abrir um arquivo *. htm* o exibe no navegador, enquanto a edição de um arquivo *. htm* inicia um editor de HTML. Os verbos padrão são localizados com a localidade do sistema operacional.

> [!NOTE]
> Ao registrar verbos padrão, não defina o valor padrão para a chave aberta. O valor padrão contém a cadeia de caracteres de exibição no menu. O sistema operacional fornece essa cadeia de caracteres para verbos padrão.

 Os arquivos de projeto devem ser registrados para iniciar uma nova instância do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] quando um usuário abrir o arquivo. O exemplo a seguir ilustra um registro de verbo padrão para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] projeto.

```
[HKEY_CLASSES_ROOT\.csproj]
@="VisualStudio.csproj.8.0"

[HKEY_CLASSES_ROOT\.csproj\OpenWithList]
[HKEY_CLASSES_ROOT\.csproj\OpenWithList\VSLauncher.exe]
@=""

[HKEY_CLASSES_ROOT\.csproj\OpenWithProgids]
"VisualStudio.csproj.8.0"=""

[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open]
[HKEY_CLASSES_ROOT\Applications\VSLauncher.exe\Shell\Open\Command]
@="C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0]
@="C# Project file"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,0"

[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.csproj.8.0\shell\Open\Command]
@="\"C:\\Program Files\\Common Files\\Microsoft Shared\\MSEnv\\VSLauncher.exe\" \"%1\""
```

 Para abrir um arquivo em uma instância existente do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] , registre uma chave DDEEXEC. O exemplo a seguir ilustra um registro de verbo padrão para um [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] arquivo *. cs* .

```
[HKEY_CLASSES_ROOT\.cs]
@="VisualStudio.cs.8.0"

[HKEY_CLASSES_ROOT\.cs\OpenWithList]
[HKEY_CLASSES_ROOT\.cs\OpenWithList\devenv.exe]
@=""

[HKEY_CLASSES_ROOT\.cs\OpenWithProgids]
"VisualStudio.cs.8.0"=""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0]
@="C# Source file"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\DefaultIcon]
@="C:\\VisualStudioPath\\VC#\\VCSPackages\\csproj.dll,1"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open]
[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\Command]
@="\"C:\\VisualStudioPath\\Common7\\IDE\\devenv.exe\" /dde \"%1\""

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec]
@="Open(\"%1\")"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Application]
@="VisualStudio.8.0"

[HKEY_CLASSES_ROOT\VisualStudio.cs.8.0\shell\Open\ddeexec\Topic]
@="system"
```

## <a name="set-the-default-verb"></a>Definir o verbo padrão
 O verbo padrão é a ação que é executada quando um usuário clica duas vezes em um arquivo no Windows Explorer. O verbo padrão é o verbo especificado como o valor padrão para a chave **HKEY_CLASSES_ROOT \\ *ProgID*\Shell** . Se nenhum valor for especificado, o verbo padrão será o primeiro verbo especificado na lista de chaves **HKEY_CLASSES_ROOT \\ *ProgID*\Shell** .

> [!NOTE]
> Se você planeja alterar o verbo padrão para uma extensão em uma implantação lado a lado, considere o impacto na instalação e remoção. Durante a instalação, o valor padrão original é substituído.

## <a name="see-also"></a>Confira também
- [Gerenciar associações de arquivos lado a lado](../extensibility/managing-side-by-side-file-associations.md)
