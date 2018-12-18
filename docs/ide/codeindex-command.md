---
title: Comando CodeIndex
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- command-line tools [Team Foundation Server]
- TFSConfig
- CodeIndex command [Team Foundation Server]
ms.assetid: b79568d4-6a64-4ca9-a1ee-3e57f92a9c5c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3f1169ff5bc9487fc062ab7cbc6e2adb01151a19
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49926144"
---
# <a name="codeindex-command"></a>Comando CodeIndex

Use o comando **CodeIndex** para gerenciar a indexação de código no Team Foundation Server. Por exemplo, você pode desejar redefinir o índice para consertar informações CodeLens ou desativar a indexação para investigar problemas de desempenho do servidor.

## <a name="required-permissions"></a>Permissões necessárias

Para usar o comando **CodeIndex**, é necessário ser um membro do grupo de segurança **Team Foundation Administrators**. Consulte [Permissões e grupos definidos para o Azure DevOps Services e o TFS](/azure/devops/organizations/security/permissions?view=vsts).

> [!NOTE]
> Mesmo que use credenciais administrativas para entrar, você deve abrir uma janela de prompt de comandos com privilégios elevados para executar esse comando. Você também deve executar esse comando a partir do nível de aplicativo para o Team Foundation.

## <a name="syntax"></a>Sintaxe

```cmd
TFSConfig CodeIndex /indexingStatus | /setIndexing:[ on | off | keepupOnly ] | /ignoreList:[ add | remove | removeAll | view ] ServerPath | /listLargeFiles [/fileCount:FileCount] [/minSize:MinSize] | /reindexAll | /destroyCodeIndex [/noPrompt] | /temporaryDataSizeLimit:[ view | <SizeInGBs> | disable ] | /indexHistoryPeriod:[ view | all | <NumberOfMonths> ] [/collectionName:CollectionName | /collectionId:CollectionId]
```

### <a name="parameters"></a>Parâmetros

|**Argumento**|**Descrição**|
|------------------| - |
|`CollectionName`|Especifica o nome da coleção de projetos. Se o nome tiver espaços, coloque o nome entre aspas, por exemplo, "Site do Fabrikam".|
|`CollectionId`|Especifica o número de identificação da coleção de projetos.|
|`ServerPath`|Especifica o caminho para um arquivo de código.|

|**Opção**|**Descrição**|
|----------------| - |
|**/indexingStatus**|Mostra o status e a configuração do serviço de indexação de código.|
|**/setIndexing:**[ on &#124; off &#124; keepupOnly ]|-   **on**: iniciar a indexação de todos os conjuntos de alterações.<br />-   **off**: interromper a indexação de todos os conjuntos de alterações.<br />-   **keepupOnly**: interromper a indexação de conjuntos de alterações criados anteriormente e iniciar apenas a indexação de novos conjuntos de alterações.|
|**/ignoreList:**[ add &#124; remove &#124; removeAll &#124; view ] `ServerPath`<br /><br /> É possível usar o caractere curinga (*) no início, no fim ou em ambas as extremidades do caminho do servidor.|Especifica uma lista de arquivos de código e seus caminhos que você não deseja indexar.<br /><br /> -   **add**: adicionar o arquivo que você não deseja indexar à lista de arquivos ignorados.<br />-   **remove**: remover o arquivo que você deseja que seja indexado na lista de arquivos ignorados.<br />-   **removeAll**: limpar a lista de arquivos ignorados e iniciar a indexação de todos os arquivos.<br />-   **view**: ver todos os arquivos que não estão sendo indexados.|
|**/listLargeFiles [/fileCount:** `FileCount` **/minSize:** `MinSize`]|Mostra o número especificado de arquivos que excede o tamanho especificado em KB. É possível usar a opção **/ignoreList** para excluir esses arquivos da indexação.|
|**/reindexAll**|Limpe os dados indexados anteriormente e reinicie a indexação.|
|**/destroyCodeIndex [/noPrompt]**|Exclua o índice de código e remota todos os dados indexados. Não requererá confirmação se você usar a opção **/noPrompt**.|
|**/temporaryDataSizeLimit**:[ exibir &#124; <`SizeInGBs`> &#124; desabilitar ]|Controle quantos dados temporários que o CodeLens cria ao processar conjuntos de alterações. O limite padrão é 2 GB.<br /><br /> -   **exibir**: mostrar o limite do tamanho atual.<br />-   `SizeInGBs`: alterar o limite do tamanho.<br />-   **desabilitar**: remover o limite do tamanho.<br /><br /> Esse limite é verificado antes de CodeLens processa um novo conjunto de alterações. Se os dados temporários excederem esse limite, o CodeLens pausará o processamento de conjuntos de alterações passados, não novos. CodeLens reiniciará o processamento depois que os dados são limpos e ficar abaixo desse limite. Limpeza executa automaticamente uma vez por dia. Isso significa que os dados temporários podem exceder esse limite até que a limpeza começa a ser executado.|
|**/indexHistoryPeriod**:[ exibir &#124; tudo &#124; <`NumberOfMonths`> ]|Controle por quanto tempo indexar o histórico de alterações. Isso afeta a quantidade de histórico que o CodeLens mostra a você. O limite padrão é 12 meses. Isso significa que o CodeLens mostra seu histórico de alterações apenas dos últimos 12 meses.<br /><br /> -   **exibir**: mostrar o número atual de meses.<br />-   **tudo**: indexar todo o histórico de alterações.<br />-   `NumberOfMonths`: Altere o número de meses usado para indexar o histórico de alterações.|
|**/collectionName:** `CollectionName`|Especifica o nome da coleção de projetos na qual executar o comando **CodeIndex**. Obrigatório se você não usar **/CollectionId**.|
|**/collectionId:** `CollectionId`|Especifica o número de identificação da coleção de projetos na qual executar o comando **CodeIndex**. Obrigatório se você não usar **/CollectionName**.|

## <a name="examples"></a>Exemplos

> [!NOTE]
> Os exemplos de empresas, organizações, produtos, nomes de domínio, endereços de email, logotipos, pessoas, lugares e eventos aqui mencionados são fictícios.  Nenhuma associação com nenhuma empresa, organização, produto, nome de domínio, endereço de email, logotipo, pessoa, locais ou eventos reais é intencional nem deve ser inferida.

 Para ver o status e a configuração de indexação do código:

```cmd
TFSConfig CodeIndex /indexingStatus /collectionName:"Fabrikam Website"
```

 Para iniciar a indexação de todos os conjuntos de alterações:

```cmd
TFSConfig CodeIndex /setIndexing:on /collectionName:"Fabrikam Website"
```

 Para interromper a indexação de conjuntos de alterações criados anteriormente e iniciar indexação apenas para novos conjuntos de alterações:

```cmd
TFSConfig CodeIndex /setIndexing:keepupOnly /collectionName:"Fabrikam Website"
```

 Para encontrar até 50 arquivos maiores que 10 KB:

```cmd
TFSConfig CodeIndex /listLargeFiles /fileCount:50 /minSize:10 /collectionName:"Fabrikam Website"
```

 Para excluir um arquivo específico da indexação e adicioná-lo à lista de arquivos ignorados:

```cmd
TFSConfig CodeIndex /ignoreList:add "$/Fabrikam Website/Catalog.cs" /collectionName:"Fabrikam Website"
```

 Para ver todos os arquivos que não estão indexados:

```cmd
TFSConfig CodeIndex /ignoreList:view
```

 Para limpar os dados indexados anteriormente e reinicie a indexação:

```cmd
TFSConfig CodeIndex /reindexAll /collectionName:"Fabrikam Website"
```

 Para salvar todo o histórico de alterações:

```cmd
TFSConfig CodeIndex /indexHistoryPeriod:all /collectionName:"Fabrikam Website"
```

 Para remover o limite de tamanho CodeLens os dados temporários e continuar a indexação independentemente do tamanho de dados temporários:

```cmd
TFSConfig CodeIndex /temporaryDataSizeLimit:disable /collectionName:"Fabrikam Website"
```

 Para excluir o índice de código com confirmação:

```cmd
TFSConfig CodeIndex /destroyCodeIndex /collectionName:"Fabrikam Website"
```

## <a name="see-also"></a>Consulte também

- [Localizar alterações de código e outro histórico com o CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md)
- [Gerenciando a configuração do servidor com TFSConfig](/tfs/server/ref/command-line/tfsconfig-cmd)