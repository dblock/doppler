[Documentation](/docs) &gt; Resources &gt; Partners

## Partners API

A partner provides [artworks](/docs/artworks).

#### Retrieving Partners

Retrieve partners by following the [partners](#{ArtsyAPI.artsy_api_root}/partners?active=true) link from [root](#{ArtsyAPI.artsy_api_root}).

```
curl -v "#{ArtsyAPI.artsy_api_root}/partners?active=true" -H "X-XAPP-Token:#{xapp_token}"
```

This endpoint accepts the following parameters.

Name       | Value                                                             |
----------:|:------------------------------------------------------------------|
active     | Retrieve active partners. This is currently required.             |

The response is a [paginated result](/docs/pagination) with embedded partners.

``` json
{
  "total_count" : 1,
  "_links" : {
    "self" : {
      "href" : "#{ArtsyAPI.artsy_api_root}/partners"
    },
    "next" : {
      "href" : "#{ArtsyAPI.artsy_api_root}/partners?cursor=..."
    }
  },
  "_embedded" : {
    "partners" : [
      {
        "id" : "...",
        ...
      }
    ]
  }
}
```

#### Retrieving an Partner

Users can retrieve a specific partner by ID by rendering the "partner" link template from [root](#{ArtsyAPI.artsy_api_root}).

```
curl -v "#{ArtsyAPI.artsy_api_root}/partners/#{id}" -H "X-XAPP-Token:#{xapp_token}"
```

## Partner JSON Format

Key              | Description                                        |
----------------:|:---------------------------------------------------|
id               | Partner ID.                                        |
created_at       | Date/time when the partner was created.            |
updated_at       | Date/time when the partner was last updated.       |
name             | Partner's name.                                    |
type             | Partner type, eg. "museum".                        |
email            | Contact e-mail.                                    |
region           | Region, eg. "North America".                       |

#### Links

Key        | Target                                          |
----------:|:------------------------------------------------|
self       | The partner resource.                           |
profile    | Partner [profile](/docs/profiles).              |
permalink  | An external location on the artsy.net website.  |
website    | Official website.                               |

#### Example

``` json
#{resource://partner/id:4f99c7b793ab4b0001000179}
```
