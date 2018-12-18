---
title: Comando CodeIndex | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- command-line tools [Team Foundation Server]
- TFSConfig
- CodeIndex command [Team Foundation Server]
ms.assetid: b79568d4-6a64-4ca9-a1ee-3e57f92a9c5c
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9586348a1862820540613a5f191132c49fa6a74d
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49282354"
---
# <a name="codeindex-command"></a>Comando CodeIndex
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use o comando **CodeIndex** para gerenciar a indexação de código no Team Foundation Server. Por exemplo, você pode desejar redefinir o índice para consertar informações CodeLens ou desativar a indexação para investigar problemas de desempenho do servidor.  
  
 **Permissões necessárias**  
  
 Para usar o comando **CodeIndex**, é necessário ser um membro do grupo de segurança **Team Foundation Administrators**. Consulte [Referência de permissões para o Team Foundation Server](http://msdn.microsoft.com/library/39997de5-b7fb-4777-b779-07de0543abe6).  
  
> [!NOTE]
>  Mesmo que use credenciais administrativas para entrar, você deve abrir uma janela de prompt de comandos com privilégios elevados para executar esse comando. Você também deve executar esse comando a partir do nível de aplicativo para o Team Foundation.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
TFSConfig CodeIndex /indexingStatus | /setIndexing:[ on | off | keepupOnly ] | /ignoreList:[ add | remove | removeAll | view ] ServerPath | /listLargeFiles [/fileCount:FileCount] [/minSize:MinSize] | /reindexAll | /destroyCodeIndex [/noPrompt] | /temporaryDataSizeLimit:[ view | <SizeInGBs> | disable ] | /indexHistoryPeriod:[ view | all | <NumberOfMonths> ] [/collectionName:CollectionName | /collectionId:CollectionId]  
```  
  
#### <a name="parameters"></a>Parâmetros  
  
|**Argumento**|**Descrição**|  
|------------------|---------------------|  
|`CollectionName`|Especifica o nome da coleção de projetos de equipe. Se o nome tiver espaços, coloque o nome entre aspas, por exemplo, “Fabrikam Web Site”.|  
|`CollectionId`|Especifica o número de identificação da coleção de projeto de equipe.|  
|`ServerPath`|Especifica o caminho para um arquivo de código.|  
  
|**Opção**|**Descrição**|  
|----------------|---------------------|  
|**/indexingStatus**|Mostra o status e a configuração do serviço de indexação de código.|  
|**/setIndexing:**[ on &#124; off &#124; keepupOnly ]|-   **on**: iniciar a indexação de todos os conjuntos de alterações.<br />-   **off**: interromper a indexação de todos os conjuntos de alterações.<br />-   **keepupOnly**: interromper a indexação de conjuntos de alterações criados anteriormente e iniciar apenas a indexação de novos conjuntos de alterações.|  
|**/ignoreList:**[ add &#124; remove &#124; removeAll &#124; view ] `ServerPath`<br /><br /> É possível usar o caractere curinga (*) no início, no fim ou em ambas as extremidades do caminho do servidor.|Especifica uma lista de arquivos de código e seus caminhos que você não deseja indexar.<br /><br /> -   **add**: adicionar o arquivo que você não deseja indexar à lista de arquivos ignorados.<br />-   **remove**: remover o arquivo que você deseja que seja indexado na lista de arquivos ignorados.<br />-   **removeAll**: limpar a lista de arquivos ignorados e iniciar a indexação de todos os arquivos.<br />-   **view**: ver todos os arquivos que não estão sendo indexados.|  
|**/listLargeFiles [/fileCount:** `FileCount` **/minSize:** `MinSize`]|Mostra o número especificado de arquivos que excede o tamanho especificado em KB. É possível usar a opção **/ignoreList** para excluir esses arquivos da indexação.|  
|**/reindexAll**|Limpe os dados indexados anteriormente e reinicie a indexação.|  
|**/destroyCodeIndex [/noPrompt]**|Exclua o índice de código e remota todos os dados indexados. Não requererá confirmação se você usar a opção **/noPrompt**.|  
|**/temporaryDataSizeLimit**:[ exibir &#124; <`SizeInGBs`> &#124; desabilitar ]|Controle quantos dados temporários que o CodeLens cria ao processar conjuntos de alterações. O limite padrão é 2 GB.<br /><br /> -   **exibir**: mostrar o limite do tamanho atual.<br />-   `SizeInGBs`: alterar o limite do tamanho.<br />-   **desabilitar**: remover o limite do tamanho.<br /><br /> Esse limite é verificado antes de CodeLens processa um novo conjunto de alterações. Se os dados temporários excederem esse limite, o CodeLens pausará o processamento de conjuntos de alterações passados, não novos. CodeLens reiniciará o processamento depois que os dados são limpos e ficar abaixo desse limite. Limpeza executa automaticamente uma vez por dia. Isso significa que os dados temporários podem exceder esse limite até que a limpeza começa a ser executado.|  
|**/indexHistoryPeriod**:[ exibir &#124; tudo &#124; <`NumberOfMonths`> ]|Controle por quanto tempo indexar o histórico de alterações. Isso afeta a quantidade de histórico que o CodeLens mostra a você. O limite padrão é 12 meses. Isso significa que o CodeLens mostra seu histórico de alterações apenas dos últimos 12 meses.<br /><br /> -   **exibir**: mostrar o número atual de meses.<br />-   **tudo**: indexar todo o histórico de alterações.<br />-   `NumberOfMonths`: Altere o número de meses usado para indexar o histórico de alterações.|  
|**/collectionName:** `CollectionName`|Especifica o nome da coleção de projetos de equipe na qual executar o comando **CodeIndex**. Obrigatório se você não usar **/CollectionId**.|  
|**/collectionId:** `CollectionId`|Especifica o número de identificação da coleção de projetos de equipe na qual executar o comando **CodeIndex**. Obrigatório se você não usar **/CollectionName**.|  
  
## <a name="examples"></a>Exemplos  
  
> [!NOTE]
>  Os exemplos de empresas, organizações, produtos, nomes de domínio, endereços de email, logotipos, pessoas, lugares e eventos aqui mencionados são fictícios.  Nenhuma associação com nenhuma empresa, organização, produto, nome de domínio, endereço de email, logotipo, pessoa, locais ou eventos reais é intencional nem deve ser inferida.  
  
 Para ver o status e a configuração de indexação do código:  
  
```  
TFSConfig CodeIndex /indexingStatus /collectionName:"Fabrikam Web Site"  
```  
  
 Para iniciar a indexação de todos os conjuntos de alterações:  
  
```  
TFSConfig CodeIndex /setIndexing:on /collectionName:"Fabrikam Web Site"  
```  
  
 Para interromper a indexação de conjuntos de alterações criados anteriormente e iniciar indexação apenas para novos conjuntos de alterações:  
  
```  
TFSConfig CodeIndex /setIndexing:keepupOnly /collectionName:"Fabrikam Web Site"  
```  
  
 Para encontrar até 50 arquivos maiores que 10 KB:  
  
```  
TFSConfig CodeIndex /listLargeFiles /fileCount:50 /minSize:10 /collectionName:"Fabrikam Web Site"  
```  
  
 Para excluir um arquivo específico da indexação e adicioná-lo à lista de arquivos ignorados:  
  
```  
TFSConfig CodeIndex /ignoreList:add "$/Fabrikam Web Site/Catalog.cs" /collectionName:"Fabrikam Web Site"  
```  
  
 Para ver todos os arquivos que não estão indexados:  
  
```  
TFSConfig CodeIndex /ignoreList:view  
```  
  
 Para limpar os dados indexados anteriormente e reinicie a indexação:  
  
```  
TFSConfig CodeIndex /reindexAll /collectionName:"Fabrikam Web Site"  
```  
  
 Para salvar todo o histórico de alterações:  
  
```  
TFSConfig CodeIndex /indexHistoryPeriod:all /collectionName:"Fabrikam Web Site"  
```  
  
 Para remover o limite de tamanho CodeLens os dados temporários e continuar a indexação independentemente do tamanho de dados temporários:  
  
```  
TFSConfig CodeIndex /temporaryDataSizeLimit:disable /collectionName:"Fabrikam Web Site"  
```  
  
 Para excluir o índice de código com confirmação:  
  
```  
TFSConfig CodeIndex /destroyCodeIndex /collectionName:"Fabrikam Web Site"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Managing server configuration with TFSConfig (Gerenciando a configuração do servidor com TFSConfig)](http://msdn.microsoft.com/en-us/94424190-3b6b-4f33-a6b6-5807f4225b62)   
 [Ferramentas de linha de comando do TFS](http://msdn.microsoft.com/en-us/be8c997a-b97b-4e59-97f5-04db0a601a6c)



