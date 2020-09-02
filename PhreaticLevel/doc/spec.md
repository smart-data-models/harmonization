## Phreatic Observed 

**Note: The latest version of this Data Model can be found at
[https://github.com/smart-data-models/dataModel.Environment](https://github.com/smart-data-models/dataModel.Environment)**

## Description
Phreatic Data Model is intended to measure, observe and control the level and quality of groundwater at a given time (T), by a fixed or mobile monitoring system.
Depending on the device used, it is also possible to measure the quality of water such as its electrical conductivity, its salt content, its temperature, etc. 
In this case, the values measured  are processed by the Data Model `WaterObserved` and  `WaterQualityObserved`. 

*Additional Information about Attributes :*

For attributes dedicated to water, a Meta Data attribute can also be used. it contains the `TimeStamp` in seconds, the `qualification`  (Correct, Incorrect) and control `status` (Level from 1 to n) of the measurement .

## Data Model

A JSON Schema corresponding to this data model can be found [here](http://fiware.github.io/data-models/specs/Environment/PhreaticObserved /schema.json).

### Common Water Phreatic parameters identification data

- `id` : Unique identifier.

- `type` : Entity type. It must be equal to `PhreaticObserved`.

- `dataProvider` : Specifies the URL to information about the provider of this information.
    - Attribute type: Property. [URL](https://schema.org/URL)
    - Optional
    
- `dateCreated` : Entity's creation time stamp.
    - Attribute type: Property. [DateTime](https://schema.org/DateTime)
    - Read-Only. Automatically generated.

- `dateModified` : Last update time stamp of this entity.
    - Attribute type: Property. [DateTime](https://schema.org/DateTime)
    - Read-Only. Automatically generated.

- `source` : A sequence of characters giving the source of the entity data.
    -   Attribute type: Property. [Text](https://schema.org/Text) or [URL](https://schema.org/URL)
    - Optional
    
- `name` : Name given to the Observation.
    - Attribute type: Property. [Text](https://schema.org/Text) 
    - Normative References: [https://schema.org/name](https://schema.org/name)
    - Optional
    
- `alternateName` : Alternative Name given to the Observation.
    - Attribute type: Property. [Text](https://schema.org/Text) 
    - Normative References: [https://schema.org/alternateName](https://schema.org/alternateName)
    - Optional
    
- `description` : Description given to the Observation.
    -   Attribute type: Property. [Text](https://schema.org/Text) 
    -   Normative References: [https://schema.org/description](https://schema.org/description)
    -   Optional
    
- `seeAlso` : Text  Link can provide additional information.
    - Attribute type: Property. [Text](https://schema.org/Text) or [URL](https://schema.org/URL)
    - Optional

### Information related to the location of the observation

- `location` : Location represented by a GeoJSON Point.
    - Attribute type: Geo Property. `geo:json`.
    - Normative References: [https://tools.ietf.org/html/draft-ietf-geojson-03](https://tools.ietf.org/html/draft-ietf-geojson-03) 
    - Mandatory if `address` is not present.
    
- `address`: Civic address of the observation.
    - Attribute type: Property. [Address](https://schema.org/address)
    - Normative References: [https://schema.org/address](https://schema.org/address)
    - Mandatory if `location` is not present.
    
- `areaServed`: Zone of level higher to the attributes `Location` & `Address` to gather and cross information (ex district, etc).
    - Attribute type: Property. List of [Text](https://schema.org/Text)
    - Normative References: [https://schema.org/areaServed](https://schema.org/areaServed)
    - Optional

### Information related to the date of the observation

- `dateObserved` : The date and time of this observation in ISO8601 UTCformat.
    - Attribute type: Property. [DateTime](https://schema.org/DateTime) or an ISO8601 interval represented as [Text](https://schema.org/Text).
    - Mandatory

- `dateObservedFrom` : Observation period : Start date and time in an ISO8601 UTCformat.
    - Attribute type: Property. [DateTime](https://schema.org/DateTime) 
    - Mandatory if `dateObserved` is not present

- `dateObservedTo` : Observation period : End date and time in an ISO8601 UTCformat.
    - Attribute type: Property. [DateTime](https://schema.org/DateTime) 
    - Mandatory if `dateObserved` is not present

### Information related to a reference to another DataModel

- `refDevice` : A reference to the device which captured this observation.
    - Attribute type: Relationship. Reference to an entity of type `Device`
    - Optional

### Information related to the condition of the measure 

- `isMobile` : The device used is Fixed (False) or Mobile (True).
    - Attribute type: Property. [Boolean](https://schema.org/Boolean)
    - Optional
    
- `measurementType` : Type of measurement processed.
    - Attribute type: Property. List of [Text](http://schema.org/Text)
   - Allowed values : (`depth`, `volume`, `quality`).
   - Optional

### Information related to the water measures 

- `investigationDepth ` : Maximum depth where the investigation was made.
  - Attribute type: Property. [Number](http://schema.org/Number)
    - Default unit: The unit code (text) of measurement given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) (max. 3 characters). For instance, <code>MTR</code> represents Meter.
   - Optional
- `waterTable` : Level at which water was found during this investigation.
   - Attribute type: Property. [Number](http://schema.org/Number)
   - Default unit: The unit code (text) of measurement given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) (max. 3 characters). For instance, <code> MTR </code> represents Meter.
   - Attribute metadata:

     -   `timestamp`: Time stamp when the last update of the attribute happened.
         -   Type: [DateTime](http://schema.org/DateTime) 

     - `qualification` : Qualification of the measurement.
         - Attribute type: Property. [Text](http://schema.org/text)
         - Allowed values : Correct, Incorrect. 
     - `status` : Control level of data collected -  Data control level 1, 2,3,...  
         - Attribute type: Property. [Text](http://schema.org/Text)
   - Optional
- `pressure` : Water Pressure.
   - Attribute type: Property. [Number](http://schema.org/Number)
   - Default unit: The unit code (text) of measurement given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) (max. 3 characters). For instance, <code> BAR </code> represents Bar.
     -   `timestamp`: Time stamp when the last update of the attribute happened.
         -   Type: [DateTime](http://schema.org/DateTime) 
     -   `qualification` : Qualification of the measurement.
         - Attribute type: Property. [Text](http://schema.org/text)
         - Allowed values : Correct, Incorrect. 
     -   `status` : Control level of data collected -  Data control level 1, 2,3,...  
         - Attribute type: Property. [Text](http://schema.org/Text)
     -   Optional
- `depth` : Depth of drinking water, since its identification `waterTable`.
   - Attribute type: Property. [Number](http://schema.org/Number)
   - Default unit: The unit code (text) of measurement given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) (max. 3 characters). For instance, <code> MTR </code> represents Meter.
     -   `timestamp`: Time stamp when the last update of the attribute happened.
         -   Type: [DateTime](http://schema.org/DateTime) 
     -   `timestamp`: Time stamp when the last update of the attribute happened.
         -   Type: [DateTime](http://schema.org/DateTime) 
     -   `qualification` : Qualification of the measurement.
         - Attribute type: Property. [Text](http://schema.org/text)
         - Allowed values : Correct, Incorrect. 
     -   `status` : Control level of data collected -  Data control level 1, 2,3,...  
         - Attribute type: Property. [Text](http://schema.org/Text)
     -   Optional

### Information related to others measures

- `pollutionRate` : Rate of pollution.
    - Attribute type: Property. [Number](http://schema.org/Number)
    - Default unit: The unit code (text) of measurement given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) (max. 3 characters). For instance, <code> P1 </code> represents Percentage.
    - Optional
-   `residueLevel` : Residue level found.
    - Attribute type: Property. [Number](http://schema.org/Number)
    - Default unit: The unit code (text) of measurement given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) (max. 3 characters). For instance, <code> M1 </code> represents milligram per liter.
    - Optional
