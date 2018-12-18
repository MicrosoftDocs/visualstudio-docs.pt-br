---
title: Personalizando o comportamento de exclusão | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.dsltools.dsldesigner.deletebehavior
helpviewer_keywords:
- Domain-Specific Language, deletion
ms.assetid: c6bf088d-52c6-4817-af45-ddae745bb5a9
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 401458a33c67d0c8d0302fddcdfd988113101e28
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49837549"
---
# <a name="customizing-deletion-behavior"></a>Personalizando o comportamento da operação de excluir
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exclusão de um elemento geralmente provoca também a exclusão de seus elementos relacionados. Todas as relações conectadas a ele e quaisquer elementos filhos são excluídos. Esse comportamento é chamado *excluir propagação*. Você pode personalizar a propagação da exclusão, por exemplo, para providenciar que os elementos adicionais relacionados sejam excluídos. Ao escrever o código do programa, você pode fazer com que a propagação de exclusão dependa do estado do modelo. Também é possível causar outras alterações em resposta a uma exclusão.  
  
 Este tópico inclui as seções a seguir:  
  
-   [Comportamento de exclusão padrão](#default)  
  
-   [Definindo a opção Propagar exclusão de uma função](#property)  
  
-   [Substituindo o fechamento da exclusão](#closure) – Use essa técnica em que a exclusão possa levar à exclusão de elementos vizinhos.  
  
-   [Usando OnDeleting e OnDeleted](#ondeleting) – usar esses métodos em que a resposta pode incluir outras ações, como atualizar um valor dentro ou fora do repositório.  
  
-   [Regras de exclusão](#rules) – usar regras para propagar atualizações de qualquer tipo no repositório, em que uma alteração possa levar a outras pessoas.  
  
-   [Eventos de exclusão](#rules) – eventos de armazenamento de uso para propagar atualizações fora do repositório, por exemplo, para outros [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] documentos.  
  
-   [Desfazer mesclagem](#unmerge) – use a operação Desfazer mesclagem para desfazer a operação de mesclagem que anexa um elemento filho ao pai.  
  
##  <a name="default"></a> Comportamento de exclusão padrão  
 Por padrão, as seguintes regras regem a propagação da exclusão:  
  
-   Se um elemento for excluído, todos os elementos incorporados também serão excluídos. Os elementos incorporados são os elementos de destino das relações de incorporação para os quais este elemento é a fonte. Por exemplo, se houver uma relação de incorporação de **álbum** à **música**, em seguida, quando determinado álbum for excluído, todas as suas músicas também serão excluídas.  
  
     Por outro lado, a exclusão de uma música não exclui o álbum.  
  
-   Por padrão, a exclusão não se propaga ao longo das relações de referência. Se não houver uma relação de referência **ArtistPlaysOnAlbum** partir **álbum** para **artista**, excluir um álbum não excluirá nenhum artista relacionado e exclusão de um artista não excluirá nenhum álbum.  
  
     No entanto, a exclusão se propaga ao longo de algumas relações internas. Por exemplo, quando um elemento do modelo é excluído, sua forma no diagrama também é excluída. O elemento e a forma estão relacionados pela relação de referência `PresentationViewsSubject`.  
  
-   Todo relacionamento conectado ao elemento, seja na origem ou no destino, é excluído. A propriedade de função do elemento na função oposta passa a não conter o elemento excluído.  
  
##  <a name="property"></a> Definindo a opção Propagar exclusão de uma função  
 Você pode fazer com que a exclusão se propague ao longo da relação de referência ou de um filho incorporado ao seu pai.  
  
#### <a name="to-set-delete-propagation"></a>Para configurar a propagação de exclusão  
  
1. No diagrama de definição de DSL, selecione a *função* a serem propagação seja excluída. A função é representada pela linha à esquerda ou à direita de uma caixa de relação de domínio.  
  
    Por exemplo, se você deseja especificar que sempre que um Álbum for excluído, os Artistas relacionados também sejam excluídos, selecione a função conectada ao Artista da classe de domínio.  
  
2. Na janela Propriedades, defina as **propaga exclusão** propriedade.  
  
3. Pressione F5 e verifique se:  
  
   -   Quando uma instância desse relacionamento é excluída, o elemento na função selecionada também é excluído.  
  
   -   Quando um elemento na função oposta é excluído, instâncias dessa relação são excluídas e os elementos relacionados a essa função são excluídos.  
  
   Você também pode ver a **propaga exclusão** opção a **detalhes de DSL** janela. Selecione uma classe de domínio e, na janela de detalhes de DSL, abra o **comportamento de exclusão** página clicando no botão ao lado da janela. O **propagar** opção é mostrada para a função oposta de cada relação. O **Excluir estilo** coluna indica se o **propagar** opção está em sua configuração padrão, mas ele não tem nenhuma efeito separado.  
  
## <a name="delete-propagation-by-using-program-code"></a>Propagação de exclusão usando o código do programa  
 As opções no arquivo Definição de DSL só permitem que você escolha se a exclusão se propaga para um vizinho imediato ou não. Para implementar um esquema mais complexo de propagação de exclusão, você pode gravar o código do programa.  
  
> [!NOTE]
>  Para adicionar o código de programa à definição de DSL, crie um arquivo de código separado na **Dsl** de projeto e escreva definições parciais para aumentar as classes na pasta código gerado. Para obter mais informações, consulte [escrevendo código para personalizar uma linguagem específica do domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md).  
  
##  <a name="closure"></a> Definindo um fechamento de exclusão  
 A operação de exclusão usa a classe _YourModel_**DeleteClosure** para determinar quais os elementos excluir, de acordo com uma seleção inicial. Ela chama `ShouldVisitRelationship()` e `ShouldVisitRolePlayer()` repetidamente, percorrendo o gráfico de relações. Você pode substituir esses métodos. ShouldVisitRolePlayer é fornecido com a identidade de um vínculo e o elemento de uma das funções do vínculo. Ele deve retornar um dos seguintes valores:  
  
-   **VisitorFilterResult.Yes**– o elemento deve ser excluído e o caminhador deve prosseguir e tentar o elemento de outros links.  
  
-   **VisitorFilterResult.DoNotCare** – o elemento não deve ser excluído, a menos que outra consulta responda que deve ser excluído.  
  
-   **VisitorFilterResult.Never** – o elemento não deve ser excluído, mesmo se outra consulta responda **Sim**, e o caminhador não deve tentar o elemento de outros links.  
  
```  
// When a musician is deleted, delete their albums with a low rating.  
// Override methods in <YourDsl>DeleteClosure in DomainModel.cs  
partial class MusicLibDeleteClosure  
{  
  public override VisitorFilterResult ShouldVisitRolePlayer  
    (ElementWalker walker, ModelElement sourceElement, ElementLink elementLink,   
    DomainRoleInfo targetDomainRole, ModelElement targetRolePlayer)  
  {  
    ArtistAppearsInAlbum link = elementLink as ArtistAppearsInAlbum;  
    if (link != null   
       && targetDomainRole.RolePlayer.Id == Album.DomainClassId)  
    {  
      // Count other unvisited links to the Album of this link.  
      if (ArtistAppearsInAlbum.GetLinksToArtists(link.Album)  
              .Where(linkAlbumArtist =>   
                     linkAlbumArtist != link &&  
                     !walker.Visited(linkAlbumArtist))  
              .Count() == 0)  
      {  
        // Should delete this role player:  
        return VisitorFilterResult.Yes;   
      }  
      else  
        // Don’t delete unless another relationship deletes it:  
        return VisitorFilterResult.DoNotCare;   
    }  
    else   
    {  
      // Test for and respond to other relationships and roles here.  
  
      // Not the relationship or role we’re interested in.  
      return base.ShouldVisitRolePlayer(walker, sourceElement,   
             elementLink, targetDomainRole, targetRolePlayer);  
    }  
  }  
}  
  
```  
  
 A técnica de fechamento garante que o conjunto de elementos e vínculos a serem excluídos seja determinado antes que a exclusão comece. O caminhador também combina os resultados de seu fechamento com os de outras partes do modelo.  
  
 No entanto, a técnica supõe que a exclusão afete apenas seus vizinhos no gráfico de relações: não é possível usar esse método para excluir um elemento em outra parte do modelo. Você não poderá usá-lo se quiser adicionar elementos ou fazer outras alterações em resposta a uma exclusão.  
  
##  <a name="ondeleting"></a> Usando OnDeleting e OnDeleted  
 Você pode substituir `OnDeleting()` ou `OnDeleted()` em uma classe de domínio ou em uma relação de domínio.  
  
1. <xref:Microsoft.VisualStudio.Modeling.ModelElement.OnDeleting%2A> é chamado quando um elemento está prestes a ser excluído, mas antes que suas relações sejam desconectadas. Ele ainda é navegável de outros elementos e ainda está em `store.ElementDirectory`.  
  
    Se vários elementos forem excluído ao mesmo tempo, OnDeleting será chamado por todos eles antes de executar as exclusões.  
  
    `IsDeleting` é verdadeiro.  
  
2. <xref:Microsoft.VisualStudio.Modeling.ModelElement.OnDeleted%2A> é chamado quando o elemento foi excluído. Ele permanece no heap do CLR para que um Desfazer possa ser realizado, se necessário, mas é desvinculado de outros elementos e removido de `store.ElementDirectory`. Para relações, a função ainda referencia os antigo representantes da função.`IsDeleted` é verdadeiro.  
  
3. OnDeleting e OnDeleted são chamados quando o usuário invoca Desfazer depois de criar um elemento e quando uma exclusão anterior é repetida em Refazer. Use `this.Store.InUndoRedoOrRollback` para evitar atualizar elementos de repositório nesses casos. Para obter mais informações, consulte [como: usar transações para atualizar o modelo](../modeling/how-to-use-transactions-to-update-the-model.md).  
  
   Por exemplo, o código a seguir exclui um Álbum quando sua última Música filha é excluída:  
  
```  
  
// Delete the parent Album when the last Song is deleted.  
// Override methods in the embedding relationship between Album and Song:  
partial class AlbumHasSongs  
{  
  protected override void OnDeleted()  
  {  
    base.OnDeleted();  
    // Don't perform in-store actions in undo:  
    if (this.Store.InUndoRedoOrRollback) return;  
    // Relationship source and target still work:  
    // Don't bother if source is already on its way out:  
    if (!this.Album.IsDeleting && !this.Album.IsDeleted)  
    {  
      if (this.Album.Songs.Count == 0)  
      {   
        this.Album.Delete();  
} } } }  
  
```  
  
 Muitas vezes, é mais prático acionar a partir da exclusão da relação do que no elemento de função, pois isso funciona quando o elemento é excluído e quando a própria relação é excluída. No entanto, para uma relação de referência, propague a exclusão quando um elemento relacionado é excluído, mas não quando a própria relação for excluída. Este exemplo exclui um Álbum quando seu último Artista colaborador é excluído, mas não responde se as relações forem excluídas:  
  
```  
using System.Linq; ...  
// Assumes a many-many reference relationship   
// between Artist and Album.    
partial class Artist  
{  
  protected override void OnDeleting()  
  {  
    base.OnDeleting();  
    if (this.Store.InUndoRedoOrRollback) return;  
    List<Album> toDelete = new List<Album>();  
    foreach (Album album in this.Albums)  
    {  
      if (album.Artists.Where(artist => !artist.IsDeleting)  
                        .Count() == 0)  
      {  
        toDelete.Add(album);  
      }  
    }  
    foreach (Album album in toDelete)  
    {  
      album.Delete();  
} } }  
  
```  
  
 Quando você executa <xref:Microsoft.VisualStudio.Modeling.ModelElement.Delete%2A> em um elemento, OnDeleting e OnDeleted são chamados. Esses métodos são realizados em linha, isto é, imediatamente antes e após a exclusão real. Se o seu código excluir dois ou mais elementos, OnDeleting e OnDeleted serão chamados em alternância em todos eles, um após o outro.  
  
##  <a name="rules"></a> Regras de exclusão e eventos  
 Como uma alternativa aos manipuladores OnDelete, você pode definir regras e eventos de exclusão.  
  
1.  **Excluindo** e **excluir** as regras são acionadas apenas em uma transação e não em Desfazer ou refazer. Você pode configurá-las para serem colocadas em fila para execução no final da transação em que a exclusão é realizada. As regras Deleting são sempre executadas antes de qualquer regra Deleted na fila.  
  
     Use regras para propagar alterações que afetam apenas os elementos no repositório, incluindo relações, elementos de diagrama e suas propriedades. Normalmente, uma regra Deleting é usada para propagar exclusão e uma regra Delete é usada para criar elementos e relações de reposição.  
  
     Para obter mais informações, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).  
  
2.  **Excluído** repositório de eventos é invocado no final de uma transação e é chamado após um Desfazer ou refazer. Ele pode, portanto, ser usado para propagar exclusões a objetos fora do repositório, tais como arquivos, entradas de banco de dados ou outros objetos no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
     Para obter mais informações, consulte [manipuladores de propagar alterações fora o modelo de evento](../modeling/event-handlers-propagate-changes-outside-the-model.md).  
  
    > [!WARNING]
    >  Quando um elemento é excluído, você pode acessar seus valores de propriedade de domínio, mas não é possível navegar nos vínculos de relação. No entanto, se você definir um evento excluído em um relacionamento, também poderá acessar os dois elementos que eram seus usuários. Assim, se você quiser responder à exclusão de um elemento de modelo, mas quiser acessar um elemento ao qual ele estava vinculado, defina um evento de exclusão no relacionamento em vez da classe de domínio do elemento modelo.  
  
### <a name="example-deletion-rules"></a>Exemplo de regras de exclusão  
  
```  
[RuleOn(typeof(Album), FireTime = TimeToFire.TopLevelCommit)]  
internal class AlbumDeletingRule : DeletingRule  
{  
  public override void ElementDeleting(ElementDeletingEventArgs e)  
  {  
    base.ElementDeleting(e);  
    // ...perform tasks to propagate imminent deletion  
  }  
}  
[RuleOn(typeof(Album), FireTime = TimeToFire.TopLevelCommit)]  
internal class AlbumDeletedRule : DeleteRule  
{  
  public override void ElementDeleted(ElementDeletedEventArgs e)  
  {  
    base.ElementDeleted(e);  
    // ...perform tasks such as creating new elements  
  }  
}  
  
// The rule must be registered:  
public partial class MusicLibDomainModel  
{  
  protected override Type[] GetCustomDomainModelTypes()  
  {  
    List<Type> types = new List<Type>(base.GetCustomDomainModelTypes());  
    types.Add(typeof(AlbumDeletingRule));  
    types.Add(typeof(AlbumDeletedRule));  
    // If you add more rules, list them here.   
    return types.ToArray();  
  }  
}  
  
```  
  
### <a name="example-deleted-event"></a>Exemplo de evento Deleted  
  
```  
partial class NestedShapesSampleDocData  
{  
  protected override void OnDocumentLoaded(EventArgs e)  
  {  
    base.OnDocumentLoaded(e);  
    DomainRelationshipInfo commentRelationship =   
          this.Store.DomainDataDirectory  
          .FindDomainRelationship(typeof(CommentsReferenceComponents));  
  
    this.Store.EventManagerDirectory.ElementDeleted.Add(commentRelationship,  
      new EventHandler<ElementDeletedEventArgs>(CommentLinkDeleted));  
  }  
  
  private void CommentLinkDeleted (object sender, ElementDeletedEventArgs e)  
  {  
    CommentsReferenceComponents link = e.ModelElement as CommentsReferenceComponents;  
    Comment comment = link.Comment;  
    Component component = link.Subject;  
    if (comment.IsDeleted)  
    {  
      // The link was deleted because the comment was deleted.  
      System.Windows.Forms.MessageBox.Show("Removed comment on " + component.Name);  
    }  
    else  
    {  
      // It was just the link that was deleted - the comment itself remains.  
      System.Windows.Forms.MessageBox.Show("Removed comment link to "   
           + component.Name);  
    }  
  }  
}  
  
```  
  
##  <a name="unmerge"></a> Desfazer a mesclagem  
 A operação que anexa um elemento filho para seu pai é chamada *mesclagem*. Ela ocorre quando um novo elemento ou grupo de elementos é criado a partir da caixa de ferramentas, ou transferida de outra parte do modelo, ou copiada da área de transferência. Além de criar uma relação de incorporação entre o pai e seu novo filho, a operação de mesclagem também pode definir relações adicionais, criar elementos auxiliares e definir valores de propriedades nos elementos. A operação de mesclagem é encapsulada em uma EMD (Diretiva de Mesclagem de Elementos).  
  
 Uma EMD também encapsula complementar *desfazer a mesclagem* ou `MergeDisconnect` operação. Se você tiver um conjunto de elementos que foi construído usando uma mesclagem, é recomendável usar a operação desfazer mesclagem associada para remover um elemento dele se quiser deixar os elementos restantes em um estado consistente. A operação desfazer mesclagem normalmente usa as técnicas descritas nas seções anteriores.  
  
 Para obter mais informações, consulte [Personalizando a criação de elemento e a movimentação](../modeling/customizing-element-creation-and-movement.md).  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md)   
 [Personalizando a criação de elemento e movimentação](../modeling/customizing-element-creation-and-movement.md)   
 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)



