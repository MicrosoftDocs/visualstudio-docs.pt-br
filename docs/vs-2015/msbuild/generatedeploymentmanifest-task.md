---
title: Tarefa GenerateDeploymentManifest | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateDeploymentManifest
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateDeploymentManifest task
- GenerateDeploymentManifest task [MSBuild]
ms.assetid: 0734ebda-734d-49c4-9642-8d9d919d45fd
caps.latest.revision: 32
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8ad0b9919c5c567662d78573573f1bf046c93552
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49261879"
---
# <a name="generatedeploymentmanifest-task"></a>Tarefa GenerateDeploymentManifest
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Gera um manifesto de implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. Um manifesto de implantação do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] descreve a implantação de um aplicativo definindo uma identidade exclusiva para a implantação, identificando as características de implantação tais como o modo online ou da instalação, especificando as configurações de atualização do aplicativo e locais de atualização e indicando o manifesto do aplicativo do [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] correspondente.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `GenerateDeploymentManifest`.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`AssemblyName`|Parâmetro `String` opcional.<br /><br /> Especifica o campo `Name` da identidade do assembly para o manifesto gerado. Se esse parâmetro não for especificado, o nome será inferido com base nos parâmetros `EntryPoint` ou `InputManifest`. Se não for possível inferir o nome, a tarefa gerará um erro.|  
|`AssemblyVersion`|Parâmetro `String` opcional.<br /><br /> Especifica o campo `Version` da identidade do assembly para o manifesto gerado. Se esse parâmetro não for especificado, a tarefa usará o valor "1.0.0.0".|  
|`CreateDesktopShortcut`|Parâmetro `Boolean` opcional.<br /><br /> Se for verdadeiro, será criado um ícone na área de trabalho durante a instalação do aplicativo ClickOnce.|  
|`DeploymentUrl`|Parâmetro `String` opcional.<br /><br /> Especifica o local de atualização para o aplicativo. Se esse parâmetro não for especificado, nenhum local de atualização será definido para o aplicativo. No entanto, se o parâmetro `UpdateEnabled` for `true`, o local da atualização deverá ser especificado. O valor especificado deve ser um caminho de URL ou UNC totalmente qualificado.|  
|`Description`|Parâmetro `String` opcional.<br /><br /> Especifica uma descrição opcional para o aplicativo.|  
|`DisallowUrlActivation`|Parâmetro `Boolean` opcional.<br /><br /> Especifica se o aplicativo deve ser executado automaticamente quando ele é aberto por meio de uma URL. Se esse parâmetro for `true`, o aplicativo só poderá ser iniciado pelo menu Iniciar. O valor padrão desse parâmetro é `false`. Esta entrada só se aplica quando o valor do parâmetro `Install` é `true`.|  
|`EntryPoint`|Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.<br /><br /> Indica o ponto de entrada para o assembly do manifesto gerado. Para um manifesto de implantação [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)], esta entrada especifica o manifesto do aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)].<br /><br /> Em [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)], a [Tarefa GenerateApplicationManifest](../msbuild/generateapplicationmanifest-task.md) exigiu um `EntryPoint` para gerar um manifesto do aplicativo. (Manifestos de assembly ou nativos não exigem um `EntryPoint`.) Esse requisito foi imposto com o erro de build: “MSB3185: EntryPoint não especificado para o manifesto”.<br /><br /> [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] não emite esse erro quando o parâmetro da tarefa `EntryPoint` não é especificado. Em vez disso, a marca \<customHostSpecified> é inserida como um filho da marca \<entryPoint>, por exemplo:<br /><br /> `<entryPoint xmlns="urn:schemas-`<br /><br /> `microsoft-com:asm.v2">`<br /><br /> `<co.v1:customHostSpecified />`<br /><br /> `</entryPoint>`<br /><br /> Você pode adicionar dependências de DLL ao manifesto do aplicativo usando as seguintes etapas:<br /><br /> 1.  Resolver as referências de assembly com uma chamada para <xref:Microsoft.Build.Tasks.ResolveAssemblyReference>.<br />2.  Passar a saída da tarefa anterior e o próprio assembly para <xref:Microsoft.Build.Tasks.ResolveManifestFiles>.<br />3.  Passar as dependências usando o parâmetro `Dependencies` para <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>.|  
|`ErrorReportUrl`|Opcional [String] (<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) parâmetro.<br /><br /> Especifica a URL da página da Web que é exibida nas caixas de diálogo durante instalações ClickOnce.|  
|`InputManifest`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Indica um documento XML de entrada para servir como base para o gerador de manifesto. Isso permite que dados estruturados, tais como definições personalizadas de manifesto, sejam refletidos no manifesto de saída. O elemento raiz do documento XML deve ser um nó de assembly no namespace asmv1.|  
|`Install`|Parâmetro `Boolean` opcional.<br /><br /> Especifica se o aplicativo é um aplicativo instalado ou um aplicativo somente online. Se esse parâmetro for `true`, o aplicativo será instalado no menu Iniciar do usuário e poderá ser removido usando a caixa de diálogo Adicionar ou Remover Programas. Se esse parâmetro for `false`, o aplicativo será destinado ao uso online de uma página da Web. O valor padrão desse parâmetro é `true`.|  
|`MapFileExtensions`|Parâmetro `Boolean` opcional.<br /><br /> Especifica se o mapeamento da extensão de nome de arquivo .deploy é usado. Se esse parâmetro for `true`, cada arquivo de programa será publicado com uma extensão de nome de arquivo .deploy. Essa opção é útil para segurança do servidor Web limitar o número de extensões de nome de arquivo deve estar desbloqueada para habilitar a implantação do aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. O valor padrão desse parâmetro é `false`.|  
|`MaxTargetPath`|Parâmetro `String` opcional.<br /><br /> Especifica o comprimento máximo permitido de um caminho de arquivo em uma implantação de aplicativo [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. Se esse parâmetro for especificado, o comprimento de cada caminho de arquivo no aplicativo é verificado em relação a esse limite. Todos os itens que excedem o limite gerarão um aviso de build. Se essa entrada não for especificada ou for zero, nenhuma verificação será executada.|  
|`MinimumRequiredVersion`|Parâmetro `String` opcional.<br /><br /> Especifica se o usuário pode ignorar a atualização. Se o usuário tiver uma versão inferior à mínima necessária, ele não terá a opção de ignorar a atualização. Esta entrada se aplica somente se o valor do parâmetro `Install` for `true`.|  
|`OutputManifest`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> opcional.<br /><br /> Especifica o nome do arquivo de manifesto de saída gerado. Se esse parâmetro não for especificado, o nome do arquivo de saída será inferido com base na identidade do manifesto gerado.|  
|`Platform`|Parâmetro `String` opcional.<br /><br /> Especifica a plataforma de destino do aplicativo. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `AnyCPU`<br />-   `x86`<br />-   `x64`<br />-   `Itanium`<br /><br /> O valor padrão é `AnyCPU`.|  
|`Product`|Parâmetro `String` opcional.<br /><br /> Especifica o nome do aplicativo. Se esse parâmetro não for especificado, o nome será inferido com base na identidade do manifesto gerado. Esse nome é usado para o nome do atalho no menu Iniciar e faz parte do nome que aparece na caixa de diálogo Adicionar ou Remover Programas.|  
|`Publisher`|Parâmetro `String` opcional.<br /><br /> Especifica o editor do aplicativo. Se esse parâmetro não for especificado, o nome será inferido com base no usuário registrado ou na identidade do manifesto gerado. Esse nome é usado para o nome da pasta no menu Iniciar e faz parte do nome que aparece na caixa de diálogo Adicionar ou Remover Programas.|  
|`SuiteNamel`|Parâmetro `String` opcional.<br /><br /> Especifica o nome da pasta no menu Iniciar, em que o aplicativo encontra-se após a implantação ClickOnce.|  
|`SupportUrl`|Parâmetro `String` opcional.<br /><br /> Especifica o link exibido na caixa de diálogo Adicionar ou Remover Programas do aplicativo. O valor especificado deve ser um caminho de URL ou UNC totalmente qualificado.|  
|`TargetCulture`|Parâmetro `String` opcional.<br /><br /> Identifica a cultura do aplicativo e especifica o campo `Language` da identidade do assembly para o manifesto gerado. Se esse parâmetro não for especificado, presume-se que o aplicativo não varia conforme a cultura.|  
|`TrustUrlParameters`|Parâmetro `Boolean` opcional.<br /><br /> Especifica se os parâmetros de cadeia de caracteres de consulta da URL devem ser disponibilizados para o aplicativo. O valor padrão desse parâmetro é `false`, que indica que parâmetros não estarão disponíveis para o aplicativo.|  
|`UpdateEnabled`|Parâmetro `Boolean` opcional.<br /><br /> Indica se o aplicativo está habilitado para atualizações. O valor padrão desse parâmetro é `false`. Esse parâmetro se aplica somente se o valor do parâmetro `Install` for `true`.|  
|`UpdateInterval`|Parâmetro `Int32` opcional.<br /><br /> Especifica o intervalo de atualização para o aplicativo. O valor padrão desse parâmetro é zero. Este parâmetro se aplica somente a quando os valores dos parâmetros `Install` e `UpdateEnabled` são ambos `true`.|  
|`UpdateMode`|Parâmetro `String` opcional.<br /><br /> Especifica se as atualizações devem ser verificadas em primeiro plano, antes do aplicativo ser iniciado ou em segundo plano, enquanto o aplicativo está em execução. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `Foreground`<br />-   `Background`<br /><br /> O valor padrão desse parâmetro é `Background`. Este parâmetro se aplica somente a quando os valores dos parâmetros `Install` e `UpdateEnabled` são ambos `true`.|  
|`UpdateUnit`|Parâmetro `String` opcional.<br /><br /> Especifica as unidades para o parâmetro `UpdateInterval`. Esse parâmetro pode ter os seguintes valores:<br /><br /> -   `Hours`<br />-   `Days`<br />-   `Weeks`<br /><br /> Este parâmetro se aplica somente a quando os valores dos parâmetros `Install` e `UpdateEnabled` são ambos `true`.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.GenerateManifestBase>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista dos parâmetros da classe Task, consulte [Classe base Task](../msbuild/task-base-class.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Tarefa GenerateApplicationManifest](../msbuild/generateapplicationmanifest-task.md)   
 [Tarefa SignFile](../msbuild/signfile-task.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



