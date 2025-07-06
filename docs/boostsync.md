# BoostSync

BoostSync is an integration tool that automatically keeps your NetSuite data in step with other systems such as HubSpot.  It removes the need to manually copy information between platforms so your team always works with the same records everywhere.

## How It Works (Non-Technical Overview)

1. **Choose what to sync** – In NetSuite you create a configuration that specifies which record types (for example customers, contacts, deals) should stay in sync.
2. **BoostSync compares the systems** – The app checks for new or updated records in each system and determines if the same record already exists in the other system.
3. **Fields are updated automatically** – When matches are found, the selected fields are kept consistent. New records can also be created when they don’t exist in the other system.
4. **Run on demand or on a schedule** – Synchronizations can be triggered manually or set to occur on a regular schedule.
5. **Monitor results** – BoostSync keeps a log of actions so you can confirm records were synced successfully.

The configuration options described below provide more detail for technical administrators, but the general idea is simply that BoostSync handles the heavy lifting of copying data back and forth.

---

## BoostSync Features and Limitations

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
