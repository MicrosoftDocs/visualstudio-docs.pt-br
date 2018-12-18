---
title: Caixa de diálogo Configurações Avançadas (Visualização Simultânea) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.cv.settings
ms.assetid: bb3d90aa-5f08-4953-9be0-be6cea11633d
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5ad91917034dd868aad6c5d78945e4c078fcecee
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749540"
---
# <a name="advanced-settings-dialog-box-concurrency-visualizer"></a>Caixa de diálogo Configurações Avançadas (Visualizador de Simultaneidade)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando a caixa de diálogo **Configurações Avançadas** da Visualização Simultânea, você pode controlar como os rastreamentos são coletados.  A caixa de diálogo tem guias para símbolos, Apenas Meu Código, buffer, filtragem, eventos CLR, marcadores, provedores e arquivos.  
  
## <a name="symbols"></a>Símbolos  
 A Visualização Simultânea usa as mesmas configurações de símbolo que o Depurador do Visual Studio. A Visualização Simultânea usa as configurações para resolver as pilhas de chamadas que estão associadas a dados de desempenho.  Ao processar rastreamentos, a Visualização Simultânea acessa os servidores de símbolo especificados na página de configurações.  Quando esses dados são acessados em uma rede, o processamento de rastreamento fica mais lento.  Para reduzir a quantidade de tempo necessária para resolver símbolos, você pode armazenar os símbolos em cache localmente. Se símbolos tiverem sido baixados, o Visual Studio os carregará do cache local.  
  
## <a name="just-my-code"></a>Apenas Meu Código  
 Por padrão, o Apenas Meu Código é o conjunto de arquivos .exe e .dll que estão associados à solução atual no Visual Studio. A Visualização Simultânea avalia esse conjunto de arquivos quando você usa o recurso Apenas Meu Código para filtrar as pilhas de chamadas. Na guia Apenas Meu Código, você pode adicionar pastas que contêm arquivos .exe e .dll para os locais que a Visualização Simultânea usa para Apenas Meu Código.  
  
 Os caminhos dos arquivos .exe e .dll são armazenados no arquivo de rastreamento quando o rastreamento é coletado.  A alteração dessa configuração não afeta nenhum rastreamento coletado anteriormente.  
  
## <a name="buffering"></a>Buffer  
 A Visualização Simultânea usa ETW (Rastreamento de Eventos para Windows) ao coletar um rastreamento.  O ETW usa diversos buffers conforme ele armazena eventos.  As configurações padrão de buffer ETW podem não ser ideais em todos os casos e, em alguns casos, podem causar problemas como eventos perdidos.  Você pode usar a guia armazenamento em buffer para definir as configurações de buffer ETW. Para obter mais informações, consulte [Rastreamento de eventos](http://go.microsoft.com/fwlink/?LinkId=234579) e [Estrutura EVENT_TRACE_PROPERTIES](http://go.microsoft.com/fwlink/?LinkId=234580).  
  
## <a name="filter"></a>Filtro  
 Na guia Filtro, você pode selecionar o conjunto de eventos que a Visualização Simultânea coleta. Selecionar um subconjunto de eventos limita os tipos de dados que são exibidos nos relatórios, reduz o tamanho de cada rastreamento e reduz o tempo necessário para processar rastreamentos.  
  
### <a name="clr-events"></a>Eventos CLR  
 Eventos gerados pelo CLR (Common Language Runtime) permitem à Visualização Simultânea resolver pilhas de chamadas gerenciadas.  Se você desabilitar a coleta de eventos CLR, o tamanho do rastreamento será reduzido, mas algumas pilhas de chamadas não serão resolvidas.  Como resultado, alguma atividade de thread da CPU pode ser categorizada incorretamente.  
  
### <a name="collect-for-native-processes"></a>Coletar para processos nativos  
 Por padrão, os eventos do CLR são coletados apenas quando um processo gerenciado é atribuído, porque eles normalmente são desnecessários para processos nativos.  Em alguns casos (por exemplo, quando um processo nativo está hospedando o CLR), você terá que coletar eventos do CLR para um processo nativo.  Se esse é o caso, selecione a caixa de seleção **Coletar Para Processos Nativos**.  
  
### <a name="disable-rundown-events"></a>Desabilitar eventos de encerramento  
 O CLR gera eventos de dois provedores: tempo de execução e encerramento.  Se você quiser coletar eventos de tempo de execução do CLR mas desejar evitar coletar eventos de encerramento, selecione a caixa de seleção **Desabilitar Eventos de Encerramento**.  Isso reduz o tamanho do arquivo de rastreamento que é gerado por coleta, mas algumas pilhas poderão não ser resolvidas. Para obter mais informações, consulte [Provedores ETW de CLR](http://msdn.microsoft.com/library/0beafad4-b2c8-47f4-b342-83411d57a51f)  
  
### <a name="sample-events"></a>Eventos de amostragem  
 Você pode usar eventos de exemplo para coletar as pilhas de chamadas associadas à execução do thread. Esses eventos são coletados aproximadamente uma vez por milissegundo para threads em execução no processo atual. Se você desabilitar a coleta de eventos de exemplo, o tamanho do rastreamento coletado será reduzido, mas não será possível exibir nenhuma pilha de chamadas associada à execução do thread.  
  
### <a name="gpu-events"></a>Eventos GPU  
 Eventos de GPU são eventos gerados pelo DirectX. Se você desabilitar a coleta de eventos de GPU, o tamanho do rastreamento coletado será reduzido, mas não será possível exibir nenhuma atividade de GPU na exibição de Utilização, tampouco nenhuma atividade do mecanismo DirectX na exibição de Threads.  
  
### <a name="file-io-events"></a>Eventos de arquivos E/S  
 Eventos de E/S de arquivo representam acessos ao disco em nome do processo atual.  Se você desabilitar eventos de E/S de arquivo, o tamanho do rastreamento será reduzido, mas o modo de exibição de Threads não relatará todas as informações sobre operações de disco ou canais de disco.  
  
## <a name="markers"></a>Marcadores  
 Na guia marcadores, você pode configurar o conjunto de provedores ETW que são mostrados como marcadores na Visualização Simultânea.  Você também pode filtrar a coleta de marcador com base no nível de importância e na categoria ETW.  Se você estiver usando o [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md) e estiver usando seu próprio provedor de marcadores, você poderá registrá-lo aqui para que ele apareça na exibição de Threads.  
  
### <a name="adding-a-new-provider"></a>Adicionar um novo provedor  
 Se seu código usa o [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md) ou gera eventos ETW que seguem a convenção <xref:System.Diagnostics.Tracing.EventSource>, você poderá exibir esses eventos na Visualização Simultânea, registrando-os nessa caixa de diálogo.  
  
 No campo Nome, digite um nome que descreva os tipos de eventos que são gerados pelo provedor.  No campo GUID, insira o GUID associado a esse provedor. (Um GUID é associado a cada provedor de ETW.)  
  
 Opcionalmente, você pode especificar se deseja filtrar eventos deste provedor, com base no nível de importância ou categoria.  Você pode usar a categoria de campo para filtrar com base nas categorias de SDK da Visualização Simultânea.  Para fazer isso, insira uma cadeia de caracteres de categorias delimitada por vírgulas ou intervalos de categorias.  Isso especifica as categorias de eventos no provedor atual para mostrar.  Se estiver adicionando um provedor <xref:System.Diagnostics.Tracing.EventSource>, você poderá usar o campo de categoria para filtrar por palavra-chave do ETW.  Já que a palavra-chave é um bitmask, você pode usar uma cadeia de caracteres de inteiros delimitada por vírgulas para especificar quais bits na máscara são definidos. Por exemplo, "1,2" define o primeiro e segundo bits, e isso se traduz para em 6 em decimal.  
  
 Você pode usar a lista de nível de importância para filtrar os eventos que tenham importância ou nível ETW menor que o valor especificado.  
  
### <a name="configuring-an-existing-provider"></a>Configurando um provedor existente  
 Para editar as configurações que estão associadas um provedor existente, selecione-o na lista e escolha o botão **Editar provedor**.  Você pode alterar as configurações de filtragem, nome e GUID.  
  
### <a name="filter-marker-data-out-of-concurrency-visualizer-reports"></a>Filtrar dados de marcador dos relatórios de Visualização Simultânea  
 Se você não deseja que os dados de um determinado provedor apareçam em rastreamentos futuros, desmarque a caixa de seleção ao lado do provedor que você deseja remover.  
  
## <a name="files"></a>Arquivos  
 Na guia **arquivos**, você pode especificar o diretório no qual os arquivos de rastreamento são armazenados sempre que um rastreamento é coletado.  A Visualização Simultânea gera quatro arquivos para cada rastreamento que coleta:  
  
- Um arquivo de ETL (log de rastreamento de eventos) do modo kernel (*.kernel.etl)  
  
- Um arquivo de log de rastreamento de eventos do modo de usuário (*.user.etl)  
  
- Um arquivo de dados da Visualização Simultânea (*.CVData)  
  
- Um arquivo de rastreamento da Visualização Simultânea (*.CVTrace)  
  
  Os dois arquivos ETL armazenam os dados brutos de rastreamento e os dois arquivos da Visualização Simultânea armazenam os dados processados.  Os arquivos brutos de ETL normalmente não são usados após o processamento de um rastreamento.  Selecionar a caixa de seleção **Excluir arquivos de ETL (Log de Rastreamento de eventos) após a análise** reduz a quantidade de dados de rastreamento que são armazenados no disco.  
  
## <a name="see-also"></a>Consulte também  
 [Apenas Meu Código](../profiling/just-my-code-threads-view.md)   
 [Marcadores da Visualização Simultânea](../profiling/concurrency-visualizer-markers.md)



