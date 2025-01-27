# Addresses

## Get all addresses

Returns all addresses associated with the specified accounts within the enterprise. This operation uses [Pagination](../guidelines/pagination.md).

### Request

`[PlatformAddress]/api/connector/v1/addresses/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "AccountIds": [
        "3db2c989-7d95-42b4-a502-a9f246db1634"
    ],
    "AddressIds": [
        "fc7b2df3-de66-48a6-907d-af4600ecd892"
    ],
    "UpdatedUtc": {
        "StartUtc": "2022-12-10T00:00:00Z",
        "EndUtc": "2022-12-17T00:00:00Z"
    },
    "Limitation": { "Count": 10 }
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `AccountIds` | array of string | optional, max 1000 items | Unique identifiers of [Companies](companies.md#company) or [Customers](customers.md#customer) within the enterprise. Required if no other filter is provided. |
| `AddressIds` | array of string | optional, max 1000 items | Unique identifiers of [Addresses](#account-address) within the enterprise. Use this property if you want to fetch specific addresses. Required if no other filter is provided. |
| `UpdatedUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval of [Address](#account-address) last update date and time. Required if no other filter is provided. |
| `Limitation` | [Limitation](../guidelines/pagination.md#limitation) | required | Limitation on the quantity of Account address returned. |

#### Time interval

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |

### Response

```javascript
{
    "Addresses": [
        {
            "Id": "fc7b2df3-de66-48a6-907d-af4600ecd892",
            "AccountId": "3db2c989-7d95-42b4-a502-a9f246db1634",
            "AccountType": "Customer",
            "Line1": "Rheinlanddamm 207-209",
            "Line2": null,
            "City": "Dortmund",
            "PostalCode": "44137",
            "CountryCode": "DE",
            "CountrySubdivisionCode": null,
            "Latitude": null,
            "Longitude": null
        }
    ],
    "Cursor": "fc7b2df3-de66-48a6-907d-af4600ecd892"
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Addresses` | array of [Account address](#account-address) | required | The collection of Account addresses, containing address and account information. |
| `Cursor` | string | required | Unique identifier of the last and hence oldest address item returned. This can be used in [Limitation](../guidelines/pagination.md#limitation) in a subsequent request to fetch the next batch of older Account address. |

#### Account address

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the address. |
| `AccountId` | string | required | Unique identifier of a [Company](companies.md#company) or a [Customer](customers.md#customer) within the enterprise. |
| `AccountType` | string | required | A discriminator specifying the [type of account](#account-type), e.g. customer or company. |
| `Line1` | string | optional | First line of the address. |
| `Line2` | string | optional | Second line of the address. |
| `City` | string | optional | The city. |
| `PostalCode` | string | optional | Postal code. |
| `CountryCode` | string | optional | ISO 3166-1 code of the [Country](countries.md#country). |
| `CountrySubdivisionCode` | string | optional | ISO 3166-2 code of the administrative division, e.g. `DE-BW`. |
| `Latitude` | number | optional | The latitude. |
| `Longitude` | number | optional | The longitude. |

#### Account type

* [Company](companies.md#company)
* [Customer](customers.md#customer)

## Add addresses

Adds one or more new addresses to the system and assign them to specified accounts.

### Request

`[PlatformAddress]/api/connector/v1/addresses/add`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "Addresses": [
        {
            "AccountId": "3db2c989-7d95-42b4-a502-a9f246db1634",
            "Line1": "Rheinlanddamm 207-209",
            "Line2": null,
            "City": "Dortmund",
            "PostalCode": "44137",
            "CountryCode": "DE",
            "CountrySubdivisionCode": null,
            "Latitude": null,
            "Longitude": null
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `Addresses` | array of [Account address parameters](#account-address-parameters), max 1000 items | required | Collection of addresses to be created. |

#### Account address parameters

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AccountId` | string | required | Unique identifier of a [Company](companies.md#company) or a [Customer](customers.md#customer) within the enterprise. |
| `Line1` | string | optional | First line of the address. |
| `Line2` | string | optional | Second line of the address. |
| `City` | string | optional | The city. |
| `PostalCode` | string | optional | Postal code. |
| `CountryCode` | string | optional | ISO 3166-1 code of the [Country](countries.md#country). |
| `CountrySubdivisionCode` | string | optional | ISO 3166-2 code of the administrative division, e.g. `DE-BW`. |
| `Latitude` | number | optional | The latitude in range of -90 to 90. |
| `Longitude` | number | optional | The longitude in range of -180 to 180. |

### Response

```javascript
{
    "Addresses": [
        {
            "Id": "fc7b2df3-de66-48a6-907d-af4600ecd892",
            "AccountId": "3db2c989-7d95-42b4-a502-a9f246db1634",
            "AccountType": "Customer",
            "Line1": "Rheinlanddamm 207-209",
            "Line2": null,
            "City": "Dortmund",
            "PostalCode": "44137",
            "CountryCode": "DE",
            "CountrySubdivisionCode": null,
            "Latitude": null,
            "Longitude": null
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Addresses` | array of [Account address](#account-address) | required | Created addresses. |

## Update addresses

Updates one or more existing addresses in the system, assigned to specified accounts.

### Request

`[PlatformAddress]/api/connector/v1/addresses/update`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "AddressUpdates" : [
        {
            "AddressId" : "fc7b2df3-de66-48a6-907d-af4600ecd892",
            "AccountId": "3db2c989-7d95-42b4-a502-a9f246db1634",
            "Line1": { "Value" : "I.P. Pavlova 5" },
            "Line2": { "Value" : null },
            "City": { "Value" : "Prague" },
            "PostalCode": { "Value" : "12000" },
            "CountryCode": { "Value" : "CZ" },
            "CountrySubdivisionCode": { "Value" : null }
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `AddressUpdates` | array of [Account address updates](#account-address-update-parameters), max 1000 items | required | Collection of addresses to be updated. |

#### Account address update parameters

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AddressId` | string | required | Unique identifier of the address. |
| `AccountId` | string | required | Unique identifier of a [Company](companies.md#company) or a [Customer](customers.md#customer) within the enterprise. |
| `Line1` | [String update value](#string-update-value) | optional | First line of the address. |
| `Line2` | [String update value](#string-update-value) | optional | Second line of the address. |
| `City` | [String update value](#string-update-value) | optional | The city. |
| `PostalCode` | [String update value](#string-update-value) | optional | Postal code. |
| `CountryCode` | [String update value](#string-update-value) | optional | ISO 3166-1 code of the [Country](countries.md#country). |
| `CountrySubdivisionCode` | [String update value](#string-update-value) | optional | ISO 3166-2 code of the administrative division, e.g. `DE-BW`. |

#### String update value

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Value` | string | optional | Value which is to be updated. |

### Response

```javascript
{
    "Addresses": [
        {
            "Id": "fc7b2df3-de66-48a6-907d-af4600ecd892",
            "AccountId": "3db2c989-7d95-42b4-a502-a9f246db1634",
            "AccountType": "Customer",
            "Line1": "I.P. Pavlova 5",
            "Line2": null,
            "City": "Prague",
            "PostalCode": "12000",
            "CountryCode": "CZ",
            "CountrySubdivisionCode": null,
            "Latitude": null,
            "Longitude": null
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Addresses` | array of [Account address](#account-address) | required | Updated addresses. |