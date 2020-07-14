---
title: Introdução à criação de jogos com o Unity
description: Introdução ao Unity e ao Visual Studio para Mac
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/20/2019
ms.technology: vs-ide-general
ms.assetid: D07FA43B-9D18-4DFA-8343-CD538FAD84DB
ms.topic: how-to
ms.openlocfilehash: da9c8b3470fee406b577b136b6c55d76c9346e44
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950657"
---
# <a name="getting-started-building-games-with-unity-in-visual-studio-for-mac"></a>Introdução à criação de jogos com o Unity no Visual Studio para Mac

O Unity é um mecanismo de jogos que permite o desenvolvimento de jogos em C#. Este passo a passo mostra como começar a desenvolver e depurar jogos do Unity usando o Visual Studio para Mac e a extensão Ferramentas do Visual Studio para Mac para Unity junto com o ambiente do Unity.

As Ferramentas do Visual Studio para Mac para Unity é uma extensão gratuita, instalada com o Visual Studio para Mac. Ela permite que os desenvolvedores do Unity aproveitem as funcionalidades de produtividade do Visual Studio para Mac, incluindo o excelente suporte do IntelliSense, as funcionalidades de depuração, entre outros.

## <a name="objectives"></a>Objetivos

> [!div class="checklist"]
> * Saiba mais sobre o desenvolvimento do Unity com o Visual Studio para Mac

## <a name="prerequisites"></a>Pré-requisitos

- Visual Studio para Mac ( [https://www.visualstudio.com/vs/mac](https://www.visualstudio.com/vs/visual-studio-mac) )
- Unity 5.6.1 Personal Edition ou superior ( [https://store.unity.com](https://store.unity.com/) , requer que uma conta do Unity.com seja executada)

## <a name="intended-audience"></a>Público-alvo

Este laboratório destina-se a desenvolvedores que estão familiarizados com o C#, embora uma ampla experiência não seja necessária.

## <a name="task-1-creating-a-basic-unity-project"></a>Tarefa 1: Criando um projeto de Unity básico

1. Inicie o **Unity**. Entre, se solicitado.

2. Clique em **Novo**.

    ![Botão Novo do Unity](media/unity-image1.png)

3. Defina o **Nome do projeto** como **"UnityLab"** e selecione **3D**. Clique em **Criar projeto**.

    ![tela Criar projeto](media/unity-image2.png)

4. Agora você está olhando para a interface padrão do Unity. Ela tem a hierarquia de cenas com objetos de jogos à esquerda, uma exibição 3D da cena em branco mostrada no meio, um painel de arquivos de projeto na parte inferior e o inspetor e serviços à direita. Obviamente, há muito mais nela do que isso, mas esses são alguns dos componentes mais importantes.

    ![Interface do Unity em branco](media/unity-image3.png)

5. Para os desenvolvedores que estão conhecendo o Unity agora, tudo o que é executado em seu aplicativo existirá dentro do contexto de uma **cena**. Um arquivo de cena é um único arquivo que contém todos os tipos de metadados sobre os recursos usados no projeto para a cena atual e suas propriedades. Ao empacotar seu aplicativo para uma plataforma, o aplicativo resultante acabará sendo uma coleção de uma ou mais cenas, além de qualquer código dependente de plataforma adicionado. Você pode ter quantas cenas desejar em um projeto.

6. A nova cena apenas tem uma câmera e uma luz direcional. Uma cena exige uma **câmera** para que qualquer item seja visível e um **Ouvinte de Áudio** para que qualquer item seja audível. Esses componentes são anexados a um **GameObject**.

7. Selecione o objeto **Câmera Principal** no painel **Hierarquia**.

    ![objeto Câmera Principal realçado no painel Hierarquia](media/unity-image4.png)

8. Selecione o painel **Inspetor** do lado direito da janela para examinar suas propriedades. As propriedades da câmera incluem informações de transformação, segundo plano, tipo de projeção, campo de visão e assim por diante. Um componente de Ouvinte de Áudio também foi adicionado por padrão, que basicamente renderiza o áudio da cena por meio de um microfone virtual anexado à câmera.

    ![painel Inspetor](media/unity-image5.png)

9. Selecione o objeto **Luz Direcional**. Isso fornece luz à cena para que os componentes, como sombreadores, saibam como renderizar objetos.

    ![objeto Luz Direcional realçado](media/unity-image6.png)

10. Use o **Inspetor** para ver que ele inclui propriedades de iluminação comuns, incluindo tipo, cor, intensidade, tipo de sombra e assim por diante.

    ![observando as propriedades no painel Inspetor](media/unity-image7.png)

11. É importante ressaltar que os projetos no Unity são um pouco diferentes de seus equivalentes do Visual Studio para Mac. Na guia **Projeto** na parte inferior, clique com o botão direito do mouse na pasta **Ativos** e selecione **Revelar no Localizador**.

    ![ação de contexto Revelar no Localizador](media/unity-image8.png)

12. Os projetos contêm as pastas **Ativos**, **Biblioteca**, **ProjectSettings** e **Temp** como você pode ver. No entanto, a única que é exibida na interface é a pasta **Ativos**. A pasta **Biblioteca** é o cache local para os ativos importados; ela mantém todos os metadados para ativos. A pasta **ProjectSettings** armazena as configurações que podem ser definidas. A pasta **Temp** é usada para arquivos temporários do Mono e do Unity durante o processo de build. Também há um arquivo de solução que você pode abrir no Visual Studio para Mac (**UnityLab.sln**, aqui).

    ![ativos no localizador](media/unity-image9.png)

13. Feche a janela **Localizador** e retorne ao **Unity**.

14. A pasta **ativos** contém todos os seus ativos, código, áudio, etc. Ele está vazio agora, mas todos os arquivos que você colocar em seu projeto aparecerão aqui. Essa é sempre a pasta de nível superior no **Editor do Unity**. Porém, sempre adicione e remova arquivos por meio da interface do Unity (ou do Visual Studio para Mac) e nunca por meio do sistema de arquivos diretamente.

    ![pasta Ativos no Unity](media/unity-image10.png)

15. O **GameObject** é fundamental para o desenvolvimento no Unity, pois quase tudo deriva desse tipo, incluindo modelos, luzes, sistemas de partículas e assim por diante. Adicione um novo objeto **Cube** à cena por meio do menu **GameObject > Objeto 3D > Cubo**.

    ![objeto Cube na cena](media/unity-image11.png)

16. Dê uma olhada rápida nas propriedades do novo **GameObject** e observe que ele tem um nome, uma marcação, uma camada e uma transformação. Essas propriedades são comuns a todos os **GameObjects**. Além disso, vários componentes foram anexados ao **Cube** para fornecer a funcionalidade necessária, incluindo filtro de malha, colisor de caixa e renderizador.

    ![propriedades do objeto de jogo](media/unity-image12.png)

17. Renomeie o objeto **Cube**, que tem o nome **"Cube"** por padrão, como **"Enemy"**. Lembre-se de pressionar **Enter** para salvar a alteração. Esse será o cubo do inimigo em nosso jogo simples.

    ![propriedade de renomeação do objeto Cube](media/unity-image13.png)

18. Adicione outro objeto **Cube** à cena usando o mesmo processo descrito acima e nomeie-o **"Player"**.

    ![renomear o segundo objeto Cube](media/unity-image14.png)

19. Marque também o objeto de jogador **"Player"** (confira o controle suspenso **Tag** logo abaixo do campo de nome). Usaremos isso no script do inimigo para ajudar a localizar o objeto de jogo jogador.

    ![como marcar o objeto de jogador](media/unity-image15.png)

20. Na exibição **Cena**, mova o objeto de jogador para longe do objeto de inimigo ao longo do eixo Z usando o mouse. Você pode mover ao longo do eixo Z selecionando e arrastando o cubo pelo painel **vermelho** em direção à linha **azul**. Como o cubo reside no espaço 3D, mas pode apenas ser arrastado em 2D por vez, o eixo no qual você arrasta é especialmente importante.

    ![exibição de cena mostrando o cubo](media/unity-image16.png)

21. Mova o cubo para baixo e para a direita ao longo do eixo. Isso atualiza a propriedade **Transform.Position** no **Inspetor**. Arraste-o para uma localização de modo semelhante ao que foi mostrado aqui para facilitar as etapas posteriores do laboratório.

    ![como mover um cubo ao longo do eixo](media/unity-image17.png)

22. Agora você pode adicionar um código para impulsionar a lógica do inimigo, de modo que ele persiga o jogador. Clique com o botão direito do mouse na pasta **Ativos** no painel **Projeto** e selecione **Criar > Script C#**.

    ![Ação de contexto do script C#](media/unity-image18.png)

23. Nomeie o novo script C# **"EnemyAI"**.

    ![Script C#](media/unity-image19.png)

24. Para anexar scripts a objetos de jogo, arraste o script recém-criado para o objeto **Enemy** no painel **Hierarquia**. Agora, esse objeto usará os comportamentos desse script.

    ![realce mostrando a adição de script ao objeto de jogo](media/unity-image20.png)

25. Selecione **Arquivo > Salvar Cenas** para salvar a cena atual. Nomeie-a **"MyScene"**.

## <a name="task-2-working-with-visual-studio-for-mac-tools-for-unity"></a>Tarefa 2: trabalhando com as ferramentas de Visual Studio para Mac para o Unity

1. A melhor maneira de editar o código C# é usar o Visual Studio para Mac. Você pode configurar o Unity para usar o Visual Studio para Mac como seu manipulador padrão. Selecione **Unity > Preferências**.

2. Selecione a guia **Ferramentas externas** . Na lista suspensa **Editor de scripts externos** , selecione **procurar** e selecione **aplicativos/Visual Studio. aplicativo**. Como alternativa, se já houver uma opção **Visual Studio**, bastará selecioná-la.

    ![guia Ferramentas Externas em Preferências](media/unity-image21.png)

3. O Unity agora está configurado para usar o **Visual Studio para Mac** para edição de script. Feche a caixa de diálogo **Preferências do Unity**.

    ![Visual Studio selecionado em Preferências](media/unity-image22.png)

4. Clique duas vezes em **EnemyAI.cs** para abri-lo no **Visual Studio para Mac**.

    ![Ativo de inimigo selecionado no Unity](media/unity-image23.png)

5. A solução do Visual Studio é simples. Ela contém uma pasta **Ativos** (a mesma do **Localizador**) e o script **EnemyAI.cs** criado anteriormente. Em projetos mais sofisticados, a hierarquia provavelmente terá uma aparência diferente do que você vê no Unity.

    ![Painel de Soluções do Visual Studio para Mac](media/unity-image24.png)

6. **EnemyAI.cs** é aberto no editor. O script inicial contém apenas os stubs para os métodos **Start** e **Update**.

7. Substitua o código do inimigo inicial pelo código abaixo.

    ```csharp
    public class EnemyAI : MonoBehaviour
    {
        public float Speed = 50;
        private Transform _playerTransform;
        private Transform _myTransform;

        void Start()
        {
            var player = GameObject.FindGameObjectWithTag("Player");
            if (!player)
            {
                Debug.LogError(
                    "Could not find the main player. Ensure it has the player tag set.");
            }
            else
            {
                _playerTransform = player.transform;
            }
            _myTransform = this.transform;
        }

        void Update()
        {
            var moveAmount = Speed * Time.deltaTime;
            _myTransform.position = Vector3.MoveTowards(_myTransform.position,
                _playerTransform.position, moveAmount);

            if (_myTransform.position == _playerTransform.position)
            {
                _myTransform.position = Vector3.back * 10;
            }
        }
    }
    ```

8. Dê uma olhada rápida no comportamento simples do inimigo que é definido aqui. No método **Start**, obtemos uma referência ao objeto de jogador (pela marcação), bem como sua **transformação**. No método **Update**, que é chamado a cada quadro, o inimigo será movido para perto do objeto de jogador. As palavras-chave e os nomes usam a codificação de cores para facilitar o entendimento da base de código no Visual Studio para Mac.

9. Salve as alterações no script do inimigo no **Visual Studio para Mac**.

## <a name="task-3-debugging-the-unity-project"></a>Tarefa 3: Depurando o projeto do Unity

1. Defina um ponto de interrupção na primeira linha de código no método **Start**. Clique na margem do editor na linha de destino ou coloque o cursor na linha e pressione **F9**.

    ![como definir o ponto de interrupção no Visual Studio para Mac](media/unity-image25.png)

2. Clique no botão **Iniciar Depuração** ou pressione **F5**. Isso criará o projeto e o anexará ao Unity para depuração.

    ![botão Iniciar no Visual Studio para Mac](media/unity-image26.png)

3. Retorne ao **Unity** e clique no botão **Executar** para iniciar o jogo.

    ![botão Executar no Unity](media/unity-image27.png)

4. O ponto de interrupção deve ser atingido e agora você pode usar as ferramentas de depuração do Visual Studio para Mac.

    ![ponto de interrupção atingido no Visual Studio para Mac](media/unity-image28.png)

5. No painel **Locais**, localize o ponteiro **this**, que referencia um objeto **EnemyAI**. Expanda a referência e veja que você pode procurar os membros associados, como **Speed**.

    ![painel de depuração de locais no Visual Studio para Mac](media/unity-image29.png)

6. Remova o ponto de interrupção do método **Start** da mesma forma que ele foi adicionado – clicando na margem dele ou selecionando a linha – e pressione **F9**.

    ![ponto de interrupção atingido no Visual Studio para Mac](media/unity-image30.png)

7. Pressione **F10** para depurar de forma parcial a primeira linha de código que localiza o objeto de jogo **Player** usando uma marcação como parâmetro.

8. Passe o mouse sobre a variável **player** dentro da janela do editor de código para exibir seus membros associados. Você ainda pode expandir a sobreposição para exibir as propriedades filho.

    ![janela de depuração no editor do Visual Studio para Mac](media/unity-image31.png)

9. Pressione **F5** ou o botão **Executar** para continuar a execução. Retorne ao Unity para ver o cubo do inimigo repetidamente se aproximar do cubo do jogador. Talvez você precise ajustar a câmera se ele não estiver visível.

    ![cena sendo reproduzida no Unity](media/unity-image32.png)

10. Alterne novamente para o **Visual Studio para Mac** e defina um ponto de interrupção na primeira linha do método **Update**. Ele deve ser atingido imediatamente.

    ![como definir um ponto de interrupção no Visual Studio para Mac](media/unity-image33.png)

11. Suponha que a velocidade seja muito rápida e desejemos testar o impacto da alteração sem reiniciar o aplicativo. Localize a variável **Speed** na janela **Automáticos** ou **Locais** e, em seguida, altere-a para **"10"** e pressione **Enter**.

    ![como ajustar as variáveis na janela locais](media/unity-image34.png)

12. Remova o ponto de interrupção e pressione **F5** para retomar a execução.

13. Retorne ao **Unity** para exibir o aplicativo em execução. O cubo do inimigo agora está se movendo a um quinto da velocidade original.

    ![janela do Unity com o aplicativo em execução](media/unity-image35.png)

14. Interrompa o aplicativo do Unity clicando no botão **Reproduzir** novamente.

    ![como interromper o aplicativo do Unity](media/unity-image36.png)

15. Retorne ao **Visual Studio para Mac**. Interrompa a sessão de depuração clicando no botão **Parar**.

    ![como interromper a sessão de depuração no Visual Studio para Mac](media/unity-image37.png)

## <a name="task-4-exploring-unity-features-in-visual-studio-for-mac"></a>Tarefa 4: explorando recursos do Unity no Visual Studio para Mac

1. O Visual Studio para Mac fornece acesso rápido à documentação do Unity no editor de código. Coloque o cursor em algum lugar no símbolo **Vector3** dentro do método **Update** e pressione **Comando ⌘ + '**.

    ![como selecionar o método no editor do Visual Studio para Mac](media/unity-image38.png)

2. Uma nova janela do navegador é aberta na documentação do **Vector3**. Feche a janela do navegador quando estiver satisfeito.

    ![a janela do navegador é aberta na documentação](media/unity-image39.png)

3. O Visual Studio para Mac também fornece alguns auxiliares para criar rapidamente classes de comportamento do Unity. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Ativos** e selecione **Adicionar > Novo MonoBehaviour**.

    ![ação de contexto do novo monobehaviour](media/unity-image40.png)

4. A classe recém-criada fornece stubs para os métodos **Start** e **Update**. Após a chave de fechamento do método **Update**, comece a digitar **"onmouseup"**. Conforme você digita, observe que o IntelliSense do Visual Studio rapidamente converge para o método que você pretende implementar. Selecione-o na lista de preenchimento automático fornecida. Ele preencherá um stub de método para você, incluindo todos os parâmetros.

    ![IntelliSense no Visual Studio para Mac](media/unity-image41.png)

5. Dentro do método **OnMouseUp**, digite **"base".** para ver todos os métodos disponíveis a serem chamados. Explore também as diferentes sobrecargas de cada função usando a opção de paginação no canto superior direito do submenu do IntelliSense.

    ![como explorar sobrecargas no Visual Studio para Mac](media/unity-image42.png)

6. O Visual Studio para Mac também permite que você defina com facilidade os novos sombreadores. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Ativos** e selecione **Adicionar > Novo Sombreador**.

    ![nova ação de sombreador no Visual Studio para Mac](media/unity-image43.png)

7. O formato de arquivo do sombreador obtém um tratamento completo de cores e fontes para torná-lo mais fácil de ler e entender.

    ![realce de sintaxe](media/unity-image44.png)

8. Retorne ao **Unity**. Você verá que, como o Visual Studio para Mac funciona com o mesmo sistema de projeto, as alterações feitas em qualquer local são sincronizadas automaticamente com as outras. Agora fica fácil sempre usar a melhor ferramenta para a tarefa.

    ![painel Ativos do Unity](media/unity-image45.png)

## <a name="summary"></a>Resumo

Neste laboratório, você aprendeu a criar um jogo com o Unity e o Visual Studio para Mac. Consulte [https://unity3d.com/learn](https://unity3d.com/learn) para saber mais sobre o Unity.
