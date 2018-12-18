---
title: Caixa de ferramentas, Guia Componentes | Microsoft Docs
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
- Toolbox, Components tab
ms.assetid: 332fafab-a763-4244-b388-15d1b5b5cc04
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 405c7db0ca437aa5462068e2be3cfcc2d76c1cae
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49203119"
---
# <a name="toolbox-components-tab"></a>Caixa de Ferramentas, Guia Componentes
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
Exibe os componentes que podem ser adicionados a designers [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e [!INCLUDE[csprcs](../../includes/csprcs-md.md)]. Além dos componentes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] incluídos no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], como os componentes <xref:System.Messaging.MessageQueue> e <xref:System.Diagnostics.EventLog>, é possível adicionar seus próprios componentes ou os componentes de terceiros a essa guia. Para obter mais informações, consulte [Como manipular guias da caixa de ferramentas](http://msdn.microsoft.com/en-us/21285050-cadd-455a-b1f5-a2289a89c4db).  
  
 Para exibir essa guia, no menu **Exibir**, selecione **Caixa de ferramentas**. Na **Caixa de ferramentas**, selecione a guia **Componentes**.  
  
 **BackgroundWorker**  
 Cria uma instância do componente `System.ComponentModel.BackgroundWorker` que pode executar uma operação em um thread separado e dedicado.  
  
 **DirectoryEntry**  
 Cria uma instância do componente <xref:System.DirectoryServices.DirectoryEntry>, que encapsula um nó ou um objeto na hierarquia do Active Directory e pode ser usada para interagir com provedores de serviços do Active Directory.  
  
 **DirectorySearcher**  
 Cria uma instância do componente <xref:System.DirectoryServices.DirectorySearcher>, que pode ser usada para executar consultas no Active Directory.  
  
 **ErrorProvider**  
 Cria uma instância do componente `System.Windows.Forms.ErrorProvider`, que indica para o usuário final que um controle em um formulário tem um erro associado a ele.  
  
 **EventLog**  
 Cria uma instância do componente <xref:System.Diagnostics.EventLog>, que pode ser usada para interagir com logs do sistema e de eventos personalizados, incluindo a gravação de eventos em um log e a leitura dos dados de log. Para obter mais informações, consulte [Introdução ao componente EventLog](http://msdn.microsoft.com/en-us/a2ba4f28-4b1a-435e-99ef-51b28e21f805).  
  
 **FileSystemWatcher**  
 Cria uma instância do componente <xref:System.IO.FileSystemWatcher>, que pode ser usada para monitorar alterações em um diretório ou arquivo ao qual você tem acesso. Para obter mais informações, consulte [Como configurar as instâncias do componente FileSystemWatcher](http://msdn.microsoft.com/en-us/2e628234-4951-4135-8a86-28b924070d50).  
  
 **HelpProvider**  
 Cria uma instância do componente `System.Windows.Forms.HelpProvider` que fornece Ajuda pop-up ou online para controles.  
  
 **ImageList**  
 Cria uma instância do componente `System.Windows.Forms.ImageList` que fornece métodos para gerenciar uma coleção de objetos `System.Drawing.Image`.  
  
 **MessageQueue**  
 Cria uma instância do componente <xref:System.Messaging.MessageQueue>, que pode ser usada para interagir com filas de mensagens, incluindo a leitura e gravação de mensagens em filas, o processamento de transações e a realização de tarefas de administração de fila. Para obter mais informações, consulte [Usando componentes de mensagens](http://msdn.microsoft.com/en-us/922dbac7-26f0-4e39-b666-ccfc184793d7).  
  
 **PerformanceCounter**  
 Cria uma instância do componente <xref:System.Diagnostics.PerformanceCounter>, que pode ser usada para interagir com contadores de desempenho do Windows, incluindo a criação de novas categorias e instâncias, a leitura de valores de contadores e a execução de cálculos nos dados do contador. Para obter mais informações, consulte [Monitorando limites de desempenho](http://msdn.microsoft.com/en-us/b8b44a55-31d0-4b45-9517-8c1b1e4fdc91).  
  
 **Processo**  
 Cria uma instância do componente <xref:System.Diagnostics.Process>, que pode ser usada para interromper, iniciar e manipular os dados associados a processos no sistema. Para obter mais informações, consulte [Monitorando e gerenciando processos do Windows](http://msdn.microsoft.com/en-us/a86bd4c1-b92c-49a0-8f32-61d67837b45e).  
  
 **SerialPort**  
 Cria uma instância do componente `System.IO.Ports.SerialPort` que fornece E/S síncrona e controlada por evento, acesso ao PIN e estados de fixação e interrupção e acesso às propriedades do driver serial.  
  
 **ServiceController**  
 Cria uma instância do componente <xref:System.ServiceProcess.ServiceController>, que pode ser usada para manipular serviços existentes, incluindo a inicialização e a interrupção de serviços e o envio de comandos para eles. Para obter mais informações, consulte [Monitorando serviços Windows](http://msdn.microsoft.com/en-us/4542ee3f-e052-4cb9-8726-58e9420de222).  
  
 **Timer**  
 Cria uma instância do componente <xref:System.Windows.Forms.Timer>, que pode ser usada para adicionar funcionalidade baseada em tempo aos aplicativos baseados no Windows. Para obter mais informações, consulte [Componente de temporizador](http://msdn.microsoft.com/library/6700e534-6382-43d5-98ed-14205435fff7).  
  
> [!NOTE]
>  Também há um <xref:System.Timers.Timer> baseado em sistema que pode ser adicionado à **Caixa de ferramentas**. Esse <xref:System.Timers.Timer> é otimizado para aplicativos de servidor e o <xref:System.Windows.Forms.Timer> do Windows Forms é mais adequado para uso no Windows Forms.  
  
## <a name="see-also"></a>Consulte também  
 [Programação com componentes](http://msdn.microsoft.com/library/d4d4fcb4-e0b8-46b3-b679-7ee0026eb9e3)   
 [Passo a passo da programação de componentes](http://msdn.microsoft.com/library/373cacf7-479e-4b05-991c-5cb18824e913)   
 [Caixa de ferramentas](../../ide/reference/toolbox.md)   
 [Caixa de diálogo Escolher Itens da Caixa de Ferramentas (Visual Studio)](http://msdn.microsoft.com/en-us/bd07835f-18a8-433e-bccc-7141f65263bb)



