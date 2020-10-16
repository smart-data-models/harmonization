# Sea Port

- required:
	- location
	- dateLastReported
	- typeOfPort
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description
The Data Model is intended to provide information about ports that can accommodate pleasure craft, commerce or passenger  transport.
It permit to represent the parameters of each port, its location, its mooring capacities and the free or paid services associated with it provided directly by the port or by professionals working on or near the port. 

*Additional Information about this Data Model :*
The following Datamodel can be used with the following data Model.
	- **BoatAuthorized** to provide by Type, SubType of boats if they are authorized to circulate and moor within the port.
	- **BoatPlaceAvailable** to provide the number of places available in the port at a given time regarding the category of the boat.
	- **BoatPlacePricing** to provide information about the price of a place in the port regarding the category of the boat.
	- **ObjectFlowObserved** to provide the number of inbound and outbound boats by Type according to a period or at a given time.

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
		- value: "SeaPort"

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
		- description: > Name given to the Repository.
		- type: "string"
	- alternateName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/alternateName"
		- description: > Alternative Name given to the Repository
		- type: "string"
	- description:
		- x-ngsi:
			- type: "Property"
			- model: "https://uri.etsi.org/ngsi-ld/description", "https://schema.org/description"
		- description: > Description of the Repository.
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

	### Information about the date of last reporting

	- dateLastReported:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > A timestamps which denotes the last time when a flow successfully reported data. The date and time of this Repository in ISO8601 UTCformat.
		- type: "string"
		- format: "date-time"

	### Information about a reference to other Data Models .

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
		- description: > Reference to a [PointOfInterest](https://github.com/smart-data-models/dataModel.PointOfInterest/blob/master/PointOfInterest/doc/spec.md) linked with the Repository.  
		- type: "string"
			- format: "URL"

	### Link to the others Data Model included SeaPort as Search Key  

	- refBoatAuthorized : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a list of [Entity](https://github.com/smart-data-models/dataModel.Port/blob/master/BoatAuthorized/doc/spec.md).  
		- type: "array"
			- format: "URL"
	- refBoatPlaceAvailable : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a list of [Entity](https://github.com/smart-data-models/dataModel.Port/blob/master/BoatPlaceAvailable/doc/spec.md).  
		- type: "array"
			- format: "URL"
	- refBoatPlacePricing : 
		- x-ngsi:
			- type: "Relationship"
			- model: "https://schema.org/URL"
		- description: > Reference to a list of [Entity](https://github.com/smart-data-models/dataModel.Port/blob/master/BoatPlacePricing/doc/spec.md).  
		- type: "array"
			- format: "URL"

	### Information related to the owner 

	- owner:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text" included references to "http://schema.org/Person", "https://schema.org/Organization", "https://schema.org/URL".
		- description: > The owners of the Device. A list of [Text], [Person], [Organisation] or [URLs].
		- type: "array"
			- items:
				- type: string
	- contractingAuthority : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Name of the contracting authority. 
		- type: "string"    

	### Information related to the manager by delegation and contact point on the harbor

	- contractingCompany : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > The Contracting Compagny responsible of the management of the port.
		- type: "string"	
	- contactPoint:
		- x-ngsi:
			- type: "Property"
			- model: [Contact Point](https://schema.org/ContactPoint)
		- description: > Contact Point for the harbor.
		- type: "string"
	- webSite:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Link to the official website of the harbor for more information..
		- type: "string"    

	### Information detailing port constraints for all type of boats. 

	- typeOfPort:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Type of harbor. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- marina, merchandise, cruise, ferry, passengers, yatching , fishing, military, river, other 
	- authorizedPropulsions:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Type of propulsions authorized to enter in the harbor. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- motor, sail, electric, oar, nuclear, lng, lpg, other 
	- maxTonnage:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum tonnage authorized to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **TNE** represents Tonne Metric.
		- type: "number"
	- numberOfPlace:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Total number of place in the harbor..
		- type: "number"
	- minLength:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Minimum length allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxLength:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum length allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxWidth:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum width allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"
	- maxDraft:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Maximum draft allowed to access the harbor. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **MTR** represents Meter.
		- type: "number"

	### Information about the general Opening Hours specification.

	- openingHoursSpecification : 
		- x-ngsi:
			- type: "Property"
			- model: http://schema.org/openingHoursSpecification
		- description: > General Opening hours specification. 
		- type: "string"

	### Information detailing the services offered by the harbor or professionals working on or near

	- portServicesProvided:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Description of the services provided directly by the harbor. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- harborOffice, weather, customsServices, porters, boatRingRental, mooringAssistance, handlingAssistance, publicWifi, privateWifi, other
	- boatSupplyingServices:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Description of the complementary supplying services for the boat offered by professionals working on or near the harbor. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- guarding, fuelStation, fuelTankerTruck , drinkingWater, TankerTruck, provisioning, dryFairing, waterFairing, repair, expertise, gangways, liftingCranes, towing, wasteWaterPumping, boatConveying, boatTransfer, other
	- facilities:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Description of the proposed facilities on the harbor. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- toilets, showers, laundry, telephone, dustbins, dumpsters, container, selectiveSortingWaste, electricTerminal, waterTerminal, indoorRoomReservation, other
	- nearbyServices:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Description of the additional services on the geographical area on or near the harbor. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- touristOffice, fittingsStores, travelAgency, exchangeOffice, medicalOffice, pharmacy, groceryStores, restaurants, presses, bar, shops, seaExcursions, cityTour, touristicExcursions, other
	- rentalSaleServices:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Description of services provided by professional sales or rental agencies on the geographical area on or near the harbor. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- boatRental, boatSale, jetSkiRental, jetSkiSale, carRental, luxuaryCarRental, vanRental, bikeRental, scooterRental, Caddie, palletTransport, other
	- transportServices:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Description of the services provided for dedicated transport and shuttle services. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- parking, shuttlesToAirport, shuttlesToRailway, internalShuttles, taxis, heliport, other
	- routeType:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > List of the different types of urban transport Mode (Metro, Bus, Tram, ...) from the urban transport Mode GFTS standard [STOP](https://developers.google.com/transit/gtfs/reference/#stopstxt). A combination of values composed only of the attribute 'description'.
		- type: "array"
			- items:
				- type: string
				- enum : tram(0), metro(1), train(2), bus(3), ferry(4), cableTram(5), cableCar(6), funicular(7), trolleybus(11), monorail(12)
	- electricTransport:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > List of the different types of electric transport proposed by the city. A combination of :
		- type: "array"
			- items:
				- type: string
				- enum :  
					- electricCar, electricBycicle, electricMotorBike, electricScooter 

	### Information related to the means of payment for services provided by the port 

	- paymentAccepted:
		- x-ngsi:
			- type: "Property"
			- model: [Payment Accepted](https://schema.org/paymentAccepted)
		- description: > Accepted payment. A combination of a list of active codes defined in the model :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- Cash, CreditCard, CryptoCurrency, other 
	- currencyAccepted:
		- x-ngsi:
			- type: "Property"
			- model: [Currencies Accepted](https://schema.org/currenciesAccepted), [Norme ISO 4217](http://en.wikipedia.org/wiki/ISO_4217), [Crypto Currencies](https://en.wikipedia.org/wiki/List_of_cryptocurrencies) , [Exchange Trading System](https://en.wikipedia.org/wiki/Local_exchange_trading_system)
		- description: > Currency accepted for payment. A combination of a list of active codes defined in the model :
		- type: "array"
			- items:
				- type: string
				- enum : 
					- EUR, USD, GBP, CHF, Bitcoin, Neo, ...