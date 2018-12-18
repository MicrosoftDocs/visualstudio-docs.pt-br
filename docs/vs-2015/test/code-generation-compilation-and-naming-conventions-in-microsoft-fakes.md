---
title: Convenções de nomenclatura, geração de código e compilação no Microsoft Fakes | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 20221de4-2a9e-4787-b99a-b5855bb90872
caps.latest.revision: 18
ms.author: gewarren
manager: douge
ms.openlocfilehash: 1de284c8d4fdfe5cb84a474641b880590c2094aa
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49895310"
---
# <a name="code-generation-compilation-and-naming-conventions-in-microsoft-fakes"></a>Geração de código, compilação e convenções de nomenclatura no Microsoft Fakes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico discute problemas e opções na compilação e geração de código do Fakes e descreve as convenções de nomenclatura para tipos, membros e parâmetros gerados pelo Fakes.  
  
 **Requisitos**  
  
-   Visual Studio Enterprise  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 [Geração e compilação de código](#BKMK_Code_generation_and_compilation)  
  
- [Configurando a geração de código de stubs](#BKMK_Configuring_code_generation_of_stubs) • [Filtragem de tipo](#BKMK_Type_filtering) • [Usando stubs em classes concretas e métodos virtuais](#BKMK_Stubbing_concrete_classes_and_virtual_methods) • [Tipos internos](#BKMK_Internal_types) • [Otimizando tempos de build](#BKMK_Optimizing_build_times) • [Evitando conflitos entre nomes de assembly](#BKMK_Avoiding_assembly_name_clashing)  
  
  [Convenções de nomenclatura do Fakes](#BKMK_Fakes_naming_conventions)  
  
- [Convenções de nomenclatura de tipo do stub e tipo do shim](#BKMK_Shim_type_and_stub_type_naming_conventions) • [Convenções de nomenclatura de propriedade delegada de shim ou campo delegado de stub](#BKMK_Shim_delegate_property_or_stub_delegate_field_naming_conventions) • [Convenções de nomenclatura de tipo de parâmetro](#BKMK_Parameter_type_naming_conventions) • [Regras recursivas](#BKMK_Recursive_rules)  
  
  [Recursos externos](#BKMK_External_resources)  
  
- [Diretrizes](#BKMK_Guidance)  
  
##  <a name="BKMK_Code_generation_and_compilation"></a> Geração e compilação de código  
  
###  <a name="BKMK_Configuring_code_generation_of_stubs"></a> Configurando a geração de código de stubs  
 A geração de tipos de stub é configurada em um arquivo XML que tem a extensão de arquivo .fakes. A estrutura do Fakes integra-se no processo de build por meio de tarefas personalizadas do MSBuild e detecta esses arquivos no momento do build. O gerador de código do Fakes compila os tipos de stub em um assembly e adiciona a referência ao projeto.  
  
 O exemplo a seguir ilustra os tipos de stub definidos em FileSystem.dll:  
  
```xml  
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">  
    <Assembly Name="FileSystem"/>  
</Fakes>  
  
```  
  
###  <a name="BKMK_Type_filtering"></a> Filtragem de tipo  
 Filtros podem ser configurados no arquivo .fakes para restringir os tipos que devem conter stubs. Você pode adicionar um número ilimitado de elementos Clear, Add e Remove sob o elemento StubGeneration para criar a lista de tipos selecionados.  
  
 Por exemplo, esse arquivo .fakes gera stubs para tipos nos namespaces System e System.IO mas exclui qualquer tipo que contém "Handle" em System:  
  
```xml  
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">  
  <Assembly Name="mscorlib" />  
  <!-- user code -->  
  <StubGeneration>  
    <Clear />  
    <Add Namespace="System!" />  
    <Add Namespace="System.IO!"/>  
    <Remove TypeName="Handle" />  
  </StubGeneration>  
  <!-- /user code -->  
</Fakes>  
```  
  
 As cadeias de caracteres de filtro usam uma gramática simples para definir como a correspondência deve ser feita:  
  
-   Filtros não diferenciam maiúsculas de minúsculas por padrão; os filtros executam uma correspondência de subcadeia de caracteres:  
  
     `el` corresponde a "hello"  
  
-   Adicionar `!` ao final do filtro tornará essa uma correspondência perfeita de maiúsculas e minúsculas:  
  
     `el!` não corresponde a "hello"  
  
     `hello!` corresponde a "hello"  
  
-   Adicionar `*` ao final do filtro fará com que ele corresponda ao prefixo da cadeia de caracteres:  
  
     `el*` não corresponde a "hello"  
  
     `he*` corresponde a "hello"  
  
-   Vários filtros em uma lista separada por ponto e vírgula são combinados como uma disjunção:  
  
     `el;wo` corresponde a "hello" e "world"  
  
###  <a name="BKMK_Stubbing_concrete_classes_and_virtual_methods"></a> Usando stubs em classes concretas e métodos virtuais  
 Por padrão, os tipos de stub são gerados para todas as classes não lacradas. É possível restringir os tipos de stub para classes abstratas por meio do arquivo de configuração .fakes:  
  
```xml  
<Fakes xmlns="http://schemas.microsoft.com/fakes/2011/">  
  <Assembly Name="mscorlib" />  
  <!-- user code -->  
  <StubGeneration>  
    <Types>  
      <Clear />  
      <Add AbstractClasses="true"/>  
    </Types>  
  </StubGeneration>  
  <!-- /user code -->  
</Fakes>  
```  
  
###  <a name="BKMK_Internal_types"></a> Tipos internos  
 O gerador de código do Fakes gerará tipos de shim e tipos de stub que são visíveis para o assembly do Fakes gerado. Para tornar os tipos internos de um assembly com shims visível para o Fakes e para seu assembly de teste, adicione atributos <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> no código do assembly com shims que proporciona visibilidade para o assembly do Fakes gerado e para o assembly de teste. Veja um exemplo:  
  
```csharp  
// FileSystem\AssemblyInfo.cs  
[assembly: InternalsVisibleTo("FileSystem.Fakes")]  
[assembly: InternalsVisibleTo("FileSystem.Tests")]  
```  
  
 **Tipos internos em assemblies com nomes fortes**  
  
 Se o assembly com shims tiver um nome forte e você quiser acessar tipos internos do assembly:  
  
- Ambos seu assembly de teste e o assembly do Fakes devem ter nomes fortes.  
  
- Você deve adicionar as chaves públicas do assemblies do Fakes e do teste aos atributos **InternalsVisibleToAttribute** nos assemblies com shims. Eis aqui como nossos atributos de exemplo no código de assembly com shims ficariam quando o assembly com shims tivesse nome forte:  
  
  ```csharp  
  // FileSystem\AssemblyInfo.cs  
  [assembly: InternalsVisibleTo("FileSystem.Fakes",  
      PublicKey=<Fakes_assembly_public_key>)]  
  [assembly: InternalsVisibleTo("FileSystem.Tests",  
      PublicKey=<Test_assembly_public_key>)]  
  ```  
  
  Se o assembly com shims tiver nome forte, a estrutura do Fakes assinará fortemente o assembly do Fakes gerado, automaticamente. Você precisa assinar fortemente o assembly de teste. Consulte [Criando e usando assemblies de nomes fortes](http://msdn.microsoft.com/library/ffbf6d9e-4a88-4a8a-9645-4ce0ee1ee5f9).  
  
  A estrutura do Fakes usa a mesma chave para assinar assemblies gerados, então você pode usar este snippet de código como um ponto de partida para adicionar o atributo **InternalsVisibleTo** do assembly do Fakes ao seu código de assembly com shims.  
  
```csharp  
[assembly: InternalsVisibleTo("FileSystem.Fakes, PublicKey=0024000004800000940000000602000000240000525341310004000001000100e92decb949446f688ab9f6973436c535bf50acd1fd580495aae3f875aa4e4f663ca77908c63b7f0996977cb98fcfdb35e05aa2c842002703cad835473caac5ef14107e3a7fae01120a96558785f48319f66daabc862872b2c53f5ac11fa335c0165e202b4c011334c7bc8f4c4e570cf255190f4e3e2cbc9137ca57cb687947bc")]  
```  
  
 Você pode especificar uma chave pública diferente para o assembly do Fakes, por exemplo, uma chave que você tenha criado para o assembly com shims, especificando o caminho completo para o arquivo **.snk** que contém a chave alternativa como o valor do atributo `KeyFile` no elemento `Fakes`\\`Compilation` do arquivo **.fakes**. Por exemplo:  
  
```xml  
<-- FileSystem.Fakes.fakes -->  
<Fakes ...>  
  <Compilation KeyFile="full_path_to_the_alternate_snk_file" />  
</Fakes>  
  
```  
  
 Em seguida, você deve usar a chave pública do arquivo **.snk** alternativo como o segundo parâmetro do atributo InternalVisibleTo para o assembly do Fakes no código de assembly com shims:  
  
```csharp  
// FileSystem\AssemblyInfo.cs  
[assembly: InternalsVisibleTo("FileSystem.Fakes",  
    PublicKey=<Alternate_public_key>)]  
[assembly: InternalsVisibleTo("FileSystem.Tests",  
    PublicKey=<Test_assembly_public_key>)]  
```  
  
 No exemplo acima, os valores de `Alternate_public_key` e `Test_assembly_public_key` podem ser iguais.  
  
###  <a name="BKMK_Optimizing_build_times"></a> Otimizando tempos de build  
 O build de assemblies do Fakes pode aumentar significativamente o tempo de build. Você pode minimizar o tempo de build, gerando os assemblies do Fakes para assemblies do .NET System e assemblies de terceiros em um projeto centralizado separado. Já que esses assemblies raramente são alterados em seu computador, é possível reutilizar os assemblies do Fakes gerados em outros projetos.  
  
 De seus projetos de teste de unidade, você pode simplesmente fazer uma referência aos assemblies do Fakes compilados que são colocados em FakesAssemblies na pasta do projeto.  
  
1.  Crie uma nova biblioteca de classes com a versão de tempo de execução do .NET que corresponde aos seus projetos de teste. Vamos chamá-la de Fakes.Prebuild. Remova o arquivo class1.cs so projeto, ele não é necessário.  
  
2.  Adicione uma referência a todos os assemblies do System e de terceiros para os quais você precisa do Fakes.  
  
3.  Adicione um arquivo .fakes para cada um dos assemblies e compile.  
  
4.  Do seu projeto de teste  
  
    -   Certifique-se de que você tem uma referência para a DLL de tempo de execução do Fakes:  
  
         C:\Arquivos de Programas\Microsoft Visual Studio 12.0\Common7\IDE\PublicAssemblies\Microsoft.QualityTools.Testing.Fakes.dll  
  
    -   Para cada assembly para o qual você criou o Fakes, adicione uma referência para o arquivo DLL correspondente na pasta Fakes.Prebuild\FakesAssemblies do seu projeto.  
  
###  <a name="BKMK_Avoiding_assembly_name_clashing"></a> Evitando conflitos entre nomes de assembly  
 Em um ambiente do Team Build, todas as saídas de build são mescladas em um único diretório. No caso de vários projetos usando falsificações, pode acontecer que assemblies do Fakes de versões diferentes substituam uns aos outros. Por exemplo, TestProject1 fakes mscorlib.dll do .NET Framework 2.0 e TestProject2 fakes mscorlib.dll para o .NET Framework 4 produziriam ambos um assembly do Fakes mscorlib.Fakes.dll.  
  
 Para evitar esse problema, o Fakes deve criar automaticamente nomes de assembly do Fakes de versão qualificada para referências que não sejam de projeto ao adicionar os arquivos .fakes. Um nome de assembly do Fakes de versão qualificada incorpora um número de versão quando você cria o nome de assembly do Fakes:  
  
 Dado um assembly MyAssembly e uma versão 1.2.3.4, o nome de assembly do Fakes é MyAssembly.1.2.3.4.Fakes.  
  
 Você pode alterar ou remover essa versão editando o atributo Version do elemento Assembly no .fakes:  
  
```xml  
attribute of the Assembly element in the .fakes:  
<Fakes ...>  
  <Assembly Name="MyAssembly" Version="1.2.3.4" />  
  ...  
</Fakes>  
  
```  
  
##  <a name="BKMK_Fakes_naming_conventions"></a> Convenções de nomenclatura do Fakes  
  
###  <a name="BKMK_Shim_type_and_stub_type_naming_conventions"></a> Convenções de nomenclatura de tipo de shim e tipo de stub  
 **Namespaces**  
  
- O sufixo .fakes é adicionado ao namespace.  
  
   Por exemplo, o namespace `System.Fakes` contém os tipos de shim do namespace System.  
  
- Global.Fakes contém o tipo de shim do namespace vazio.  
  
  **Nomes de tipo**  
  
- O prefixo Shim é adicionado ao nome de tipo para criar o nome de tipo do shim.  
  
   Por exemplo, ShimExample é o tipo de shim do tipo Example.  
  
- O prefixo Stub é adicionado ao nome de tipo para criar o nome de tipo do stub.  
  
   Por exemplo, StubIExample é o tipo de stub do tipo IExample.  
  
  **Argumentos de tipo e estruturas de tipo aninhado**  
  
- Os argumentos de tipo genérico são copiados.  
  
- A estrutura de tipo aninhado é copiada para os tipos de shim.  
  
###  <a name="BKMK_Shim_delegate_property_or_stub_delegate_field_naming_conventions"></a> Convenções de nomenclatura de propriedade delegada de shim ou campo delegado de stub  
 **Regras básicas** para nomenclatura de campos, começando por um nome vazio:  
  
- O nome do método é acrescentado.  
  
- Se o nome do método for uma implementação de interface explícita, os pontos serão removidos.  
  
- Se o método for genérico, `Of`*n* será acrescentado, em que *n* é o número de argumentos de método genérico.  
  
  **Nomes de método especiais** como setters ou getter da propriedade são tratados conforme descrito na tabela a seguir.  
  
|Se o método for…|Exemplo|Nome do método anexado|  
|-------------------|-------------|--------------------------|  
|Um **construtor**|`.ctor`|`Constructor`|  
|Um **construtor** estático|`.cctor`|`StaticConstructor`|  
|Um **acessador** com nome de método composto de duas partes separadas por "_" (como getters de propriedade)|*kind_name* (caso mais frequente, mas não imposto por ECMA)|*NameKind*, em que ambas as partes foram colocadas em maiusculas e trocadas|  
||Getter de propriedade `Prop`|`PropGet`|  
||Setter de propriedade `Prop`|`PropSet`|  
||Adicionador de eventos|`Add`|  
||Removedor de eventos|`Remove`|  
|Um **operador** composto de duas partes|`op_name`|`NameOp`|  
|Por exemplo: operador +|`op_Add`|`AddOp`|  
|Para um **operador de conversão**, o tipo retornado é anexado.|`T op_Implicit`|`ImplicitOpT`|  
  
 **Observações**  
  
-   **Getters e setters de indexadores** são tratados de modo similar à propriedade. O nome padrão de um indexador é `Item`.  
  
-   Os nomes de **tipo de parâmetro** são transformados e concatenados.  
  
-   O **tipo retornado** será ignorado a menos que haja uma ambiguidade de sobrecarga. Se esse for o caso, o tipo retornado será acrescentado ao final do nome  
  
###  <a name="BKMK_Parameter_type_naming_conventions"></a> Convenções de nomenclatura de tipo de parâmetro  
  
|Fornecido|A cadeia de caracteres acrescentada é…|  
|-----------|-------------------------|  
|Um **tipo**`T`|T<br /><br /> O namespace, estrutura aninhada e tics genéricos são descartados.|  
|Um **parâmetro de saída**`out T`|`TOut`|  
|Um **parâmetro ref**`ref T`|`TRef`|  
|Um **tipo de matriz**`T[]`|`TArray`|  
|Uma **matriz multidimensional** tipo `T[ , , ]`|`T3`|  
|Um **ponteiro** tipo `T*`|`TPtr`|  
|Um **tipo genérico**`T<R1, …>`|`TOfR1`|  
|Um **argumento de tipo genérico**`!i` de tipo `C<TType>`|`Ti`|  
|Um **argumento de tipo genérico**`!!i` do método `M<MMethod>`|`Mi`|  
|Um **tipo aninhado**`N.T`|`N` é acrescentado, depois `T`|  
  
###  <a name="BKMK_Recursive_rules"></a> Regras recursivas  
 As regras a seguir são aplicadas recursivamente:  
  
-   Já que o Fakes usa C# para gerar os assemblies do Fakes, qualquer caractere que produziria um token do C# inválido é escapado para "_" (sublinhado).  
  
-   Se um nome resultante corresponde a qualquer membro do tipo declarativo, um esquema de numeração é usado, acrescentando um contador de dois dígitos, começando por 01.  
  
##  <a name="BKMK_External_resources"></a> Recursos externos  
  
###  <a name="BKMK_Guidance"></a> Diretrizes  
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](http://go.microsoft.com/fwlink/?LinkID=255188)  
  
## <a name="see-also"></a>Consulte também  
 [Isolando código em teste com Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md)



