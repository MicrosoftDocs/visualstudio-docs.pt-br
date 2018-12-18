---
title: Manipuladores de eventos propagam alterações fora do modelo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, events
ms.assetid: 0ac8d1e4-239f-4370-ba1d-3769bb38b8a5
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 7bfddc0903c520469833a0f160444202edf07c32
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49823691"
---
# <a name="event-handlers-propagate-changes-outside-the-model"></a>Manipuladores de eventos propagam alterações fora do modelo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No SDK de modelagem e visualização, você pode definir manipuladores de eventos do repositório para propagar alterações aos recursos fora do repositório, como variáveis de fora da store, arquivos, modelos em outros repositórios ou outro [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões. Manipuladores de eventos de Store são executados após o término da transação na qual ocorreu o evento de gatilho. Eles também são executados em uma operação de desfazer ou refazer. Portanto, ao contrário das regras de repositório de eventos de armazenamento são mais úteis para atualizar os valores que estão fora do repositório. Diferentemente dos eventos do .NET, manipuladores de eventos de armazenamento são registrados para escutar em uma classe: você não precisa registrar um manipulador separado para cada instância. Para obter mais informações sobre como escolher entre diferentes maneiras de manipular as alterações, consulte [respondendo a e propagando alterações](../modeling/responding-to-and-propagating-changes.md).  
  
 A superfície de gráfica e outros controles de interface do usuário são exemplos de recursos externos que podem ser manipulados pelo repositório de eventos.  
  
### <a name="to-define-a-store-event"></a>Para definir um evento de armazenamento  
  
1. Escolha o tipo de evento que você deseja monitorar. Para obter uma lista completa, examine as propriedades de <xref:Microsoft.VisualStudio.Modeling.EventManagerDirectory>. Cada propriedade corresponde a um tipo de evento. Usada com mais frequência são tipos de evento:  
  
   -   `ElementAdded` – disparado quando um elemento de modelo, link de relação, forma ou conector é criado.  
  
   -   ElementPropertyChanged – disparado quando o valor de um `Normal` propriedade de domínio é alterada. O evento é disparado somente se os valores novos e antigos não são iguais. O evento não pode ser aplicado às propriedades de armazenamento calculadas e personalizadas.  
  
        Ele não pode ser aplicado a propriedades da função que correspondem aos links do relacionamento. Em vez disso, use `ElementAdded` para monitorar a relação de domínio.  
  
   -   `ElementDeleted` – disparado depois de um elemento de modelo, relação, forma ou conector foi excluído. Você ainda pode acessar os valores de propriedade do elemento, mas ele será não têm nenhuma relação a outros elementos.  
  
2. Adicione uma definição de classe parcial para _{1&gt;yourdsl&lt;1_**DocData** em um arquivo de código separado no **DslPackage** projeto.  
  
3. Escreva o código do evento como um método, como no exemplo a seguir. Ele pode ser `static`, a menos que você deseja acessar `DocData`.  
  
4. Substituir `OnDocumentLoaded()` para registrar o manipulador. Se você tiver mais de um manipulador, você pode registrá-los todos no mesmo lugar.  
  
   O local do código de registro não é crítico. `DocView.LoadView()` é um local alternativo.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using Microsoft.VisualStudio.Modeling;  
  
namespace Company.MusicLib  
{  
  partial class MusicLibDocData  
  {  
    // Register store events here or in DocView.LoadView().  
    protected override void OnDocumentLoaded()  
    {  
      base.OnDocumentLoaded(); // Don’t forget this.  
  
      #region Store event handler registration.       
      Store store = this.Store;  
      EventManagerDirectory emd = store.EventManagerDirectory;  
      DomainRelationshipInfo linkInfo = store.DomainDataDirectory  
          .FindDomainRelationship(typeof(ArtistAppearsInAlbum));  
      emd.ElementAdded.Add(linkInfo,   
          new EventHandler<ElementAddedEventArgs>(AddLink));  
      emd.ElementDeleted.Add(linkInfo,   
          new EventHandler<ElementDeletedEventArgs>(RemoveLink));  
  
      #endregion Store event handlers.  
    }  
  
    private void AddLink(object sender, ElementAddedEventArgs e)  
    {  
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;  
      if (link != null)   
            ExternalDatabase.Add(link.Artist.Name, link.Album.Title);  
    }  
    private void RemoveLink(object sender, ElementDeletedEventArgs e)  
    {  
      ArtistAppearsInAlbum link = e.ModelElement as ArtistAppearsInAlbum;  
      if (link != null)   
            ExternalDatabase.Delete(link.Artist.Name, link.Album.Title);  
    }  
  }  
  
}  
  
```  
  
## <a name="using-events-to-make-undoable-adjustments-in-the-store"></a>Usando eventos para fazer ajustes que podem ser desfeitos na Store  
 Eventos de Store não são normalmente usados para propagar alterações dentro do armazenamento, como o manipulador de eventos é executado depois que a transação for confirmada. Em vez disso, você usaria uma regra do repositório. Para obter mais informações, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).  
  
 No entanto, você pode usar um manipulador de eventos para fazer atualizações adicionais para o repositório, se você quiser que o usuário poderá desfazer as atualizações adicionais separadamente do evento original. Por exemplo, suponha que caracteres em letras minúsculas são a convenção e para títulos de álbum. Você pode escrever um manipulador de eventos de armazenamento que corrige o título em letras minúsculas depois que o usuário digitou em letras maiusculas. Mas o usuário pode usar o comando Desfazer para cancelar a sua correção, restaurando os caracteres de letras maiusculas. Remove um segundo desfazer a alteração do usuário.  
  
 Por outro lado, se você escreveu uma regra do repositório para fazer a mesma coisa, a alteração do usuário e sua correção seria na mesma transação, para que o usuário não foi possível desfazer o ajuste sem perder a alteração original.  
  
```  
  
partial class MusicLibDocView  
{  
    // Register store events here or in DocData.OnDocumentLoaded().  
    protected override void LoadView()  
    {  
      /* Register store event handler for Album Title property. */  
      // Get reflection data for property:  
      DomainPropertyInfo propertyInfo =   
        this.DocData.Store.DomainDataDirectory  
        .FindDomainProperty(Album.TitleDomainPropertyId);  
      // Add to property handler list:  
      this.DocData.Store.EventManagerDirectory  
        .ElementPropertyChanged.Add(propertyInfo,  
        new EventHandler<ElementPropertyChangedEventArgs>  
             (AlbumTitleAdjuster));  
  
      /*  
      // Alternatively, you can set one handler for   
      // all properties of a class.  
      // Your handler has to determine which property changed.  
      DomainClassInfo classInfo = this.Store.DomainDataDirectory  
           .FindDomainClass(typeof(Album));  
      this.Store.EventManagerDirectory  
          .ElementPropertyChanged.Add(classInfo,  
        new EventHandler<ElementPropertyChangedEventArgs>  
             (AlbumTitleAdjuster));  
       */  
      return base.LoadView();  
    }  
  
// Undoable adjustment after a property is changed.   
// Method can be static since no local access.  
private static void AlbumTitleAdjuster(object sender,  
         ElementPropertyChangedEventArgs e)  
{  
  Album album = e.ModelElement as Album;  
  Store store = album.Store;  
  
  // We mustn't update the store in an Undo:  
  if (store.InUndoRedoOrRollback   
      || store.InSerializationTransaction)  
      return;  
  
  if (e.DomainProperty.Id == Album.TitleDomainPropertyId)  
  {  
    string newValue = (string)e.NewValue;  
    string lowerCase = newValue.ToLowerInvariant();  
    if (!newValue.Equals(lowerCase))  
    {  
      using (Transaction t = store.TransactionManager  
            .BeginTransaction("adjust album title"))  
      {  
        album.Title = lowerCase;  
        t.Commit();  
      } // Beware! This could trigger the event again.  
    }  
  }  
  // else other properties of this class.  
}  
  
```  
  
 Se você gravar um evento que atualiza o repositório:  
  
-   Use `store.InUndoRedoOrRollback` Evite fazer alterações a elementos de modelo em Desfazer. O Gerenciador de transações definirá tudo no armazenamento de volta ao estado original.  
  
-   Use `store.InSerializationTransaction` Evite fazer alterações enquanto o modelo está sendo carregado do arquivo.  
  
-   Suas alterações fará com que mais eventos sejam disparados. Certifique-se de que você evite um loop infinito.  
  
## <a name="store-event-types"></a>Tipos de evento Store  
 Cada tipo de evento corresponde a uma coleção em Store.EventManagerDirectory. Você pode adicionar ou remover manipuladores de eventos a qualquer momento, mas é comum o uso para adicioná-las quando o documento é carregado.  
  
|`EventManagerDirectory` Nome da propriedade|Executado quando|  
|-------------------------------------------|-------------------|  
|ElementAdded|Uma instância de uma classe de domínio, o relacionamento de domínio, forma, conector ou diagrama é criada.|  
|ElementDeleted|Um elemento de modelo foi removido do diretório do elemento da loja e não é mais a origem ou destino de qualquer relação. O elemento, na verdade, não é excluído da memória, mas é mantido no caso de um Desfazer futuras.|  
|ElementEventsBegun|Invocado no final de uma transação externa.|  
|ElementEventsEnded|Invocado quando todos os outros eventos que tenham sido processados.|  
|ElementMoved|Um elemento de modelo foi movido de um repositório de partição para outra.<br /><br /> Isso não é relacionado ao local de uma forma no diagrama.|  
|ElementPropertyChanged|O valor de uma propriedade de domínio foi alterado. Isso é executado somente se os valores novos e antigos são diferentes.|  
|RolePlayerChanged|Uma das duas funções (termina) de uma relação faz referência a um novo elemento.|  
|RolePlayerOrderChanged|Em uma função com multiplicidade maior que 1, a sequência de links foi alterado.|  
|TransactionBeginning||  
|TransactionCommitted||  
|TransactionRolledBack||  
  
## <a name="see-also"></a>Consulte também  
 [Respondendo a alterações e propagando-](../modeling/responding-to-and-propagating-changes.md)   
 [Código de amostra: diagramas de circuito](http://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)



