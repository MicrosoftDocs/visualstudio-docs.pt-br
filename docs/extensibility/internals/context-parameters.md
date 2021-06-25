---
title: Parâmetros de contexto | Microsoft Docs
description: Saiba mais sobre parâmetros de contexto no IDE (ambiente de desenvolvimento integrado) do Visual Studio que definem o estado de um projeto quando você adiciona ou implementa um assistente.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- wizards, context parameters
- context parameters
ms.assetid: 1a062dcb-8a8f-40dd-bea9-3d10f9448966
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 536e5abf92884c5c19399e73b4e1773e66919657
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898221"
---
# <a name="context-parameters"></a>Parâmetros de contexto
No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado), você pode adicionar assistentes às caixas de diálogo **novo projeto**, **Adicionar novo item** ou **Adicionar subprojeto** . Os assistentes adicionados estão disponíveis no menu **arquivo** ou clicando com o botão direito do mouse em um projeto no **Gerenciador de soluções**. O IDE passa parâmetros de contexto para a implementação do assistente. Os parâmetros de contexto definem o estado do projeto quando o IDE chama o assistente.

 O IDE inicia os assistentes definindo o <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> sinalizador na chamada do IDE para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> método do projeto. Quando definido, o projeto deve fazer com que o `IVsExtensibility::RunWizardFile` método seja executado usando o nome do assistente registrado ou GUID e outros parâmetros de contexto que o IDE passa para ele.

## <a name="context-parameters-for-new-project"></a>Parâmetros de contexto para novo projeto

| Parâmetro | Descrição |
|-------------------------| - |
| `WizardType` | Tipo de assistente registrado ( <xref:EnvDTE.Constants.vsWizardNewProject> ) ou o GUID que indica o tipo de assistente. Na [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] implementação, o GUID do assistente é {0F90E1D0-4999-11D1-B6D1-00A0C90F2744}. |
| `ProjectName` | Uma cadeia de caracteres que é o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] nome do projeto exclusivo. |
| `LocalDirectory` | Local local dos arquivos de projeto de trabalho. |
| `InstallationDirectory` | Caminho do diretório da [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] instalação do is. |
| `FExclusive` | Sinalizador booliano que indica que o projeto deve fechar soluções abertas. |
| `SolutionName` | Nome do arquivo de solução sem a parte do diretório ou a extensão *. sln* . O nome do arquivo *. suo* também é criado usando `SolutionName` . Quando esse argumento não é uma cadeia de caracteres vazia, o assistente usa <xref:EnvDTE._Solution.Create%2A> antes de adicionar o projeto com o <xref:EnvDTE._Solution.AddFromTemplate%2A> . Se esse nome for uma cadeia de caracteres vazia, use <xref:EnvDTE._Solution.AddFromTemplate%2A> sem chamar <xref:EnvDTE._Solution.Create%2A> . |
| `Silent` | Booliano que indica se o assistente deve ser executado silenciosamente como se o **término** fosse clicado ( `TRUE` ). |

## <a name="context-parameters-for-add-new-item"></a>Parâmetros de contexto para adicionar novo item

| Parâmetro | Descrição |
|-------------------------| - |
| `WizardType` | Tipo de assistente registrado ( <xref:EnvDTE.Constants.vsWizardAddItem> ) ou o GUID que indica o tipo de assistente. Na [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] implementação, o GUID do assistente é {0F90E1D1-4999-11D1-B6D1-00A0C90F2744}. |
| `ProjectName` | Uma cadeia de caracteres que é o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] nome do projeto exclusivo. |
| `ProjectItems` | Localização local que contém arquivos de projeto de trabalho. |
| `ItemName` | Nome do item a ser adicionado. Esse nome é o nome de arquivo padrão ou o nome do arquivo que o usuário digita na caixa de diálogo **Adicionar itens** . O nome é baseado nos sinalizadores que são definidos no arquivo *. vsdir* . O nome pode ser um valor nulo. |
| `InstallationDirectory` | Caminho do diretório da [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] instalação do is. |
| `Silent` | Booliano que indica se o assistente deve ser executado silenciosamente como se o **término** fosse clicado ( `TRUE` ). |

## <a name="context-parameters-for-add-sub-project"></a>Parâmetros de contexto para Add sub Project

| Parâmetro | Descrição |
|-------------------------| - |
| `WizardType` | Tipo de assistente registrado ( <xref:EnvDTE.Constants.vsWizardAddSubProject> ) ou o GUID que indica o tipo de assistente. Na [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] implementação, o GUID do assistente é {0F90E1D2-4999-11D1-B6D1-00A0C90F2744}. |
| `ProjectName` | Uma cadeia de caracteres que é o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] nome do projeto exclusivo. |
| `ProjectItems` | Ponteiro para a `ProjectItems` coleção na qual o assistente Opera. Esse ponteiro é passado para o assistente com base na seleção de hierarquia do projeto. Um usuário normalmente seleciona uma pasta na qual colocar o item e, em seguida, chama a caixa de diálogo **Adicionar item** do projeto. |
| `LocalDirectory` | Local local dos arquivos de projeto de trabalho. |
| `ItemName` | Nome do item a ser adicionado. Esse nome é o nome de arquivo padrão ou o nome do arquivo que o usuário digita na caixa de diálogo **Adicionar itens** . O nome é baseado nos sinalizadores que são definidos no arquivo *. vsdir* . O nome pode ser um valor nulo. |
| `InstallationDirectory` | Caminho do diretório da [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] instalação. |
| `Silent` | Booliano que indica se o assistente deve ser executado silenciosamente como se o **término** fosse clicado ( `TRUE` ). |

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- [Parâmetros personalizados](../../extensibility/internals/custom-parameters.md)
- [Assistentes](../../extensibility/internals/wizards.md)
- [Arquivo do assistente (. vsz)](../../extensibility/internals/wizard-dot-vsz-file.md)
- [Parâmetros de contexto para iniciar assistentes](/previous-versions/tz690efs(v=vs.140))