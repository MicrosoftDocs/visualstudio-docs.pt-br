---
title: Como Depurar um mecanismo de depuração personalizado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, debugging
- debugging [Debugging SDK], custom debug engines
ms.assetid: df27a8d6-3938-45ff-b47f-b684e80b38a0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: bdc01eec9982f7e3a03cd84424bc56b031846a7d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49858856"
---
# <a name="how-to-debug-a-custom-debug-engine"></a>Como Depurar um mecanismo de depuração personalizado
O mecanismo de depuração (DES) é iniciado de um tipo de projeto na <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> método. Isso significa que a Alemanha é iniciada sob o controle da instância do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] controlar o tipo de projeto. No entanto, essa instância do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] não é possível depurar o DE. A seguir estão as etapas que permitem a depuração DE seu personalizado.  
  
> [!NOTE]
>  : O procedimento "Debug um mecanismo de depuração personalizado", você deve aguardar o DE iniciar antes que você pode anexar a ela. Se você colocar uma caixa de mensagem no início do seu DE que aparece quando o DE é iniciado, você pode anexar nesse momento e, em seguida, desmarque a caixa de mensagem para continuar. Dessa forma, você pode capturar todos os eventos DE.  
  
> [!WARNING]
>  Você deve ter a depuração remota instalados antes de tentar os procedimentos a seguir. Ver [depuração remota](../../debugger/remote-debugging.md) para obter detalhes.  
  
## <a name="debug-a-custom-debug-engine"></a>Depurar um mecanismo de depuração personalizado  
  
1. Inicie *msvsmon.exe*, Monitor de depuração remota.  
  
2. Dos **ferramentas** menu no *msvsmon.exe*, selecione **opções** para abrir o **opções** caixa de diálogo.  
  
3. Selecione a opção "sem autenticação" e clique em **Okey**.  
  
4. Iniciar uma instância do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e abra o projeto DE personalizado.  
  
5. Inicie uma segunda instância de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] e abra seu projeto personalizado que inicia o DE (para o desenvolvimento, isso normalmente é no hive do registro experimental que é definido quando VSIP é instalado).  
  
6. Na segunda instância de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], carregar um arquivo de origem do seu projeto personalizado e iniciar o programa a ser depurado. Aguarde alguns instantes para permitir que o DE carregar ou aguarde até que um ponto de interrupção é atingido.  
  
7. Na primeira instância do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (com seu projeto DE), selecione **anexar ao processo** da **depurar** menu.  
  
8. No **anexar ao processo** caixa de diálogo, altere o **transporte** para **remoto (somente nativo sem autenticação)**.  
  
9. Alterar o **qualificador** para o nome do seu computador (Observação: há um histórico das entradas, portanto, você precisa digitar esse nome apenas uma vez).  
  
10. No **processos disponíveis** , selecione a instância do seu DE que está em execução e clique no **Attach** botão.  
  
11. Após carregaram os símbolos no seu DE, colocar pontos de interrupção em seu código DE.  
  
12. Sempre que você para e reiniciar o processo de depuração, repita as etapas 6 a 10.  
  
## <a name="debug-a-custom-project-type"></a>Depurar um tipo de projeto personalizado  
  
1. Iniciar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] no hive do registro normal e carga seu projeto de tipo de projeto (Isso é, o código-fonte para o tipo de projeto, não uma instanciação de seu tipo de projeto).  
  
2. Abra as propriedades do projeto e vá para o **depurar** página. Para o **comando**, digite o caminho para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (por padrão, isso é *[unidade]* \Program Files\Microsoft [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 8\Common7\IDE\devenv.exe).  
  
3. Para o **argumentos de comando**, digite `/rootsuffix exp` para o hive do registro experimental (criado quando o VSIP foi instalado).  
  
4. Clique em **OK** para aceitar as alterações.  
  
5. Inicie o tipo de projeto pressionando **F5**. Isso inicia uma segunda instância do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
6. Neste ponto, você pode colocar pontos de interrupção em seu código de origem do tipo de projeto.  
  
7. Na segunda instância de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], carregar ou criar uma nova instância de seu tipo de projeto. Durante a criação ou carga, seus pontos de interrupção podem ser atingidos.  
  
8. O tipo de projeto de depuração.  
  
9. Se você optar por depurar o processo de iniciar a DE, você pode executar as etapas no procedimento "Debug um mecanismo de depuração personalizada" para anexar a seu DE após ele é iniciado. Isso lhe dá três instâncias do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] em execução: um para sua fonte de tipo de projeto, um segundo para o tipo de projeto instanciado e um terceiro anexado ao seu DE.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)