---
title: Como configurar destinos e tarefas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
ms.assetid: 92814100-392a-471d-96fd-e26f637d6cc2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5ceb9415648d4ad5bcfa4c16ca7f10b3a88a6db4
ms.sourcegitcommit: 8ee7efb70a1bfebcb6dd9855b926a4ff043ecf35
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39078108"
---
# <a name="how-to-configure-targets-and-tasks"></a>Como configurar destinos e tarefas
Tarefas do MSBuild selecionadas podem ser definidas para serem executadas no ambiente de destino, independentemente do ambiente do computador de desenvolvimento. Por exemplo, quando você usa um computador de 64 bits para criar um aplicativo destinado a uma arquitetura de 32 bits, as tarefas selecionadas são executadas em um processo de 32 bits.  
  
> [!NOTE]
>  Se uma tarefa de build é escrita em uma linguagem .NET como Visual C# ou Visual Basic e essa tarefa não usa recursos nativos nem ferramentas, ela será executada em qualquer contexto de destino sem adaptação.  
  
## <a name="usingtask-attributes-and-task-parameters"></a>Parâmetros de tarefa e atributos UsingTask  
 Os atributos `UsingTask` a seguir afetam todas as operações de uma tarefa em um processo de build específico:  
  
-   O atributo `Runtime`, se presente, define a versão do CLR (Common Language Runtime) e pode assumir qualquer um destes valores: `CLR2`, `CLR4`, `CurrentRuntime` ou `*` (qualquer tempo de execução).  
  
-   O atributo `Architecture`, se presente, define a plataforma e o número de bit e pode assumir qualquer um destes valores: `x86`, `x64`, `CurrentArchitecture` ou `*` (qualquer arquitetura).  
  
-   O atributo `TaskFactory`, se presente, define a fábrica de tarefas que cria e executa a instância de tarefa e usa apenas o valor `TaskHostFactory`. Para obter mais informações, confira [Fábricas de tarefas](#task-factories) mais adiante neste documento.  
  
```xml  
<UsingTask TaskName="SimpleTask"   
   Runtime="CLR2"  
   Architecture="x86"  
   AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v3.5.dll" />  
```  
  
 Você também pode usar os parâmetros `MSBuildRuntime` e `MSBuildArchitecture` para definir o contexto de destino de uma tarefa individual.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <Target Name="MyTarget">  
      <SimpleTask MSBuildRuntime="CLR2" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
```  
  
 Antes do MSBuild executar uma tarefa, ele procura uma correspondência `UsingTask` que tem o mesmo contexto de destino.  Parâmetros especificados no `UsingTask` mas não na tarefa correspondente são considerados com correspondência.  Parâmetros especificados na tarefa mas não no `UsingTask` correspondente também são considerados com correspondência. Se os valores de parâmetro não forem especificados no `UsingTask` nem na tarefa, os valores assumem o valor `*` por padrão (qualquer parâmetro).  
  
> [!WARNING]
>  Se mais de um `UsingTask` existe e todos têm atributos `TaskName`, `Runtime` e `Architecture` correspondentes, o último a ser avaliado substitui os outros.  
  
 Se os parâmetros são definidos na tarefa, o MSBuild tenta encontrar um `UsingTask` que corresponde a esses parâmetros ou que, pelo menos, não está em conflito com eles.  Mais de um `UsingTask` pode especificar o contexto de destino da mesma tarefa.  Por exemplo, uma tarefa com executáveis diferentes para ambientes de destino diferentes pode ser semelhante a esta:  
  
```xml  
<UsingTask TaskName="MyTool"   
   Runtime="CLR2"  
   Architecture="x86"  
   AssemblyFile="$(MyToolsPath)\MyTool.v2.0.dll" />  
  
<UsingTask TaskName="MyTool"   
   Runtime="CLR4"  
   Architecture="x86"  
   AssemblyFile="$(MyToolsPath)\MyTool.4.0.dll" />  
  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <Target Name="MyTarget">  
      <MyTool MSBuildRuntime="CLR2" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
  
```  
  
## <a name="task-factories"></a>Fábricas de tarefas  
 Antes de executar uma tarefa, o MSBuild verifica para ver se ela é designada para ser executada no contexto do software atual.  Se a tarefa for designada desse modo, o MSBuild a passará para AssemblyTaskFactory, que a executará no processo atual; caso contrário, o MSBuild passará a tarefa para TaskHostFactory, que executará a tarefa em um processo correspondente ao contexto de destino. Mesmo se o contexto atual e o contexto de destino corresponderem, você poderá forçar a execução fora de processo de uma tarefa (para fins de isolamento, segurança ou outros) configurando `TaskFactory` para `TaskHostFactory`.  
  
```xml  
<UsingTask TaskName="MisbehavingTask"   
   TaskFactory="TaskHostFactory"  
   AssemblyFile="$(MSBuildToolsPath)\MyTasks.dll">  
</UsingTask>  
```  
  
## <a name="phantom-task-parameters"></a>Parâmetros de tarefa fantasma  
 Como qualquer outro parâmetro de tarefa, `MSBuildRuntime` e `MSBuildArchitecture` podem ser definidos de propriedades de build.  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <PropertyGroup>  
      <FrameworkVersion>3.0</FrameworkVersion>  
   </PropertyGroup>  
   <Target Name="MyTarget">  
      <SimpleTask MSBuildRuntime="$(FrameworkVerion)" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
```  
  
 Ao contrário de outros parâmetros de tarefa, `MSBuildRuntime` e `MSBuildArchitecture` não são aparentes para a tarefa em si.  Para escrever uma tarefa que reconhece o contexto no qual ela é executada, é necessário testar o contexto chamando o .NET Framework ou usar propriedades de build para passar as informações de contexto por meio de outros parâmetros de tarefa.  
  
> [!NOTE]
>  Os atributos `UsingTask` podem ser definidos no conjunto de ferramentas e nas propriedades do ambiente.  
  
 Os parâmetros `MSBuildRuntime` e `MSBuildArchitecture` fornecem a maneira mais flexível de definir o contexto de destino, mas também é a mais limitada em escopo.  Por um lado, como eles são definidos na própria instância de tarefa e só são avaliados quando a tarefa está prestes a ser executada, eles podem derivar seu valor do escopo completo de propriedades disponíveis em tempo de avaliação e em tempo de build.  Por outro lado, esses parâmetros se aplicam somente a uma instância específica de uma tarefa em um destino específico.  
  
> [!NOTE]
>  Os parâmetros de tarefa são avaliados no contexto do nó pai, não no contexto do host da tarefa. As variáveis de ambiente que são dependentes do tempo de execução ou da arquitetura (como o local *Arquivos de Programas*) serão avaliadas como o valor que corresponde ao nó pai.  No entanto, se a mesma variável de ambiente for lida diretamente pela tarefa, ela será avaliada corretamente no contexto do host da tarefa.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar destinos e tarefas](../msbuild/configuring-targets-and-tasks.md)
