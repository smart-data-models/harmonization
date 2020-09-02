# **Photo-voltaic Device**

- required:
	- location
	- dateLastReported
- type: "object"
  - allOf:
  	- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
  	- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The Data Model is intended to describe the mechanical, electrical and thermal characteristics of photo-voltaic panels according to : 
	- *STC - Standard Test Condition*
		- Sunshine 1000 Wm² / Radiation 1.5 AM / Temp 25° Celsius / Air Masse 0 m/s. 
	- *NOCT - Normal Operating Cell Temperature*  
		- Sunshine 800 Wm² / Radiation 1.5 AM / Temp 20° Celsius / Air Masse 1 m/s.

The measures performed for STC and NOCT are 
	- [Pmax]	Maximum Nominal Power measured in **WTT** represents Watt..
	- [Umpp]	Optimal operating voltage measured in **VLT** represents Volt.
	- [Impp]	Optimal Operating Current measured in **AMP** represents Ampere.
	- [Uoc]		Open Circuit Voltage measured in **VLT** represents Volt.
	- [Isc]		Short Circuit Current measured in **AMP** represents Ampere.

*Additional Information about Data Model:*
This Data Model can be used directly as a main entity to describe the device [PHOTOVOLTAIC] or as a sub-entity of the Data Model [DEVICE] using a reference by the `refDevice` attribute. 

## Data Model

- properties:

	### Common parameters for data identification.

	- id:
		- x-ngsi:
			- type: "Property"
			- type : "string"
		- Description: "mandatory element for NGSI"
		- format: "uri"
	- type:
		- x-ngsi:
			- type: "Property"
		- Description: "Entity type, mandatory element for NGSI"
		- type : "string"
		- value: "PhotovoltaicDevice"
	- dataProvider:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/URL"
		- description: > Specifies the URL to information about the provider of this information
		- type: "string"
			- format: "URL"
	- source:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > A sequence of characters giving the source of the entity data.
		- type: "string"
	- name:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/name"
		- description: > Name given to the observation.
		- type: "string"
	- alternateName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/alternateName"
		- description: > Alternative Name given to the observation
		- type: "string"
	- description:
		- x-ngsi:
			- type: "Property"
			- model: "https://uri.etsi.org/ngsi-ld/description", "https://schema.org/description"
		- description: > Description of the observation.
		- $ref: 'https://jason-fox.github.io/swagger-datamodel-test/common.yaml#/Description'
	- seeAlso:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > Text or Link that can provide additional information.
		- type: "string"

	### Information about Location and Address.

	- location
		- x-ngsi:
			- type: type: "Geo Property".
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Geometry"
		- description: > Location represented by a GeoJSon geometry [Point, LineString, Polygon, MultiPoint, MultiLineString, MultiPolygon]
	- address:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/address"
		- description: > Civic Address
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Address"
	- areaServed:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Zone of level higher to the attributes Location & Address to gather and cross information (ex district, etc)
		- type: "string"

	### Information related to the date of last reporting

	- dateLastReported:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > A timestamps which denotes the last time when the device successfully reported data. Date and time in an ISO8601 UTCformat.
		- type: "string"
			- format: "date-time"

	### Information about a reference to other Data Models.

	- refDevice : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to the Main Entity [Device](https://github.com/smart-data-models/dataModel.Device/blob/master/Device/doc/spec.md) if used as second link.  
		- type: "string"
			- format: "URL"
	- refPointOfInterest : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the observation.  
		- type: "string"
			- format: "URL"

	### Information related to the model 

	- brandname:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/brand"
		- description: > Brand Name.
		- type: "string"
	- modelName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/model"
		- description: > Model Name.
		- type: "string"
	- manufacturerName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/manufacturer"
		- description: > Manufacturer Name.
		- type: "string"
	- serialNumber:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/serialNumber",
		- description: > List of serial numbers of Photo-voltaic device supplied by the manufacturer and assembled in operating mode on a single location.
		- type: "number"
	- application:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Target application regarding the Type of Solar panel (In our case `electric`). A unique value of :
		- type: "string"
		- enum : 
			- electric, thermal, other
	- typeOfUse :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Accepted use regarding its positioning in an indoor / outdoor environment. A unique value of :
		- type: "string"
		- enum : 
			- indoor, outdoor, mixed, other
	- instalationMode:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Positioning of the device in relation to a ground reference system. A unique value of :
		- type: "string"
		- enum : 
			- ground, wall, pole, roofing, other
	- instalationCondition:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Condition and possibility of use in the following environments. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- extremeHeat, extremeCold, extremeHumidity, extremeClimate, desert, sand, marine, saline, dust, seismic, other
	- possibilityOfUse:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Possibility of use. A unique value of :
		- type: "string"
		- enum : 
			- stationary, mobile, mixed, other
	- documentation:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > Technical Documentation (Installation / maintenance / used).
		- type: "string"
	- owner:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text" included references to "http://schema.org/Person", "https://schema.org/Organization", "https://schema.org/URL".
		- description: > The owners of the Device. A list of [Text], [Person], [Organisation] or [URLs].
		- type: "array"
			- items:
				- type: string

	### Information related to type of Panel

	- cellType:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text".
		- description: > Type of cells used to built the photo-voltaic unit. 2 kinds of Technologies *`Cristalline`* or  *`Thin layers`*. A unique value of :
		- type: "string"
		- enum : 
			- monocrystalline, polycrystalline, amorphousSilicon, CIS, CfTe, other
	- integrationMode:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text".
		- description: > Method of integrating the panels on a support. A unique value of :
		- type: "string"
		- enum : 
			- IAB, ISB, overlay, other

	### Information about Mechanical Data for a Solar Panel

	- cellDimension : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > External dimension of a cell. The format is structured by a sub-property of 3 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **MMT** represents Millimeter.
		- type: "number"
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items:
				- length
				- width
				- thickness
	- moduleDimension : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > External dimension of a module. A module can be an assembly of 1 to n cells. The format is structured by a sub-property of 3 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **MMT** represents Millimeter.
		- type: "number"
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items:
				- length
				- width
				- thickness	
	- moduleNbCells:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Number of `cells` per `module`.
		- type: "number"
	- panelDimension : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > External dimension of a Panel. A solar panel can be an assembly of 1 to n modules, which themselves are made of several cells which collect heat from the sun's rays. The format is structured by a sub-property of 3 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **MMT** represents Millimeter.
		- type: "number"
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items:
				- length
				- width
				- thickness
	- PanelNbModules:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Number of `Modules` per `Panel`. 
		- type: "number"
	- panelWeight:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Weight of a panel (Sometime the reference used is Kg / m²). The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **KGM** represents Kilogram.
		- type: "number"
	- areaWeight:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Area Weight measured in Kg/m². The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **28** represents Kilogram per square meter.
		- type: "number"

	### Information about Security Classification

	- applicationClass : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Evaluation of the potential hazards associated with the module. A unique value of :
		- type: "string"
		- enum : 
			- A, B, C
	- fireClass : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Evaluation to the fire (IEC 61730). A unique value of :
		- type: "string"
		- enum : 
			- A, B, C
	- protectionIP :   
		- x-ngsi:
			- type: "Property"
			- model: [IP_Code/EN 60529](https://en.wikipedia.org/wiki/IP_Code),
		- description: > IP "*Ingress Protection*" for the Junction Box. This is the level classifies and rates the degree of protection provided by mechanical casings and electrical enclosures against intrusion, dust, accidental contact, and water according to International Electrotechnical Commission standard (EN 60-529).
			- First digit: Solid particle protection (Single numeral: 0–6 or "X"). 
			- Second digit: Liquid ingress protection (Single numeral: 0–9 or "X" ).
			- Third digit: Personal Protection  against access to dangerous parts (optional additional letter).
			- Fourth digit: Other protections (optional additional letter).
		- type: "string"
	- pTCClass :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > The Positive Temperature Coefficient of resistance - *PTC*, describes the relative change of a physical property that is associated with a given change in positive temperature. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "number"
	- nTCClass :  
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > The Negative Temperature Coefficient of resistance - *NTC*, describes the relative change of a physical property that is associated with a given change in negative temperature. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "number"
	- MaxPressureLoad :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Maximum mechanics Pressure (shear, elasticity, compression) load on a Panel. The format is structured by a sub-property of 3 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **PAL** represents Pascal.
		- type: "number"
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items:
				- hail
				- snow
				- wind

	### Information about Temperatures Characteristics

	- panelOperatingTemperature : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Ambient operating temperature range. This is the minimum and maximum resistance to cold and heat for using the panel. The format is structured by a sub-property of 2 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- min
				- max

	- cellOperatingTemperature : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > This is the nominal operating temperature range of the cells in which it collects solar energy. The format is structured by a sub-property of 2 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **CEL** represents Degree Celsius.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- temp
				- variationMax

	- TemperatureCoefficient : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Temperature influence coefficient on the panel. The format is structured by a sub-property of 3 items. 
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- Pmax in Watt
				- Uoc in Volt
				- Isc in Ampere

	### Information about to the Nominal Value

	- NominalPower:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Nominal Power for the **panel**. This is the same value of items [Pmax] for [moduleSTC] attribute. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **WTT** represents Watt.
		- type: "number"

	- MaximumSystemVoltage:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Maximum system voltage permitted for the **module**. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **VLT** represents Volt.
		- type: "number"

	### Information about Electric Data *STC - NOCT* for a module

	- moduleSTC : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Standard Test Condition measurements. The format is structured by a sub-property of 5 items. 
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- Pmax in Watt
				- Umpp in Volt
				- Impp in Ampere
				- Uoc in Volt
				- Isc in Ampere

	- moduleNOCT : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Normal Operating Cell Temperature measurements. The format is structured by a sub-property of 5 items.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- Pmax in Watt
				- Umpp in Volt
				- Impp in Ampere
				- Uoc in Volt
				- Isc in Ampere

	- moduleYieldRate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Average Yield Rate based on the [NominalPower]. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "number"

	### Information about Performance at Low Irradiance 

	- performanceLowIrradiance:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Average relative yield to Performance at Low Irradiance. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "number"

	### Information about Panel Life Cycle and Energy Production 

	- panelLifetime:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Average lifetime of a panel. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **ANN** represents Year.
		- type: "number"

	- panelYieldCurve:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Option 1 - Energy production yield curve of the panel from its [NominalPower] at [T0] and along its [panelLifetime]. The Measurements provided in the list are a sequence of *Energy Production Capacity* represented in *Percent* starting at *5 years* with a *Step* of *5 years* according to the information provided by the manufacturer. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "number"
		- type: "array"
			- items:
				- type: string

	- panelYieldRate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Option 2 - Panel energy loss rate per year from its [NominalPower] at `T0` and along its  [panelLifetime] according to the information provided by the manufacturer. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **P1** represents Percent.
		- type: "number"

	- panelTiltReference : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number",
		- description: > Panel tilt reference limit for best performance. The format is structured by a sub-property of 2 items. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes). For instance, **DD** represents Degree Unit of Angle.
		- type: [StructuredValue](http://schema.org/StructuredValue)
			- type: string
			- items :
				- min
				- max

