# MuleAvro
Avro Schema in Mule 4

Introduction: This document talks about how to implement avro schema and what are the possible ways to serialize and de-serialize the avro message.

Assumptions:
1.	Audience knows the basics of Mule 4 with Anypoint Studio 7.4.X
2.	A generic employee schema will be used as a use case.

What is avro schema:
Avro, being a schema-based serialization utility, accepts schemas as input. In spite of various schemas being available, Avro follows its own standards of defining schemas. These schemas describe the following details −
•	type of file (record by default)
•	location of record
•	name of the record
•	fields in the record with their corresponding data types
Using these schemas, you can store serialized values in binary format using less space. These values are stored without any metadata.
Creating Avro Schemas
The Avro schema is created in JavaScript Object Notation (JSON) document format, which is a lightweight text-based data interchange format. It is created in one of the following ways −
•	A JSON string
•	A JSON object
•	A JSON array
Example − The following example shows a schema, which defines a document, under the name space Tutorialspoint, with name Employee, having fields name and age.
{
   "type" : "record",
   "namespace" : "Tutorialspoint",
   "name" : "Employee",
   "fields" : [
      { "name" : "Name" , "type" : "string" },
      { "name" : "Age" , "type" : "int" }
   ]
}

Mule 4 supports Avro Schema serialization/de-serialization of Avro based messages.

Use case description:
As part of this demonstration, we have created a sample avro schema – ‘employee.avro.json’ as below:

{
	"namespace": "com.uhg.avro",
	"name": "com.uhg.avro.Employee",
	"type": "record",
	"fields": [
		{
			"name": "employeeId",
			"type": "int"
		},
		{
			"name": "firstname",
			"type": "string"
		},
		{
			"name": "lastname",
			"type": "string"
		},
		{
			"name": "address",
			"type": "string"
		},
		{
			"name": "notes",
			"type": "string"
		}
	]
} 

This schema will be used to create a sample avro based message (serialized) and will be written in a file and the same file will be picked up by another flow (Deserializer). This flow will de-serialize the contents of the avro file and place the contents in a json file format.

Serializer:
 


Logs:
Serializer:
INFO  2020-03-11 23:31:22,203 [[MuleRuntime].cpuIntensive.01: [muleavro].Serializer.CPU_INTENSIVE @7e72eb2b] [event: 50a27210-63c2-11ea-b791-a483e75ffd78] org.mule.runtime.core.internal.processor.LoggerMessageProcessor: {
  "Avro payload": [
    {
      employeeId: 0 as Number {class: "java.lang.Integer"},
      firstname: "Ankur0" as String {class: "org.apache.avro.util.Utf8"},
      lastname: "Parashar" as String {class: "org.apache.avro.util.Utf8"},
      address: "Sample address: Kentucky islands" as String {class: "org.apache.avro.util.Utf8"},
      notes: "some more information" as String {class: "org.apache.avro.util.Utf8"}
    }, 
    {
      employeeId: 1 as Number {class: "java.lang.Integer"},
      firstname: "Ankur1" as String {class: "org.apache.avro.util.Utf8"},
      lastname: "Parashar" as String {class: "org.apache.avro.util.Utf8"},
      address: "Sample address: Kentucky islands" as String {class: "org.apache.avro.util.Utf8"},
      notes: "some more information" as String {class: "org.apache.avro.util.Utf8"}
    }, 
    {
      employeeId: 2 as Number {class: "java.lang.Integer"},
      firstname: "Ankur2" as String {class: "org.apache.avro.util.Utf8"},
      lastname: "Parashar" as String {class: "org.apache.avro.util.Utf8"},
      address: "Sample address: Kentucky islands" as String {class: "org.apache.avro.util.Utf8"},
      notes: "some more information" as String {class: "org.apache.avro.util.Utf8"}
    }, 
    {
      employeeId: 3 as Number {class: "java.lang.Integer"},
      firstname: "Ankur3" as String {class: "org.apache.avro.util.Utf8"},
      lastname: "Parashar" as String {class: "org.apache.avro.util.Utf8"},
      address: "Sample address: Kentucky islands" as String {class: "org.apache.avro.util.Utf8"},
      notes: "some more information" as String {class: "org.apache.avro.util.Utf8"}
    }, 
    {
      employeeId: 4 as Number {class: "java.lang.Integer"},
      firstname: "Ankur4" as String {class: "org.apache.avro.util.Utf8"},
      lastname: "Parashar" as String {class: "org.apache.avro.util.Utf8"},
      address: "Sample address: Kentucky islands" as String {class: "org.apache.avro.util.Utf8"},
      notes: "some more information" as String {class: "org.apache.avro.util.Utf8"}
    }, 
    {
      employeeId: 5 as Number {class: "java.lang.Integer"},
      firstname: "Ankur5" as String {class: "org.apache.avro.util.Utf8"},
      lastname: "Parashar" as String {class: "org.apache.avro.util.Utf8"},
      address: "Sample address: Kentucky islands" as String {class: "org.apache.avro.util.Utf8"},
      notes: "some more information" as String {class: "org.apache.avro.util.Utf8"}
    }
  ] as Array {encoding: "UTF-8", mediaType: "application/avro; charset=UTF-8; schemaurl=\"java.io.BufferedInputStream@262eef39\"", mimeType: "application/avro", contentLength: 736}
}
INFO  2020-03-11 23:31:22,265 [[MuleRuntime].io.13: [muleavro].Serializer.BLOCKING @b068456] [event: 50a27210-63c2-11ea-b791-a483e75ffd78] org.mule.runtime.core.internal.processor.LoggerMessageProcessor: File generated

Deserializer:
INFO  2020-03-11 23:31:23,284 [[MuleRuntime].cpuIntensive.02: [muleavro].Deserializer.CPU_INTENSIVE @24b1dbc9] [event: 519eac61-63c2-11ea-b791-a483e75ffd78] org.mule.runtime.core.internal.processor.LoggerMessageProcessor: {
  "Deserialized avro payload": [
    {
      "employeeId": 0,
      "firstname": "Ankur0",
      "lastname": "Parashar",
      "address": "Sample address: Kentucky islands",
      "notes": "some more information"
    },
    {
      "employeeId": 1,
      "firstname": "Ankur1",
      "lastname": "Parashar",
      "address": "Sample address: Kentucky islands",
      "notes": "some more information"
    },
    {
      "employeeId": 2,
      "firstname": "Ankur2",
      "lastname": "Parashar",
      "address": "Sample address: Kentucky islands",
      "notes": "some more information"
    },
    {
      "employeeId": 3,
      "firstname": "Ankur3",
      "lastname": "Parashar",
      "address": "Sample address: Kentucky islands",
      "notes": "some more information"
    },
    {
      "employeeId": 4,
      "firstname": "Ankur4",
      "lastname": "Parashar",
      "address": "Sample address: Kentucky islands",
      "notes": "some more information"
    },
    {
      "employeeId": 5,
      "firstname": "Ankur5",
      "lastname": "Parashar",
      "address": "Sample address: Kentucky islands",
      "notes": "some more information"
    }
  ]
}

Reference:
1.	Mule configuration xml:
2.	Sample employee.avro.json. This needs to be maintained under src/main/resources
{
	"namespace": "com.uhg.avro",
	"name": "com.uhg.avro.Employee",
	"type": "record",
	"fields": [
		{
			"name": "employeeId",
			"type": "int"
		},
		{
			"name": "firstname",
			"type": "string"
		},
		{
			"name": "lastname",
			"type": "string"
		},
		{
			"name": "address",
			"type": "string"
		},
		{
			"name": "notes",
			"type": "string"
		}
	]
}
3.	How the validations are handled: What if the message is non as per avro designed? Yes, during serialization it will error out stating the mismatch. For example, highlighted section is out of sync element:
%dw 2.2
output application/avro schemaUrl="employee.avro.json"
---
(0 to 5) map {
	employeeId: $$,
	firstname: "Ankur" ++ $$,
	lastname: "Parashar",
	address: "Sample address: Kentucky islands",
	notes: "some more information",
	test: "Free test"
}

Now when this is tested:
ERROR 2020-03-11 23:46:25,116 [[MuleRuntime].cpuIntensive.03: [muleavro].Serializer.CPU_INTENSIVE @a35630e] [event: 6b288961-63c4-11ea-b791-a483e75ffd78] org.mule.runtime.core.internal.exception.OnErrorPropagateHandler: 
********************************************************************************
Message               : "Invalid field name `test` similar options are: 
- notes
- address
- lastname
- firstname
- employeeId

10| 	test: "Free test"
     ^^^^
Trace:
  at main (line: 10, column: 2), while writing Avro at 
10| 	test: "Free test"
     ^^^^.

10| 	test: "Free test"
     ^^^^
Trace:
  at main (line: 10, column: 2)" evaluating expression: "%dw 2.2
output application/avro schemaUrl="employee.avro.json"
---
(0 to 5) map {
	employeeId: $$,
	firstname: "Ankur" ++ $$,
	lastname: "Parashar",
	address: "Sample address: Kentucky islands",
	notes: "some more information",
	test: "Free test"
}
".
Error type            : MULE:EXPRESSION
Element               : Serializer/processors/0 @ muleavro:muleavro.xml:34 (Transform Message)
Element XML           : <ee:transform doc:name="Transform Message" doc:id="fc307cc9-0c39-4963-a4cf-a0d1b3acc89a">
<ee:message>
<ee:set-payload>%dw 2.2
output application/avro schemaUrl="employee.avro.json"
---
(0 to 5) map {
	employeeId: $$,
	firstname: "Ankur" ++ $$,
	lastname: "Parashar",
	address: "Sample address: Kentucky islands",
	notes: "some more information",
	test: "Free test"
}</ee:set-payload>
</ee:message>
</ee:transform>

  (set debug level logging or '-Dmule.verbose.exceptions=true' for everything)

4.	More references:
https://www.tutorialspoint.com/avro/avro_schemas.htm
https://docs.mulesoft.com/mule-runtime/4.2/dataweave-formats#format_avro
