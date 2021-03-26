---
title: Gerenciando o carregamento de projetos em uma solução | Microsoft Docs
description: Saiba como os desenvolvedores podem reduzir os tempos de carregamento da solução e gerenciar o comportamento de carregamento do projeto criando um Gerenciador de carga de solução.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, managing project loading
ms.assetid: 097c89d0-f76a-4aaf-ada9-9a778bd179a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 425f610e8a473460cb7d9170138521e2e7bee08a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073086"
---
# <a name="manage-project-loading-in-a-solution"></a>Gerenciar o carregamento do projeto em uma solução
As soluções do Visual Studio podem conter um grande número de projetos. O comportamento padrão do Visual Studio é carregar todos os projetos em uma solução no momento em que a solução é aberta e não permitir que o usuário acesse qualquer um dos projetos até que todos tenham terminado o carregamento. Quando o processo de carregamento do projeto durar mais de dois minutos, será exibida uma barra de progresso mostrando o número de projetos carregados e o número total de projetos. O usuário pode descarregar projetos enquanto trabalha em uma solução com vários projetos, mas esse procedimento tem algumas desvantagens: os projetos descarregados não são criados como parte de um comando de solução de recompilação, e as descrições do IntelliSense de tipos e membros de projetos fechados não são exibidas.

 Os desenvolvedores podem reduzir os tempos de carregamento da solução e gerenciar o comportamento de carregamento do projeto criando um Gerenciador de carga de solução. O Gerenciador de carga de solução pode garantir que os projetos sejam carregados antes de iniciar uma compilação em segundo plano, atrasar o carregamento em segundo plano até que outras tarefas em segundo plano sejam concluídas e executar outras tarefas de gerenciamento de carga do projeto.

## <a name="create-a-solution-load-manager"></a>Criar um Gerenciador de carga de solução
 Os desenvolvedores podem criar um Gerenciador de carga de solução implementando <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager> e aconselhando o Visual Studio de que o Gerenciador de carga de solução está ativo.

### <a name="activate-a-solution-load-manager"></a>Ativar um Gerenciador de carga de solução
 O Visual Studio permite apenas um Gerenciador de carga de solução em um determinado momento, portanto, você deve aconselhar o Visual Studio quando desejar ativar o Gerenciador de carga de solução. Se um segundo Gerenciador de carga de solução for ativado posteriormente, o Gerenciador de carga de solução será desconectado.

 Você deve obter o <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> serviço e definir o [__VSPROPID4. Propriedade VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) :

```csharp
IVsSolution pSolution = GetService(typeof(SVsSolution)) as IVsSolution;
object objLoadMgr = this;   //the class that implements IVsSolutionManager
pSolution.SetProperty((int)__VSPROPID4.VSPROPID_ActiveSolutionLoadManager, objLoadMgr);
```

 O <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadManager.OnDisconnect%2A> método é chamado quando o Visual Studio está sendo desligado ou quando um pacote diferente assumiu o como o Gerenciador de carga de solução ativo chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.SetProperty%2A> com o [__VSPROPID4. VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) propriedade.

#### <a name="strategies-for-different-kinds-of-solution-load-manager"></a>Estratégias para diferentes tipos de Gerenciador de carga de solução
 Você pode implementar gerenciadores de carga de solução de maneiras diferentes, dependendo dos tipos de soluções que eles devem gerenciar.

 Se o Gerenciador de carga de solução pretende gerenciar o carregamento da solução em geral, ele pode ser implementado como parte de um VSPackage. O pacote deve ser definido como AutoLoad adicionando o <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> no VSPackage com um valor de <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionOpening_guid> . O Gerenciador de carga de solução pode ser ativado no <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> método.

> [!NOTE]
> Para obter mais informações sobre o carregamento automático de pacotes, consulte [carregando VSPackages](../extensibility/loading-vspackages.md).

 Como o Visual Studio reconhece apenas o último Gerenciador de carga de solução a ser ativado, os gerentes de carga de solução geral devem sempre detectar se há um Gerenciador de carga existente antes da ativação. Se estiver chamando `GetProperty()` no serviço de solução para [__VSPROPID4. VSPROPID_ActiveSolutionLoadManager](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_ActiveSolutionLoadManager>) retorna `null` , não há nenhum Gerenciador de carga de solução ativo. Se não retornar NULL, verifique se o objeto é o mesmo que o seu Gerenciador de carga de solução.

 Se o Gerenciador de carga de solução pretende gerenciar apenas alguns tipos de solução, o VSPackage pode assinar eventos de carga de solução (chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> ) e usar o manipulador de eventos para <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A> ativar o Gerenciador de carga de solução.

 Se o Gerenciador de carga de solução pretende gerenciar apenas soluções específicas, as informações de ativação podem ser mantidas como parte do arquivo de solução chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> a seção de pré-solução.

 Os gerenciadores de carga de solução específicos devem ser desativados no <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents.OnAfterCloseSolution%2A> manipulador de eventos, a fim de não entrar em conflito com outros gerenciadores de carga de solução.

 Se você precisar de um Gerenciador de carga de solução apenas para manter as propriedades de carregamento do projeto global (por exemplo, propriedades definidas em uma página de opções), você pode ativar o Gerenciador de carga da solução no <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> manipulador de eventos, persistir a configuração nas propriedades da solução e desativar o Gerenciador de carga da solução.

## <a name="handle-solution-load-events"></a>Manipular eventos de carregamento da solução
 Para assinar eventos de carga de solução, chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AdviseSolutionEvents%2A> quando você ativar seu Gerenciador de carga de solução. Se você implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents> , poderá responder a eventos relacionados a diferentes propriedades de carregamento de projeto.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeOpenSolution%2A>: Esse evento é acionado antes de uma solução ser aberta.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeBackgroundSolutionLoadBegins%2A>: Esse evento é acionado depois que a solução é totalmente carregada, mas antes do carregamento do projeto em segundo plano começar novamente.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterBackgroundSolutionLoadComplete%2A>: Esse evento é acionado depois que uma solução é totalmente carregada inicialmente, independentemente de existir ou não um Gerenciador de carregamento de solução. Ele também é acionado após carga em segundo plano ou carga de demanda sempre que a solução é totalmente carregada. Ao mesmo tempo, <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExistsAndFullyLoaded_guid> é reativada.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnQueryBackgroundLoadProjectBatch%2A>: Esse evento é acionado antes do carregamento de um projeto (ou projetos). Para garantir que outros processos em segundo plano sejam concluídos antes de os projetos serem carregados, defina `pfShouldDelayLoadToNextIdle` como **true**.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnBeforeLoadProjectBatch%2A>: Esse evento é acionado quando um lote de projetos está prestes a ser carregado. Se `fIsBackgroundIdleBatch` for true, os projetos serão carregados em segundo plano; se `fIsBackgroundIdleBatch` for false, os projetos serão carregados de forma síncrona como resultado de uma solicitação de usuário, por exemplo, se o usuário expandir um projeto pendente no Gerenciador de soluções. Você pode lidar com esse evento para fazer um trabalho caro que, de outra forma, precisaria ser feito no <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> .

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionLoadEvents.OnAfterLoadProjectBatch%2A>: Esse evento é acionado após o carregamento de um lote de projetos.

## <a name="detect-and-manage-solution-and-project-loading"></a>Detectar e gerenciar a solução e o carregamento do projeto
 Para detectar o estado de carga de projetos e soluções, chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProperty%2A> com os seguintes valores:

- [__VSPROPID4. VSPROPID_IsSolutionFullyLoaded](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsSolutionFullyLoaded>): `var` retorna `true` se a solução e todos os seus projetos são carregados, caso contrário `false` .

- [__VSPROPID4. VSPROPID_IsInBackgroundIdleLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInBackgroundIdleLoadProjectBatch>): `var` retorna `true` se um lote de projetos estiver sendo carregado em segundo plano no momento, caso contrário `false` .

- [__VSPROPID4. VSPROPID_IsInSyncDemandLoadProjectBatch](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID4.VSPROPID_IsInSyncDemandLoadProjectBatch>): `var` retorna `true` se um lote de projetos está sendo carregado de forma síncrona como resultado de um comando de usuário ou outra carga explícita, caso contrário `false` .

- [__VSPROPID2. VSPROPID_IsSolutionClosing](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2.VSPROPID_IsSolutionClosing>): `var` retorna `true` se a solução está sendo fechada no momento, caso contrário `false` .

- [__VSPROPID. VSPROPID_IsSolutionOpening](<xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID.VSPROPID_IsSolutionOpening>): `var` retorna `true` se uma solução está sendo aberta no momento; caso contrário, `false` .

Você também pode garantir que projetos e soluções sejam carregados chamando um dos seguintes métodos:

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureSolutionIsLoaded%2A>: chamar esse método força os projetos em uma solução a serem carregados antes que o método seja retornado.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectIsLoaded%2A>: chamar esse método força os projetos `guidProject` a serem carregados antes que o método retorne.

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution4.EnsureProjectsAreLoaded%2A>: chamar esse método força o projeto a `guidProjectID` carregar antes que o método retorne.
