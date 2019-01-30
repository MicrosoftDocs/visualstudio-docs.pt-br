---
title: Destinos do MSBuild | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, targets
ms.assetid: 8060b4d2-e4a9-48cf-a437-852649ceb417
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b94c9a78d3541645edf959aedb295d1a2379ce3
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54978809"
---
# <a name="msbuild-targets"></a>Destinos do MSBuild
Destinos agrupam tarefas em uma ordem específica e permitem que o processo de build seja decomposto em unidades menores. Por exemplo, um destino pode excluir todos os arquivos no diretório de saída para se preparar para o build, enquanto outro compila as entradas para o projeto e as coloca no diretório vazio. Para obter mais informações sobre tarefas, consulte [Tarefas](../msbuild/msbuild-tasks.md).  
  
## <a name="declare-targets-in-the-project-file"></a>Declarar destinos no arquivo de projeto  
 Os destinos são declarados no arquivo de projeto com o elemento [Destino](../msbuild/target-element-msbuild.md). Por exemplo, o XML a seguir cria um destino chamado Constructo, que chama a tarefa Csc com o tipo de item de Compilação.  
  
```xml  
<Target Name="Construct">  
    <Csc Sources="@(Compile)" />  
</Target>  
```  
  
 Como as propriedades do MSBuild, destinos podem ser redefinidos. Por exemplo,  
  
```xml  
<Target Name="AfterBuild" >  
    <Message Text="First occurrence" />  
</Target>  
<Target Name="AfterBuild" >  
    <Message Text="Second occurrence" />  
</Target>  
```  
  
 Se AfterBuild for executado, ele exibirá apenas "segunda ocorrência".  
  
## <a name="target-build-order"></a>Ordem de build de destino  
 Os destinos deverão ser ordenados se a entrada para um destino depender da saída de outro. Há várias maneiras de especificar a ordem na qual os destinos são executados.  
  
-   Destinos Iniciais  
  
-   Destinos padrão  
  
-   Primeiro destino  
  
-   Dependências de destino  
  
-   `BeforeTargets` e `AfterTargets` (MSBuild 4.0)  

Um destino nunca é executado duas vezes durante uma único build, mesmo se um destino posterior no build depender dele. Depois da execução de um destino, sua contribuição para o build será concluída.  

Para obter detalhes e mais informações sobre a ordem de build de destino, confira [Ordem de build de destino](../msbuild/target-build-order.md).  

## <a name="target-batching"></a>Envio em lote de destinos  
Um elemento de destino pode ter um atributo `Outputs` que especifica os metadados no formato %(\<Metadata>). Nesse caso, o MSBuild executa o destino uma vez para cada valor exclusivo de metadados, agrupando ou colocando em "lote" os itens que têm esse valor de metadados. Por exemplo,  
  
```xml  
<ItemGroup>  
    <Reference Include="System.Core">  
      <RequiredTargetFramework>3.5</RequiredTargetFramework>  
    </Reference>  
    <Reference Include="System.Xml.Linq">  
      <RequiredTargetFramework>3.5</RequiredTargetFramework>  
    </Reference>  
    <Reference Include="Microsoft.CSharp">  
      <RequiredTargetFramework>4.0</RequiredTargetFramework>  
    </Reference>  
</ItemGroup>  
<Target Name="AfterBuild"  
    Outputs="%(Reference.RequiredTargetFramework)">  
    <Message Text="Reference:  
      @(Reference->'%(RequiredTargetFramework)')" />  
</Target>  
```  
  
 coloca os itens de Referência em lote por seus metadados de RequiredTargetFramework. O resultado do destino é semelhante a este:  
  
```  
Reference: 3.5;3.5  
Reference: 4.0  
```  
  
 A separação de lote de destinos raramente é usada em builds reais. A separação de lote de tarefas é mais comum. Para obter mais informações, consulte [Envio em lote](../msbuild/msbuild-batching.md).  
  
## <a name="incremental-builds"></a>Builds incrementais  
 Os builds incrementais são builds que são otimizados para que os destinos com arquivos de saída que estão atualizados em relação aos seus arquivos de entrada correspondentes não sejam executados. Um elemento de destino pode ter atributos `Inputs` e `Outputs`, indicando quais itens o destino espera como entrada e quais itens ele gera como saída.  
  
 Se todos os itens de saída estiverem atualizados, o MSBuild ignora o destino, o que melhora significativamente a velocidade de build. Isso é chamado de build incremental do destino. Se apenas alguns arquivos forem atualizados, o MSBuild executa o destino sem os itens atualizados. Isso é chamado de build incremental parcial do destino. Para obter mais informações, confira [Builds incrementais](../msbuild/incremental-builds.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Como: Usar o mesmo destino em vários arquivos de projeto](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)