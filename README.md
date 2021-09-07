# OpenTHC Lab Result Model
An opinionated Cannabis Laboratory Results model for exchanging data using the [OpenTHC model](https://github.com/openthc/api).

## OpenTHC, In their own words.

"The world of cannabis regulatory compliance is complex and large. There are hundreds of vendors, each with a common goal but without an API, partial API, or have implemented a unique flavor. The goal of this interface is to provide a basis for data interoperability."

"An important first step for bringing the industry together is to start talking in with common terms, a second is a common interface. The OpenTHC API Specification aims to define core parts of this data model and suggested interfaces."

Find more here: [github:OpenTHC/Api](https://github.com/openthc/api)  
and here: [https://openthc.org/](https://openthc.org/)  

## A Proposed Laboratory Result Model

Existing OpenTHC participants are already using a model to submit  samples lotted for laboratory testing. A basic schema example of it can be found [here](https://api.openthc.org/json-example#lab-sample). An example JSON object of it can be found [here](lab_sample.json).Within that model is an item list containing small objects representing common demographic details of a sample (e.g. inventory ID numbers, sizes and weights, type labels, etc.).

This proposed model returns that item along with the result to provide reference as sent by the source license holder. The following is a sort of relationship model illustrating the fit.

![image](OpenTHC_LabResultObject.svg)

# lab_result model

## The identifier fields:
* **id**: a ULID unique to this result.  
* **source_license**: the laboratory business identifier.  
* **target_license**: the sample source business identifier.  

## The timestamp fields:
* **received_at**:  the ISO 8601 timestamp of when the lab received the sample.  
* **completed_at**: the ISO 8601 timestamp of when the lab completed testing.

## The demographics data sent by the source:
* **lab_sample_item**: an item from the `lab_sample` object's `item_list`.

## The list of analytes and their measures:
* **metric_list**: an array of result metrics.

### The Result Metric Model
* **id**: a ULID unique to this metric.
* **reference**: An object describing the analyte demographics:  
  * **id**: a ULID unique to this Reference.
  * **common_name**: a common or colloquial version of the scientific name selected.
  * **reference_name**: the scientific name used by the laboratory for precision.
  * **reference_id**: an ID number representing the Reference analyte.
  * **reference_type**: an identifier of where the Reference ID is catalogued.
  * **reference_link**: a URL link to the Reference ID.  
  * **is_rnd**: a boolean state indicating whether or not the reference reported is reported for compliance, or for research purposes.
* **type**: An object describing the measure type (e.g. analyte, summary, etc.)  
  * **id**: a ULID unique to this type.  
  * **name**: the name of this type.  
  * **description**: the description of this type.
* **category**: An object describing the analyte category (e.g. cannabinoid, pesticide, etc.)  
  * **id**: a ULID unique to this category.  
  * **name**: the name of this category.  
  * **description**: the description of this category.  
* **quantity**: An object describing the results of analysis of the analyte:  
  * **qty**: the analysis quant.
  * **uom**: the quant's unit of measure.
  * **lod**: the limit of detection reported for this analyte.
  * **loq**: the limit of quantitation reported for this analyte.
  * **loq**: the limit of quantitation reported for this analyte.
  * **action_limit**: any action limit imposed.

## A JSON Example
An [example `lab_result` JSON object is available here](lab_result.json).
