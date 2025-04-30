# Introduction to Amazon DynamoDB

DynamoDB is a fast and flexible NoSQL database supporting both document and key-value data models.

Each table requires a primary key, and sometimes has a sort key as well. The combo of primary key and sort key uniquely identifies each item in a DynamoDB table.

When creating a table you are able to specify both the primary key and sort key.

Each table contains multiple items. An item is a group of attributes that is uniquely identifiable among all the other items. Items are like rows. No limit to number of items you can store in a table.

Each item composed of one or more attributes. Attributes are fundamental data elements. Similar to columns in other database systems, but each item can have different attributes.

Each item requires the primary key and sort key (if used), but otherwise you can use different attributes.

## Creating and modifying items

You can create and view items via the "explore items: music" page.

Faster ways to load data into DynamoDB include using the AWS Data Pipeline, programmatically loading data, or using one of the free tools available on the internet.

You can also modify existing items.

## Querying and scanning

There are two ways to query a DynamoDB table: Query and Scan.

A query operation finds items based on primary key and optionally sort key. It is fully indexed and so it runs very fast. A query is the most efficient way to retrieve data from a DynamoDB table.

Scanning involves looking through every item in a table, so it is less efficient and can take significant time for larger tables.

## Knowledge check

Which statement BEST describes the flexibility of adding attributes to items in a DynamoDB table? New attributes can be added to some items without affecting others

Which of the following statements is TRUE about inserting data into a DynamoDB table? You can insert items with different attributes into the same table

What should you consider before deleting a DynamoDB table? The need for a backup of the data

Which operation is used to retrieve data from a DynamoDB table based on specific criteria? Query

What is the relationship between a Primary Key and a Sort Key in an Amazon DynamoDB table? They uniquely identify each item when used in combination

**Source:** [AWS Certified Solutions Architect - Associate (Subscription - Partner Subscription)](https://explore.skillbuilder.aws/learn/learning-plans/2159/aws-certified-solutions-architect-associate-subscription-partner-subscription), AWS Training & Certification.