---
title: Definindo uma imagem de plano de fundo em um diagrama
description: Saiba que, no SDK Visual Studio Visualização e Modelagem, você pode definir a imagem de plano de fundo para um designer gerado usando código personalizado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9304117932b92408f12a23747253de66dfd767d1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385663"
---
# <a name="setting-a-background-image-on-a-diagram"></a>Definindo uma imagem de plano de fundo em um diagrama
No Visual Studio SDK de Visualização e Modelagem, você pode definir a imagem de plano de fundo para um designer gerado usando código personalizado.

## <a name="setting-the-background-image"></a>Configuração da imagem da tela de fundo

#### <a name="to-set-a-background-image-for-a-generated-designer"></a>Para configurar uma imagem de plano de fundo de um designer gerado

1. Copie o arquivo de imagem que você deseja usar como plano de fundo do diagrama no diretório Dsl\Resources do projeto atual.

2. No **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta Dsl\Resources, aponte para Adicionar e clique **em Item Existente**.

3. Na caixa **de diálogo Adicionar Item** Existente, navegue até a pasta Dsl\Resources.

4. Na lista **Arquivos do tipo** , clique em Arquivos de **Imagem**.

5. Clique no arquivo de imagem que você copiou para o diretório e clique em **Adicionar**.

6. Clique com o botão direito do mouse em Dsl e clique **em Propriedades** para abrir as propriedades do projeto Dsl.

7. Na guia **Recursos,** clique em **Este projeto não contém um arquivo de recursos padrão. Clique aqui para criar um.**

8. Adicione o arquivo de imagem ao arquivo de recurso arrastando a imagem **Gerenciador de Soluções** para a janela de recursos.

9. Abra o menu Arquivo e clique na opção para salvar as propriedades do projeto.

10. Verifique se o arquivo Dsl\Properties\Resources.resx existe e se possui o arquivo Resources.Designer.cs nele.

11. Se Resources.Designer.cs estiver ausente, clique no arquivo Resources.resx **no Gerenciador de Soluções**.

12. Na janela **Propriedades,** de definir a `Custom Tool` propriedade como `ResXFileCodeGenerator` .

13. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto Dsl, aponte para **Adicionar** e clique em **Nova Pasta**.

14. Nomeia a pasta **Personalizado.**

15. Clique com o botão direito do mouse na pasta Personalizado, aponte **para Adicionar** e clique em **Novo Item**.

16. Na caixa **de diálogo Adicionar Novo Item** , na lista **Modelos** , clique em Arquivo **de Código**.

17. Na caixa **Nome,** digite `BackgroundImage.cs` e clique em **Adicionar**.

18. Copie o código a seguir no arquivo BackgroundImage.cs, ajustando o namespace, o nome da classe do diagrama e o nome do recurso do arquivo de imagem.

     Substitua "MyDiagramClass" pelo nome da classe parcial do diagrama definido em Dsl\GeneratedCode\Diagrams.cs. Também é possível recuperar o namespace correto do arquivo Dsl\GeneratedCode\Diagrams.cs.

    ```csharp
    using System;
    using Microsoft.VisualStudio.Modeling.Diagrams;

    // Fix the namespace:
    namespace Fabrikam.MyLanguage
    {
      // Fix the Diagram Class name - get it from GeneratedCode\Diagram.cs

      public partial class Language29Diagram
      {
        protected override void InitializeInstanceResources()
        {
          // Fix the Resources namespace and the Image resource name:
          ImageField backgroundField = new ImageField("background",
              Fabrikam.MyLanguage.Properties.Resources.MyPicture);

          backgroundField.DefaultFocusable = false;
          backgroundField.DefaultSelectable = false;
          backgroundField.DefaultVisibility = true;
          backgroundField.DefaultUnscaled = false;

          shapeFields.Add(backgroundField);

          backgroundField.AnchoringBehavior
            .SetTopAnchor(AnchoringBehavior.Edge.Top, 0.01);
          backgroundField.AnchoringBehavior
            .SetLeftAnchor(AnchoringBehavior.Edge.Left, 0.01);
          backgroundField.AnchoringBehavior
            .SetRightAnchor(AnchoringBehavior.Edge.Right, 0.01);
          backgroundField.AnchoringBehavior
            .SetBottomAnchor(AnchoringBehavior.Edge.Bottom, 0.01);

          base.InitializeInstanceResources();
        }
      }
    }
    ```

     Para obter mais informações sobre como personalizar o modelo com o código do programa, consulte Navegando e atualizando um [modelo no código do programa.](../modeling/navigating-and-updating-a-model-in-program-code.md)

## <a name="see-also"></a>Confira também

- [Definindo formas e conectores](../modeling/defining-shapes-and-connectors.md)
- [Personalizando campos de texto e imagem](../modeling/customizing-text-and-image-fields.md)
- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
