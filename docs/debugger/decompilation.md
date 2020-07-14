---
title: Descompilar código .NET durante a depuração | Microsoft Docs
ms.date: 2/2/2020
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- decompilation, debugger, exception
- debugging [Visual Studio], decompilation, source not found
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.openlocfilehash: b7d9ed2f2ceeae21b85fdb8227e65715cb07bc8b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350557"
---
# <a name="generate-source-code-from-net-assemblies-while-debugging"></a>Gerar código-fonte de assemblies do .NET durante a depuração

Ao depurar um aplicativo .NET, você pode achar que deseja exibir o código-fonte que você não tem. Por exemplo, dividindo uma exceção ou usando a pilha de chamadas para navegar até um local de origem.

> [!NOTE]
> * A geração de código-fonte (descompilação) só está disponível para aplicativos .NET e é baseada no projeto [ILSpy](https://github.com/icsharpcode/ILSpy) de código-fonte aberto.
> * A descompilação só está disponível no Visual Studio 2019 16,5 e posterior.
> * Aplicar o atributo [SuppressIldasmAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.compilerservices.suppressildasmattribute) a um assembly ou módulo impede que o Visual Studio tente a descompilação.

## <a name="generate-source-code"></a>Gerar código-fonte

Quando você estiver Depurando e nenhum código-fonte estiver disponível, o Visual Studio mostrará o documento de **origem não encontrado** ou, se você não tiver símbolos para o assembly, o documento **nenhum símbolo carregado** . Ambos os documentos têm uma opção de **código-fonte de descompilação** que gera código C# para o local atual. O código C# gerado pode ser usado assim como qualquer outro código-fonte. Você pode exibir o código, inspecionar variáveis, definir pontos de interrupção e assim por diante.

### <a name="no-symbols-loaded"></a>Nenhum símbolo carregado

A ilustração a seguir mostra a mensagem **nenhum símbolo carregado** .

![Captura de tela sem documento carregado de símbolo](media/decompilation-no-symbol-found.png)

### <a name="source-not-found"></a>Origem não encontrada

A ilustração a seguir mostra a mensagem **fonte não encontrada** .

![Captura de tela do documento fonte não encontrada](media/decompilation-no-source-found.png)

## <a name="generate-and-embed-sources-for-an-assembly"></a>Gerar e inserir fontes para um assembly

Além de gerar o código-fonte para um local específico, você pode gerar todo o código-fonte para um determinado assembly .NET. Para fazer isso, vá para a janela **módulos** e, no menu de contexto de um assembly .net, e selecione o comando **descompilar código-fonte** . O Visual Studio gera um arquivo de símbolo para o assembly e, em seguida, insere a origem no arquivo de símbolo. Em uma etapa posterior, você pode [extrair](#extract-and-view-the-embedded-source-code) o código-fonte incorporado.

![Captura de tela do menu de contexto do assembly na janela de módulos com o comando de origem de descompilação.](media/decompilation-decompile-source-code.png)

## <a name="extract-and-view-the-embedded-source-code"></a>Extrair e exibir o código-fonte inserido

Você pode extrair os arquivos de origem inseridos em um arquivo de símbolo usando o comando **extrair código-fonte** no menu de contexto da janela **módulos** .

![Captura de tela do menu de contexto do assembly na janela de módulos com o comando extrair fontes.](media/decompilation-extract-source-code.png)

Os arquivos de origem extraídos são adicionados à solução como [arquivos diversos](../ide/reference/miscellaneous-files.md). O recurso de arquivos diversos está desativado por padrão no Visual Studio. Você pode habilitar esse recurso na caixa de seleção **ferramentas**  >  **Options**  >  documentos do**ambiente**  >  **Documents**  >  **Mostrar arquivos diversos na Gerenciador de soluções** . Sem habilitar esse recurso, você não poderá abrir o código-fonte extraído.

![Captura de tela da página opção de ferramentas com a opção diversos arquivos habilitada.](media/decompilation-tools-options-misc-files.png)

Os arquivos de origem extraídos aparecem nos arquivos diversos em **Gerenciador de soluções**.

![Captura de tela do Gerenciador de soluções com arquivos diversos.](media/decompilation-solution-explorer.png)

## <a name="known-limitations"></a>Limitações conhecidas

### <a name="requires-break-mode"></a>Requer o modo de interrupção

A geração do código-fonte usando a descompilação só é possível quando o depurador está no modo de interrupção e o aplicativo é pausado. Por exemplo, o Visual Studio entra no modo de interrupção quando atinge um ponto de interrupção ou uma exceção. Você pode facilmente disparar o Visual Studio para interromper na próxima vez em que o seu código for executado usando o comando **Break All** ( ![ ícone interromper tudo ](media/decompilation-break-all.png) ).

### <a name="decompilation-limitations"></a>Limitações de descompilação

A geração do código-fonte do formato intermediário (IL) usado em assemblies .NET tem algumas limitações inerentes. Como tal, o código-fonte gerado não se parece com o código-fonte original. A maioria das diferenças é em locais onde as informações no código-fonte original não são necessárias no tempo de execução. Por exemplo, informações como espaço em branco, comentários e nomes de variáveis locais não são necessárias em tempo de execução. Recomendamos que você use a origem gerada para entender como o programa está em execução e não como uma substituição para o código-fonte original.

### <a name="debug-optimized-or-release-assemblies"></a>Depurar assemblies otimizados ou de versão

Ao depurar o código que foi descompilado de um assembly que foi compilado usando otimizações do compilador, você pode ter os seguintes problemas:
- Os pontos de interrupção nem sempre podem ser associados ao local de fornecimento correspondente.
- A depuração pode nem sempre passar para o local correto.
- As variáveis locais podem não ter nomes precisos.
- Algumas variáveis podem não estar disponíveis para avaliação.

Mais detalhes podem ser encontrados no problema do GitHub: [integração do ICSharpCode. decompilador ao depurador do vs](https://github.com/icsharpcode/ILSpy/issues/1901).

### <a name="decompilation-reliability"></a>Confiabilidade de descompilação

Uma porcentagem relativamente pequena de tentativas de descompilação pode resultar em falha. Isso ocorre devido a um erro de referência nula de ponto de sequência em ILSpy.  Reduzimos a falha ao detectar esses problemas e, normalmente, falha na tentativa de descompilação.

Mais detalhes podem ser encontrados no problema do GitHub: [integração do ICSharpCode. decompilador ao depurador do vs](https://github.com/icsharpcode/ILSpy/issues/1901).

### <a name="limitations-with-async-code"></a>Limitações com código assíncrono

Os resultados de descompilação de módulos com padrões de código Async/Await podem estar incompletos ou falhar inteiramente. A implementação ILSpy de Async/Await e yield State-Machines é implementada apenas parcialmente. 

Mais detalhes podem ser encontrados no problema do GitHub: [status do gerador de PDB](https://github.com/icsharpcode/ILSpy/issues/1422).

### <a name="just-my-code"></a>Apenas Meu Código

As configurações de [apenas meu código (JMC)](https://docs.microsoft.com/visualstudio/debugger/just-my-code) permitem que o Visual Studio Percorra o sistema, a estrutura, a biblioteca e outras chamadas que não são de usuário. Durante uma sessão de depuração, a janela **módulos** mostra quais módulos de código o depurador está tratando como meu código (código do usuário).

A descompilação de módulos otimizados ou de versão produz código que não é de usuário. Se o depurador interromper o código de não-usuário descompilado, por exemplo, a janela **nenhuma fonte** será exibida. Para desabilitar apenas meu código, navegue até **ferramentas**  >  **Opções** (ou **Debug**  >  **Opções**de depuração) > **depuração**  >  **geral**e, em seguida, desmarque **habilitar apenas meu código**.

### <a name="extracted-sources"></a>Fontes extraídas

O código-fonte extraído de um assembly tem as seguintes limitações:
- O nome e o local dos arquivos gerados não são configuráveis.
- Os arquivos são temporários e serão excluídos pelo Visual Studio.
- Os arquivos são colocados em uma única pasta e qualquer hierarquia de pastas que as fontes originais tinham não ser usada.
- O nome de arquivo para cada arquivo contém um hash de soma de verificação do arquivo.

### <a name="generated-code-is-c-only"></a>O código gerado é somente C#
A descompilação gera apenas arquivos de código-fonte em C#. Não há nenhuma opção para gerar arquivos em qualquer outro idioma.
