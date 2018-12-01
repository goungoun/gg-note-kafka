# Why Avro for Kafka by Jay Kreps

> Reference: https://www.confluent.io/blog/avro-kafka-data/?fbclid=IwAR1fQ2_3Q6V7lCbvy2tYaf40s-4eI_bnHucAOZ5EPOSAILZuyOe6OLqYKbU

## Why Avro for stream data?
- It has a idrect apping to and from JSON
- It has very compact format
- It is very fast
- It has great bindings for a wide variety of programming languages
- You can generate Java objects that make working with event data easier, but it does not require code generation so tools can be written generically for nay data stream
- It has righ, extensible schema language defined in pure JSON
- It has the best notion of compatability for evolving your data over time

## Why JSON is inefficient?
- The bulk of JSON, repeating every field name with every single record, is what makes JSON inefficient for high-ovlume usage

## Example - Sale of a product

- Define five fields
~~~json
{
  "type": "record",
  "doc":"This event records the sale of a product",
  "name": "ProductSaleEvent",
  "fields" : [
    {"name":"time", "type":"long", "doc":"The time of the purchase"},
    {"name":"customer_id", "type":"long", "doc":"The customer"},
    {"name":"product_id", "type":"long", "doc":"The product"},
    {"name":"quantity", "type":"int"},
    {"name":"payment",
     "type":{"type":"enum",
	     "name":"payment_types",
             "symbols":["cash","mastercard","visa"]},
     "doc":"The method of payment"}
  ]
}
~~~

- event
~~~json
{
  "time": 1424849130111,
  "customer_id": 1234,
  "product_id": 5678,
  "quantity":3,
  "payment_type": "mastercard"
}
~~~

## How to use?
- Associate a schema with each Kafka topic
- Let producers and consumers knows the right fields of the data stream
- Protect downstream: Only valid data will be permitted in the topic



