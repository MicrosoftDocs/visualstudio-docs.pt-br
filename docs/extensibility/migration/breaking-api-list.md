---
title: Alterações da API da Visual Studio 2022 Preview
description: Saiba mais sobre as alterações de API que causam falha na compilação das extensões do VS existentes ao migrar extensões para o Visual Studio 2022 Preview.
ms.date: 06/08/2021
ms.topic: reference
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 9427b7a75ad53fc9a0795b249d96431113aba36d
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308662"
---
# <a name="breaking-api-changes-in-visual-studio-2022"></a>Alterações da API da Visual Studio 2022

[!INCLUDE [preview-note](../includes/preview-note.md)]

Se você estiver migrando uma extensão para o Visual Studio 2022, as alterações significativas listadas aqui poderão afetar você.

## <a name="reference-assemblies-no-longer-installed"></a>Assemblies de referência não estão mais instalados

Muitos dos assemblies que você pode ter referenciado que o MSBuild resolveu de um diretório Visual Studio instalação não estão mais instalados. Você deve usar o NuGet para adquirir os assemblies de referência Visual Studio SDK necessários. Confira [Modernizar projetos](update-visual-studio-extension.md#modernize-your-vsix-project) para ver as etapas detalhadas para fazer isso.

## <a name="removed-apis"></a>APIs removidas

No Visual Studio 2022, várias APIs foram removidas como parte da mudança Visual Studio adiante. Uma lista das APIs removidas pode ser encontrada na página [Lista de APIs Removidas.](removed-api-list.md)

## <a name="interop-breaking-changes"></a>Alterações da interop da quebra

Muitas de nossas APIs foram alteradas no Visual Studio 2022, geralmente com alterações simples que são simples para seu código acomodar.

Para gerenciar as alterações significativas, estamos planejando fornecer um novo mecanismo para a distribuição de assemblies de interop. Especificamente, para Visual Studio 2022 e além, fornecemos um único assembly de interop com definições para muitas interfaces Visual Studio públicas comuns. Esse assembly contém definições gerenciadas para muitas interfaces Visual Studio se movendo para fora de vários assemblies de interop. O novo assembly de interop é distribuído por meio do `Microsoft.VisualStudio.Interop` pacote NuGet.

No entanto, Visual Studio componentes que são usados principalmente em contextos nativos e têm um número baixo de alterações significativas continuarão a ter seus próprios assemblies de interop (por exemplo, o assembly do depurador ainda será VisualStudio.Debugger.Interop.dll como acontece hoje). Em qualquer caso, os assemblies podem ser referenciados do seu aplicativo, assim como são hoje.

Essa é uma alteração significativa e significa que as extensões que usam APIs no e no assembly criado nessa nova abordagem não são compatíveis com versões mais antigas do Visual Studio usando o assembly de interop anterior.

Isso tem algumas vantagens muito importantes que facilitarão a atualização da extensão Visual Studio 2022:

- Todas as APIs interrompidas se tornarão erros de tempo de com build, facilitando a encontrar e corrigir.
- Você só precisa atualizar o código que usa uma API que foi interrompida no Visual Studio 2022.
- Você não poderá usar acidentalmente a API antiga e agora interrompida.

Em geral, essas alterações resultarão em uma versão mais estável do Visual Studio para todos os usuários. A principal desvantagem dessa abordagem é que os assemblies gerenciados não poderão ser executados no Visual Studio 2019 e no Visual Studio 2022 sem compilar seu código uma vez para cada versão de Visual Studio de destino.

Ao trabalhar com erros de compilação devido às diferenças de API entre o Visual Studio 2019 e o Visual Studio 2022, você poderá encontrar a API ou o padrão que você está enfrentando listado abaixo com diretrizes sobre como corrigi-la.

### <a name="int-or-uint-where-intptr-is-expected"></a>`int` ou `uint` onde `IntPtr` é esperado

Esperamos que esse seja um erro muito comum. Para tornar Visual Studio 2022 um processo de 64 bits, algumas de nossas APIs de interop tiveram que ser corrigidas, onde supõem que um ponteiro poderia caber em um inteiro de 32 bits para realmente usar um valor de tamanho de ponteiro.

Exemplo de erro:

> Argumento 3: não é possível converter de 'out uint' para 'out System.IntPtr'

Basta atualizar seu código para esperar ou `IntPtr` fornecer ou onde ou costumava ser para resolver a `UIntPtr` `int` `uint` quebra.

Correção de exemplo:

```diff
-shell.LoadLibrary(myGuid, myFlags, out uint ptrLib);
+shell.LoadLibrary(myGuid, myFlags, out IntPtr ptrLib);
```

### <a name="an-interop-type-defined-in-two-assemblies"></a>Um tipo de interop definido em dois assemblies

Quando o compilador C# relata um erro de que um tipo que você está usando está definido em dois assemblies, você provavelmente está referenciando um assembly da versão do Visual Studio 2019 do SDK que você não deve mais referenciar.

Exemplo de erro:

> erro CS0433: o tipo 'IVsDpiAware' existe em 'Microsoft.VisualStudio.Interop, Version=17.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' e 'Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'

Consulte nossa tabela [de remapeamento](migrated-assemblies.md) de assembly de referência para ver qual nome de assembly é o nome preferencial no Visual Studio 2022.
Considerando os dois assemblies nomeados no erro de exemplo acima e observando essa tabela, observe que `Microsoft.VisualStudio.Interop` é o novo nome do assembly. Em seguida, a correção seria remover a `Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime` referência para do projeto.

Em alguns casos, oferecemos um pacote Visual Studio versão 2022 para o assembly preterido que contém encaminhadores de tipo. Quando isso estiver disponível, você  terá a opção de atualizar sua referência de pacote para a versão Visual Studio 2022 em vez de removê-la. Os encaminhadores de tipo resolverão o erro do compilador.

Tenha em mente que, às vezes, essas referências podem vir por referência de pacote transitivo e, portanto, pode ser mais difícil de remover do que uma referência direta feita no arquivo de projeto. Nesses casos, certifique-se de que todas as suas referências de pacote direto estão usando Visual Studio pacotes do SDK 2022 em si. Você pode consultarproject.assets.js *para* identificar a cadeia de pacotes responsáveis por trazer o assembly preterido. Atualizar uma referência de pacote transitivo para uma Visual Studio 2022 é tão fácil quanto instalá-la como uma referência direta.

Se não for possível alterar a árvore de dependência (por exemplo, porque ela envolve uma dependência de terceiros), você poderá adicionar uma referência de pacote direto ao pacote pré-Visual Studio 2022 e adicionar metadados a esse item para resolver o erro do `ExcludeAssets="compile"` `PackageReference` compilador. Mas tenha em mente que, com essa técnica, sua extensão pode manter uma dependência em um assembly pré-Visual Studio 2022 e sua extensão pode funcionar mal em runtime.

### <a name="missing-reference-to-an-interop-assembly"></a>Referência ausente a um assembly de interop

Ao referenciar um assembly compilado no SDK do Visual Studio 2022, você pode receber um erro sobre a falta de uma referência de assembly.

Exemplo de erro:

> Erro CS0012 O tipo 'IVsTextViewFilter' é definido em um assembly que não é referenciado. Você deve adicionar uma referência ao assembly 'Microsoft.VisualStudio.TextManager.Interop, Version=7.1.40304.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'

Usando a [tabela de remapeamento](migrated-assemblies.md)de assembly de referência , você pode confirmar que o assembly solicitado não é, na verdade, um que você deve fazer referência.

A melhor correção é atualizar sua dependência para uma versão compilada no SDK do Visual Studio 2022 para que o assembly de interop removido não seja mais solicitado pelo compilador.

Em alguns casos, oferecemos um pacote Visual Studio versão 2022 para o assembly preterido que contém encaminhadores de tipo. Quando isso estiver disponível, você terá a opção de adicionar uma referência de pacote à versão Visual Studio 2022 do pacote obsoleto para que os encaminhadores de tipo resolvam o erro do compilador.

### <a name="iasyncserviceprovider-is-missing"></a>`IAsyncServiceProvider` está ausente

Há duas definições dessa interface, em dois namespaces. Apenas um deles foi destinado ao consumo gerenciado.

Visual Studio 2019 Namespace | Visual Studio 2022 Namespace | Uso pretendido
--|--|--
Microsoft.VisualStudio.Shell.IAsyncServiceProvider | Microsoft.VisualStudio.Shell.IAsyncServiceProvider | Consumo de código gerenciado
Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider | Microsoft.VisualStudio.Shell.COMAsyncServiceProvider.IAsyncServiceProvider | somente a interop de baixo nível

Se você vir um erro sobre , pode ser que você estava usando aquele destinado `IAsyncServiceProvider` ao código nativo (a segunda linha). 
Se sim, você pode atualizar para o novo namespace ou alternar para a interface mais amigável.

### <a name="dte-and-_dte-type-cast-failures"></a>`DTE` e `_DTE` falhas de cast de tipo

`DTE` e `_DTE` são ambas interfaces. Um deriva do outro. No entanto, Visual Studio 2022, os tipos base e derivado são trocados.
Isso faz com que determinadas atribuições de tipo ou casts falhem.

Isso também significa que, onde você costumava usar `new DTE()` , agora você deve usar `new _DTE()` .

### <a name="missing-argument-on-a-method-invocation"></a>Argumento ausente em uma invocação de método

Alguns métodos não declaram mais argumentos padrão para os parâmetros opcionais na API de interop.
Se você receber um erro sobre um argumento ausente para uma chamada de interop COM e o parâmetro chamar para um tipo, o valor padrão anterior que a API de `object` interop do Visual Studio 2019 definiu pode ter sido , portanto, considere adicionar como seu argumento para resolver o erro de compilação. `""` `""`

Quando estiver em dúvida sobre qual era o argumento padrão, tente alternar o contexto do serviço de linguagem do Visual Studio 2022 para o Visual Studio 2019 para que você receba o IntelliSense com os assemblies de interop mais antigos para ver qual era o argumento padrão e, em seguida, adicione-o explicitamente ao seu código. Ele continuará a funcionar bem quando compilado para o Visual Studio 2019, mas agora será compilado para Visual Studio 2022.

Correção de exemplo:

```diff
-process4.Attach2();
+process4.Attach2("");
```
