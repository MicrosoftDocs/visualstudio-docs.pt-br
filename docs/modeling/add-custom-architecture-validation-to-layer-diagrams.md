---
title: Adicionar validação de arquitetura personalizada a diagramas de dependência
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, adding custom validation
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: e9343ed8fdb1f3993fcd5c2f70595fd4bdd92dcd
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49875444"
---
# <a name="add-custom-architecture-validation-to-dependency-diagrams"></a>Adicionar validação de arquitetura personalizada a diagramas de dependência

No Visual Studio, os usuários podem validar o código-fonte em um projeto em um modelo de camada para que eles possam verificar que o código-fonte está em conformidade com as dependências em um diagrama de dependência. Há um algoritmo de validação padrão, mas você pode definir suas próprias extensões de validação.

Quando o usuário seleciona o **validar arquitetura** de comando em um diagrama de dependência, o método de validação padrão será invocado, seguido por quaisquer extensões de validação que foram instaladas.

> [!NOTE]
> Em um diagrama de dependência, a principal finalidade da validação é comparar o diagrama com o código do programa em outras partes da solução.

Você pode empacotar sua extensão de validação de camada em um Visual Studio Integration extensão (VSIX), que você pode distribuir a outros usuários do Visual Studio. Você pode colocar seu validador um VSIX por si só, ou você pode combiná-lo no mesmo VSIX que outras extensões. Você deve escrever o código do validação em seu próprio projeto do Visual Studio, e não no mesmo projeto que outras extensões.

> [!WARNING]
> Depois que você criou um projeto de validação, copie o [código de exemplo](#example) no final deste tópico e edite que para suas próprias necessidades.

## <a name="requirements"></a>Requisitos

Ver [requisitos de](../modeling/extend-layer-diagrams.md#prereqs).

## <a name="defining-a-layer-validator-in-a-new-vsix"></a>Definindo um validador de camada em um novo VSIX

O método mais rápido de criar um validador é usar o modelo de projeto. Isso coloca o código e o manifesto do VSIX no mesmo projeto.

### <a name="to-define-an-extension-by-using-a-project-template"></a>Para definir uma extensão usando um modelo de projeto

1. Criar um projeto em uma nova solução, usando o **novo projeto** comando as **arquivo** menu.

2. No **novo projeto** caixa de diálogo **projetos de modelagem**, selecione **extensão de validação do Designer de camada**.

    O modelo cria um projeto que contém um pequeno exemplo.

   > [!WARNING]
   > Para tornar o modelo funcione corretamente:
   >
   > - Edite as chamadas `LogValidationError` para remover os argumentos opcionais `errorSourceNodes` e `errorTargetNodes`.
   > - Se você usar as propriedades personalizadas, aplique a atualização mencionada em [adicionar propriedades personalizadas a diagramas de dependência](../modeling/add-custom-properties-to-layer-diagrams.md).

3. Edite o código para definir a validação. Para obter mais informações, consulte [Programando a validação](#programming).

4. Para testar a extensão, consulte [depurando a validação de camada](#debugging).

   > [!NOTE]
   > O método será chamado apenas em circunstâncias específicas, e os pontos de interrupção não funcionará automaticamente. Para obter mais informações, consulte [depurando a validação de camada](#debugging).

5. Para instalar a extensão na instância principal do Visual Studio ou em outro computador, localize o *. VSIX* arquivo na *bin* directory. Copie-o para o computador no qual você deseja instalá-lo e, em seguida, clique duas vezes nele. Para desinstalá-lo, escolha **extensões e atualizações** sobre o **ferramentas** menu.

## <a name="adding-a-layer-validator-to-a-separate-vsix"></a>Adicionando um validador de camada a um VSIX separado

Se você quiser criar um VSIX que contém validadores de camada, comandos e outras extensões, é recomendável que você crie um projeto para definir o VSIX e projetos separados para os manipuladores.

### <a name="to-add-layer-validation-to-a-separate-vsix"></a>Para adicionar a validação de camada a um VSIX separado

1.  Crie um projeto de biblioteca de classes em uma solução nova ou existente do Visual Studio. No **novo projeto** caixa de diálogo, clique em **Visual c#** e, em seguida, clique em **biblioteca de classes**. Esse projeto conterá a classe de validação de camada.

2.  Identifique ou crie um projeto de VSIX em sua solução. Um projeto do VSIX contém um arquivo chamado **vsixmanifest**. Se você tiver que adicionar um projeto VSIX, siga estas etapas:

    1.  No **novo projeto** diálogo caixa, escolha **Visual c#**, **extensibilidade**, **projeto VSIX**.

    2.  Na **Gerenciador de soluções**, no menu de atalho do projeto VSIX, **definir como projeto de inicialização**.

3.  Na **vsixmanifest**, em **ativos**, adicione o projeto de validação de camada como um componente de MEF:

    1.  Escolher **novo**.

    2.  No **adicionar novo ativo** caixa de diálogo, defina:

         **Type** = **Microsoft.VisualStudio.MefComponent**

         **Código-fonte** = **um projeto na solução atual**

         **Projeto** = *seu projeto de validador*

4.  Você também deve adicioná-lo como uma validação de camada:

    1.  Escolher **novo**.

    2.  No **adicionar novo ativo** caixa de diálogo, defina:

         **Type** = **Microsoft.VisualStudio.ArchitectureTools.Layer.Validator**. Isso não é uma das opções na lista suspensa. Você deve inseri-lo usando o teclado.

         **Código-fonte** = **um projeto na solução atual**

         **Projeto** = *seu projeto de validador*

5.  Volte para o projeto de validação de camada e adicione as seguintes referências de projeto:

    |**Referência**|**O que isso permite que você faça**|
    |-|-|
    |Microsoft.VisualStudio.GraphModel.dll|Ler o gráfico de arquitetura|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema.dll|Ler que o código DOM associado às camadas|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|Ler o modelo de camada|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility|Ler e atualizar formas e diagramas.|
    |System.ComponentModel.Composition|Defina o componente de validação usando Managed Extensibility Framework (MEF)|
    |Microsoft.VisualStudio.Modeling.Sdk.[version]|Definir as extensões de modelagem|

6.  Copie o código de exemplo no final deste tópico para o arquivo de classe no projeto da biblioteca de validador para conter o código para a validação. Para obter mais informações, consulte [Programando a validação](#programming).

7.  Para testar a extensão, consulte [depurando a validação de camada](#debugging).

    > [!NOTE]
    > O método será chamado apenas em circunstâncias específicas, e os pontos de interrupção não funcionará automaticamente. Para obter mais informações, consulte [depurando a validação de camada](#debugging).

8.  Para instalar o VSIX na instância principal do Visual Studio ou em outro computador, localize o **. VSIX** arquivo na **bin** diretório do projeto VSIX. Copie-o no computador em que você deseja instalar o VSIX. Clique duas vezes no arquivo VSIX no Windows Explorer.

     Para desinstalar, use **extensões e atualizações** sobre o **ferramentas** menu.

##  <a name="programming"></a> Validação de programação

Para definir uma extensão de validação de camada, você define uma classe que tem as seguintes características:

- A forma geral da declaração é da seguinte maneira:

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

- Quando você detectar um erro, pode reportá-lo usando `LogValidationError()`.

  > [!WARNING]
  > Não use os parâmetros opcionais de `LogValidationError`.

Quando o usuário chama o **validar arquitetura** comando de menu, o sistema de tempo de execução de camada analisa as camadas e seus artefatos para gerar um gráfico. O gráfico tem quatro partes:

- Os modelos de camada de solução do Visual Studio que são representados como nós e links no gráfico.

- O código, itens de projeto e outros artefatos que são definidos na solução e representados como nós e links que representam as dependências descobertas pelo processo de análise.

- Links de nós de camada para os nós de artefato de código.

- Nós que representam erros descobertos pelo validador.

Quando o gráfico foi construído, o método padrão de validação é chamado. Quando isso for concluído, qualquer método de validação de extensão instalada é chamado em ordem não especificada. O gráfico é passado para cada `ValidateArchitecture` método, que pode verificar o gráfico e relatar quaisquer erros que encontrar.

> [!NOTE]
> Isso não é o mesmo que o processo de validação que pode ser usado em linguagens específicas de domínio.

Métodos de validação não devem alterar o modelo de camada ou o código que está sendo validado.

O modelo de gráfico é definido em <xref:Microsoft.VisualStudio.GraphModel>. As classes principais são <xref:Microsoft.VisualStudio.GraphModel.GraphNode> e <xref:Microsoft.VisualStudio.GraphModel.GraphLink>.

Cada nó e cada Link tem uma ou mais categorias que especificam o tipo de elemento ou de relacionamento que ele representa. Os nós de um gráfico comum têm as seguintes categorias:

- Dsl.LayerModel

- Dsl.Layer

- Dsl.Reference

- CodeSchema_Type

- CodeSchema_Namespace

- CodeSchema_Type

- CodeSchema_Method

- CodeSchema_Field

- CodeSchema_Property

Links de camadas para elementos no código possuem a categoria "Representa".

##  <a name="debugging"></a> Validação de depuração

Para depurar a extensão de validação de camada, pressione CTRL + F5. Uma instância experimental do Visual Studio é aberto. Nesse caso, abra ou crie um modelo de camada. Esse modelo deve ser associado ao código e deve ter pelo menos uma dependência.

### <a name="test-with-a-solution-that-contains-dependencies"></a>Teste com uma solução que contém as dependências

A validação não é executada, a menos que as seguintes características estejam presentes:

- Há pelo menos um link de dependência no diagrama de dependência.

- Há camadas no modelo que estão associadas a elementos de código.

Na primeira vez que você inicia uma instância experimental do Visual Studio para testar sua extensão de validação, abra ou crie uma solução que tem as seguintes características.

### <a name="run-clean-solution-before-validate-architecture"></a>Execute a limpar solução antes de validar a arquitetura

Sempre que você atualiza seu código de validação, use o **limpar solução** comando as **Build** menu na solução de avaliação, antes de testar o comando validar. Isso é necessário porque os resultados da validação são armazenados em cache. Se você não tiver atualizado o diagrama de dependência de teste ou em seu código, os métodos de validação não serão executados.

### <a name="launch-the-debugger-explicitly"></a>Iniciar o depurador explicitamente

A validação é executada em um processo separado. Portanto, os pontos de interrupção no método de validação não serão disparados. Você deve anexar o depurador ao processo explicitamente quando a validação foi iniciada.

Para anexar o depurador ao processo de validação, inserir uma chamada a `System.Diagnostics.Debugger.Launch()` no início de seu método de validação. Quando a caixa de diálogo de depuração for exibida, selecione a instância principal do Visual Studio.

Como alternativa, você pode inserir uma chamada para `System.Windows.Forms.MessageBox.Show()`. Quando a caixa de mensagem for exibida, vá para a instância principal do Visual Studio e, na **Debug** menu, clique em **anexar ao processo**. Selecione o processo que é denominado **Graphcmd.exe**.

Sempre iniciar a instância experimental pressionando CTRL + F5 (**iniciar sem depuração**).

### <a name="deploying-a-validation-extension"></a>Implantando uma extensão de validação

Para instalar sua extensão de validação em um computador no qual uma versão adequada do Visual Studio está instalada, abra o arquivo VSIX no computador de destino.

##  <a name="example"></a> Exemplo de código

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

## <a name="see-also"></a>Consulte também

- [Estender diagramas de dependência](../modeling/extend-layer-diagrams.md)
