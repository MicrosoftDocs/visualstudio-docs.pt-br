---
title: Usando cobertura de código para determinar quanto código está sendo testado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code coverage
ms.assetid: 800fc739-acd2-4242-84cb-1d83b4d82cf9
caps.latest.revision: 38
ms.author: gewarren
manager: douge
ms.openlocfilehash: adeca654f14fd068c7ce1cb042e57dbc3891cbf4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49834052"
---
# <a name="using-code-coverage-to-determine-how-much-code-is-being-tested"></a>Usando cobertura de código para determinar quanto código está sendo testado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para determinar que proporção do código do projeto está sendo testada de fato por testes codificados, como os testes de unidade, você pode usar o recurso de cobertura de código do Visual Studio. Para se proteger efetivamente contra bugs, os testes devem utilizar ou "cobrir" uma grande proporção de seu código.  
  
 A análise de cobertura de código pode ser aplicada ao código gerenciado (CLI) e não gerenciado (nativo).  
  
 A cobertura de código é uma opção quando você executa métodos de teste usando o Gerenciador de Testes. A tabela de resultados mostra a porcentagem do código que foi executada em cada assembly, classe e método. Além disso, o editor de código-fonte mostra que código foi testado.  
  
 ![Resultados da cobertura de código com coloração](../test/media/codecoverage1.png "CodeCoverage1")  
  
 **Requisitos**  
  
-   Visual Studio Enterprise  
  
### <a name="to-analyze-code-coverage-on-unit-tests-in-test-explorer"></a>Para analisar a cobertura de código em testes de unidade no Gerenciador de Testes  
  
1.  No menu **Teste**, escolha **Analisar Cobertura de Código**.  
  
2.  Para ver quais linhas foram executadas, escolha o ![Ícone Mostrar Coloração de Cobertura de Código](../test/media/codecoverage-showcoloringicon.png "CodeCoverage ShowColoringIcon")**Mostrar Coloração de Cobertura de Código**.  
  
     Para alterar as cores ou usar a formatação em negrito, escolha **Ferramentas**, **Opções**, **Ambiente**, **Fontes e Cores**, **Mostrar configurações de: Editor de Texto**. Em **Exibir Itens**, ajuste os itens de cobertura.  
  
3.  Se os resultados mostrarem baixa cobertura, investigue quais partes do código não estão sendo utilizadas e escreva mais testes para abrangê-las. As equipes de desenvolvimento normalmente desejam uma cobertura de código de aproximadamente 80%. Em algumas situações, uma cobertura menor é aceitável. Por exemplo, uma cobertura menor é aceitável onde um código é gerado a partir de um modelo padrão.  
  
> [!TIP]
>  Para obter resultados precisos:  
> 
> - Verifique se a otimização do compilador será desativada.  
> 
>   Se você estiver trabalhando com código não gerenciado (nativo), use uma compilação de depuração.  
>   -   Verifique se você está gerando arquivos .pdb (símbolo) para cada assembly.  
> 
>   Se você não obtiver os resultados esperados, consulte [Solução de problemas de cobertura de código](../test/troubleshooting-code-coverage.md). . Não se esqueça de executar novamente a cobertura de código depois de atualizar seu código. Os resultados de cobertura e a coloração de código não serão atualizados automaticamente depois que você alterar o código ou executar os testes.  
  
## <a name="reporting-in-blocks-or-lines"></a>Emissão de relatórios em os blocos ou linhas  
 A cobertura de código é contada em *blocos*. Um bloco é uma parte do código com exatamente um ponto de entrada e de saída.  Se o fluxo de controle do programa passar por um bloco durante a execução do teste, esse bloco será considerado coberto. O número de vezes que o bloco é usado não tem efeito sobre o resultado.  
  
 Você também pode ter os resultados exibidos em termos de linhas escolhendo **Adicionar/Remover Colunas** no cabeçalho da tabela. Se a execução do teste utilizou todos os blocos de código em qualquer linha de código, isso será contado como uma linha. Onde uma linha contém alguns os blocos de código que foram utilizados e outros não, isso é contado como uma linha parcial.  
  
 Alguns usuários preferem uma contagem de linhas porque as porcentagens correspondem mais aproximadamente ao tamanho dos fragmentos que você vê no código-fonte. Um bloco longo de cálculo contaria como um único bloco mesmo se ocupar muitas linhas.  
  
## <a name="managing-code-coverage-results"></a>Gerenciando os resultados da cobertura de código  
 A janela Resultados da Cobertura de Código geralmente mostra o resultado da execução mais recente. Os resultados podem variar se você alterar os dados de teste ou, se você executar apenas alguns dos testes cada vez.  
  
 A janela de cobertura de código também pode ser usada para exibir os resultados anteriores ou os resultados obtidos em outros computadores.  
  
 É possível mesclar os resultados de várias execuções, por exemplo, das execuções que usam dados de teste diferentes.  
  
-   **Para exibir um conjunto de resultados anterior**, selecione-o no menu suspenso. O menu mostra uma lista temporária que foi desmarcada quando você abrir uma nova solução.  
  
-   **Para exibir os resultados de uma sessão anterior**, escolha **Importar Resultados da Cobertura de Código**, navegue até a pasta TestResults em sua solução e importe um arquivo .coverage.  
  
     A coloração de cobertura podem estar incorreta se o código-fonte foi alterado desde que o arquivo .coverage foi gerado.  
  
-   **Para tornar os resultados legíveis como texto**, escolha **Exportar Resultados da Cobertura de Código**. Isso gera um arquivo .coveragexml legível que você pode processar com outras ferramentas ou enviar facilmente por email.  
  
-   **Para enviar resultados para outra pessoa**, envie um arquivo .coverage ou um arquivo .coveragexml exportado. A pessoa poderá importar o arquivo. Se ela tiver a mesma versão do código-fonte, poderá consultar a coloração de cobertura.  
  
## <a name="merging-results-from-different-runs"></a>Mesclando resultados de execuções diferentes  
 Em algumas situações, os blocos diferentes em seu código serão usados dependendo dos dados de teste. Portanto, você pode querer combinar os resultados de execuções de testes diferentes.  
  
 Por exemplo, suponhamos que, ao executar um teste com a entrada “2 ", você descobre que 50% de uma função específica está coberta. Quando você executa o teste uma segunda vez com a entrada “- 2 " você consulta a exibição de cores de cobertura que a outra 50% da função está coberto. Agora você mescla os resultados das duas execuções de testes, e a exibição do relatório e da coloração de cobertura mostra que 100% da função foi coberta.  
  
 Use o ![ícone do botão de Mesclagem na janela Cobertura de Código](../test/media/codecoverage-mergeicon.png "CodeCoverage-MergeIcon")**Mesclar resultados da cobertura de código** para fazer isso. Você pode escolher qualquer combinação de execuções recentes ou resultados importados. Se você quiser combinar resultados exportados, importe-os primeiro.  
  
 Use **Exportar Resultados da Cobertura de Código** para salvar os resultados de uma operação de mesclagem.  
  
### <a name="limitations-in-merging"></a>Limitações na mesclagem  
  
-   Se você mesclar dados de cobertura de versões diferentes do código, os resultados serão mostrados separadamente, mas não combinados. Para obter resultados totalmente combinados, use a mesma compilação do código, alterando apenas os dados do teste.  
  
-   Se você combinar um arquivo de resultados que foi exportado e depois importado, só poderá exibir os resultados por linhas, não por blocos. Use o comando **Adicionar/Remover Colunas** para mostrar os dados da linha.  
  
-   Se você combinar os resultados dos testes de um projeto do ASP.NET, os resultados dos testes separados serão exibidos, mas não combinados. Isso se aplica apenas aos artefatos do ASP.NET em si: os resultados dos outros assemblies serão combinados.  
  
## <a name="excluding-elements-from-the-code-coverage-results"></a>Excluindo elementos dos resultados da cobertura de código  
 Você pode excluir elementos específicos em seu código das pontuações de cobertura, por exemplo, se o código é gerado a partir de um modelo de texto. Adicione o atributo `System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverage` a qualquer um dos seguintes elementos de código: class, struct, method, property, property setter ou getter, event. Observe que excluir uma classe não exclui as classes derivadas.  
  
 Por exemplo:  
  
```csharp  
  
using System.Diagnostics.CodeAnalysis;   
...  
public class ExampleClass1  
{   
    [ExcludeFromCodeCoverage]  
    void ExampleMethod() {...}  
  
    [ExcludeFromCodeCoverage] // exclude property  
    int ExampleProperty1   
    { get {...} set{...}}  
  
    int ExampleProperty2  
    {  
        get  
        {  
            ...  
        }  
        [ExcludeFromCodeCoverage] // exclude setter  
        set  
        {  
            ...  
        }  
    }  
  
}  
[ExcludeFromCodeCoverage]  
class ExampleClass2 { ... }  
  
```  
  
```vb  
Imports System.Diagnostics.CodeAnalysis  
  
Class ExampleClass1          
    <ExcludeFromCodeCoverage()>  
    Public Sub ExampleSub1()  
        ...  
    End Sub  
  
    ' Exclude property  
    < ExcludeFromCodeCoverage()>  
    Property ExampleProperty1 As Integer  
        ...  
    End Property  
  
    ' Exclude setter  
    Property ExampleProperty2 As Integer  
        Get  
            ...  
        End Get  
        <ExcludeFromCodeCoverage()>  
        Set(ByVal value As Integer)  
            ...  
        End Set  
    End Property  
End Class  
  
<ExcludeFromCodeCoverage()>  
Class ExampleClass2  
...  
End Class  
  
```  
  
```cpp#  
// A .cpp file compiled as managed (CLI) code.  
using namespace System::Diagnostics::CodeAnalysis;  
...  
public ref class ExampleClass1  
{  
  public:  
    [ExcludeFromCodeCoverage]  
    void ExampleFunction1() { ... }  
  
    [ExcludeFromCodeCoverage]  
    property int ExampleProperty2 {...}  
  
    property int ExampleProperty2 {  
      int get() { ... }  
     [ExcludeFromCodeCoverage]  
      void set(int value) { ...  }  
   }  
  
}  
  
[ExcludeFromCodeCoverage]  
public ref class ExampleClass2  
{ ... }  
  
```  
  
### <a name="excluding-elements-in-native-c-code"></a>Excluindo elementos em código C++ nativo  
 Para excluir os elementos não gerenciados (nativos) em código C++:  
  
```cpp  
  
#include <CodeCoverage\CodeCoverage.h>  
...  
  
// Exclusions must be compiled as unmanaged (native):  
#pragma managed(push, off)  
  
// Exclude a particular function:  
ExcludeFromCodeCoverage(Exclusion1, L"MyNamespace::MyClass::MyFunction");  
  
// Exclude all the functions in a particular class:  
ExcludeFromCodeCoverage(Exclusion2, L"MyNamespace::MyClass2::*");  
  
// Exclude all the functions generated from a particular template:   
ExcludeFromCodeCoverage(Exclusion3, L"*::MyFunction<*>");  
  
// Exclude all the code from a particular .cpp file:  
ExcludeSourceFromCodeCoverage(Exclusion4, L"*\\unittest1.cpp");  
  
// After setting exclusions, restore the previous managed/unmanaged state:  
#pragma managed(pop)  
  
```  
  
 Use as seguintes macros:  
  
 `ExcludeFromCodeCoverage(` *ExclusionName* `, L"` *FunctionName* `");`  
  
 `ExcludeSourceFromCodeCoverage(` *ExclusionName* `, L"` *SourceFilePath* `");`  
  
-   *ExclusionName* é qualquer nome exclusivo.  
  
-   *FunctionName* é um nome de função totalmente qualificado. Pode conter curingas. Por exemplo, para excluir todas as funções de uma classe, escreva `MyNamespace::MyClass::*`  
  
-   *SourceFilePath* é o local ou o caminho UNC de um arquivo .cpp. Pode conter curingas. O exemplo a seguir exclui todos os arquivos em um diretório específico: `\\MyComputer\Source\UnitTests\*.cpp`  
  
-   `#include <CodeCoverage\CodeCoverage.h>`  
  
-   Coloque as chamadas para as macros de exclusão no namespace global, não em qualquer namespace ou classe.  
  
-   Você pode colocar as exclusões no arquivo de código de teste de unidade ou no arquivo de código do aplicativo.  
  
-   As exclusões devem ser criadas como o código não gerenciado (nativo), definindo a opção de compilador ou usando `#pragma managed(off)`.  
  
> [!NOTE]
>  Para excluir funções em código C++/CLI, aplique o atributo `[System::Diagnostics::CodeAnalysis::ExcludeFromCodeCoverage]` à função. Esse é o mesmo para o C#.  
  
### <a name="including-or-excluding-additional-elements"></a>Incluindo ou excluindo elementos adicionais  
 A análise de cobertura de código é executada apenas em assemblies carregados e para os quais um arquivo .pdb está disponível no mesmo diretório que o arquivo .dll ou .exe. Portanto, em algumas circunstâncias, você pode estender o conjunto de assemblies que é incluído obtendo cópias dos arquivos .pdb apropriados.  
  
 Você pode exercer mais controle sobre quais assemblies e elementos são selecionados para análise de cobertura de código escrevendo um arquivo .runsettings. Por exemplo, você pode excluir os assemblies de tipos específicos sem precisar adicionar atributos às suas classes. Para obter mais informações, consulte [Personalizando a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).  
  
## <a name="analyzing-code-coverage-in-the-build-service"></a>Analisando a cobertura de código no serviço de compilação  
 Quando você faz check-in de seu código, os testes serão executados no servidor de compilação, juntamente com os outros testes de outros membros da equipe. (Se você ainda não tiver configurado isso, consulte [Executar testes no processo de build](http://msdn.microsoft.com/library/d05743a1-c5cf-447e-bed9-bed3cb595e38).) É útil analisar a cobertura de código no serviço de compilação, pois isso dá o panorama mais recente e mais abrangente da cobertura no projeto inteiro. Também incluirá os testes automatizados do sistema e outros testes codificados que você normalmente não executa nos computadores de desenvolvimento.  
  
1. No Team Explorer, abra **Compilações** e adicione ou edite uma definição de build.  
  
2. Na página **Processo**, expanda **Testes Automatizados**, **Fonte de Teste**, **Configurações de Execução**. Defina **Tipo de Arquivo de Configurações de Execução** como **Cobertura de Código Habilitada**.  
  
    Se você tiver mais de uma definição de Fonte de Teste, repita essa etapa para cada uma.  
  
   - <em>Mas não há nenhum campo nomeado **tipo de arquivo de configurações de execução</em>*. *  
  
      Em **Testes Automatizados**, selecione **Assembly de Teste** e escolha o botão de reticências **[...]** no final da linha. Na caixa de diálogo **Adicionar/Editar Execução de Teste**, em **Test Runner**, selecione **Visual Studio Test Runner**.  
  
   ![Configurar a definição de build para cobertura de código](../test/media/codecoverage-plaincc.png "CodeCoverage plainCC")  
  
   Depois que a compilação é executada, os resultados da cobertura de código são anexados à execução do teste e aparecem no resumo de compilação.  
  
## <a name="analyzing-code-coverage-in-a-command-line"></a>Analisando a cobertura de código em uma linha de comando  
 Para executar testes a partir da linha de comando, use vstest.console.exe. A cobertura de código é uma opção desse utilitário. Para obter mais informações, consulte [Opções de linha de comando de VSTest.Console.exe](http://msdn.microsoft.com/library/52e1689d-b1a8-4589-bd98-99a55acd0a11).  
  
1.  Inicie o Prompt de Comando do Desenvolvedor do Visual Studio:  
  
     No menu **Iniciar** do Windows, escolha **Todos os Programas**, **Microsoft Visual Studio**, **Ferramentas do Visual Studio** e **Prompt de Comando do Desenvolvedor**.  
  
2.  Execute:  
  
     `vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage`  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Se você não ver resultados da cobertura de código, consulte [Solução de problemas de cobertura de código](../test/troubleshooting-code-coverage.md).  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="guidance"></a>Diretrizes  
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](http://go.microsoft.com/fwlink/?LinkID=255188)  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando análise de cobertura de código](../test/customizing-code-coverage-analysis.md)   
 [Solução de problemas de cobertura de código](../test/troubleshooting-code-coverage.md)   
 [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)



