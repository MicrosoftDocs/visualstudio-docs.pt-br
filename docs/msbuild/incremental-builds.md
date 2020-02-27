---
title: Builds incrementais | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- msbuild, incremental builds
ms.assetid: 325e28c7-4838-4e3f-b672-4586adc7500c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7283d67710a3b5b319b2d25a1c5d6535fed83b9
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633714"
---
# <a name="incremental-builds"></a>Builds incrementais

Os builds incrementais são builds que são otimizados para que os destinos que têm arquivos de saída que estão atualizados em relação aos seus arquivos de entrada correspondentes não sejam executados. Um elemento de destino pode ter um atributo de `Inputs`, que indica quais itens o destino espera como entrada e um atributo de `Outputs`, que indica quais itens ele gera como saída. O MSBuild tenta localizar um mapeamento de 1 para 1 entre os valores desses atributos. Se existir um mapeamento de 1 para 1, o MSBuild comparará o carimbo de hora de cada item de entrada com o carimbo de hora do seu item de saída correspondente. Arquivos de saída que não tenham nenhum mapeamento de 1 para 1 são comparados com todos os arquivos de entrada. Um item será considerado atualizado se seu arquivo de saída tiver a mesma idade ou for mais recente que seu arquivo ou arquivos de entrada.

> [!NOTE]
> Quando o MSBuild avalia os arquivos de entrada, somente o conteúdo da lista na execução atual é considerado. As alterações na lista da última compilação não tornam automaticamente um destino desatualizado.

Se todos os itens de saída estiverem atualizados, o MSBuild ignorará o destino. Esse *build incremental* do destino pode melhorar significativamente a velocidade de build. Se apenas alguns arquivos estiverem atualizados, o MSBuild executará o destino, mas ignora os itens atualizados e, portanto, traz todos os itens atualizados. Esse processo é conhecido como um *build incremental parcial*.

Mapeamentos de 1 para 1 em geral são produzidos por transformações de item. Para obter mais informações, consulte [Transformações](../msbuild/msbuild-transforms.md).

 Considere o destino a seguir.

```xml
<Target Name="Backup" Inputs="@(Compile)"
    Outputs="@(Compile->'$(BackupFolder)%(Identity).bak')">
    <Copy SourceFiles="@(Compile)" DestinationFiles=
        "@(Compile->'$(BackupFolder)%(Identity).bak')" />
</Target>
```

O conjunto de arquivos representados pelo tipo de item `Compile` é copiado para um diretório de backup. Os arquivos de backup têm a extensão de nome de arquivo *.bak*. Se os arquivos representados pelo tipo de item `Compile` ou os arquivos de backup correspondentes, não forem excluídos ou modificados após o destino de Backup ser executado, o destino de Backup é ignorado em builds subsequentes.

## <a name="output-inference"></a>Inferência de saída

O MSBuild compara os atributos `Inputs` e `Outputs` de um destino para determinar se o destino deve executar. Idealmente, o conjunto de arquivos existente após a conclusão de um build incremental deve permanecer o mesmo independentemente de os destinos associados serem executados ou não. Como propriedades e itens que são criados ou alterados por tarefas podem afetar o build, o MSBuild deverá inferir seus valores, mesmo se o destino que os afeta for ignorado. Esse processo é conhecido como *inferência de saída*.

Há três casos:

- O destino tem um atributo `Condition` que é avaliado como `false`. Nesse caso, o destino não é executado e não tem nenhum efeito no build.

- O destino tem saídas desatualizadas e é executado para atualizá-las.

- O destino não tem saídas desatualizadas e é ignorado. O MSBuild avalia o destino e faz alterações em itens e propriedades como se o destino tivesse sido executado.

Para oferecer suporte à compilação incremental, as tarefas devem garantir que o valor de atributo `TaskParameter` de qualquer elemento `Output` seja igual a um parâmetro de entrada da tarefa. Estes são alguns exemplos:

```xml
<CreateProperty Value="123">
    <Output PropertyName="Easy" TaskParameter="Value" />
</CreateProperty>
```

Esse código cria a propriedade Easy, que tem o valor "123", independentemente de o destino ser ou não executado ou ignorado.

A partir do MSBuild 3.5, a interferência de saída é executada automaticamente em grupos de propriedade e item em um destino. Tarefas `CreateItem` não são necessárias em um destino e devem ser evitadas. Além disso, tarefas `CreateProperty` devem ser usadas em um destino apenas para determinar se um destino foi executado.

Antes do MSBuild 3.5, você pode usar a tarefa [CreateItem](../msbuild/createitem-task.md).

## <a name="determine-whether-a-target-has-been-run"></a>Determinar se um destino foi executado

Por causa da inferência de saída, é necessário adicionar uma tarefa `CreateProperty` a um destino para examinar itens e propriedades para que você possa determinar se o destino foi executado. Adicione a tarefa `CreateProperty` ao destino e dê a ela um elemento `Output` cujo `TaskParameter` seja "ValueSetByTask".

```xml
<CreateProperty Value="true">
    <Output TaskParameter="ValueSetByTask" PropertyName="CompileRan" />
</CreateProperty>
```

Esse código cria a propriedade CompileRan e atribui a ela o valor `true`, mas apenas se o destino é executado. Se o destino for ignorado, CompileRan não será criado.

## <a name="see-also"></a>Confira também

- [Destinos](../msbuild/msbuild-targets.md)
