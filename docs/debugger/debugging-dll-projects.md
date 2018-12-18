---
title: Depurar projetos DLL | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging DLLs
- templates, debugging DLLs
- DLLs, debugging
- debugging [Visual Studio], DLLs
ms.assetid: 433cab30-d191-460b-96f7-90d2530ca243
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c00740b31e5b9d7cc5678bfc248e673a57e59ccf
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305306"
---
# <a name="debug-dlls-in-visual-studio-c-c-visual-basic-f"></a>Depurar DLLs no Visual Studio (C#, C++, Visual Basic, F#)

Uma DLL (biblioteca de vínculo dinâmico) é uma biblioteca que contém o código e dados que podem ser usados por mais de um aplicativo. Você pode usar o Visual Studio para criar, compilar, configurar e depurar DLLs. 

## <a name="create-a-dll"></a>Criar uma DLL

Os seguintes modelos de projeto do Visual Studio podem criar DLLs:

- C#, Visual Basic, ou F# biblioteca de classes 
- C#ou a biblioteca de controles (WCF) de formulários do Windows do Visual Basic 
- C++ Dynamic-Link Library (DLL)

Para obter mais informações, consulte [técnicas de depuração do MFC](../debugger/mfc-debugging-techniques.md).

Depuração de uma biblioteca de WCF é semelhante à depuração de uma biblioteca de classes. Para obter detalhes, consulte [controles dos Windows Forms](/dotnet/framework/winforms/controls/index).  

Você geralmente chama uma DLL de outro projeto. Quando você depura o projeto de chamada, dependendo da configuração de DLL, você pode intervir e depurar o código da DLL. 

## <a name="vxtskdebuggingdllprojectschangingdefaultconfigurations"></a> Configuração de depuração da DLL

Quando você usa um modelo de projeto do Visual Studio para criar um aplicativo, [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] cria automaticamente as configurações necessárias para as configurações de compilação de depuração e versão. Você pode alterar essas configurações, se necessário. Para obter mais informações, confira os seguintes artigos:

- [Configurações do projeto para uma configuração de depuração de C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [Configurações do projeto para configurações de depuração do C#](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Definições do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [Como definir configurações de depuração e versão](../debugger/how-to-set-debug-and-release-configurations.md)  
  
### <a name="set-c-debuggableattribute"></a>Definir DebuggableAttribute C++

Para que o depurador anexar a uma DLL do C++, o código de C++ deve emitir `DebuggableAttribute`. 

**Para definir `DebuggableAttribute`:**

1. Selecione o projeto de DLL do C++ no **Gerenciador de soluções** e selecione o **Properties** ícone, ou clique com botão direito no projeto e selecione **propriedades**. 
   
1. No **propriedades** painel, em **vinculador** > **depuração**, selecione **Sim (/ /ASSEMBLYDEBUG)** para  **Assembly Depurável**. 

Para obter mais informações, consulte [/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute).  

### <a name="vxtskdebuggingdllprojectsexternal"></a> Definir locais de arquivo do DLL de C/C++ 

Para depurar uma DLL externo, um projeto de chamada deve ser capaz de localizar a DLL, sua [arquivo. PDB](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)e quaisquer outros arquivos que requer que a DLL. Você pode criar uma tarefa de compilação personalizada para copiar esses arquivos para seus  *\<pasta do projeto > \Debug* pasta de saída, ou você pode copiar os arquivos neles manualmente.

Para projetos do C/C++, você pode definir o cabeçalho e locais de arquivos do LIB nas páginas de propriedade do projeto, em vez de copiá-los para a pasta de saída. 

**Para definir o C/C++ de cabeçalho e LIB arquivos locais:**

1. Selecione o projeto de DLL de C/C++ no **Gerenciador de soluções** e selecione o **Properties** ícone, ou clique com botão direito no projeto e selecione **propriedades**. 
   
1. Na parte superior a **propriedades** painel, em **Configuration**, selecione **todas as configurações de**.
   
1. Sob **C/C++** > **geral** > **diretórios de inclusão adicionais**, especifique a pasta que contém arquivos de cabeçalho.
   
1. Sob **vinculador** > **geral** > **diretórios de bibliotecas adicionais**, especifique a pasta que contém os arquivos LIB. 
   
1. Sob **vinculador** > **entrada** > **dependências adicionais**, especifique o caminho completo e nome de arquivo para os arquivos LIB.

1. Selecione **OK**.

Para obter mais informações sobre configurações de projeto do C++, consulte [páginas de propriedade (Visual C++)](/cpp/ide/property-pages-visual-cpp).
  
##  <a name="vxtskdebuggingdllprojectsbuildingadebugversion"></a> Criar uma versão de depuração  

Certifique-se de criar uma versão de depuração da DLL antes de iniciar a depuração. Para depurar uma DLL, um aplicativo de chamada deve ser capaz de encontrar sua [arquivo. PDB](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md) e quaisquer outros arquivos que requer que a DLL. 

Você pode criar uma tarefa de compilação personalizada para copiar os arquivos DLL para seu  *\<chamar a pasta do projeto > \Debug* pasta de saída, ou você pode copiar os arquivos neles manualmente.

Certifique-se de chamar a DLL no local correto. Isso pode parecer óbvio, mas se um aplicativo de chamada localiza e carrega uma cópia diferente da DLL, o depurador nunca atingirá os pontos de interrupção que você definir. 

##  <a name="vxtskdebuggingdllprojectswaystodebugthedll"></a> Depurar uma DLL  

É possível executar uma DLL diretamente. Ele deve ser chamado por um aplicativo, normalmente um *.exe* arquivo. Para obter mais informações, consulte [criar e gerenciar projetos do Visual C++](/cpp/ide/creating-and-managing-visual-cpp-projects). 

Para depurar uma DLL, você pode [iniciar a depuração de aplicativo de chamada](#vxtskdebuggingdllprojectsthecallingapplication), ou [debug do projeto de DLL](how-to-debug-from-a-dll-project.md) especificando seu aplicativo de chamada. Você também pode usar o depurador [janela imediata](#vxtskdebuggingdllprojectstheimmediatewindow) para avaliar os métodos ou funções de DLL em tempo de design, sem usar um aplicativo de chamada.

Para obter mais informações, consulte [começar com o depurador](getting-started-with-the-debugger.md).

### <a name="vxtskdebuggingdllprojectsthecallingapplication"></a> Iniciar a depuração de aplicativo de chamada

O aplicativo que chama uma DLL pode ser:  
  
- Um aplicativo a partir um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto na mesma ou em uma solução diferente da DLL.  
- Um aplicativo existente que já esteja implantado e em execução em um computador de teste ou produção.  
- Localizado na Web e acessado por meio de uma URL.  
- Um aplicativo web com uma página da web que insere a DLL.  
  
Para depurar uma DLL de um aplicativo de chamada, você pode:  
  
- Abra o projeto para o aplicativo de chamada e iniciar a depuração, selecionando **Debug** > **iniciar depuração** ou pressionando **F5**.  

  ou  

- Anexe a um aplicativo que já esteja implantado e em execução em um computador de teste ou produção. Use esse método para DLLs em sites ou em aplicativos web. Para obter mais informações, consulte [como: anexar a um processo em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md).  
  
Antes de começar a depurar o aplicativo de chamada, defina um ponto de interrupção na DLL. Ver [usando pontos de interrupção](../debugger/using-breakpoints.md). Quando o ponto de interrupção DLL for atingido, você pode percorrer o código, observando a ação em cada linha. Para obter mais informações, consulte [navegar pelo código no depurador](../debugger/navigating-through-code-with-the-debugger.md).
  
Durante a depuração, você pode usar o **módulos** para verificar as DLLs e *.exe* o aplicativo seja carregado de arquivos. Para abrir o **módulos** janela, durante a depuração, selecione **Debug** > **Windows** > **módulos**. Para obter mais informações, consulte [como: usar a janela módulos](../debugger/how-to-use-the-modules-window.md). 

###  <a name="vxtskdebuggingdllprojectstheimmediatewindow"></a> Usar a janela imediata  

Você pode usar o **imediato** janela para avaliar os métodos ou funções de DLL em tempo de design. O **imediato** janela desempenha a função de um aplicativo de chamada. 

>[!NOTE]
>Você pode usar o **imediato** janela em tempo de design com a maioria dos tipos de projeto. Não há suporte para SQL, projetos da web ou script.

Por exemplo, para testar um método chamado `Test` na classe `Class1`:

1. Com o projeto DLL aberto, abra o **Immediate** janela selecionando **Debug** > **Windows** > **imediato**ou pressionando **Ctrl**+**Alt**+**eu**.  
   
1. Instanciar um objeto do tipo `Class1` digitando o seguinte C# de código no **imediato** janela e pressionando a tecla **Enter**. Esse código gerenciado funciona para C# e Visual Basic, com alterações de sintaxe apropriadas:  
   
   ```csharp
   Class1 obj = new Class1();  
   ```  
  
   No C#, todos os nomes devem ser totalmente qualificados. Todos os métodos ou variáveis devem ser o escopo atual e o contexto de quando o serviço de linguagem tenta avaliar a expressão.  
   
1. Supondo que `Test` aceite um parâmetro `int`, avalie `Test` usando a janela **Imediato**:  
   
   ```csharp
   ?obj.Test(10);  
   ```  
   
   O resultado é impressa na **imediato** janela.  
   
1. Você pode continuar a depuração do `Test` colocando um ponto de interrupção dentro dele e avaliando a função novamente.  
   
   O ponto de interrupção será atingido e você pode percorrer `Test`. Após a execução do `Test`, o Depurador voltará ao modo Design.

##  <a name="vxtskdebuggingdllprojectsmixedmodedebugging"></a> Depuração de modo misto  

Você pode escrever um aplicativo de chamada para uma DLL de com em código gerenciado ou nativo. Se seu aplicativo nativo chama uma DLL gerenciada e você quiser depurar os dois, você pode habilitar os depuradores gerenciados e nativos nas propriedades do projeto. O processo exato depende se você deseja iniciar a depuração de projeto de DLL ou o projeto de aplicativo de chamada. Para obter mais informações, consulte [como: depurar no modo misto](../debugger/how-to-debug-in-mixed-mode.md). 

Você também pode depurar uma DLL nativa de um projeto de chamada gerenciada. Para obter mais informações, consulte [como depurar código gerenciado e nativo](how-to-debug-managed-and-native-code.md). 

## <a name="see-also"></a>Consulte também  
 [Depurar o código gerenciado](../debugger/debugging-managed-code.md)   
 [Tipos de projeto do Visual C++](../debugger/debugging-preparation-visual-cpp-project-types.md)   
 [Tipos de projeto do C#, F# e Visual Basic](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [Configurações do projeto para uma configuração de depuração do C++](../debugger/project-settings-for-a-cpp-debug-configuration.md)   
 [Configurações do projeto para configurações de depuração do C#](../debugger/project-settings-for-csharp-debug-configurations.md)   
 [Definições do projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)   
 [Segurança do depurador](../debugger/debugger-security.md)
