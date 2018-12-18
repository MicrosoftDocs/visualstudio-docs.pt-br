---
title: Depurando projetos de DLL | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging DLLs
- templates, debugging DLLs
- DLLs, debugging
- debugging [Visual Studio], DLLs
ms.assetid: 433cab30-d191-460b-96f7-90d2530ca243
caps.latest.revision: 41
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c5177d7bd43a0bc1ba29778ba99cc891fd9f739b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792379"
---
# <a name="debugging-dll-projects"></a>Depurando projetos de DLL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os modelos a seguir criam DLLs:  
  
- Biblioteca de Classes (C++, C# e Visual Basic)  
  
- (C++, C# e Visual Basic): Biblioteca de Controle Windows Forms  
  
   A depuração de uma Biblioteca de Controles do Windows é semelhante à depuração de um projeto de Biblioteca de Classe. Na maioria dos casos, você chamará o controle do Windows de outro projeto. Ao depurar o projeto de chamada, você poderá entrar no código do controle do Windows, definir pontos de interrupção e executar outras operações de depuração. Para obter mais informações, consulte [controles dos Windows Forms](http://msdn.microsoft.com/library/f050de8f-4ebd-4042-94b8-edf9a1dbd52a).  
  
- (C# e Visual Basic): Biblioteca de Controles da Web  
  
   Para obter mais informações, consulte [biblioteca de controle da Web (código gerenciado)](../debugger/web-control-library-managed-code.md).  
  
- (C++): Controle ActiveX do MFC e Controle Activex de Dispositivo Inteligente do MFC  
  
   Os controles ActiveX são controles que podem ser baixados pela Internet em um computador de cliente, e exibidos e ativados em páginas da Web.  
  
   A depuração dos controles do ActiveX é semelhante à depuração de outros tipos de controles porque não podem ser executadas como autônomas, mas devem ser inseridas em uma página da Web HTML. Para obter mais informações, consulte [como: depurar um controle ActiveX](../debugger/how-to-debug-an-activex-control.md).  
  
- (C++): DLL de Dispositivo Inteligente do MFC  
  
   Para obter mais informações, consulte [técnicas de depuração MFC](../debugger/mfc-debugging-techniques.md).  
  
  Esta seção também contém informações sobre os seguintes tópicos:  
  
- [Como depurar de um projeto de DLL](../debugger/how-to-debug-from-a-dll-project.md)  
  
- [Como depurar no modo misto](../debugger/how-to-debug-in-mixed-mode.md)  
  
  Este tópico contém as seções a seguir, que fornecem considerações sobre como se preparar para depurar bibliotecas de classe:  
  
- [Criação de uma versão de depuração](#vxtskdebuggingdllprojectsbuildingadebugversion)  
  
- [Depuração de modo misto](#vxtskdebuggingdllprojectsmixedmodedebugging)  
  
- [Alterando as configurações padrão](#vxtskdebuggingdllprojectschangingdefaultconfigurations)  
  
- [Maneiras de depurar a DLL](#vxtskdebuggingdllprojectswaystodebugthedll)  
  
- [O aplicativo de chamada](#vxtskdebuggingdllprojectsthecallingapplication)  
  
- [Controles em uma página da Web](#vxtskdebuggingdllprojectscontrolsonawebpage)  
  
- [A janela imediata](#vxtskdebuggingdllprojectstheimmediatewindow)  
  
##  <a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a> Criação de uma versão de depuração  
 Não importa como você inicia a depuração, certifique-se de compilar a versão de Depuração da DLL primeiro e verifique se a versão de Depuração está no local onde o aplicativo espera encontrá-la. Isso pode parecer óbvio, mas se você esquecer desta etapa, o aplicativo poderá encontrar uma versão diferente da DLL e carregá-la. O programa continuará a ser executado enquanto você se pergunta o porquê do ponto de interrupção nunca ter sido atingido. Quando você estiver depurando, você pode verificar quais DLLs seu programa carregou abrindo o depurador **módulos** janela. O **módulos** janela lista cada DLL ou EXE carregado no processo que você está depurando. Para obter mais informações, consulte [como: usar a janela módulos](../debugger/how-to-use-the-modules-window.md).  
  
 Para que o depurador conecte-se ao código escrito em C++, o código deverá emitir `DebuggableAttribute`. Você pode adicionar isso ao seu código automaticamente por meio da vinculação com o [/ASSEMBLYDEBUG](http://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982) a opção de vinculador.  
  
##  <a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a> Depuração de modo misto  
 O aplicativo de chamada que chama a DLL pode ser escrito em código gerenciado ou em código nativo. Se a DLL gerenciada for chamada por código nativo e você quiser depurar os dois, os depuradores gerenciados e nativos deverão estar habilitados. Você pode selecionar na  **\<projeto > páginas de propriedade** caixa de diálogo ou janela. Como você faz isso depende de a depuração ser iniciada do projeto de DLL ou do projeto de aplicativo de chamada. Para obter mais informações, consulte [como: depurar no modo misto](../debugger/how-to-debug-in-mixed-mode.md).  
  
##  <a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a> Alterando as configurações padrão  
 Quando você cria um projeto de aplicativo de console com o modelo de projeto, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria automaticamente as configurações necessárias para as configurações de Depuração e Versão. Se necessário, você pode alterar essas configurações. Para obter mais informações, consulte [configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md), [configurações do projeto para configurações de depuração do c#](../debugger/project-settings-for-csharp-debug-configurations.md), [configurações do projeto para uma configuração de depuração do Visual Basic ](../debugger/project-settings-for-a-visual-basic-debug-configuration.md), e [como: Set Debug and Release Configurations](../debugger/how-to-set-debug-and-release-configurations.md).  
  
##  <a name="vxtskdebuggingdllprojectswaystodebugthedll"></a> Maneiras de depurar a DLL  
 Cada um dos projetos nesta seção cria uma DLL. Você não pode executar uma DLL diretamente. Ela deve ser chamada por um aplicativo, geralmente um EXE. Para obter mais informações, consulte [criando e gerenciando projetos do Visual C++](http://msdn.microsoft.com/library/11003cd8-9046-4630-a189-a32bf3b88047). O aplicativo de chamada pode conter qualquer um dos seguintes critérios:  
  
-   Um aplicativo compilado em outro projeto na mesma solução do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que contém a biblioteca de classes.  
  
-   Um aplicativo existente já implantado em um teste ou em um computador de produção.  
  
-   Localizado na Web e acessado por meio de uma URL.  
  
-   Um aplicativo da Web que contém uma página da Web que insere a DLL.  
  
###  <a name="vxtskdebuggingdllprojectsthecallingapplication"></a> Depurar o aplicativo de chamada  
 Para depurar uma DLL, comece depurando o aplicativo de chamada, normalmente um EXE ou um aplicativo Web. Há várias maneiras de depurá-lo.  
  
- Se você tiver um projeto para o aplicativo de chamada, você pode abrir o projeto e iniciar a execução do **depurar** menu. Para obter mais informações, consulte [como: Iniciar execução](http://msdn.microsoft.com/en-us/b0fe0ce5-900e-421f-a4c6-aa44ddae453c).  
  
- Se o aplicativo de chamada for um programa existente já implantado em um teste ou em um computador de produção e já estiver em execução, você poderá conectar-se a ele. Use este método se a DLL for um controle hospedado pelo Internet Explorer ou um controle em uma página da Web. Para obter mais informações, consulte [como: anexar a um processo em execução](http://msdn.microsoft.com/en-us/636d0a52-4bfd-48d2-89ad-d7b9ca4dc4f4).  
  
- Você pode depurá-lo no projeto da DLL. Para obter mais informações, consulte [como: depurar de um projeto de DLL](../debugger/how-to-debug-from-a-dll-project.md).  
  
- Você pode depurá-lo partir o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **imediato** janela. Nesse caso, o **imediato** janela desempenha a função do aplicativo.  
  
  Antes de começar a depurar o aplicativo de chamada, convém definir um ponto de interrupção na biblioteca de classes. Para obter mais informações, consulte [pontos de interrupção e Tracepoints](http://msdn.microsoft.com/en-us/fe4eedc1-71aa-4928-962f-0912c334d583). Quando o ponto de interrupção for atingido, você poderá percorrer o código, observando a ação em cada linha até isolar o problema. Para obter mais informações, consulte [visão geral de revisão de código](http://msdn.microsoft.com/en-us/8791dac9-64d1-4bb9-b59e-8d59af1833f9).  
  
###  <a name="vxtskdebuggingdllprojectscontrolsonawebpage"></a> Controles em uma página da Web  
 Para depurar um controle de página de Web, crie uma página do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] que o insira caso ainda não exista uma página do tipo. Em seguida, coloque os pontos de interrupção no código da página da Web, bem como no código de controle. Você chama a página da Web do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 Antes de começar a depurar o aplicativo de chamada, você desejará definir um ponto de interrupção no arquivo DLL. Quando o ponto de interrupção for atingido, você poderá percorrer o código, observando a ação em cada linha até isolar o problema. Para obter mais informações, consulte [pontos de interrupção e Tracepoints](http://msdn.microsoft.com/en-us/fe4eedc1-71aa-4928-962f-0912c334d583).  
  
###  <a name="vxtskdebuggingdllprojectstheimmediatewindow"></a> A janela imediata  
 Você pode avaliar funções ou métodos na DLL sem ter um aplicativo de chamada. Fazer a depuração em tempo de design e você usar o **imediato** janela. Para depurar dessa maneira, execute as seguintes etapas enquanto o projeto da DLL estiver aberto:  
  
1.  Abra o depurador **imediato** janela.  
  
2.  Para testar um método chamado `Test` na classe `Class1`, crie uma instância de um objeto do tipo `Class1` digitando o seguinte código em C# na janela Imediato. Esse código gerenciado funciona para o Visual Basic e C++, com as alterações de sintaxe apropriadas:  
  
    ```  
    Class1 obj = new Class1();  
    ```  
  
     No C#, todos os nomes devem ser totalmente qualificados. Além disso, todos os métodos ou variáveis devem estar no escopo e no contexto atuais da sessão de depuração.  
  
3.  Supondo que `Test` usa um `int` parâmetro, avaliar `Test` usando o **imediato** janela:  
  
    ```  
    ?obj.Test(10)  
    ```  
  
     O resultado será impresso na **imediato** janela.  
  
4.  Você pode continuar a depuração do `Test` colocando um ponto de interrupção dentro dele e avaliando a função novamente:  
  
    ```  
    ?obj.Test(10);  
    ```  
  
     O ponto de interrupção será atingido e você poderá depurar `Test`. Após a execução do `Test`, o Depurador voltará ao modo Design.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)   
 [Tipos de projeto do Visual C++](../debugger/debugging-preparation-visual-cpp-project-types.md)   
 [Tipos de projeto do C#, F# e Visual Basic](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [Configurações do projeto para configurações de depuração de C#](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Configurações do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Segurança do depurador](../debugger/debugger-security.md)



