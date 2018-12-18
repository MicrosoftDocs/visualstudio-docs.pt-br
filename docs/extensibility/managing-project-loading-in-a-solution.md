---
title: O carregamento do projeto em uma solução de gerenciamento | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2ead4834f1d29baff099eedbf464c1ba6344ca6c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49950193"
---
# <a name="manage-project-loading-in-a-solution"></a>Gerenciar o carregamento do projeto em uma solução
Soluções do Visual Studio podem conter um grande número de projetos. O comportamento do Visual Studio padrão é carregar todos os projetos em uma solução no momento em que a solução for aberta e para não permitir que o usuário acesse qualquer um dos projetos até que todos eles concluiu o carregamento. Quando o processo de carregamento de projeto vai durar mais de dois minutos, uma barra de progresso é exibida mostrando o número de projetos carregados e o número total de projetos. O usuário pode descarregar projetos enquanto estiver trabalhando em uma solução com vários projetos, mas esse procedimento tem algumas desvantagens: os projetos descarregados não são compilados como parte de um comando recompilar solução e IntelliSense descrições dos tipos e membros de fechado projetos não são exibidos.  
  
 Os desenvolvedores podem reduzir tempos de carregamento de solução e gerenciar o comportamento de carregamento, criando uma carga de solução Gerenciador de projeto. O Gerenciador de carga de solução Certifique-se de que os projetos sejam carregados antes de iniciar uma compilação em segundo plano, atrasar o carregamento de plano de fundo até que outras tarefas em segundo plano sejam concluídas e realizar outras tarefas de gerenciamento de carga de projeto.  
  
## <a name="create-a-solution-load-manager"></a>Criar uma carga de solução Gerenciador  
 Os desenvolvedores podem criar Gerenciador de uma carga de solução com a implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager> e sugerindo que o Visual Studio que o Gerenciador de carga de solução está ativo.  
  
### <a name="activate-a-solution-load-manager"></a>Ativar um Gerenciador de carga de solução  
 Visual Studio permite que apenas um Gerenciador de carga de solução em um determinado momento, portanto, você precisará informar o Visual Studio quando você deseja ativar a carga de solução gerenciador. Se um segundo Gerenciador de carga de solução é ativado mais tarde, seu Gerenciador de carga de solução será desconectado.  
  
 Você deve obter o <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> de serviço e defina o <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> propriedade:  
  
```csharp  
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;  
object objLoadMgr = this;   //the class that implements IVsSolutionManager  
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);  
```  
  
 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A> método é chamado quando o Visual Studio está sendo desligado ou quando um pacote diferente assumiu como o Gerenciador de carga de solução ativa chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A> com o <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> propriedade.  
  
#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>Estratégias para diferentes tipos de Gerenciador de carga de solução  
 Você pode implementar gerenciadores de carga de solução de diferentes maneiras, dependendo dos tipos de soluções que eles devem gerenciar.  
  
 Se o Gerenciador de carga de solução destina-se para gerenciar a solução de carregamento em geral, ele pode ser implementado como parte de um VSPackage. O pacote deve ser definido como autoload adicionando o <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> sobre o VSPackage com um valor de <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid>. O Gerenciador de carga de solução, em seguida, pode ser ativado no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método.  
  
> [!NOTE]
>  Para obter mais informações sobre pacotes realiza o carregamento automático, consulte [carregar VSPackages](../extensibility/loading-vspackages.md).  
  
 Como o Visual Studio reconhece apenas o última solução Gerenciador de carga a ser ativado, gerenciadores de carga de solução geral sempre devem detectar se há um Gerenciador de carga existente antes de ativar a mesmos. Se chamar `GetProperty()` no serviço para solução <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4> retorna `null`, não há nenhum Gerenciador de carga de solução ativa. Se ele retornar nulo, verifique se o objeto é o mesmo que seu gerente de carga de solução.  
  
 Se o Gerenciador de carga de solução destina-se para gerenciar apenas alguns tipos de solução, o VSPackage pode assinar eventos de carregamento de solução (chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A>) e usar o manipulador de eventos para <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A> para ativar o Gerenciador de carga de solução.  
  
 Se o Gerenciador de carga de solução destina-se para gerenciar apenas soluções específicas, as informações de ativação podem ser persistente como parte do arquivo de solução chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> para a seção de solução de pré-lançamento.  
  
 Gerenciadores de carga de solução específica devem desativar a mesmos no <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A> manipulador de eventos, para não entram em conflito com outros gerenciadores de carga de solução.  
  
 Se precisar de um Gerenciador de carga de solução somente para persistir as propriedades de carga global de projetos (por exemplo, propriedades definidas em uma página de opções), você pode ativar o Gerenciador de carga de solução no <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> manipulador de eventos, manter a configuração nas propriedades da solução, em seguida, Desative o Gerenciador de carga de solução.  
  
## <a name="handle-solution-load-events"></a>Manipular eventos de carga de solução  
 Para assinar eventos de carregamento de solução, chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> quando você ativa o Gerenciador de carga de solução. Se você implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents>, você pode responder a eventos relacionados ao carregar propriedades de projeto diferente.  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>: Esse evento é acionado antes que uma solução é aberta.
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>: Esse evento é acionado depois que a solução seja completamente carregada, mas antes da tela de fundo, carregar o projeto começa novamente.
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>: Esse evento é acionado depois que uma solução totalmente inicialmente é carregada, se há um Gerenciador de carga de solução. Ele também é acionado após o carregamento em segundo plano ou demanda de carga sempre que a solução torna-se totalmente carregada. Ao mesmo tempo, <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid> for reativado.  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>: Esse evento é acionado antes do carregamento de um projeto (ou projetos). Para garantir que outros processos em segundo plano sejam concluídos antes que os projetos sejam carregados, defina `pfShouldDelayLoadToNextIdle` à **verdadeiro**.  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>: Esse evento é disparado quando um lote de projetos está prestes a ser carregado. Se `fIsBackgroundIdleBatch` for true, os projetos devem ser carregados em segundo plano; se `fIsBackgroundIdleBatch` for falso, os projetos são a ser carregado de forma síncrona como resultado de uma solicitação de usuário, por exemplo se o usuário expande um projeto pendente no Gerenciador de soluções. Você pode manipular esse evento para fazer o trabalho de que outra forma precisaria ser feito em <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>.  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>: Esse evento é acionado depois que um lote de projetos foi carregado.  
  
## <a name="detect-and-manage-solution-and-project-loading"></a>Detectar e gerenciar a solução e o carregamento do projeto  
 Para detectar o estado de carregamento de projetos e soluções, chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A> com os seguintes valores:  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>: `var` retorna `true` se a solução e todos os seus projetos forem carregados, caso contrário, `false`.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>: `var` retorna `true` se um lote de projetos está atualmente sendo carregado em segundo plano, caso contrário, `false`.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4>: `var` retorna `true` se um lote de projetos está atualmente sendo carregado de forma síncrona como resultado de um comando de usuário ou outro carregamento explícito, caso contrário, `false`.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>: `var` retorna `true` se a solução está atualmente sendo fechada, caso contrário, `false`.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>: `var` retorna `true` se uma solução está atualmente sendo aberta, caso contrário, `false`.  
  
  Você também pode garantir que os projetos e soluções são carregadas chamando um dos seguintes métodos:  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>: chamar esse método força os projetos em uma solução para carregar antes que o método retorna.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>: chamar esse método força os projetos na `guidProject` carregar antes que o método retorna.  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>: chamar esse método força o projeto no `guidProjectID` carregar antes que o método retorna.  
