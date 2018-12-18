---
title: Especificando o local do arquivo VSPackage ao Shell do VS | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, file location
- VSPackages, managed package file location
ms.assetid: beb8607a-4183-4ed2-9ac8-7527f11513b1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 63948a464a43284f3b9205d185e4b0a4e39155e4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49856230"
---
# <a name="specifying-vspackage-file-location-to-the-vs-shell"></a>Especificando o local do arquivo do VSPackage para o Shell do VS
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] deve ser capaz de localizar a DLL para carregar o VSPackage do assembly. Você pode localizá-lo de várias maneiras, conforme descrito na tabela a seguir.  


| Método | Descrição |
| - | - |
| Use a chave de registro de base de código. | A chave de base de código pode ser usada para direcionar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para carregar o assembly de VSPackage a partir de qualquer caminho de arquivo totalmente qualificado. O valor da chave deve ser o caminho de arquivo para a DLL. Isso é a melhor maneira de ter [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] carregar seu assembly de pacote. Às vezes, essa técnica é conhecida como a "técnica de diretório de instalação de base de código/privadas". Durante o registro o valor da Base de código é passado para as classes de atributo de registro por meio de uma instância das <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute.RegistrationContext> tipo. |
| Colocar a DLL para o **PrivateAssemblies** directory. | Coloque o assembly na **PrivateAssemblies** subdiretório do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] directory. Assemblies localizados no **PrivateAssemblies** são detectadas automaticamente, mas não são visíveis na **Add References** caixa de diálogo. A diferença entre **PrivateAssemblies** e **PublicAssemblies** são que os assemblies no **PublicAssemblies** são enumerados no **adicionar referências**  caixa de diálogo. Se você optou por não usar a técnica de "diretório de instalação de base de código/privada", você deve instalar para o **PrivateAssemblies** directory. |
| Use um assembly de nome forte e a chave do registro de Assembly. | A chave do Assembly pode ser usada para direcionar explicitamente [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para carregar um forte chamado assembly VSPackage. O valor da chave deve ser o nome forte do assembly. |
| Colocar a DLL para o **PublicAssemblies** directory. | Por fim, o assembly também pode ser colocado na **PublicAssemblies** subdiretório. Assemblies localizados no **PublicAssemblies** são detectados automaticamente e também aparecerão na **Add References** da caixa de diálogo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].<br /><br /> Assemblies de VSPackage só devem ser colocados na **PublicAssemblies** gerenciados de diretório se eles contêm componentes que se destinam a ser reutilizado por outros desenvolvedores de VSPackage. A maioria dos assemblies não atende a esse critério. |

> [!NOTE]
>  Use assemblies de nome forte, assinados para todos os assemblies dependentes. Esses assemblies também devem ser instalados em seu próprio diretório ou cache de assembly global (GAC). Isso protege contra conflitos com assemblies que têm o mesmo nome de arquivo base, conhecido como associação de nome fraco.