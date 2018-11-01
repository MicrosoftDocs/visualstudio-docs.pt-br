# <a name="contributing"></a>Contribuição

Obrigado pelo seu interesse em contribuir para a documentação do Visual Studio!

Neste tópico, você verá o processo básico para adicionar ou atualizar o conteúdo no [site de documentação do Visual Studio](https://docs.microsoft.com/visualstudio).

Neste tópico, abordaremos:

* [Processo de contribuição](#process-for-contributing)
* [Lista de verificação de orientação](#guidance-checklist)
* [Criando os documentos](#building-the-docs)
* [Contribuindo com exemplos](#contributing-to-samples)
* [Contrato de Licença do Colaborador](#contributor-license-agreement)

## <a name="process-for-contributing"></a>Processo de contribuição

**Etapa 1:** abra um problema que descreve o artigo que deseja escrever e como ele se relaciona com o conteúdo existente.
O conteúdo dentro da pasta **docs** é separado em seções organizadas por área de conteúdo (por exemplo, depurador). Tente determinar a pasta correta para seu novo conteúdo. Obter comentários sobre sua proposta. 

Você pode ignorar esta primeira etapa de pequenas alterações.

**Etapa 2:** crie fork do repositório `MicrosoftDocs/visualstudio-docs`.

**Etapa 3:** crie um `branch` para seu artigo.

**Etapa 4:** escreva seu artigo.

Se for um novo tópico, você poderá usar esse [arquivo de modelo](./styleguide/template.md) como ponto de partida. Ele contém as diretrizes de escrita e também explica os metadados necessários para cada artigo, como informações do autor.

Navegue até a pasta que corresponde à localização do Sumário determinado para o seu artigo na etapa 1.
Essa pasta contém os arquivos Markdown para todos os artigos nesta seção. Se necessário, crie uma pasta para colocar os arquivos do seu conteúdo.

Para imagens e outros recursos estáticos, adicione-os à subpasta chamada **mídia**. Se estiver criando uma pasta para o conteúdo, adicione uma pasta de mídia à nova pasta.

Siga a sintaxe de Markdown apropriada. Confira o [guia de estilo](./styleguide/template.md) para obter mais informações.

### <a name="example-structure"></a>Exemplo de estrutura

    docs
      /debugger
          debugging-installed-app-package.md
          /media
              debugging-installed-app-package.png

**Etapa 5:** envie uma PR (Solicitação de Pull) do branch para `MicrosoftDocs/visualstudio-docs/master`.

Se a PR estiver resolvendo um problema existente, adicione a palavra-chave `Fixes #Issue_Number` à mensagem de confirmação ou à descrição da PR para que o problema possa ser encerrado automaticamente quando a PR for mesclada. Para obter mais informações, confira [Closing issues via commit messages](https://help.github.com/articles/closing-issues-via-commit-messages/) (Encerrando problemas por meio de mensagens de confirmação).

A equipe do Visual Studio examinará a PR e informará se a alteração está boa ou se há outras atualizações/alterações necessárias para aprová-la.

**Etapa 6:** faça as atualizações necessárias no branch, conforme discutido com a equipe.

Os mantenedores mesclarão sua PR no branch mestre depois que os comentários forem aplicados e sua alteração estiver boa.

Em um determinado ritmo, efetuaremos push de todas as confirmações do branch mestre para o branch dinâmico e, em seguida, você poderá ver sua colaboração ao vivo em https://docs.microsoft.com/visualstudio/.

## <a name="dos-and-donts"></a>O que FAZER e o que NÃO FAZER

Abaixo, há uma lista curta de regras de orientação que você deve considerar ao contribuir para a documentação do .NET.

- **NÃO FAZER:** não nos surpreenda com solicitações de pull grandes. Em vez disso, registre um problema e inicie uma discussão para que possamos concordar sobre o que fazer antes de você gastar muito tempo nisso.
- **FAZER:** leia o [guia de estilo](./styleguide/template.md) e as diretrizes sobre [voz e tom](./styleguide/voice-tone.md).
- **FAZER:** use o arquivo de [modelo](./styleguide/template.md) como o ponto de partida do seu trabalho.
- **FAZER:** crie um branch separado em seu fork antes de trabalhar nos artigos.
- **FAZER:** siga o [fluxo de trabalho do GitHub Flow](https://guides.github.com/introduction/flow/).
- **FAZER:** faça postagem em blogs e no Twitter (ou em outros) sobre suas contribuições, com frequência.

> [!NOTE]
> Você poderá observar que, no momento, alguns dos tópicos não estão seguindo todas as diretrizes especificadas aqui e também no [guia de estilo](./styleguide/template.md). Estamos trabalhando para atingir a consistência em todo o site. Verifique a lista de [problemas em aberto](https://github.com/dotnet/docs/issues?q=is%3Aissue+is%3Aopen+label%3Aguidelines-adherence) que estamos acompanhando, no momento, para essa meta específica.

## <a name="building-the-docs"></a>Criando os documentos

A documentação é escrita em [GitHub Flavored Markdown](https://help.github.com/categories/writing-on-github/) e criada usando [DocFX](https://dotnet.github.io/docfx/) e outras ferramentas de publicação/construção internas. Está hospedada em [docs.microsoft.com](https://docs.microsoft.com/dotnet).

Se desejar criar documentos localmente, você precisará instalar o [DocFX](https://dotnet.github.io/docfx/). As versões mais recentes são as melhores.

Há várias maneiras de usar o DocFX e a maioria delas é abordada no [guia de introdução ao DocFX](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html).
As instruções a seguir usam a versão [com base em linha de comando](https://dotnet.github.io/docfx/tutorial/docfx_getting_started.html#2-use-docfx-as-a-command-line-tool) da ferramenta.
Se estiver familiarizado com outras maneiras listadas no link acima, fique à vontade para usá-las.

**Observação:** no momento, o DocFX requer o .NET Framework no Windows ou no Mono (para Linux ou macOS). Esperamos portá-lo para o .NET Core no futuro.

Você pode criar e visualizar o site resultante localmente usando um servidor Web interno. Navegue até a pasta de documentos principais no seu computador e digite o seguinte comando:

```
docfx -t default --serve
```

Isso iniciará a versão prévia local em [localhost:8080](http://localhost:8080). Em seguida, você poderá exibir as alterações ao acessar `http://localhost:8080/[path]`, como http://localhost:8080/articles/welcome.html.

**Observação:** a versão prévia local, no momento, não contém nenhum tema para que a aparência não seja a mesma que a do site de documentação. Estamos trabalhando para corrigir essa experiência.

# <a name="contributing-to-samples"></a>Contribuindo com exemplos

Por enquanto, inclua o código de exemplo necessário como blocos de código embutidos em seu artigo. O repositório tem uma pasta de trechos de código, mas isso não está pronto para contribuições públicas.
