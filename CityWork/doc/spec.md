# **City Works**

- required: "object"
	- location
	- workDate
	- workLastDateUpdate
	- workZone
- type: "object"
	- allOf:
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/Location-Commons"
		- "$ref": "https://smart-data-models.github.io/data-models/common-schema.json#/definitions/GSMA-Commons"
- description: >

## Description

The Data Model is is a contextual description of urban works carried out on a road axis and which can impact individual (Cars, motorcycles, bicycles, .) or common transport (Tram, Bus, subway).
It contains a geographic representation making it possible to locate its work from a specific JSON Object and at a more global level (Road segment, Road, District, ...) in order to assess the potential impacts on the circulation.

*Note about the relation with other Data Model:* 
The impacts on public transport (bus, metro, tram, schoolbus, etc.), schools, cultural or sporting events are taken into account in this data model.
In order to describe each impact, a structured value from 0 to N occurrences is proposed, where each element is a string in the format: `lineImpact`: [A list of segment impact with `Free Text` or `GeoProperty` or a reference to another entity `SegmentEntity`, separated by a comma]

*Note about the GeoJSON object :* 
It may represent a region of space (a Geometry), a spatially-bounded entity (a Feature), or a list of features (a Feature Collection). refer to the document [geojson](https://tools.ietf.org/pdf/draft-ietf-geojson-03.pdf) for more information about the modelisation and the possible value.

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
		- value: "CityWork"
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
		- description: > Name given to the works / observation.
		- type: "string"
	- alternateName:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/alternateName"
		- description: > Alternative Name given to the works / observation.
		- type: "string"
	- description:
		- x-ngsi:
			- type: "Property"
			- model: "https://uri.etsi.org/ngsi-ld/description", "https://schema.org/description"
		- description: > Description of the works / observation.
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
			- type: type: "Property".
			- model: "https://tools.ietf.org/html/rfc7946".
		- description: > Location represented by a GeoJSon geometry [Point, LineString, Polygon, MultiPoint, MultiLineString, MultiPolygon]
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Geometry"
	- address:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/address"
		- description: > Adress civic of the work.
		- $ref: "https://github.com/smart-data-models/data-models/blob/master/common-schema.yaml#/Address"
	- areaServed:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Zone of level higher to the attributes `Location` & `Address` to gather and cross information (ex district, etc)
		- type: "string"
	- territorialArea:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Territorial area. Level higher to the attribute `areaServed`. A list of Free Text.
		- type: "string"

	### Information related to the date of last reporting of a flow

  - dateLastReported:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > A timestamp which denotes the last time when the device successfully reported data. The date and time of this observation in ISO8601 UTCformat.
		- type: "string"
			- format: "date-time"
	    
	### Information about the Work Number abd date of works.

	- workNumber : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Number assigned to the work. 
		- type: "string"
	- workState : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Work progress status in the case of their acceptance. A unique value of : 
		- type: "string"
			- enum :
				- pendingPlanning, planned, validatedInPlanning, pendingAuthorization, instructionInProgress, investigated, authorized, reject, open, pendingExtension, approved, nonCompliantOccupation, completed, draft, all, planningCompleted, canceled, pendingCancellation, pendingDocument, supported, editedDecrees, decreeToBeSigned, Received
	- workDate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Date and time (Day or period) of the works represented by an ISO8601 UTC format. It can be represented by an specific time instant or by an ISO8601 interval to separate attributes `startDate, endDate`.
		- type: "string"
			- format: "date-time"
	- startDate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: >  Start date and time of the works in an ISO8601 UTC format. The attribute can be used in addition to the `workDate` attribute when it corresponds to a time interval to be highlighted.
		- type: "string"
			- format: "date-time"
	- endDate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > End date and time of the works in an ISO8601 UTC format. The attribute can be used in addition to the `workDate` attribute when it corresponds to a time interval to be highlighted.
		- type: "string"
			- format: "date-time"

	### Information about the General Opening Hours specification.

	- openingHoursSpecification : 
		- x-ngsi:
			- type: "Property"
			- model: http://schema.org/openingHoursSpecification
		- description: > General Opening hours specification (dayOfWeek / opens / closes / publicHolidays). This attribute can be used to specify the authorized days and times for the works in a normal context.
		- type: "string"

	### Information related to the contracting Authority and authorization

	- contractingAuthority : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Name of the contracting authority. 
		- type: "string"
	- contactPoint:
		- x-ngsi:
			- type: "Property"
			- model: [Contact Point](https://schema.org/ContactPoint). 
		- description: > Contact Point for the contracting Authority.  
		- type: "string"
	- decrees : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text", "https://schema.org/URL"
		- description: > A List of text where each element is a string with the URL to download or the name of the decree.
		- type: "array"
			- type: "string"
	- workLastDateUpdate:
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/DateTime"
		- description: > Last date for updating a contractual element of the work.
		- type: "string"
			- format: "date-time"

	### Information related to the Contracting Company

	- mainContractingCompany : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > The Main Contracting Compagny responsible of the works.
		- type: "string"	
	- othersContractingCompany : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > A List of Text where each element is a string with the name of the contracting Companies under the responsibility of the main Contracting Company.
		- type: "array"
			- type: "string"

	### Information related to works type and its typology 

	- workLevel :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Positioning of the works in relation to a ground reference system. A combination of :
		- type: "array"
			- type: "string"
			- items :
				- enum :
					- ground, underGround, surface, aerial, wall, roofing, other
	- workTarget :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Categories of works regarding the different profession. A combination of example listed below :
		- type: "array"
			- type: "string"
			- items :
			  - enum :
			  	- roadsAndPublicDomain, roads, pavement, publicDomain, railWayTrack, tramway, busCorridor, publicTransport, bicyclePath, sideWalk, landScapedArea, infrastructure, suportStructures, riprap, streetParking, offStreetParking, cityMotorBike, cityBike, cityCar, cityScooter, electricityNetworks, gasNetworks, drinkingWater, sanitation, rainyWaters, urbanHeating, telecom-RMT-VideoNetworks, telecomNetworks, videoNetworks, rMTNetworks, opticalFibers, networks, copperCable, fireHydrants, CoringPenetrometry, publicDecorativeLighting, trafficSignalingRegulation, urbanFurniture, exploratoryWork, surfaceOccupation, historicalMonuments, frameRoof, speedReductionDevices, coldAndAirCon, generator, coldGroup, overheadLine, catainers, tagsAndPosters, papersCollection, vrd, movingHoistNacelleTruck, scaffolding, variousWorks
	- workNature : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Nature of the works. A combination of example listed below : 
		- type: "array"
			- type: string
			- items :
				- enum : 
					- construction, creation, renovation, refurbishment, survey, control, experimentation, counting, repair, renewal, extension, rehabilitation, landfill, reinforcement, consolidation, upgrading, maintenance, connection, staking, investigation, miscellaneousWorks, miscellaneousInstallation, cleaning, drivingSwitch, Installation-OR-layout, pruning, demolition, riprap, craneLifting, OverheadLinesWorksintervention, supportImplantation, additionalInvestigations, securedPerimeter, roadSign, siteInstallation, trenchOpening, ManholeOpeningToRestoreService, manholeOpening, safetyRailsInstallation, collection, pulling, MowingDeburring, filmShooting, safetyAndComplianceWork, surfaceOccupationAuthorization, brushCutting, treeCutting, tarring, replacement, tonnageExemption
	- infrastructureFunction :
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text",
		- description: > Function of the infrastructure impacted by the works. A combination of :
		- type: "array"
			- type: "string"
			- items :
				- enum :
					- distribution, collection, transportation, other	
	- encroachment : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Impact of the works on public, private area. A combination of : 
		- type: "array"
			- type: "string"
			- items :
				- enum :
					- public, private, residential, other

	### Information related to works, impacts and restrictions

	- typeOfInteventionRequest : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Initial type of request to do the works. 
			- type: "string"
			- enum :
				- authorizationRequest, urgentWorks, InterventionNotice, other
	- workReason : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Reasons of the works in case of urgent intervention. A combination of : 
		- type: "array"
			- type: "string"
			- items :
				- enum :
					- landslide, rockfall, flood, waterLeak, gazLeak, powerCut, collapse, sagging, fire, derailment, other 
	- workZone : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/text"
		- description: > Zone of Works. A combination of : 
		- type: "array"
			- items :
			- type: "string"
			  - enum :
			  	- road, path, offRoad, sideWalk, bridge, tunnel, bicyclePath, busCorridor, tramwayLine, railwayLine, subwayLine, dock, parksGardens, beach, parking, heliport, harbor, airport, river, protectArea, rockyArea, floodArea, sevesoArea, riskArea, mountainousArea, other.
	- workDisposition : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Specific rules taken for the works. A structured value from 0 to N occurrences where each items has the following format : `Disposition`: with sub properties  `startDate`, `endDate`,  `dayOfWeek`, `comment` 
		- type: "object"
			- items : 
				- disposition : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > Disposition : Free text. for example The list below:  
					- type: "string"
						- enum :
							- noRestriction, sidewalkClosureOrReduction, sidewalkClosure, sidewalkReduction, laneClosure, laneReduction, laneDeviation, bicyclePathClosure, bicyclePathReduction, bicyclePathDeviation, parkingModification, parkingForbidden, alternatingLights, circulationManualControl, speedReduction 
					- type: "Property"
						- startDate:
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/DateTime"
							- description: >  Start Date and time of the disposition.
							- type: "string"
								- format: "date-time"
						- endDate:
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/DateTime"
							- description: >  End Date and time of the disposition.
							- type: "string"
								- format: "date-time"
						- dayOfWeek : 
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/string"
							- description: >  Days of week days applicable to the disposition.
							- type : "string",
								- enum : Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday, PublicHolidays
						- comment : 
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/string"
						- description: >  Additional comment linked to the disposition (ex for speedReduction, can be the value).
							- type : "string"
	
	- workOtherImpact : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Other impact. A list of free value. For example a : 
		- type: "array"
			- type: "string"
			- items :
			- enum :
				- parkingOnZEBRA, layingCablesOnGround, shopsTerrace, ...
	- isMobile : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Boolean"
		- description: > Characteristic on the mobility of the works : `false` for Fixed (default) and `true` for Mobile. 
		- type: "Boolean"
	
	### Information related to exceptional derogation   
	
	- countOfDerogation : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of derofations granted to the work Number . 
		- type: "Number"
	- derogation : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > derogation granted for carrying out work on days and times.  A structured value from 0 to N occurrences where each items has the following format `derogationType` :  with sub properties  `startDate`, `endDate`,  `dayOfWeek`, `comment` 
		- type: "object"
			- items : 
				- derogationType: 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > Type of derogation granted. Free text (ex : WorkNigth, BRH, ...):  
					- type: "Property"
						- startDate:
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/DateTime"
							- description: >  Start Date and time of the derogation.
							- type: "string"
								- format: "date-time"
						- endDate:
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/DateTime"
							- description: >  End Date and time of the derogation.
							- type: "string"
								- format: "date-time"
						- dayOfWeek : 
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/string"
							- description: >  Days of week days applicable to the derogation.
							- type : "string",
								- enum : Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday, PublicHolidays
						- comment : 
							- x-ngsi:
								- type: "Property"
								- model: "https://schema.org/string"
							- description: >  Additional comment linked to the derogation Type.
							- type : "string"
	
	### Information identifying impacts on roads
	
	- isMainRoadImpactedHTR : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Boolean"
		- description: > Main traffic road ? Default `false`
		- type: "Boolean"
	- countOfRoadImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of roads impacted by the works. 
		- type: "Number"
	- roadImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Roads impacted by the works and the details of the roads concerned by the work. A structured value from 0 to N occurrences where each items is a string in the format : `roadImpact`:[List of Segment Impacted or Free Text or geo-property, separated by a comma]. If `isMainRoadImpactedHTR` = true, The first item is this one.
		- type: "array"
			- items : 
				- roadImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > [Free Text] or Reference to an entity [ROAD] if exists
					- type: "string"
				- segmentImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > List of [Free text] or [GeoProperty] or a Reference to an entity [SegmentRoad] if exists
					- type: "array"
						- type: "string"
	- allowedVehicle : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Text"
		- description: > Type of vehicle authorized to circulate. A combination of 
		- type: "array"
			- type: "string"
			- items : 
			  - enum :
			  	- all Vehicle, firefighters, police, emergencyVehicle, companiesTrucks, bus, tramway, subway, car, trucks, bicycle, motorcycle, lorry, trailer, van, sweepingMachine
	- maxAuthorizedTonnage : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Roads impacted by the works with Maximum tonnage authorized. A structured value from 0 to N occurrences where each items is a string in the format : `roadImpact`:[maxTonnage]. If `isMainRoadImpactedHTR` = true, The first item is this one.
		- type: "array"
			- items : 
				- roadImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > [Free Text] or Reference to an entity [ROAD] if exists
					- type: "string"
				- maxTonnage : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Number"
					- description: > Maximum tonnage authorized. The unit code (text) is given using the [UN/CEFACT Common Codes](http://wiki.goodrelations-vocabulary.org/Documentation/UN/CEFACT_Common_Codes) . For instance, **TNE** represents Tonne Metric.
					- type: "Number"
	
	### Information identifying impacts on Public Services
	##### Format of the structured value for each attribut of this section
	###### A structured value from 0 to N occurrences where each items is a string in the format : 
	###### `lineImpact` :[A list of segment impact with [Free Text] or [GeoProperty] or a Reference to an {SegmentEntity], separated by a comma]
	
	- countOfBusLineImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of Bus Lines impacted by the works. 
		- type: "Number"
	- busImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Bus lines impacted by the works. A structured value from 0 to N occurrences.
		- type: "array"
			- items : 
				- lineImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A unique value of [Free Text] or Reference to an entity [BUSLINE] if exists
					- type: "string"
				- segmentImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A List of [Free Text] or [GeoProperty] or a Reference to an entity  [BUSSEGMENT] if exists.
					- type: "array"
						- type: "string"
	- countOfSchoolBusLineImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of School Bus Lines impacted by the works. 
		- type: "Number"
	- schoolBusImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Scholl Bus lines impacted by the works.
		- type: "array"
			- items : 
				- lineImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A unique value of [Free Text] or Reference to an entity [SCHOOLBUSLINE] if exists
					- type: "string"
				- segmentImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A List of [Free Text] or [GeoProperty] or a Reference to an entity [SCHOOLBUSSEGMENT] if exists.
					- type: "array"
						- type: "string"
	- countOftramwayLineImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of tramway Lines impacted by the works. 
		- type: "Number"
	- tramwayImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > tramway Line impacted by the works. A structured value from 0 to N occurrences.
		- type: "array"
			- items : 
				- lineImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A unique value of [Free Text] or Reference to an entity [TRAMWAYLINE]if exists
					- type: "string"
				- segmentImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A List of [Free Text] or [GeoProperty] or a Reference to an entity [TRAMWAYSEGMENT] if exists.
					- type: "array"
						- type: "string"
	- countOfSubwayLineImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of Subway Lines impacted by the works. 
		- type: "Number"
	- subwayImpacted :  
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Subway lines impacted by the works. A structured value from 0 to N occurrences.
		- type: "array"
			- items : 
				- lineImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A unique value of [Free Text] or Reference to an entity [SUBWAYLINE] if exists
					- type: "string"
				- segmentImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A List of [Free Text] or [GeoProperty] or a Reference to an entity [SUBWAYSEGMENT] if exists.
					- type: "array"
						- type: "string"
	- countOfRailwayLineImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of Railway Lines impacted by the works. 
		- type: "Number"
	- railwayImpacted :  
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Rail lines impacted by the works.
		- type: "array"
			- items : 
				- lineImpact : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A unique value of [Free Text] or Reference to an entity [RAILLINE] if exists
					- type: "string"
				- segmentImpact : 
					- x-ngsi:
						- type: "Property"
					- model: "https://schema.org/Text"
					- description: > A List of [Free Text] or [GeoProperty] or a Reference to an entity [RAILSEGMENT] if exists.
				- type: "array"
						- type: "string"
	
	### Information related to educational establishment Impacted by the works
	
	- countOfSchoolImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of University, School, ... impacted by the works. 
		- type: "Number"
	- SchoolImpact : 
		- x-ngsi:
			- type: "Property"
		- model: ""https://schema.org/text""
		- description: > List of free text or or [GeoProperty] or a Reference to an entity [SCHOOL] if exist. 
		- type: "array"
			- type: "string"
	
	### Information identifying impacts on Public Station (subway, Bus, ...)
	##### Format of the structured value for each attribut of this section
	###### A structured value from 0 to N occurrences where each items is a string in the format : 
	###### `stationType` of GTFS : [A list of segment impact with [Free Text] or [GeoProperty] or a Reference to an {Entity], separated by a comma]
	
	- countOfStationImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of Railway Lines impacted by the works. 
		- type: "Number"
	- stationImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "http://schema.org/StructuredValue"
		- description: > Station Impacted by the works. A structured value from 0 to N occurrences  
		- type: "array"
			- items : 
				- stationType : 
					- x-ngsi:
						- type: "Property"
						- model: "https://schema.org/Text"
					- description: > A unique value composed only of the attribut 'description' (subway, Bus, Tram, ...) from the urban transport Mode GFTS standard [STOP](https://developers.google.com/transit/gtfs/reference/#stopstxt). 
					- type: "string"
						- enum : tram, subway, rail, bus, ferry, cableTram, aerialLift, funicular, trolleybus, monorail
				- stationId : 
					- x-ngsi:
						- type: "Property"
					- model: "https://schema.org/Text"
					- description: > A list of [Free Text] or [GeoProperty] or a Reference to an entity [STATION] / [POI] if exists. (https://github.com/smart-data-models/dataModel.Transportation/blob/master/Station/doc/spec.md) if used.
				- type: "array"
						- type: "string"
	
	### Information related to Events Impacted by the works
	
	- countOfEventImpacted : 
		- x-ngsi:
			- type: "Property"
			- model: "https://schema.org/Number"
		- description: > Count of Events impacted by the works. 
		- type: "Number"
	- eventsImpact : 
		- x-ngsi:
			- type: "Relationship"
		- model: ""https://schema.org/URL""
		- description: > List of free text or to the entity [Events](https://github.com/smart-data-models/dataModel.Tourism/blob/master/Events/doc/spec.md) if exist. 
		- type: "array"
			- type: "string"
