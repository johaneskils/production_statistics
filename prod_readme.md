# Point of Care Laboratory Information System

```text
A hospital laboratory organization supporting multiple primary care units and hospital wards across several hospital locations may have thousands of nurses performing bedside and near-patient testing daily.

Hundreds of different analyses are performed on thousands of instruments distributed across many locations. User access rights, traceability, and identification of which instrument performed a specific analysis are essential requirements.

Configuring and maintaining a Point of Care Laboratory Information System (POC-LIS) is a complex operational task. As more wards, instruments, and analyses are added, the administrative workload increases significantly.

Running a Point of Care service involves:
- user administration
- ward and instrument configuration
- billing procedures
- quality assurance
- service and support
- regulatory traceability

Even when most information is stored within the POC-LIS, the operational environment changes continuously:
- instruments are replaced or removed
- users transfer or retire
- wards change structure
- analyses are added or discontinued

A laboratory information system therefore carries a long-term operational history that must remain transparent and traceable over time due to regulatory requirements.

Patient testing performed by non-laboratory staff must maintain the same quality, traceability, and safety standards as testing performed inside the central laboratory.

Adding a single user is manageable, but adding hundreds of users with correct ward and instrument access rights becomes time-consuming and error-prone when handled manually.

By combining information exports from:
- the main LIS
- the POC-LIS
- HR systems
- customer/ward information systems
- production and billing statistics

it becomes possible to automate operational reporting and create a better overview of:
- production statistics
- billing validation
- instrument distribution
- access administration
- operational workload

To automate these workflows, the input information must first be transformed into structured and machine-readable representations.

In practice, translation tables and shared keys are often necessary because different systems may use different identifiers for the same ward, instrument group, or customer unit.

Some analyses may also be billed as grouped analysis packages rather than as individual analytes, which further increases the need for structured relational mappings.

```

## Simplification

```text
In a production system, user access would normally include validity dates, active/inactive status, and historical traceability. These fields are omitted in this demo to keep the core relational logic clear.
```

## Generation of production statistics

### random_gen.ipynb

```text
Jupyter notebook that create the following files with production statistics:
```

#### instruments.csv 

A generation of the different equipment classes found at a specific ward/location.
```text
instrument_id,unit_id,instrument_class
I001,A1,ALPHA
I004,A1,ALPHA
I006,A1,ALPHA
...
```

#### equipment.csv

Created from the instruments.csv file and are used for generating the file for user import.
```text
unit_id,equipment_class
A1,ALPHA
A1,BETA
A1,DELTA
A1,GAMMA
...
```

#### production_results.csv

Based on the date range, instrument locations, number of instruments in total to generate results from and the equipment classes a production file is generated.

```text
result_id,run_date,instrument_id,result_count
R00001,2026-01-01,I001,83
R00002,2026-01-02,I001,111
R00003,2026-01-03,I001,174
...
```

# Calculation and report generation of production statistics

### prod_statistics.ipynb

Jupiter notebook file, that require Matplotlib and Pandas.

The demo uses four CSV input files:

```text
users.csv
access_rules.csv
instruments.csv
production_results.csv
```