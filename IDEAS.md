# Idea Document

## Cleaning and Imputing Data

### Using FEMA Data to add/fill fields
* Create `distanceToNearestWaterBody` field using FEMA Data
* Use FEMA data to fill unknowns for `ratedFloodZone`

### Handling unknowns

* `buildingDamageAmount`: drop
* `buildingPropertyValue`: drop
* `floodEvent`: impute using predominant value by `yearOfLoss`
* `waterDepth`: impute using median value by `floodEvent` and `reportedZipCode`
* `floodWaterDuration`: impute using median value by `yearOfLoss` and `reportedZipCode`
* `ratedFloodZone`: drop
* `causeOfDamage`: unknown flag
* `numberOfFloorsInTheInsuredBuilding`: impute using median value in `buildingDescriptionCode`
* `occupancyType`: impute using predominant value by `reportedZipCode`