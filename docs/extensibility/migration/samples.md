---
title: Exemplo de ImageOptimizer para atualizar extensões do Visual Studio
description: Siga um exemplo para saber como atualizar uma extensão do Visual Studio para trabalhar com o Visual Studio 2022 Preview.
ms.date: 06/08/2021
ms.topic: sample
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 12bbc159884c16ea89849e5c97a4b87292f7089d
ms.sourcegitcommit: 674d3fafa7c9e0cb0d1338027ef419a49c028c36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2021
ms.locfileid: "112602217"
---
# <a name="imageoptimizer---update-a-visual-studio-extension-step-by-step"></a>ImageOptimizer-atualizar uma extensão do Visual Studio passo a passo

[!INCLUDE [preview-note](../includes/preview-note.md)]

Este guia mostrará todas as etapas necessárias para adicionar o suporte ao Visual Studio 2022 enquanto mantém o suporte ao Visual Studio 2019 usando a extensão do otimizador de imagem como um estudo de caso.  
Isso é destinado a ser um guia completo com links de confirmação de git para cada etapa, mas você está livre para ver a PR finalizada aqui: [https://github.com/madskristensen/ImageOptimizer/pull/46](https://github.com/madskristensen/ImageOptimizer/pull/46) .

Também temos [exemplos adicionais](#other-samples) no final deste guia.

## <a name="step-1---modernize-the-project"></a>Etapa 1 – modernizar o projeto

Consulte [modernizar o projeto](update-visual-studio-extension.md#modernize-your-vsix-project).

[e052465 de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/e052465f30e6bed37e6d76eac016047095e8e18b)

Primeiro, vamos aumentar o VSIX e o projeto de teste de unidade para o .NET 4.7.2 na página de propriedades dos projetos:

   ![Tapa de versão do Framework](media/samples/framework-bump.png)

O otimizador de imagem referenciou alguns pacotes antigos de 14. * e 15. * personalizados. em vez disso, instalaremos o [ `Microsoft.VisualStudio.Sdk` pacote NuGet](https://www.nuget.org/packages/microsoft.visualstudio.sdk) que consolida todas as nossas referências necessárias.

```Diff
-  <ItemGroup>
-    <PackageReference Include="Madskristensen.VisualStudio.SDK">
-      <Version>14.0.0-beta4</Version>
-    </PackageReference>
-    <PackageReference Include="Microsoft.VSSDK.BuildTools">
-      <Version>15.8.3247</Version>
-      <IncludeAssets>runtime; build; native; contentfiles; analyzers</IncludeAssets>
-      <PrivateAssets>all</PrivateAssets>
-    </PackageReference>
-  </ItemGroup>

+  <ItemGroup>
+    <PackageReference Include="Microsoft.VisualStudio.SDK">
+      <Version>16.9.31025.194</Version>
+    </PackageReference>
+  </ItemGroup>
```

A criação do projeto é realizada com sucesso e obtemos alguns avisos de Threading. Corrigimos esses avisos clicando `ctrl` e `.` e usando o IntelliSense para adicionar as linhas de troca de thread ausentes.

## <a name="step-2---refactor-source-code-into-a-shared-project"></a>Etapa 2 – refatorar o código-fonte em um projeto compartilhado

Consulte [projetos compartilhados](update-visual-studio-extension.md#use-shared-projects-for-multi-targeting).

O suporte ao Visual Studio 2022 requer a adição de um novo projeto compartilhado que conterá o código-fonte da extensão que será compartilhado entre os projetos VSIX do Visual Studio 2019 e do Visual Studio 2022.

1. Adicionar um novo projeto compartilhado à sua solução

   [abf249d de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/abf249d5a4bed9010652f3f3fc4753c7c771c892)

   ![Adicionar projeto compartilhado](media/samples/add-shared-project.png)

1. Adicione uma referência ao projeto compartilhado ao projeto VSIX.

   [e8e941e de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/e8e941e5a5482cc15f5b9e7e4f1727f5cab5b12c)

   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="Adicionar referência de projeto compartilhado" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. Mova os arquivos de código-fonte (CS, XAML, resx) para o novo projeto compartilhado **, exceto** para o seguinte:
    - `source.extension.vsixmanifest`
    - Arquivos de metadados de extensão (ícones, licenças, notas de versão, etc.)
    - Arquivos VSCT
    - Arquivos vinculados
    - Ferramentas externas ou bibliotecas que precisam ser incluídas no VSIX

   [f31f051 de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/f31f0515305623988f2c355ed3bf5952fc8f1d9e)

   ![Mover arquivos para o projeto compartilhado](media/samples/move-to-shared-project.png)

1. Agora, mova todos os metadados, arquivos VSCT, arquivos vinculados e ferramentas/bibliotecas externas para um local compartilhado e adicione-os de volta como itens vinculados ao projeto VSIX. **Não remova** `source.extension.vsixmanifest` .

   [confirmação de git 73ba920-movendo arquivos](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/73ba920b7db0bdb7c4d66aa9bc932c268efd49cb)

   [confirmação de git d5e36b2-adicionando ferramentas/bibliotecas externas](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/d5e36b2d047290d38ffc977511510bc03e257f13)

   1. Para este projeto, precisamos mover o ícone de extensão, o arquivo VSCT e as ferramentas externas para nossa nova pasta `ImageOptimizer\Resources` . Copie-os para a pasta compartilhada e remova-os do projeto VSIX.
   1. Adicionou-os de volta como itens vinculados e se os itens já estiverem vinculados podem permanecer como estão (licença, por exemplo).
   1. Valide se a ação de compilação e outras propriedades estão definidas corretamente nos arquivos vinculados adicionados, selecionando cada uma e verificando a janela de ferramentas de propriedades. Para nosso projeto, tivemos que definir o seguinte:
       - Defina `icon.png` a ação de compilação como `Content` e marcada como incluir no VSIX como `true`
       - Definir `ImageOptimizer.vsct` a ação de compilação como `VSCTComplile` e incluir no VSIX como `false`
       - Defina toda a ação de compilação dos arquivos em `Resources\Tools` para `Content` e marcada como incluir no VSIX para `true`

           ![Adicionar arquivos vinculados ao projeto VSIX](media/samples/add-linked-files.png)

       - Além disso, `ImageOptimizer.cs` é uma dependência de `ImageOptimizer.vsct` , para isso, precisamos adicionar manualmente essa dependência ao arquivo csproj:

          ```diff  
          - <Content Include="..\SharedFiles\ImageOptimizer.vsct">
          -   <Link>ImageOptimizer.vsct</Link>
          - </Content>
          - <Compile Include="..\SharedFiles\ImageOptimizer.cs">
          -   <Link>ImageOptimizer.cs</Link>
          - </Compile>

          + <VSCTCompile Include="..\SharedFiles\ImageOptimizer.vsct">
          +   <ResourceName>Menus.ctmenu</ResourceName>
          +   <Generator>VsctGenerator</Generator>
          +   <LastGenOutput>..\SharedFiles\ImageOptimizer.cs</LastGenOutput>
          + </VSCTCompile>
          + <Compile Include="..\SharedFiles\ImageOptimizer.cs">
          +   <AutoGen>True</AutoGen>
          +   <DesignTime>True</DesignTime>
          +   <DependentUpon>..\SharedFiles\ImageOptimizer.vsct</DependentUpon>
          + </Compile>
          ```

       - Se a janela de ferramentas de propriedades impedir que você defina uma ação de compilação específica, você poderá modificar manualmente o csproj como feito acima e definir a ação de compilação conforme necessário.

1. Crie seu projeto para validar as alterações e corrigir quaisquer erros/problemas. Verifique a seção [perguntas](update-visual-studio-extension.md#q--a) frequentes para problemas comuns.

## <a name="step-3---add-a-visual-studio-2022-vsix-project"></a>Etapa 3 – adicionar um projeto VSIX do Visual Studio 2022

Consulte [Adicionar o destino do Visual Studio 2022](update-visual-studio-extension.md#add-a-visual-studio-2022-target).

1. Adicione um novo projeto VSIX à sua solução.
1. Remova qualquer código-fonte adicional no novo projeto, exceto para `source.extension.vsixmanifest.`

   ![Criar um novo projeto VSIX](media/samples/visual-studio-2022-vsix-initial.png)

1. Adicione uma referência ao seu projeto compartilhado.

   [dd49cb2 de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/dd49cb227b52c46206bf4be5c25790ac0377568d)

   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="Adicionar referência ao projeto compartilhado" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. Adicione os arquivos vinculados do projeto VSIX do Visual Studio 2019 e valide se as propriedades "ação de compilação" e "inclusão no VSIX" correspondem. Copie também sobre o `source.extension.vsixmanifest` arquivo, modificando-o posteriormente para dar suporte ao Visual Studio 2022.

   [98c43ee de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/98c43ee6fbe912c38a1275542c44c65e11d7dbd9)

   ![Adicionar arquivos vinculados ao projeto VSIX](media/samples/visual-studio-2022-add-linked-files.png)

1. Uma tentativa de compilação mostra que não há uma referência a `System.Windows.Forms` . Basta adicioná-lo ao nosso projeto do Visual Studio 2022 e recompilar.

   [de71ccd de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/de71ccd9baff703aa6679392ad41a2cfe7bd7d72)

   ```Diff
   + <Reference Include="System.Windows.Forms" />
   ```

1. Atualização `Microsoft.VisualStudio.SDK` e `Microsoft.VSSDK.BuildTools` referências de pacote para as versões do Visual Studio 2022.

   [d581fc3 de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/d581fc3c954974124dc7e31e5ecc85f78f7828ab)

   > [!NOTE]
   > Essas são as versões mais recentes disponíveis quando este guia foi criado. É recomendável que você obtenha as versões mais recentes disponíveis.
   >
   > ```diff
   > -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
   > +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview-1-31216-1036" />
   > -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
   > +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-Visual Studio 2022-g3f11f5ab" />
   > ```

1. Edite seu `source.extension.vsixmanifest` arquivo para refletir direcionando o Visual Studio 2022.

   [9d393c7 de confirmação git](https://github.com/madskristensen/ImageOptimizer/pull/46/commits/9d393c708c04ac4af48d1eb9ce3da4470db5d5cc)
   1. Defina a `<InstallationTarget>` marca para refletir o Visual Studio 2022 e indicar uma carga AMD64:

      ```xml
      <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
          <ProductArchitecture>amd64</ProductArchitecture>
      </InstallationTarget>
      ```

   1. Modifique o pré-requisito para incluir apenas o Visual Studio 2022 e superior:

      ```Diff
      - <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,)" DisplayName="Visual Studio core editor" />
      + <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[17.0,)" DisplayName="Visual Studio core editor" />
      ```

E pronto!

Com isso, a criação agora produz os VSIX do Visual Studio 2019 e do Visual Studio 2022.

## <a name="other-samples"></a>Outras amostras

- [Ferramentas de Propower](https://github.com/microsoft/VS-PPT/pull/244)
  - PeekF1
    - Permite a exibição de um navegador da Web com informações de ajuda sobre a classe/o objeto selecionado.
  - FixMixedTabs
    - Examina seus documentos e substitui guias por espaços ou vice-versa

## <a name="next-steps"></a>Próximas etapas

Prepare-se para atualizar sua extensão lendo este [Guia de início a conclusão](update-visual-studio-extension.md).
