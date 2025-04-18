# BoostSync Features and Limitations

BoostSync is a data synchronization tool designed to connect and align data between NetSuite and HubSpot systems. This document outlines the core components and their limitations.

## Configurations

Configurations define the synchronization relationship between record types across systems.

**Key Features:**

- Establish sync relationships between NetSuite and HubSpot objects
- Support for one-way or bi-directional synchronization
- Customizable through filters, deduplication keys, and mapping rules

**Limitations:**

- Each record type can only have one configuration (1:1 mapping only)
- No support for one-to-many relationships between systems
- Duplicate records are automatically marked ineligible for syncing
- Deleted objects aren't automatically replaced - errors will log until the object is deleted from both systems

## Filters

Filters determine which records are eligible for synchronization.

**Key Features:**

- Custom logic for record eligibility
- Support for queries, datasets, and search-based filtering

**Limitations:**

- Records must meet filter criteria in both systems to be matched
- Misaligned filters can result in duplicate records being created

## Deduplication Keys

Deduplication keys establish how records are matched across systems.

**Key Features:**

- Support for up to three fields as matching criteria
- Single keys (common-key) or multiple keys (common-composite-key)
- Typical examples include email addresses for contacts

**Limitations:**

- Keys are automatically converted to lowercase (case-insensitive matching)
- Multiple matching records result in duplicates being neglected
- Key value changes after initial sync won't affect existing record pairings

## Field Mappings

Field mappings control which data points synchronize between paired records.

**Key Features:**

- One-way or bi-directional field synchronization options
- Custom mapping tables for multi-select fields

**Limitations:**

- Static mapping direction (cannot change dynamically based on record state)
- No support for multi-field logic or calculated mappings
- Field types must be compatible between systems
- Only fields available directly on the record can be mapped

## Association Mappings

Association mappings handle relationships between objects across systems.

**Key Features:**
- Support for 1:1 associations (primary company, parent company)
- Support for 1:many associations (line items, related contacts)

**Limitations:**
- Associated objects must also be included in sync configurations
- Only objects in filter criteria can be associated (exception: line items)
- Line items are treated as part of the opportunity record rather than separate entities
