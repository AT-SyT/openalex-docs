# 📚 Venue

## The `Venue` object

### `id`

_String:_ The [OpenAlex ID](./#the-openalex-id) for this venue.

```json
id: "https://openalex.org/V1983995261"
```

### `issn_l`

_String:_ The [ISSN-L](https://en.wikipedia.org/wiki/International\_Standard\_Serial\_Number#Linking\_ISSN) identifying this venue.

ISSN is a global and unique ID for serial publications. However, different media versions of a given publication (e.g., print and electronic) often have _different_ ISSNs. This is why we can't have nice things. The ISSN-L or Linking ISSN solves the problem by designating a single canonical ISSN for all media versions of the title. It's _usually_ the same as the print ISSN.

```json
issn_l: "2167-8359"
```

### `issn`

_List:_ The [ISSNs](https://en.wikipedia.org/wiki/International\_Standard\_Serial\_Number) used by this venue. Many publications have multiple ISSNs ([see above](venue.md#issn\_l)), so [ISSN-L](venue.md#issn\_l) should be used when possible.

```json
issn:["2167-8359"]
```

### `display_name`

_String:_ The name of the venue.

```json
display_name: "PeerJ"
```

### `publisher`

_String:_ The name of this venue's publisher. Publisher is a tricky category, as journals often change publishers, publishers merge, publishers have subsidiaries ("imprints"), and of course no one is consistent in their naming. In the future, we plan to roll out support for a more structured publisher field, but for now it's just a string.

```json
publisher: "Peerj"
```

### `works_count`

_Integer:_ The number of [`Works`](work.md) this this venue hosts.

```json
works_count: 20184 
```

### `cited_by_count`

_Integer:_ The total number of [`Works`](work.md) that cite a `Work` hosted in this venue.

```json
cited_by_count: 133702 
```

### `is_oa`

_Boolean:_ **todo**&#x20;

```json
is_oa: true 
```

### `is_in_doaj`

_Boolean:_ **todo**&#x20;

```json
is_in_doaj: true 
```

### `homepage_url`

_String:_ **todo**&#x20;

```json
homepage_url: "http://www.peerj.com/" 
```

### `ids`

_Object:_ All the external identifiers that we know about for this venue. IDs are expressed as URIs whenever possible. Possible ID types:

* `openalex` (_String:_ this venue's [OpenAlex ID](./#the-openalex-id). Same as [`Venue.id`](venue.md#id))
* `issn_l` (_String:_ this venue's ISSN-L. Same as [`Venue.issn_l`](venue.md#issn\_l))
* `mag`  (_Integer:_ this venue's [Microsoft Academic Graph](https://www.microsoft.com/en-us/research/project/microsoft-academic-graph/) ID)
* `issn` (_List:_ a list of this venue's ISSNs. Same as [`Venue.issn`](venue.md#issn))

{% hint style="info" %}
Many venues are missing one or more ID types (either because we don't know the ID, or because it was never assigned). Keys for null IDs are not displayed.
{% endhint %}

```json
ids: {
    openalex: "https://openalex.org/V1983995261",
    issn_l: "2167-8359",
    issn: [
        "2167-8359"
    ],
    mag: 1983995261
}
```

### `x_concepts`

{% hint style="danger" %}
The "x" in `x_concepts` is because it's experimental and subject to removal with very little warning. We plan to replace it with a custom link to the Concepts API endpoint.&#x20;
{% endhint %}

_List:_ The `Concepts` most frequently applied to works hosted by this venue. Each is represented as a [dehydrated Concept](concept.md#the-dehydratedconcept-object) object, with one additional attribute:

`score` (_Float_): The strength of association between this venue and the listed concept, from 0-100.

```json
x_concepts: [
    {
        id: "https://openalex.org/C86803240",
        wikidata: null,
        display_name: "Biology",
        level: 0,
        score: 86.7
    },
    {
        id: "https://openalex.org/C185592680",
        wikidata: null,
        display_name: "Chemistry",
        level: 0,
        score: 51.4
    },
    
    // and so forth
]
```

### `counts_by_year`

_List:_ [`works_count`](venue.md#works\_count) and [`cited_by_count`](venue.md#cited\_by\_count) for each of the last ten years, binned by year. To put it another way: each year, you can see how many new works this venue started hosting, and how many times _any_ work in this venue got cited.

If the venue was founded less than ten years ago, there will naturally be fewer than ten years in this list.

```json
counts_by_year: [
    {
        year: 2021,
        works_count: 4338,
        cited_by_count: 127268
    },
    {
        year: 2020,
        works_count: 4363,
        cited_by_count: 119531
    },
    
    // and so forth
]
```



### `works_api_url`

_String:_ A URL that will get you a list of all this venue's `Works`.

We express this as an API URL (instead of just listing the works themselves) because sometimes a venue's publication list is too long to reasonably fit into a single `Venue` object.

```json
works_api_url: "https://api.openalex.org/works?filter=host_venue.id:V1983995261",
```



### `updated_date`

_String:_ The last time anything in this `Venue` object changed, expressed as an [ISO 8601](https://en.wikipedia.org/wiki/ISO\_8601) date string. This date is updated for _any change at all_, including increases in various counts.

```json
updated_date: "2022-01-02T00:00:00"
```









## The `DehydratedVenue` object

The `DehydratedVenue` is stripped-down [`Venue`](venue.md#the-venue-object) object, with most of its properties removed to save weight. Its only remaining properties are:

* [`id`](venue.md#id)``
* [`issn_l`](venue.md#issn\_l)``
* [`issn`](venue.md#issn)``
* [`display_name`](venue.md#display\_name)``
* ``[`publisher`](venue.md#publisher)``
