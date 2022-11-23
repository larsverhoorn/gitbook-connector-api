# Sources

## Get all sources

Returns all sources from which reservations can be coming from. Note this operation uses [Pagination](../guidelines/pagination.md).

### Request

`[PlatformAddress]/api/connector/v1/sources/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "Limitation": {
        "Count": 10,
        "Cursor": null
    }
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `Limitation` | [Limitation](../guidelines/pagination.md#limitation) | required | Limitation on the quantity of source data returned. |

### Response

```javascript
{
    "Sources": [
        {
            "Id": "bbe29c21-401a-4746-b97d-af1f00e1bb8b",
            "Name": "Booking.com",
            "Type": "OnlineTravelAgency"
        },
        {
            "Id": "22e42a59-b321-43f8-a5d1-af1f00e1bb8b",
            "Name": "Hostelworld",
            "Type": "OnlineTravelAgency"
        },
        {
            "Id": "b5a55d41-bbc5-48d0-a01b-af1f00e1bb8b",
            "Name": "SynXis",
            "Type": "OnlineTravelAgency"
        }
    ],
    "Cursor": "b5a55d41-bbc5-48d0-a01b-af1f00e1bb8b"
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Sources` | array of [Source](#source) | required | The reservation sources. |
| `Cursor` | string | required | Unique identifier of the last and hence oldest source returned. This can be used in [Limitation](../guidelines/pagination.md#limitation) in a subsequent request to fetch the next batch of older sources. |

#### Source

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the source. |
| `Name` | string | required | Name of the source. |
| `Type` | string [Source type](#source-type) | required | Type of the source. |


#### Source type

* `OnlineTravelAgency`
* `CentralReservationSystem`
* `GlobalDistributionSystem`
* `AlternativeDistributionSystem`
* `SalesAndCateringSystem`
* `PropertyManagementSystem`
* `TourOperatorSystem`
* `OnlineBookingEngine`
* `Kiosk`
* `Agent`
* ...