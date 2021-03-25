---
title: Especificando o local do arquivo VSPackage para o Shell do VS | Microsoft Docs
description: Saiba como você pode possibilitar que o Visual Studio localize a DLL do assembly para carregar o VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: efec1ac3f7ccb3884265f3740108aaef261e9378
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064055"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>Especificando o local do arquivo do VSPackage para o Shell do VS
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] deve ser capaz de localizar a DLL do assembly para carregar o VSPackage. Você pode localizá-lo de várias maneiras, conforme descrito na tabela a seguir.

| Método | Descrição |
| - | - |
| Use a chave do registro CodeBase. | A chave CodeBase pode ser usada para direcionar a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] carga do assembly VSPackage de qualquer caminho de arquivo totalmente qualificado. O valor da chave deve ser o caminho do arquivo para a DLL. Essa é a melhor maneira de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] carregar o assembly do pacote. Essa técnica, às vezes, é conhecida como a "técnica do diretório de instalação privada/CodeBase". Durante o registro, o valor da codebase é passado para as classes de atributo de registro por meio de uma instância do <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext> tipo. |
| Coloque a DLL no diretório **PrivateAssemblies** | Coloque o assembly no subdiretório **PrivateAssemblies** do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] diretório. Os assemblies localizados em **PrivateAssemblies** são detectados automaticamente, mas não são visíveis na caixa de diálogo **Adicionar referências** . A diferença entre **PrivateAssemblies** e **PublicAssemblies** é que os assemblies em **PublicAssemblies** são enumerados na caixa de diálogo **Adicionar referências** . Se você optou por não usar a técnica "CodeBase/diretório de instalação privada", deverá instalar o no diretório **PrivateAssemblies** |
| Use um assembly de nome forte e a chave do registro do assembly. | A chave do assembly pode ser usada para direcionar explicitamente o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] carregamento de um assembly nomeado VSPackage forte. O valor da chave deve ser o nome forte do assembly. |
| Coloque a DLL no diretório **PublicAssemblies** | Por fim, o assembly também pode ser colocado no subdiretório **PublicAssemblies** . Os assemblies localizados em **PublicAssemblies** são detectados automaticamente e também serão exibidos na caixa de diálogo **Adicionar referências** no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .<br /><br /> Os assemblies VSPackage só devem ser colocados no diretório **PublicAssemblies** se contiverem componentes gerenciados que devem ser reutilizados por outros desenvolvedores de VSPackage. A maioria dos assemblies não atende a esse critério. |

> [!NOTE]
> Use assemblies com nomes fortes e assinados para todos os seus assemblies dependentes. Esses assemblies também devem ser instalados em seu próprio diretório ou no GAC (cache de assembly global). Isso protege contra conflitos com assemblies que têm o mesmo nome de arquivo base, conhecido como associação de nome fraco.
