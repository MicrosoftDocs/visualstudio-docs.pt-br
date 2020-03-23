---
title: 'Passo a passo: Usar APIs do criador de perfil | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
ms.assetid: c2ae0b3e-a0ca-4967-b4df-e319008f520e
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 81071a44b51b1441782b25741126873fc720ed7b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/18/2020
ms.locfileid: "74779877"
---
# <a name="walkthrough-using-profiler-apis"></a>Passo a passo: usando APIs do criador de perfil

O passo a passo usa um aplicativo C# para demonstrar como usar as APIs de Ferramentas de criação de perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Você usará as APIs do criador de perfil para limitar a quantidade de dados coletados durante a criação de perfil de instrumentação.

 As etapas neste passo a passo geralmente se aplicam a um aplicativo C/C++. Para cada idioma, você precisará configurar o ambiente de compilação adequadamente.

 Normalmente, você começará a analisar o desempenho do aplicativo usando a criação de perfil de amostra. Se a criação de perfil de amostra não fornecer informações que indiquem um gargalo, a criação de perfil de instrumentação poderá fornecer um nível maior de detalhes. A criação de perfil de instrumentação é muito útil para investigar a interação de thread.

 No entanto, um nível maior de detalhe significa que mais dados são coletados. Você pode perceber que a criação de perfil de instrumentação cria arquivos de dados grandes. Além disso, provavelmente a instrumentação afetará o desempenho do aplicativo. Para saber mais, confira [Noções básicas sobre valores de dados de instrumentação](../profiling/understanding-instrumentation-data-values.md) e [Noções básicas sobre valores de dados de amostragem](../profiling/understanding-sampling-data-values.md)

 O criador de perfil do Visual Studio permite que você limite a coleta de dados. Este passo a passo oferece um exemplo de como limitar a coleta de dados usando as APIs do criador de perfil. O criador de perfil do Visual Studio fornece uma API para controlar a coleta de dados de dentro de um aplicativo.

 ::: moniker range="vs-2017"
 Para o código nativo, as APIs do criador de perfil do Visual Studio estão em *VSPerf.dll*. O arquivo de cabeçalho, *VSPerf.h*, e a biblioteca de importação, *VSPerf.lib*, estão localizados no diretório *Microsoft Visual Studio\2017\Team Tools\Performance Tools\PerfSDK*.  Para aplicativos de 64 bits, a pasta é *Microsoft Visual Studio\2017\Team Tools\Performance Tools\x64\PerfSDK*
 ::: moniker-end

 Para código gerenciado, as APIs do profiler estão no *Microsoft.VisualStudio.Profiler.dll*. Essa DLL é encontrada no diretório *Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools*. Para aplicativos de 64 bits, a pasta é *Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools\x64*. Para saber mais, confira [Profiler](/previous-versions/ms242704(v=vs.140)).

## <a name="prerequisites"></a>Pré-requisitos
 Este passo a passo pressupõe que a escolha do ambiente de desenvolvimento está configurada para dar suporte à depuração e amostragem. Os tópicos a seguir fornecem uma visão geral desses pré-requisitos:

- [Como: Escolher métodos de coleta](../profiling/how-to-choose-collection-methods.md)

- [Como: Referenciar informações de símbolos do Windows](../profiling/how-to-reference-windows-symbol-information.md)

 Por padrão, quando o criador de perfil é iniciado, ele coleta dados no nível global. O código a seguir no início do programa desativa a criação de perfil global.

```csharp
DataCollection.StopProfile(
ProfileLevel.Global,
DataCollection.CurrentId);
```

 Você pode desativar a coleta de dados na linha de comando sem usar uma chamada de API. As etapas a seguir pressupõem que o ambiente de compilação de linha de comando está configurado para executar as ferramentas de criação de perfil e como suas ferramentas de desenvolvimento. Isso inclui as configurações necessárias para VSInstr e VSPerfCmd. Consulte [ferramentas de criação de perfil de linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md).

## <a name="limit-data-collection-using-profiler-apis"></a>Limitar a coleta de dados usando APIs do criador de perfil

#### <a name="to-create-the-code-to-profile"></a>Para criar o código para o perfil

1. Crie um novo projeto C# no Visual Studio, ou use uma compilação de linha de comando, dependendo de sua preferência.

    > [!NOTE]
    > O build precisa referenciar a biblioteca *Microsoft.VisualStudio.Profiler.dll*, localizada no diretório *Microsoft Visual Studio\Shared\Common\VSPerfCollectionTools*.

2. Copie e cole o código a seguir em seu projeto:

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;
    using Microsoft.VisualStudio.Profiler;

    namespace ConsoleApplication1
    {
        class Program
        {
            public class A
            {
                private int _x;

                public A(int x)
                {
                    _x = x;
                }

                public int DoNotProfileThis()
                {
                    return _x * _x;
                }

                public int OnlyProfileThis()
                {
                    return _x + _x;
                }

                public static void Main()
                {
                    DataCollection.StopProfile(
                    ProfileLevel.Global,
                    DataCollection.CurrentId);

                    A a = new A(2);
                    Console.WriteLine("2 square is {0}", a.DoNotProfileThis());

                    DataCollection.StartProfile(
                    ProfileLevel.Global,
                    DataCollection.CurrentId);

                    int x;
                    x = a.OnlyProfileThis();

                    DataCollection.StopProfile(
                    ProfileLevel.Global,
                    DataCollection.CurrentId);

                    Console.WriteLine("2 doubled is {0}", x);
                }
            }

        }
    }
    ```

#### <a name="to-collect-and-view-data-in-the-visual-studio-ide"></a>Para coletar e exibir dados no IDE do Visual Studio

1. Abra o IDE do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. No menu **Analisar,** aponte para **Profiler**e selecione **Nova sessão de desempenho**.

2. Adicione o binário compilado à lista **Destinos** na janela **Gerenciador de Desempenho**. Clique com botão direito do mouse em **Destinos** e, em seguida, selecione **Adicionar Binário de Destino**. Localize o binário na caixa de diálogo **Adicionar Binário de Destino** e clique em **Abrir**.

3. Selecione **Instrumentação**, na lista **Método**, na barra de ferramentas **Gerenciador de Desempenho**.

4. Clique em **Iniciar a Criação de Perfil**.

    O criador de perfil instrumentará e executará o binário e criará um arquivo de relatório de desempenho. O arquivo de relatório de desempenho aparecerá no nó **Relatórios** do **Gerenciador de Desempenho**.

5. Abra o arquivo de relatório de desempenho resultante.

   Por padrão, quando o criador de perfil for iniciado, ele coletará dados no nível global. O código a seguir no início do programa desativa a criação de perfil global.

```csharp
DataCollection.StopProfile(
ProfileLevel.Global,
DataCollection.CurrentId);
```

#### <a name="to-collect-and-view-data-at-the-command-line"></a>Para coletar e exibir dados na linha de comando

1. Compile uma versão de depuração do código de exemplo que você criou no procedimento "Criar o código para o perfil" neste passo a passo.

2. Para criar o perfil de um aplicativo gerenciado, digite o comando a seguir para definir as variáveis de ambiente apropriadas:

     **VsPerfCLREnv /traceon**

3. Digite este comando: **VSInstr \<filename>.exe**

4. Digite este comando: **VSPerfCmd /start:trace /output:\<filename>.vsp**

5. Digite este comando: **VSPerfCmd /globaloff**

6. Execute seu programa.

7. Digite este comando: **VSPerfCmd /shutdown**

8. Digite este comando: **VSPerfReport /calltrace:\<filename>.vsp**

     Um arquivo .*csv* é criado no diretório atual com os dados de desempenho resultantes.

## <a name="see-also"></a>Confira também

- [Profiler](/previous-versions/ms242704(v=vs.140))
- [Referência de API do profiler do Visual Studio (nativa)](../profiling/visual-studio-profiler-api-reference-native.md)
- [Começando](../profiling/getting-started-with-performance-tools.md)
- [Criar perfil da linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md)
