[Documentation](/docs) &gt; Resources &gt; Artworks

## Artworks API

An artwork is an artistic production created by an [artist](/docs/artists), multiple artists or an artist collective. An artwork may be part of a series and be reproduced in prints. Artworks are available from Artsy [partners](/docs/partners).

#### Retrieving Artworks

Retrieve artworks by following the [artworks](#{ArtsyAPI.artsy_api_root}/artworks) link from [root](#{ArtsyAPI.artsy_api_root}).

```
curl -v "#{ArtsyAPI.artsy_api_root}/artworks?public=true" -H "X-XAPP-Token:#{xapp_token}"
```

This endpoint accepts the following parameters.

Name       | Value                                                             |
----------:|:------------------------------------------------------------------|
public     | Retrieve publicly available artworks. This is currently required. |

The response is a [paginated result](/docs/pagination) with embedded artworks.

``` json
{
  "total_count" : 1,
  "_links" : {
    "self" : {
      "href" : "#{ArtsyAPI.artsy_api_root}/artworks"
    },
    "next" : {
      "href" : "#{ArtsyAPI.artsy_api_root}/artworks?cursor=..."
    }
  },
  "_embedded" : {
    "artworks" : [
      {
        "id" : "...",
        ...
      }
    ]
  }
}
```

#### Retrieving an Artwork

Users can retrieve a specific artwork by ID by rendering the "artwork" link template from [root](#{ArtsyAPI.artsy_api_root}).

```
curl -v "#{ArtsyAPI.artsy_api_root}/artworks/#{id}" -H "X-XAPP-Token:#{xapp_token}"
```

## Artwork JSON Format

Key                       | Description                                                                  |
-------------------------:|:-----------------------------------------------------------------------------|
id                        | Artwork ID.                                                                  |
created_at                | Date/time when the artwork was created.                                      |
updated_at                | Date/time when the artwork was last updated.                                 |
title                     | Title.                                                                       |
category                  | Category.                                                                    |
medium                    | Medium.                                                                      |
dimensions                | Artwork dimensions in inches and cm.                                         |
date                      | Date, can be a range, period or a year.                                      |
website                   | Website, typically for net art.                                              |
signature                 | Artist signature, when present on the artwork.                               |
series                    | Information about the series this work is part of.                           |
provenance                | Provenance.                                                                  |
literature                | Mentions of the work in publications.                                        |
exhibition_history        | Exhibition history.                                                          |
collecting_institution    | Collecting institution.                                                      |
additional_information    | Additional artwork information.                                              |
image_rights              | Additional image rights.                                                     |
blurb                     | Short text blurb about the artwork.                                          |
unique                    | Indicates a unique single artwork, generally applied to design objects.      |
cultural_maker            | Can be substituted for artist when no artist is available.                   |
can_inquire               | True when the artwork can be inquired on with an Artsy representative.       |
can_acquire               | True when the artwork can be acquired from Artsy via e-commerce.             |
can_share                 | Allow sharing on social networks.                                            |
sale_message              | Purchasing information, which may include price.                             |
sold                      | True if the artwork has been sold.                                           |
image_versions            | Available image versions.                                                    |

#### Links

Key        | Target                                           |
----------:|:-------------------------------------------------|
self       | The artwork resource.                            |
thumbnail  | Default image thumbnail.                         |
image:self | Curied image location.                           |
permalink  | An external location on the artsy.net website.   |
partner    | [Partner](/docs/partners) that owns the artwork. |

#### Embedded Collections

Key           | Target                                                                          |
-------------:|:--------------------------------------------------------------------------------|
artist_links  | A set of links to the [artists](/docs/artists) of this artwork.                 |
edition_sets  | A set of artwork [edition sets](/docs/edition_set) available for this artwork.  |

#### Example

``` json
{
  "id" : "515b244238ad2d3bc500001f",
  "created_at" : "2013-04-02T18:32:34.000Z",
  "updated_at" : "2014-08-28T17:25:30.000Z",
  "title" : "Allegory",
  "category" : "Painting",
  "medium" : "Oil on panel",
  "date" : "c. 1530",
  "dimensions" : {
    "in" : {
      "text" : "16 15/16 x 15 7/16 in",
      "height" : 16.9375,
      "width" : 15.4375,
      "depth" : null,
      "diameter" : null
    },
    "cm" : {
      "text" : "43 x 39.2 cm",
      "height" : 43.0,
      "width" : 39.2,
      "depth" : null,
      "diameter" : null
    }
  },
  "website" : "",
  "signature" : "",
  "series" : "",
  "provenance" : "",
  "literature" : "",
  "exhibition_history" : "",
  "collecting_institution" : "National Gallery of Art, Washington D.C.",
  "additional_information" : "...",
  "image_rights" : "Courtesy National Gallery of Art, Washington",
  "blurb" : "",
  "unique" : false,
  "cultural_maker" : "Venetian 16th Century",
  "can_inquire" : false,
  "can_acquire" : false,
  "can_share" : true,
  "sale_message" : null,
  "sold" : false,
  "_links" : {
    "curies" : [
      {
        "name" : "image",
        "href" : "http://static.artsy.net/additional_images/515b244538ad2d3bc5000026/3/{?rel}",
        "templated" : true
      }
    ],
    "thumbnail" : {
      "href" : "http://static.artsy.net/additional_images/515b244538ad2d3bc5000026/3/medium.jpg"
    },
    "image:self" : {
      "href" : "{?image_version}.jpg"
    },
    "partner" : {
      "href" : "#{ArtsyAPI.artsy_api_root}/api/partners/4f99c7b793ab4b0001000179"
    },
    "self" : {
      "href" : "#{ArtsyAPI.artsy_api_root}/api/artworks/515b244238ad2d3bc500001f"
    },
    "permalink" : {
      "href" : "http://artsy.net/artwork/venetian-16th-century-allegory"
    }
  },
  "image_versions" : ["small", "square", "medium", "tall", "large", "larger", "normalized"],
  "_embedded" : {
    "artist_links" : [
      {
        "id" : "515b212e9562c86fb800104a",
        "_links" : {
          "self" : {
            "href" : "#{ArtsyAPI.artsy_api_root}/api/artists/515b212e9562c86fb800104a"
          },
          "artist" : {
            "href" : "#{ArtsyAPI.artsy_api_root}/api/artists/515b212e9562c86fb800104a"
          }
        }
      }
    ],
    "edition_sets" : []
  }
}
```
