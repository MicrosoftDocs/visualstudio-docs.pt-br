---
title: Definindo uma imagem de plano de fundo em um diagrama
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 82466360fd4f891d28e0218a540d27c803a39662
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47858868"
---
# <a name="setting-a-background-image-on-a-diagram"></a>Definindo uma imagem de plano de fundo em um diagrama
Na visualização do Visual Studio e SDK de modelagem, você pode definir a imagem de plano de fundo de um designer gerado usando código personalizado.

## <a name="setting-the-background-image"></a>Configurando a imagem de plano de fundo

#### <a name="to-set-a-background-image-for-a-generated-designer"></a>Para configurar uma imagem de plano de fundo de um designer gerado

1.  Copie o arquivo de imagem que você deseja usar como plano de fundo do diagrama no diretório Dsl\Resources do projeto atual.

2.  Na **Gerenciador de soluções**, clique com botão direito na pasta Dsl\Resources, aponte para **Add**e, em seguida, clique em **Item existente**.

3.  No **Add Existing Item** caixa de diálogo, navegue até a pasta dsl\resources.

4.  No **arquivos de tipo** , clique em **arquivos de imagem**.

5.  Clique no arquivo de imagem que você copiou para o diretório e, em seguida, clique em **adicionar**.

6.  Clique com botão direito Dsl e, em seguida, clique em **propriedades** para abrir as propriedades do projeto Dsl.

7.  Sobre o **recursos** , clique em **este projeto não contém um arquivo de recursos padrão. Clique aqui para criar um.**

8.  Adicionar o arquivo de imagem ao arquivo de recurso, arrastando a imagem do **Gerenciador de soluções** na janela de recursos.

9. Abra o menu Arquivo e clique na opção para salvar as propriedades do projeto.

10. Verifique se o arquivo Dsl\Properties\Resources.resx existe e se possui o arquivo Resources.Designer.cs nele.

11. Se Resources.Designer.cs estiver ausente, clique no arquivo resx na **Gerenciador de soluções**.

12. No **propriedades** janela, defina as `Custom Tool` propriedade `ResXFileCodeGenerator`.

13. Na **Gerenciador de soluções**, clique com botão direito no projeto Dsl, aponte para **Add**e clique em **nova pasta**.

14. Nomeie a pasta **personalizado**.

15. Clique com botão direito na pasta personalizado, aponte para **Add**e clique em **Novo Item**.

16. No **Adicionar Novo Item** na caixa de **modelos** , clique em **arquivo de código**.

17. No **nome** , digite `BackgroundImage.cs`e clique em **Add**.

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

     Para obter mais informações sobre como personalizar o modelo com o código do programa, consulte [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

## <a name="see-also"></a>Consulte também

- [Definindo formas e conectores](../modeling/defining-shapes-and-connectors.md)
- [Personalizando campos de texto e imagem](../modeling/customizing-text-and-image-fields.md)
- [Navegando por um modelo no código do programa e atualizando-o](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
