---
title: Adicionar validação de arquitetura personalizada a diagramas de dependência
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- dependency diagrams, adding custom validation
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 98482eed6c1ed5a8ac2e3bbb7b5ada6af9517c1d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546908"
---
# <a name="add-custom-architecture-validation-to-dependency-diagrams"></a>Adicionar validação de arquitetura personalizada a diagramas de dependência

No Visual Studio, os usuários podem validar o código-fonte em um projeto em um modelo de camada para que eles possam verificar se o código-fonte está em conformidade com as dependências em um diagrama de dependência. Há um algoritmo de validação padrão, mas você pode definir suas próprias extensões de validação.

Quando o usuário seleciona o comando **validar arquitetura** em um diagrama de dependência, o método de validação padrão é invocado, seguido por todas as extensões de validação que foram instaladas.

> [!NOTE]
> Em um diagrama de dependência, a principal finalidade da validação é comparar o diagrama com o código do programa em outras partes da solução.

Você pode empacotar sua extensão de validação de camada em um VSIX (extensão de integração do Visual Studio), que pode ser distribuído para outros usuários do Visual Studio. Você pode posicionar o validador em um VSIX por si só, ou pode combiná-lo no mesmo VSIX que outras extensões. Você deve escrever o código do validador em seu próprio projeto do Visual Studio, não no mesmo projeto que outras extensões.

> [!WARNING]
> Depois de criar um projeto de validação, copie o [código de exemplo](#example) no final deste tópico e, em seguida, edite-o para suas próprias necessidades.

## <a name="requirements"></a>Requisitos

Consulte [requisitos](../modeling/extend-layer-diagrams.md#requirements).

## <a name="defining-a-layer-validator-in-a-new-vsix"></a>Definindo um validador de camada em um novo VSIX

O método mais rápido de criar um validador é usar o modelo de projeto. Isso coloca o código e o manifesto do VSIX no mesmo projeto.

### <a name="to-define-an-extension-by-using-a-project-template"></a>Para definir uma extensão usando um modelo de projeto

1. Crie um novo projeto de **extensão de validação do designer de camada** .

    O modelo cria um projeto que contém um pequeno exemplo.

   > [!WARNING]
   > Para que o modelo funcione corretamente:
   >
   > - Editar chamadas para `LogValidationError` para remover os argumentos opcionais `errorSourceNodes` e `errorTargetNodes` .
   > - Se você usar propriedades personalizadas, aplique a atualização mencionada em [Adicionar propriedades personalizadas a diagramas de dependência](../modeling/add-custom-properties-to-layer-diagrams.md).

2. Edite o código para definir sua validação. Para obter mais informações, consulte [validação de programação](#programming).

3. Para testar a extensão, consulte [depuração da validação da camada](#debugging).

   > [!NOTE]
   > Seu método será chamado apenas em circunstâncias específicas e os pontos de interrupção não funcionarão automaticamente. Para obter mais informações, consulte [depuração da validação da camada](#debugging).

::: moniker range="vs-2017"

4. Para instalar a extensão na instância principal do Visual Studio ou em outro computador, localize o arquivo *. vsix* no diretório *bin* . Copie-o para o computador em que você deseja instalá-lo e clique duas vezes nele. Para desinstalá-lo, escolha **extensões e atualizações** no menu **ferramentas** .

::: moniker-end

::: moniker range=">=vs-2019"

4. Para instalar a extensão na instância principal do Visual Studio ou em outro computador, localize o arquivo *. vsix* no diretório *bin* . Copie-o para o computador em que você deseja instalá-lo e clique duas vezes nele. Para desinstalá-lo, escolha **gerenciar extensões** no menu **extensões** .

::: moniker-end

## <a name="adding-a-layer-validator-to-a-separate-vsix"></a>Adicionando um validador de camada a um VSIX separado

Se você quiser criar um VSIX que contenha validadores de camada, comandos e outras extensões, recomendamos que você crie um projeto para definir o VSIX e separe projetos para os manipuladores.

### <a name="to-add-layer-validation-to-a-separate-vsix"></a>Para adicionar validação de camada a um VSIX separado

1. Crie um projeto de **Biblioteca de Classes**. Este projeto conterá a classe de validação de camada.

2. Localize ou crie um **projeto VSIX** em sua solução. Um projeto VSIX contém um arquivo chamado **Source. Extension. vsixmanifest**.

3. No **Gerenciador de soluções**, no menu de clique com o botão direito do mouse no projeto VSIX, escolha **definir como projeto de inicialização**.

4. Em **Source. Extension. vsixmanifest**, em **ativos**, adicione o projeto de validação de camada como um componente do MEF:

    1. Escolha **Novo**.

    2. Na caixa de diálogo **Adicionar novo ativo** , defina:

         **Tipo**  =  de **Microsoft. VisualStudio. MefComponent**

         **Origem**  =  do **Um projeto na solução atual**

         **Projeto**  =  do *seu projeto de validador*

5. Você também deve adicioná-lo como uma validação de camada:

    1. Escolha **Novo**.

    2. Na caixa de diálogo **Adicionar novo ativo** , defina:

         **Tipo**  =  de **Microsoft. VisualStudio. ArchitectureTools. Layer. Validator**. Essa não é uma das opções na lista suspensa. Você deve inseri-lo no teclado.

         **Origem**  =  do **Um projeto na solução atual**

         **Projeto**  =  do *seu projeto de validador*

6. Retorne ao projeto de validação de camada e adicione as seguintes referências de projeto:

    |**Referência**|**O que isso permite que você faça**|
    |-|-|
    |Microsoft.VisualStudio.GraphModel.dll|Ler o grafo de arquitetura|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema.dll|Ler o código DOM associado às camadas|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|Ler o modelo de camada|
    |Microsoft. VisualStudio. ArchitectureTools. Extensibility|Ler e atualizar formas e diagramas.|
    |System. ComponentModel. composição|Definir o componente de validação usando o Managed Extensibility Framework (MEF)|
    |Microsoft. VisualStudio. Modeling. Sdk. versão|Definir extensões de modelagem|

7. Copie o código de exemplo no final deste tópico para o arquivo de classe no projeto de biblioteca do validador para conter o código para sua validação. Para obter mais informações, consulte [validação de programação](#programming).

8. Para testar a extensão, consulte [depuração da validação da camada](#debugging).

    > [!NOTE]
    > Seu método será chamado apenas em circunstâncias específicas e os pontos de interrupção não funcionarão automaticamente. Para obter mais informações, consulte [depuração da validação da camada](#debugging).

9. Para instalar o VSIX na instância principal do Visual Studio ou em outro computador, localize o arquivo **. vsix** no diretório **bin** do projeto VSIX. Copie-o para o computador em que você deseja instalar o VSIX. Clique duas vezes no arquivo VSIX no Windows Explorer.

## <a name="programming-validation"></a><a name="programming"></a>Validação de programação

Para definir uma extensão de validação de camada, você define uma classe que tem as seguintes características:

- A forma geral da declaração é a seguinte:

  ```csharp
  using System.ComponentModel.Composition;
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema;
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
  using Microsoft.VisualStudio.GraphModel;
  ...
   [Export(typeof(IValidateArchitectureExtension))]
    public partial class Validator1Extension :
                    IValidateArchitectureExtension
    {
      public void ValidateArchitecture(Graph graph)
      {
         GraphSchema schema = graph.DocumentSchema;
        ...
    } }
  ```

- Ao descobrir um erro, você pode relatá-lo usando `LogValidationError()` .

  > [!WARNING]
  > Não use os parâmetros opcionais de `LogValidationError` .

Quando o usuário chama o comando de menu **validar arquitetura** , o sistema de tempo de execução de camada analisa as camadas e seus artefatos para produzir um grafo. O grafo tem quatro partes:

- Os modelos de camada da solução do Visual Studio que são representados como nós e links no grafo.

- O código, itens de projeto e outros artefatos que são definidos na solução e representados como nós e links que representam as dependências descobertas pelo processo de análise.

- Links dos nós de camada para os nós de artefato de código.

- Nós que representam erros descobertos pelo validador.

Quando o grafo tiver sido construído, o método de validação padrão será chamado. Quando isso for concluído, todos os métodos de validação de extensão instalados serão chamados em ordem não especificada. O grafo é passado para cada `ValidateArchitecture` método, que pode verificar o grafo e relatar quaisquer erros que encontrar.

> [!NOTE]
> Isso não é o mesmo que o processo de validação que pode ser usado em linguagens específicas de domínio.

Os métodos de validação não devem alterar o modelo de camada ou o código que está sendo validado.

O modelo de gráfico é definido em <xref:Microsoft.VisualStudio.GraphModel> . Suas classes principais são <xref:Microsoft.VisualStudio.GraphModel.GraphNode> e <xref:Microsoft.VisualStudio.GraphModel.GraphLink> .

Cada nó e cada link tem uma ou mais categorias que especificam o tipo de elemento ou relação que ele representa. Os nós de um grafo típico têm as seguintes categorias:

- DSL. LayerModel

- DSL. Layer

- DSL. referência

- CodeSchema_Type

- CodeSchema_Namespace

- CodeSchema_Type

- CodeSchema_Method

- CodeSchema_Field

- CodeSchema_Property

Os links de camadas para elementos no código têm a categoria "representa".

## <a name="debugging-validation"></a><a name="debugging"></a>Validação de depuração

Para depurar sua extensão de validação de camada, pressione CTRL + F5. Uma instância experimental do Visual Studio é aberta. Nessa instância, abra ou crie um modelo de camada. Esse modelo deve ser associado ao código e deve ter pelo menos uma dependência.

### <a name="test-with-a-solution-that-contains-dependencies"></a>Testar com uma solução que contém dependências

A validação não é executada, a menos que as seguintes características estejam presentes:

- Há pelo menos um link de dependência no diagrama de dependência.

- Há camadas no modelo que estão associadas a elementos de código.

Na primeira vez que você iniciar uma instância experimental do Visual Studio para testar sua extensão de validação, abra ou crie uma solução que tenha essas características.

### <a name="run-clean-solution-before-validate-architecture"></a>Executar solução limpa antes de validar a arquitetura

Sempre que você atualizar o código de validação, use o comando **limpar solução** no menu **Compilar** da solução experimental, antes de testar o comando validar. Isso é necessário porque os resultados da validação são armazenados em cache. Se você não tiver atualizado o diagrama de dependência de teste ou seu código, os métodos de validação não serão executados.

### <a name="launch-the-debugger-explicitly"></a>Iniciar o depurador explicitamente

A validação é executada em um processo separado. Portanto, os pontos de interrupção no seu método de validação não serão disparados. Você deve anexar o depurador ao processo explicitamente quando a validação for iniciada.

Para anexar o depurador ao processo de validação, insira uma chamada para `System.Diagnostics.Debugger.Launch()` no início do seu método de validação. Quando a caixa de diálogo depuração for exibida, selecione a instância principal do Visual Studio.

Como alternativa, você pode inserir uma chamada para `System.Windows.Forms.MessageBox.Show()` . Quando a caixa de mensagem for exibida, vá para a instância principal do Visual Studio e, no menu **depurar** , clique em **anexar ao processo**. Selecione o processo chamado **Graphcmd.exe**.

Sempre inicie a instância experimental pressionando CTRL + F5 (**Iniciar sem depuração**).

### <a name="deploying-a-validation-extension"></a>Implantando uma extensão de validação

Para instalar a extensão de validação em um computador no qual uma versão adequada do Visual Studio esteja instalada, abra o arquivo VSIX no computador de destino.

## <a name="example-code"></a><a name="example"></a>Código de exemplo

```csharp
using System;
using System.ComponentModel.Composition;
using System.Globalization;
using System.Linq;
using System.Text.RegularExpressions;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.GraphModel;

namespace Validator3
{
    [Export(typeof(IValidateArchitectureExtension))]
    public partial class Validator3Extension : IValidateArchitectureExtension
    {
        /// <summary>
        /// Validate the architecture
        /// </summary>
        /// <param name="graph">The graph</param>
        public void ValidateArchitecture(Graph graph)
        {
            if (graph == null) throw new ArgumentNullException("graph");

            // Uncomment the line below to debug this extension during validation
            // System.Windows.Forms.MessageBox.Show("Attach 2 to GraphCmd.exe with process id " + System.Diagnostics.Process.GetCurrentProcess().Id);

            // Get all layers on the diagram
            foreach (GraphNode layer in graph.Nodes.GetByCategory("Dsl.Layer"))
            {
                System.Threading.Thread.Sleep(100);
                // Get the required regex property from the layer node
                string regexPattern = "^[a-zA-Z]+$"; //layer[customPropertyCategory] as string;
                if (!string.IsNullOrEmpty(regexPattern))
                {
                    Regex regEx = new Regex(regexPattern);

                    // Get all referenced types in this layer including those from nested layers so each
                    // type is validated against all containing layer constraints.
                    foreach (GraphNode containedType in layer.FindDescendants().Where(node => node.HasCategory("CodeSchema_Type")))
                    {
                        // Check the type name against the required regex
                        CodeGraphNodeIdBuilder builder = new CodeGraphNodeIdBuilder(containedType.Id, graph);
                        string typeName = builder.Type.Name;
                        if (!regEx.IsMatch(typeName))
                        {
                            // Log an error
                            string message = string.Format(CultureInfo.CurrentCulture, Resources.InvalidTypeNameMessage, typeName);
                            this.LogValidationError(graph, typeName + "TypeNameError", message, GraphErrorLevel.Error, layer);
                        }
                    }
                }

            }

        }
    }
}
```

## <a name="see-also"></a>Confira também

- [Estender diagramas de dependência](../modeling/extend-layer-diagrams.md)
