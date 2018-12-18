---
title: Itens de projeto comuns do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, common project items
ms.assetid: 1eba3721-cc12-4b80-9987-84923ede5e2e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: dd3b51046ce3a4b589cb77ce27d1e103a6b8a6c5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937506"
---
# <a name="common-msbuild-project-items"></a>Itens de projeto comuns do MSBuild
Em [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)], um item é uma referência nomeada a um ou mais arquivos. Itens contêm metadados, como nomes de arquivos, caminhos e números de versão. Todos os tipos de projeto em [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] têm vários itens em comum. Esses itens são definidos no arquivo *Microsoft.Build.CommonTypes.xsd*.  

## <a name="common-items"></a>Itens comuns  
 Esta é uma lista de todos os itens de projeto em comum.  

### <a name="reference"></a>Referência  
 Representa uma referência de assembly (gerenciado) no projeto.  

|Nome de metadados de item|Descrição|  
|---------------|-----------------|  
|HintPath|Cadeia de caracteres opcional. O caminho relativo ou absoluto do assembly.|  
|Nome|Cadeia de caracteres opcional. O nome de exibição do assembly, por exemplo, “System.Windows.Forms.”|  
|FusionName|Cadeia de caracteres opcional. Especifica o nome de fusão simples ou forte para o item.<br /><br /> Quando esse atributo estiver presente, é possível economizar tempo, pois o arquivo do assembly não precisa ser aberto para obter o nome de fusão.|  
|SpecificVersion|Booliano opcional. Especifica se apenas a versão no nome de fusão deve ser referenciada.|  
|Aliases|Cadeia de caracteres opcional. Quaisquer aliases da referência.|  
|Particular|Booliano opcional. Especifica se a referência deve ser copiada para a pasta de saída. Esse atributo corresponde à propriedade **Copiar Local** da referência que está no Visual Studio IDE.|  

### <a name="comreference"></a>COMReference  
 Representa uma referência a um componente COM (não gerenciado) no projeto.  

|Nome de metadados de item|Descrição|  
|---------------|-----------------|  
|Nome|Cadeia de caracteres opcional. O nome de exibição do componente.|  
|Guid|Cadeia de caracteres opcional. Um GUID para o componente, no formato {12345678-1234-1234-1234-1234567891234}.|  
|VersionMajor|Cadeia de caracteres opcional. A parte principal do número de versão do componente. Por exemplo, “5” se o número de versão completo for “5,46”.|  
|VersionMinor|Cadeia de caracteres opcional. A parte secundária do número de versão do componente. Por exemplo, “46” se o número de versão completo for “5,46”.|  
|LCID|Cadeia de caracteres opcional. O LocaleID do componente.|  
|WrapperTool|Cadeia de caracteres opcional. O nome da ferramenta wrapper usada no componente, por exemplo, “tlbimp”.|  
|Isolada|Booliano opcional. Especifica se o componente é um componente sem registro.|  

### <a name="comfilereference"></a>COMFileReference  
 Representa uma lista de bibliotecas de tipo que alimentam o destino ResolvedComreference.  

|Nome de metadados de item|Descrição|  
|---------------|-----------------|  
|WrapperTool|Cadeia de caracteres opcional. O nome da ferramenta wrapper usada no componente, por exemplo, “tlbimp”.|  

### <a name="nativereference"></a>NativeReference  
 Representa um arquivo de manifesto nativo ou uma referência a esse arquivo.  

|Nome de metadados de item|Descrição|  
|---------------|-----------------|  
|Nome|Cadeia de caracteres obrigatória. O nome de base do arquivo de manifesto.|  
|HintPath|Cadeia de caracteres obrigatória. O caminho relativo do arquivo de manifesto.|  

### <a name="projectreference"></a>ProjectReference  
 Representa uma referência a outro projeto.  

|Nome de metadados de item|Descrição|  
|---------------|-----------------|  
|Nome|Cadeia de caracteres opcional. O nome de exibição da referência.|  
|Projeto|Cadeia de caracteres opcional. Um GUID para a referência, no formato {12345678-1234-1234-1234-1234567891234}.|  
|Pacote|Cadeia de caracteres opcional. O caminho do arquivo de projeto que está sendo referenciado.|  
|ReferenceOutputAssembly|Booliano opcional. Se estiver definido como `false`, não inclui a saída do projeto referenciado como uma [referência](#Reference) deste projeto, mas ainda garante que o outro projeto seja compilado antes desse. Assume o padrão de `true`.|

### <a name="compile"></a>Compilar  
 Representa os arquivos de origem do compilador.  


| Nome de metadados de item | Descrição |
|-----------------------| - |
| DependentUpon | Cadeia de caracteres opcional. Especifica o arquivo do qual esse arquivo depende para compilar corretamente. |
| AutoGen | Booliano opcional. Indica se o arquivo foi gerado para o projeto pelo ambiente de desenvolvimento integrado (IDE) [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. |
| Link | Cadeia de caracteres opcional. O caminho de notação a ser exibido quando o arquivo está fisicamente fora da influência do arquivo de projeto. |
| Visível | Booliano opcional. Indica se o arquivo no **Gerenciador de Soluções** deve ser exibido no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. |
| CopyToOutputDirectory | Cadeia de caracteres opcional. Determina se o arquivo deve ser copiado para o diretório de saída. Os valores são:<br /><br /> 1.  Nunca<br />2.  Sempre<br />3.  PreserveNewest |

### <a name="embeddedresource"></a>EmbeddedResource  
 Representa os recursos a serem inseridos no assembly gerado.  


| Nome de metadados de item | Descrição |
|-----------------------| - |
| DependentUpon | Cadeia de caracteres opcional. Especifica o arquivo do qual esse arquivo depende para compilar corretamente |
| Gerador | Cadeia de caracteres obrigatória. O nome de qualquer gerador de arquivo executado nesse item. |
| LastGenOutput | Cadeia de caracteres obrigatória. O nome do arquivo criado por qualquer gerador de arquivo executado nesse item. |
| CustomToolNamespace | Cadeia de caracteres obrigatória. O namespace no qual qualquer gerador de arquivo executado nesse item deve criar código. |
| Link | Cadeia de caracteres opcional. O caminho de notação será exibido se o arquivo estiver localizado fisicamente fora da influência do projeto. |
| Visível | Booliano opcional. Indica se o arquivo no **Gerenciador de Soluções** deve ser exibido no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. |
| CopyToOutputDirectory | Cadeia de caracteres opcional. Determina se o arquivo deve ser copiado para o diretório de saída. Os valores são:<br /><br /> 1.  Nunca<br />2.  Sempre<br />3.  PreserveNewest |
| LogicalName | Cadeia de caracteres obrigatória. O nome lógico do recurso inserido. |

### <a name="content"></a>Conteúdo  
 Representa os arquivos não compilados no projeto, mas pode ser inserido ou publicado junto com ele.  


| Nome de metadados de item | Descrição |
|-----------------------| - |
| DependentUpon | Cadeia de caracteres opcional. Especifica o arquivo do qual esse arquivo depende para compilar corretamente. |
| Gerador | Cadeia de caracteres obrigatória. O nome de qualquer gerador de arquivo executado nesse item. |
| LastGenOutput | Cadeia de caracteres obrigatória. O nome do arquivo criado por qualquer gerador de arquivo executado nesse item. |
| CustomToolNamespace | Cadeia de caracteres obrigatória. O namespace no qual qualquer gerador de arquivo executado nesse item deve criar código. |
| Link | Cadeia de caracteres opcional. O caminho de notação a ser exibido se o arquivo estiver localizado fisicamente fora da influência do projeto. |
| PublishState | Cadeia de caracteres obrigatória. O estado de publicação do conteúdo, seja:<br /><br /> -   Padrão<br />-   Incluído<br />-   Excluído<br />-   DataFile<br />-   Pré-requisito |
| IsAssembly | Booliano opcional. Especifica se o arquivo é um assembly. |
| Visível | Booliano opcional. Indica se o arquivo no **Gerenciador de Soluções** deve ser exibido no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. |
| CopyToOutputDirectory | Cadeia de caracteres opcional. Determina se o arquivo deve ser copiado para o diretório de saída. Os valores são:<br /><br /> 1.  Nunca<br />2.  Sempre<br />3.  PreserveNewest |

### <a name="none"></a>Nenhum  
 Representa arquivos que não devem ter função no processo de build.  


| Nome de metadados de item | Descrição |
|-----------------------| - |
| DependentUpon | Cadeia de caracteres opcional. Especifica o arquivo do qual esse arquivo depende para compilar corretamente. |
| Gerador | Cadeia de caracteres obrigatória. O nome de qualquer gerador de arquivo executado nesse item. |
| LastGenOutput | Cadeia de caracteres obrigatória. O nome do arquivo criado por qualquer gerador de arquivo executado nesse item. |
| CustomToolNamespace | Cadeia de caracteres obrigatória. O namespace no qual qualquer gerador de arquivo executado nesse item deve criar código. |
| Link | Cadeia de caracteres opcional. O caminho de notação a ser exibido se o arquivo estiver localizado fisicamente fora da influência do projeto. |
| Visível | Booliano opcional. Indica se o arquivo no **Gerenciador de Soluções** deve ser exibido no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. |
| CopyToOutputDirectory | Cadeia de caracteres opcional. Determina se o arquivo deve ser copiado para o diretório de saída. Os valores são:<br /><br /> 1.  Nunca<br />2.  Sempre<br />3.  PreserveNewest |

### <a name="baseapplicationmanifest"></a>BaseApplicationManifest  
 Representa o manifesto do aplicativo base do build e contém [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] informações de segurança de implantação.  

### <a name="codeanalysisimport"></a>CodeAnalysisImport  
 Representa o projeto do FxCop a ser importado.  

### <a name="import"></a>Importar  
 Representa assemblies cujos namespaces devem ser importados pelo compilador [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)].  

## <a name="see-also"></a>Consulte também  
 [Propriedades de projeto comuns do MSBuild](../msbuild/common-msbuild-project-properties.md)
