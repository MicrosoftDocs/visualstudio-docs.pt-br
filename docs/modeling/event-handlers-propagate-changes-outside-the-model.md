---
title: Manipuladores de eventos propagam alterações fora do modelo
description: Saiba que, no SDK de visualização e modelagem, você pode definir manipuladores de eventos de armazenamento para propagar alterações para recursos fora da loja.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, programming domain models
- Domain-Specific Language, events
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 115d26840f321792712392367794e443e41543a2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388939"
---
# <a name="event-handlers-propagate-changes-outside-the-model"></a>Manipuladores de eventos propagam alterações fora do modelo

No SDK de visualização e modelagem, você pode definir manipuladores de eventos de armazenamento para propagar alterações para recursos fora da loja, como variáveis de não armazenamento, arquivos, modelos em outras lojas ou outras extensões do Visual Studio. Os manipuladores de eventos de armazenamento são executados após o término da transação na qual o evento de disparo ocorreu. Eles também são executados em uma operação de desfazer ou refazer. Portanto, ao contrário das regras de armazenamento, os eventos de armazenamento são mais úteis para atualizar os valores que estão fora do repositório. Ao contrário dos eventos do .NET, os manipuladores de eventos de armazenamento são registrados para escutar uma classe: você não precisa registrar um manipulador separado para cada instância. Para obter mais informações sobre como escolher entre diferentes maneiras de lidar com alterações, consulte [respondendo e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

A superfície gráfica e outros controles de interface do usuário são exemplos de recursos externos que podem ser tratados por eventos de armazenamento.

### <a name="to-define-a-store-event"></a>Para definir um evento de repositório

1. Escolha o tipo de evento que você deseja monitorar. Para obter uma lista completa, examine as propriedades de <xref:Microsoft.VisualStudio.Modeling.EventManagerDirectory> . Cada propriedade corresponde a um tipo de evento. Os tipos de evento usados com mais frequência são:

    - `ElementAdded` -disparado quando um elemento de modelo, link de relação, forma ou conector é criado.

    - ElementPropertyChanged-disparado quando o valor de uma `Normal` propriedade de domínio é alterado. O evento será disparado somente se os valores novos e antigos não forem iguais. O evento não pode ser aplicado a propriedades de armazenamento calculadas e personalizadas.

         Ele não pode ser aplicado às propriedades de função que correspondem aos links de relação. Em vez disso, use `ElementAdded` para monitorar a relação de domínio.

    - `ElementDeleted` -disparado depois que um elemento de modelo, relação, forma ou conector foi excluído. Você ainda pode acessar os valores de Propriedade do elemento, mas ele não terá nenhuma relação com outros elementos.

2. Adicione uma definição de classe parcial para _YourDsl_**DocData** em um arquivo de código separado no projeto **DslPackage** .

3. Escreva o código do evento como um método, como no exemplo a seguir. Pode ser `static` , a menos que você queira acessar `DocData` .

4. Substituir `OnDocumentLoaded()` para registrar o manipulador. Se você tiver mais de um manipulador, poderá registrá-los todos no mesmo local.

O local do código de registro não é crítico. `DocView.LoadView()` é um local alternativo.

```csharp
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
      base.OnDocumentLoaded(); // Don't forget this.

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

## <a name="use-events-to-make-undoable-adjustments-in-the-store"></a>Usar eventos para fazer ajustes desfeitos na loja

Os eventos de armazenamento normalmente não são usados para propagar alterações no repositório, pois o manipulador de eventos é executado depois que a transação é confirmada. Em vez disso, você usaria uma regra de armazenamento. Para obter mais informações, consulte [regras propagar alterações no modelo](../modeling/rules-propagate-changes-within-the-model.md).

No entanto, você pode usar um manipulador de eventos para fazer atualizações adicionais na loja, se quiser que o usuário consiga desfazer as atualizações adicionais separadamente do evento original. Por exemplo, suponha que caracteres minúsculos sejam a Convenção comum para títulos de álbuns. Você poderia escrever um manipulador de eventos de armazenamento que corrija o título para letras minúsculas depois que o usuário o tiver digitado em letras maiúsculas. Mas o usuário pode usar o comando Desfazer para cancelar a correção, restaurando os caracteres em maiúsculas. Uma segunda desfazer removeria a alteração do usuário.

Por outro lado, se você escreveu uma regra de repositório para fazer a mesma coisa, a alteração do usuário e sua correção estarão na mesma transação, para que o usuário não possa desfazer o ajuste sem perder a alteração original.

```csharp
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

Se você escrever um evento que atualize o repositório:

- Use `store.InUndoRedoOrRollback` para evitar fazer alterações em elementos de modelo em desfazer. O Gerenciador de transações definirá tudo no repositório de volta para seu estado original.

- Use `store.InSerializationTransaction` para evitar fazer alterações enquanto o modelo está sendo carregado do arquivo.

- Suas alterações farão com que outros eventos sejam disparados. Certifique-se de evitar um loop infinito.

## <a name="store-event-types"></a>Armazenar tipos de evento

Cada tipo de evento corresponde a uma coleção em Store. EventManagerDirectory. Você pode adicionar ou remover manipuladores de eventos a qualquer momento, mas é comum adicioná-los quando o documento é carregado.

|`EventManagerDirectory` Nome da propriedade|Executado quando|
|-|-|
|ElementAdded|Uma instância de uma classe de domínio, relação de domínio, forma, conector ou diagrama é criada.|
|ElementDeleted|Um elemento de modelo foi removido do diretório de elementos do repositório e não é mais a origem ou o destino de nenhuma relação. O elemento não é realmente excluído da memória, mas é retido no caso de um futuro desfazer.|
|ElementEventsBegun|Chamado no final de uma transação externa.|
|ElementEventsEnded|Chamado quando todos os outros eventos foram processados.|
|ElementMoved|Um elemento de modelo foi movido de uma partição de repositório para outra.<br /><br /> Isso não está relacionado ao local de uma forma no diagrama.|
|ElementPropertyChanged|O valor de uma propriedade de domínio foi alterado. Isso será executado somente se os valores antigo e novo forem desiguais.|
|RolePlayerChanged|Uma das duas funções (extremidades) de uma relação faz referência a um novo elemento.|
|RolePlayerOrderChanged|Em uma função com multiplicidade maior que 1, a sequência de links foi alterada.|
|TransactionBeginning||
|TransactionCommitted||
|TransactionRolledBack||

## <a name="see-also"></a>Confira também

- [Respondendo a alterações e propagando-as](../modeling/responding-to-and-propagating-changes.md)
- [Código de exemplo: diagramas de circuito](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
