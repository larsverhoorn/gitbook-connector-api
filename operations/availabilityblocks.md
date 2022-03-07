# Availability blocks

## Get all availability blocks

> This feature is being actively developed, features and behavior of this operation may change at short notice.

Returns all availability blocks filtered by services, unique identifiers and other filters.

### Request

`[PlatformAddress]/api/connector/v1/availabilityBlocks/getAll`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "AvailabilityBlockIds": [
        "aaaa654a4a94-4f96-9efc-86da-bd26d8db"
    ],
    "ServiceIds": [
        "bd26d8db-86da-4f96-9efc-e5a4654a4a94"
    ],
    "CreatedUtc" : {
        "StartUtc": "2020-11-04T00:00:00Z",
        "EndUtc": "2020-11-05T00:00:00Z"
    },
    "UpdatedUtc" : {
        "StartUtc": "2020-11-04T00:00:00Z",
        "EndUtc": "2020-11-05T00:00:00Z"
    },
    "CollidingUtc" : {
        "StartUtc": "2020-11-05T00:00:00Z",
        "EndUtc": "2020-11-05T00:00:00Z"
    },
    "States": [
        "Confirmed"
    ],
    "ExternalIdentifiers": [
        "Block-0001"
    ],
    "Extent": {
        "AvailabilityBlocks": true,
        "Adjustments": true,
        "ServiceOrders": false
    }
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `AvailabilityBlockIds` | string | optional, max 1000 items | Unique identifiers of the requested [Availability blocks](#availability-block). |
| `ServiceIds` | string | optional, max 1000 items | Unique identifiers of the [Services](services.md#service) to which [Availability blocks](#availability-block) are assigned. |
| `CreatedUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval in which the [Availability blocks](#availability-block) were created. |
| `UpdatedUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval in which the [Availability blocks](#availability-block) were updated. |
| `CollidingUtc` | [Time interval](#time-interval) | optional, max length 3 months | Interval in which the [Availability blocks](#availability-block) are active. |
| `States` | array of string [Availability block state](#availability-block-state) | optional | States the availability blocks should be in. |
| `ExternalIdentifiers` | string | optional, max 1000 items | Identifiers of [Availability block](#availability-block)s from external systems. |
| `Extent` | [Availability block extent](#availability-block-extent) | required | Extent of data to be returned. E.g. it is possible to specify that related service orders (for example [Reservations](reservations.md#reservation)) are returned. |

#### Time interval

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |

#### Availability block state

* `Confirmed` - The block deducts availability and can have reservations assigned.
* `Optional` - The block deducts availability and cannot have reservations assigned.
* `Inquired` - The block does not deduct availability and cannot have reservations assigned \(waitlist\).
* `Released` - The block deducts availability, but only for reservations assigned to the block before release. Remaining availability is returned back to general availability \(waitlist\).
* `Canceled` - The block does not deduct availability and cannot have reservations assigned \(waitlist\). 

#### Availability block extent

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AvailabilityBlocks` | bool | optional | Whether the response should contain the general availability blocks. |
| `Adjustments` | bool | optional | Whether the response should contain individual availability adjustments related to availability blocks. |
| `ServiceOrders` | bool | optional | Whether the response should contain reservations related to availability blocks. |

### Response

```javascript
{
    "AvailabilityBlocks": [
        {
            "Id": "aaaa654a4a94-4f96-9efc-86da-bd26d8db",
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "RateId": "ed4b660b-19d0-434b-9360-a4de2ea42eda",
            "VoucherId": null,
            "BookerId": null,
            "Budget": {
                "Currency": "USD",
                "Value": 48.0
            },
            "State": "Confirmed",
            "ReservationPurpose": "Leisure",
            "CreatedUtc": "2021-10-11T13:32:32Z",
            "UpdatedUtc": "2021-10-11T13:32:32Z",
            "StartUtc": "2021-10-14T00:00:00Z",
            "EndUtc": "2021-10-17T00:00:00Z",
            "ReleasedUtc": "2021-10-13T00:00:00Z",
            "ExternalIdentifier": "Block-0001"
            "Name": "Wedding group",
            "Notes": "Have a nice stay"
        }
    ],
    "ServiceOrders": [
        {
            "Id": "5281b551-bd90-4def-b211-acbd00d3ac8c",
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "GroupId": "edad92db-0b60-4b91-a090-acbd00d3ac75",
            "Number": "61",
            "ChannelNumber": "68845CDD-1340-49B5-9071-ACBD00B1D091",
            "ChannelManagerNumber": null,
            "ChannelManagerGroupNumber": null,
            "ChannelManager": null,
            "State": "Confirmed",
            "Origin": "Connector",
            "CreatedUtc": "2020-11-05T12:50:40Z",
            "UpdatedUtc": "2020-11-06T07:59:19Z",
            "CancelledUtc": null,
            "StartUtc": "2020-11-05T00:00:00Z",
            "EndUtc": "2020-11-06T00:00:00Z",
            "ReleasedUtc": null,
            "RequestedCategoryId": "1268c440-21c5-415d-bf58-ac87008b2bda",
            "AssignedResourceId": "f97a6b96-b17f-421f-9b97-ac87008b3324",
            "AssignedResourceLocked": false,
            "BusinessSegmentId": null,
            "CompanyId": null,
            "TravelAgencyId": null,
            "AvailabilityBlockId": "aaaa654a4a94-4f96-9efc-86da-bd26d8db",
            "RateId": "ed4b660b-19d0-434b-9360-a4de2ea42eda",
            "VoucherId": null,
            "AdultCount": 2,
            "ChildCount": 0,
            "CustomerId": "c2730cbc-53ca-440d-8b30-ac87008b30af",
            "CompanionIds": []
        }
    ],
    "Adjustments": [
        {
            "AvailabilityBlockId": "aaaa654a4a94-4f96-9efc-86da-bd26d8db",
            "ResourceCategoryId": "1268c440-21c5-415d-bf58-ac87008b2bda",
            "StartUtc": "2020-11-05T23:00:00Z",
            "EndUtc": "2020-11-06T23:00:00Z",
            "UnitCount": 6
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AvailabilityBlocks` | array of [Availability block](#availability-block) | optional | Availability blocks. |
| `ServiceOrders` | array of [Reservation](reservations.md#reservation) | optional | Service orders (for example [Reservations](reservations.md#reservation)) linked to availability blocks. |
| `Adjustments` | array of [Availability block adjustment](#availability-block-adjustment) | optional | Availability adjustments of availability blocks. |

#### Availability block

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `Id` | string | required | Unique identifier of the availability block. |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service) the block is assigned to. |
| `RateId` | string | required | Unique identifier of the [Rate](rates.md#rate) the block is assigned to. |
| `VoucherId` | string | optional | Unique identifier of the [Voucher](vouchers.md#voucher) used to access specified private [Rate](rates.md#rate). |
| `BookerId` | string | optional | Unique identifier of the [Customer](customers.md#customer) on whose behalf the block was made. |
| `Budget` | [Currency value](accountingitems.md#currency-value) | optional | The tentative budget for the total price of reservations in the block. |
| `State` | string [Availability block state](#availability-block-state) | required | State of the availability block. |
| `ReservationPurpose` | string [Reservation purpose](reservations.md#reservation-purpose) | optional | The purpose of the block. |
| `CreatedUtc` | string | required | Creation date and time of the block in UTC timezone in ISO 8601 format. |
| `UpdatedUtc` | string | required | Last update date and time of the block in UTC timezone in ISO 8601 format. |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |
| `ReleasedUtc` | string | required | The moment when the block and its availability is released in UTC timezone in ISO 8601 format. |
| `ExternalIdentifier` | string | optional, max 255 characters | Identifier of the block from external system. |
| `Name` | string | optional | The name of the block in Mews. |
| `Notes` | string | optional | Additional notes of the block. |

#### Availability block adjustment

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AvailabilityBlockId` | string | required | Unique identifier of the [Availability block](#availability-block) whose availability is updated. |
| `ResourceCategoryId` | string | required | Unique identifier of the [Resource category](resources.md#resource-category) whose availability is updated. |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |
| `UnitCount` | string | required | Adjustment value applied on the interval. |

## Add availability blocks

> This feature is being actively developed, features and behavior of this operation might change on short notice.

Adds availability blocks which are used to group related [Availability updates](#availability-update). This makes limiting public availability easier and more organized.

### Request

`[PlatformAddress]/api/connector/v1/availabilityBlocks/add`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "AvailabilityBlocks": [
        {
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "RateId": "ed4b660b-19d0-434b-9360-a4de2ea42eda",
            "VoucherCode": null,
            "Name": "Mr. Smith's block",
            "StartUtc": "2020-11-05T00:00:00Z",
            "EndUtc": "2020-11-06T00:00:00Z",
            "ReleasedUtc": "2020-11-04T00:00:00Z",
            "ExternalIdentifier": "Block-0001",
            "Budget": {  
               "Value": 500,
               "Currency": "EUR"
            },
            "ReservationPurpose": null,
            "Notes": null,
            "State": "Confirmed"
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `AvailabilityBlocks` | array of [Availability block parameters](#availability-block-parameters) | required, max 1000 items | Availability blocks to be added. |

#### Availability block parameters

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ServiceId` | string | required | Unique identifier of the [Service](services.md#service) to assign block to. |
| `RateId` | string | required | Unique identifier of the [Rate](rates.md#rate) to assign block to. |
| `VoucherCode` | string | optional | Voucher code providing access to specified private [Rate](rates.md#rate). |
| `Name` | string | optional | The name of the block. |
| `StartUtc` | string | required | Start of the interval in UTC timezone in ISO 8601 format. |
| `EndUtc` | string | required | End of the interval in UTC timezone in ISO 8601 format. |
| `ReleasedUtc` | string | required | The moment when the block and its availability is released. |
| `ExternalIdentifier` | string | optional, max 255 characters | Identifier of the block from external system. |
| `Budget` | [Currency value](accountingitems.md#currency-value) | optional | The tentative budget for the total price of reservations. |
| `ReservationPurpose` | string [Reservation purpose](reservations.md#reservation-purpose) | optional | The purpose of the block. |
| `Notes` | string | optional | Additional notes of the block. |
| `State` | string [Availability block state](#availability-block-state) | required | State of the availability block. |

### Response

```javascript
{
    "AvailabilityBlocks": [
        {
            "Id": "aaaa654a4a94-4f96-9efc-86da-bd26d8db",
            "ServiceId": "bd26d8db-86da-4f96-9efc-e5a4654a4a94",
            "RateId": "ed4b660b-19d0-434b-9360-a4de2ea42eda",
            "StartUtc": "2020-11-05T00:00:00Z",
            "EndUtc": "2020-11-06T00:00:00Z",
            "ReleasedUtc": "2020-11-04T00:00:00Z",
            "ExternalIdentifier": "Block-0001"
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AvailabilityBlocks` | array of [Availability block](#availability-block) | required | Availability blocks. |

### Reservation purpose

* Leisure
* Business
* Student

## Update availability blocks

> This feature is being actively developed, features and behavior of this operation might change on short notice.

Updates information about the specified [Availability block](#availability-block).

### Request

`[PlatformAddress]/api/connector/v1/availabilityBlocks/update`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "AvailabilityBlocks": [
        {
            "AvailabilityBlockId": "aaaa654a4a94-4f96-9efc-86da-bd26d8db",
            "Name": {"Value": "Mr. John Snow block"},
            "StartUtc":{"Value": "2021-07-05T00:00:00Z"},
            "EndUtc":{"Value": "2021-07-15T00:00:00Z"},
            "ReleasedUtc":{"Value": "2021-07-04T00:00:00Z"},
            "ExternalIdentifier": {"Value": "123456798"}
        }
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `AvailabilityBlocks` | array of [Availability block update parameters](#availability-block-update-parameters) | required, max 1000 items | Availability blocks to be updated. |

#### Availability block update parameters

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `AvailabilityBlockId` | string | required | Unique identifier of the [Availability block](#availability-block). |
| `Name` | [String update value](#string-update-value) | optional | The name of the block \(or `null` if the name should not be updated\). |
| `StartUtc` | [String update value](#string-update-value) | required | Start of the interval in UTC timezone in ISO 8601 format \(or `null` if the start time should not be updated\). |
| `EndUtc` | [String update value](#string-update-value) | required | End of the interval in UTC timezone in ISO 8601 format \(or `null` if the end time should not be updated\). |
| `ReleasedUtc` | [String update value](#string-update-value) | required | The moment when the block and its availability is released \(or `null` if the released time should not be updated\). |
| `ExternalIdentifier` | [String update value](#string-update-value) | optional, max 255 characters | Identifier of the block from external system \(or `null` if the identifier should not be updated\). |

#### String update value

| Property | Type | Contract | Description |
| --- | --- | --- | --- |
| `Value` | string | optional | Value which is to be updated. |

### Response

```javascript
{}
```

## Delete availability blocks

Delete availability blocks. Note that an availability block containing active reservations (reservations which are not `Canceled`) cannot be deleted.

### Request

`[PlatformAddress]/api/connector/v1/availabilityBlocks/delete`

```javascript
{
    "ClientToken": "E0D439EE522F44368DC78E1BFB03710C-D24FB11DBE31D4621C4817E028D9E1D",
    "AccessToken": "C66EF7B239D24632943D115EDE9CB810-EA00F8FD8294692C940F6B5A8F9453D",
    "Client": "Sample Client 1.0.0",
    "AvailabilityBlockIds": [
        "e5a4654a4a94-86da-4f96-9efc-bd26d8db",
        "aaaa654a4a94-4f96-9efc-86da-bd26d8db"
    ]
}
```

| Property | Type | Contract | Description |
| :-- | :-- | :-- | :-- |
| `ClientToken` | string | required | Token identifying the client application. |
| `AccessToken` | string | required | Access token of the client application. |
| `Client` | string | required | Name and version of the client application. |
| `AvailabilityBlockIds` | array of string | required, max 1000 items | Unique identifier of the Availability block to delete. |

### Response

```javascript
{}
```