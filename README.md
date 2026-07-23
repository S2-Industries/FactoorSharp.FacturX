# FactoorSharp

Core: [![NuGet](https://img.shields.io/nuget/v/FactoorSharp.FacturX?color=blue)](https://www.nuget.org/packages/FactoorSharp.FacturX/)
PDF: [![NuGet](https://img.shields.io/nuget/v/FactoorSharp.FacturX.PDF?color=blue)](https://www.nuget.org/packages/FactoorSharp.FacturX.PDF/)
Validation: [![NuGet](https://img.shields.io/nuget/v/FactoorSharp.FacturX.Validator?color=blue)](https://www.nuget.org/packages/FactoorSharp.FacturX.Validator/)

FactoorSharp is a .NET library for creating, processing, and validating 
Factur-X (ZUGFeRD) and XRechnung documents.

The library is the successor of the popular ZUGFeRD-csharp library (https://github.com/stephanstapel/ZUGFeRD-csharp).

It is designed for developers who need a reliable and standards-compliant way 
to handle electronic invoices in modern .NET applications, backend systems, 
and enterprise environments.

You can find all available license options here:  
https://www.factoorsharp.com/?utm_source=github&utm_medium=readme&utm_campaign=facturx


## Overview

FactoorSharp provides a unified approach to working with structured invoice data 
across different standards. It supports both hybrid formats (Factur-X / PDF-A/3) 
and fully structured formats (XRechnung / UBL / CII).

The library focuses on correctness, performance, and seamless integration into 
existing software systems.


## Features

- Creation of Factur-X (ZUGFeRD) documents including PDF/A-3 embedding 
- Generation and processing of XRechnung (UBL and CII formats) 
- Validation of documents against relevant standards 
- Extraction and transformation of structured invoice data 
- Designed for backend processing and automation scenarios 
- Suitable for integration into APIs, services, and enterprise systems 


## Installation

Install the package via NuGet:

```bash
dotnet add package FactoorSharp.FacturX
```

The API is designed to be straightforward and easy to integrate into existing workflows:

```csharp
FacturXInvoice.SetLicense("...");

var invoice = FacturXInvoice.CreateInvoice("Invoice-01", new DateTime(2025,09,03), CurrencyCodes.EUR)
    .SetSeller(name: "BikeTech GmbH",
               postcode: "10115",
               city: "Berlin",
               street: "Radweg 12",
               country: CountryCodes.DE,
               id: String.Empty,
               globalID: new GlobalID(GlobalIDSchemeIdentifiers.GLN, "4000001123452"),
               legalOrganization: new LegalOrganization(GlobalIDSchemeIdentifiers.GLN, "4000001123452", "BikeTech GmbH"))
    .SetBuyer(name: "CityRider AG",
              postcode: "20457",
              city: "Hamburg",
              street: "Hafenstraße 45",
              country: CountryCodes.DE,
              id: "DE987654321");
invoice.AddTradeLineItem(name: "Trekkingrad",
                         netUnitPrice: 799.0m,
                         unitCode: QuantityCodes.C62,
                         grossUnitPrice: 799.0m,
                         billedQuantity: 1,
                         taxType: TaxTypes.VAT,
                         categoryCode: TaxCategoryCodes.S,
                         taxPercent: 19,
                         sellerAssignedID: "BIKE-1");

decimal taxTotalAmount = 799.0m / 100m * 19m;

invoice.AddApplicableTradeTax(basisAmount: 799.0m,
                              percent: 19m,
                    taxAmount: taxTotalAmount,
                              typeCode: TaxTypes.VAT,
                              categoryCode: TaxCategoryCodes.S);

invoice.SetTotals(lineTotalAmount: 799.0m,
                    taxBasisAmount: 799.0m,
                    taxTotalAmount: taxTotalAmount,
                    grandTotalAmount: 799.0m + taxTotalAmount,
                    duePayableAmount: 799.0m + taxTotalAmount
                    );

invoice.Save("factur-x.xml",
            version: ZUGFeRDVersion.Version23,
            profile: Profile.Extended);
```

## Licensing Model
FactoorSharp is a commercial product licensed per company.
The license model is based on the following principles:
* The license is granted to a company, not to individual users 
* Usage is based on the number of developers working with the library 
* Different license tiers are available (e.g. Freelancer, SME, Corporate) 
* Customers are expected to select a license that reflects their actual usage 

The model follows a fair-use approach and does not enforce strict technical limits.

## Subscription and Perpetual Use
FactoorSharp is provided under a subscription model.
During an active subscription, customers receive:
* Access to updates and new versions 
* Support services 

After the subscription ends:
* The last available version remains usable indefinitely 
* No further updates or support are included

## Redistribution
FactoorSharp can be used within customer applications, including SaaS solutions.
Redistribution is permitted under the condition that an appropriate license
(including redistribution rights) has been obtained.
The software itself and license keys must not be shared with third parties.

## Data Protection and Privacy
FactoorSharp processes document data only for technical purposes.
When validating or processing documents (such as Factur-X or XRechnung),
the transmitted data may contain personal information (e.g. names, addresses).
The following principles apply:
* Data is processed only temporarily during the request 
* No storage of document content takes place 
* No use for analytics, training, profiling, or any other purposes occurs 
All data remains under the control of the customer.

## License Validation
The library may periodically validate the license by communicating with a license server.
The following data may be transmitted:
* License key 
* Hashed IP address 
* Hashed username 
* Hashed domain 
This information is used exclusively to verify license compliance and prevent misuse.

## Disclaimer
FactoorSharp is a technical tool for processing structured invoice data.
No guarantee is given for:
* Legal compliance of generated documents 
+ Correctness in all business or regulatory contexts 
Users are responsible for ensuring compliance with applicable laws and regulations.

## License
This software is licensed, not sold.
For full terms and conditions, including detailed legal and data protection provisions,
please refer to:

https://www.factoorsharp.de/de/Home/Agb/?utm_source=github&utm_medium=readme&utm_campaign=facturx

## Support
Support is available during an active subscription period.

## About
FactoorSharp is developed and maintained by:  
STwo Industries GmbH  
Eichenkoppel 19  
22399 Hamburg  
Germany
