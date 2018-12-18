---
title: Builds incrementais | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- msbuild, incremental builds
ms.assetid: 325e28c7-4838-4e3f-b672-4586adc7500c
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 187761ce813081877434c2a7c3a570059bc556ee
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812316"
---
# <a name="incremental-builds"></a>Builds incrementais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Os builds incrementais são builds que são otimizados para que os destinos que têm arquivos de saída que estão atualizados em relação aos seus arquivos de entrada correspondentes não sejam executados. Um elemento de destino pode ter um atributo de `Inputs`, que indica quais itens o destino espera como entrada e um atributo de `Outputs`, que indica quais itens ele gera como saída. O MSBuild tenta localizar um mapeamento de 1 para 1 entre os valores desses atributos. Se existir um mapeamento de 1 para 1, o MSBuild comparará o carimbo de hora de cada item de entrada com o carimbo de hora do seu item de saída correspondente. Arquivos de saída que não tenham nenhum mapeamento de 1 para 1 são comparados com todos os arquivos de entrada. Um item será considerado atualizado se seu arquivo de saída tiver a mesma idade ou for mais recente que seu arquivo ou arquivos de entrada.  
  
 Se todos os itens de saída estiverem atualizados, o MSBuild ignorará o destino. Esse *build incremental* do destino pode melhorar significativamente a velocidade de build. Se apenas alguns arquivos estiverem atualizados, o MSBuild executará o destino, mas ignora os itens atualizados e, portanto, traz todos os itens atualizados. Isso é conhecido como um *build parcial incremental*.  
  
 Mapeamentos de 1 para 1 em geral são produzidos por transformações de item. Para obter mais informações, consulte [Transformações](../msbuild/msbuild-transforms.md).  
  
 Considere o destino a seguir.  
  
```  
<Target Name="Backup" Inputs="@(Compile)"   
    Outputs="@(Compile->'$(BackupFolder)%(Identity).bak')">  
    <Copy SourceFiles="@(Compile)" DestinationFiles=  
        "@(Compile->'$(BackupFolder)%(Identity).bak')" />  
</Target>  
```  
  
 O conjunto de arquivos representados pelo tipo de item `Compile` são copiados para um diretório de backup. Os arquivos de backup têm a extensão de nome de arquivo .bak. Se os arquivos representados pelo tipo de item `Compile` ou os arquivos de backup correspondentes, não forem excluídos ou modificados após o destino de Backup ser executado, o destino de Backup é ignorado em builds subsequentes.  
  
## <a name="output-inference"></a>Inferência de saída  
 O MSBuild compara os atributos `Inputs` e `Outputs` de um destino para determinar se o destino deve executar. Idealmente, o conjunto de arquivos existente após a conclusão de um build incremental deve permanecer o mesmo independentemente de os destinos associados serem executados ou não. Como propriedades e itens que são criados ou alterados por tarefas podem afetar o build, o MSBuild deverá inferir seus valores, mesmo se o destino que os afeta for ignorado. Isso é conhecido como *inferência de saída*.  
  
 Há três casos:  
  
- O destino tem um atributo `Condition` que é avaliado como `false`. Nesse caso, o destino não é executado e não tem nenhum efeito no build.  
  
- O destino tem saídas desatualizadas e é executado para atualizá-las.  
  
- O destino não tem saídas desatualizadas e é ignorado. O MSBuild avalia o destino e faz alterações em itens e propriedades como se o destino tivesse sido executado.  
  
  Para oferecer suporte à compilação incremental, as tarefas devem garantir que o valor de atributo `TaskParameter` de qualquer elemento `Output` seja igual a um parâmetro de entrada da tarefa. Estes são alguns exemplos:  
  
```  
<CreateProperty Value="123">  
    <Output PropertyName="Easy" TaskParameter="Value" />  
</CreateProperty>  
```  
  
 Isso cria a propriedade Fácil, que tem o valor "123", independentemente de o destino ser ou não executado ou ignorado.  
  
```  
<CreateItem Include="a.cs;b.cs">  
    <Output ItemName="Simple" TaskParameter="Include" />  
</CreateItem>  
```  
  
 Isso cria o tipo de item Simples, que tem dois itens, "a.cs" e "b.cs", independentemente de o destino ser ou não executado ou ignorado.  
  
 A partir do MSBuild 3.5, a interferência de saída é executada automaticamente em grupos de propriedade e item em um destino. Tarefas `CreateItem` não são necessárias em um destino e devem ser evitadas. Além disso, tarefas `CreateProperty` devem ser usadas em um destino apenas para determinar se um destino foi executado.  
  
## <a name="determining-whether-a-target-has-been-run"></a>Determinando se um destino foi executado  
 Por causa da inferência de saída, é necessário adicionar uma tarefa `CreateProperty` a um destino para examinar itens e propriedades para que você possa determinar se o destino foi executado. Adicione a tarefa `CreateProperty` ao destino e dê a ela um elemento `Output` cujo `TaskParameter` seja "ValueSetByTask".  
  
```  
<CreateProperty Value="true">  
    <Output TaskParameter="ValueSetByTask" PropertyName="CompileRan" />  
</CreateProperty>  
```  
  
 Isso cria a propriedade CompileRan e atribui a ela o valor `true`, mas apenas se o destino for executado. Se o destino for ignorado, CompileRan não será criado.  
  
## <a name="see-also"></a>Consulte também  
 [Destinos](../msbuild/msbuild-targets.md)



