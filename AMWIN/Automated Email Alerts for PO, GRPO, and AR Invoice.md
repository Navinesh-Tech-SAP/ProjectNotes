# Project: Automated Email Alerts for PO, GRPO, and AR Invoice in SAP Business One

## 1. Project Overview

Developed an automated email alert system for SAP Business One to send Purchase Order (PO), Goods Receipt PO (GRPO), and Accounts Receivable (AR) Invoice documents as PDF attachments to the respective vendors or customers.

The application generates PDF files using Crystal Reports, sends email notifications based on document conditions, and updates email status fields in the SAP database to track processing.

## 2. Technologies and Components Used

* **SAP Business One:** Document management and business process integration.
* **SAP HANA:** Database queries and document data retrieval.
* **C#:** Application development and email automation.
* **Crystal Reports:** PDF generation for SAP documents.
* **Task Scheduler:** Automatic execution of the application at scheduled intervals.
* **Crystal Reports DLLs:** Used for report processing and PDF export.

### Crystal Reports DLLs

* `CrystalDecisions.ReportSource`
* `CrystalDecisions.Shared`
* `CrystalDecisions.CrystalReports.Engine`

## 3. Functional and Technical Implementation

### 3.1 Purchase Order (PO)

**Functional Implementation:**

* Created User-Defined Fields (UDFs) for **To and CC email addresses** to maintain vendor email recipients.
* Configured the application to send PO PDF attachments to the specified recipients when a new Purchase Order is created.
* Updated the email status UDF to **Yes** after successful email processing.

**Technical Implementation:**

* Retrieved PO document details from SAP HANA.
* Generated the PO PDF using Crystal Reports.
* Used the vendor-specific email addresses maintained in the UDFs to send automated email notifications.

### 3.2 Goods Receipt PO (GRPO)

**Functional Implementation:**

* Modified the stored procedure logic to identify Purchase Orders that have been used to create a GRPO.
* Set the email status to **No** for the relevant PO when the GRPO condition was met, preventing the PO email alert from being triggered under that condition.

**Technical Implementation:**

* Updated the stored procedure logic to check the relationship between PO and GRPO documents.
* Integrated the status condition into the email automation workflow to control when PO email notifications should be processed.

### 3.3 Accounts Receivable (AR) Invoice

**Functional Implementation:**

* Configured the application to identify AR Invoices created on the current processing date.
* Generated PDF copies of the invoices and sent them to the respective customers.
* Updated the email status field in the AR Invoice document to track email processing.

**Technical Implementation:**

* Retrieved invoice details using SAP HANA queries.
* Generated invoice PDFs through Crystal Reports.
* Automated customer email notifications with PDF attachments.
* Updated the invoice email status after processing.

## 4. Technical Challenges and Troubleshooting

### 4.1 Crystal Reports DLL Compatibility

**Issue:** The application encountered compatibility issues involving Crystal Reports assemblies with different platform configurations.

**Resolution:**

* Investigated the Crystal Reports assembly versions and platform compatibility.
* Identified the relevant 64-bit assembly and checked the assemblies available in the Global Assembly Cache (GAC).
* Used the appropriate 64-bit Crystal Reports components to resolve the PDF generation issue.

### 4.2 SAP HANA Connection in Crystal Reports

**Issue:** Crystal Reports PDF generation failed because the SAP HANA database connection was not passed correctly to the report generation method.

**Resolution:**

* Initially tested the report using a hardcoded `DocEntry`.
* Investigated the report database connection configuration.
* Modified the code to pass the SAP HANA connection details correctly during report generation.

### 4.3 Missing Data in PO PDF Reports

**Issue:** Some PO PDFs were generated with complete data, while others were generated without the expected values.

**Resolution:**

* Investigated the report templates and identified that separate `.rpt` files were maintained for normal vendors and subcontracting vendors.
* Coordinated with the functional team to understand the differences between the report templates and their business requirements.
* Adjusted the report selection and generation logic according to the appropriate vendor category.

### 4.4 Document Date and Server Downtime Handling

**Issue:** The application initially used the current document date to identify documents for email processing. If the server was unavailable during the scheduled execution, documents created before the next successful run could be missed.

**Resolution:**

* Investigated the date-based document selection logic.
* Tested the processing logic using a hardcoded document date to validate the issue.
* Identified the need for a more reliable date-handling mechanism to avoid missing documents during server downtime.

**Note:** For a robust production implementation, a configurable date range or last-processed timestamp is preferable to a permanently hardcoded date, as it allows missed documents to be recovered without repeatedly processing unrelated records.

## 5. Testing and Deployment

* Built the application and deployed the executable to the test environment.
* Configured Windows Task Scheduler to execute the application automatically.
* Tested PO and AR Invoice PDF generation and email notifications against the test database.
* Verified the email functionality and document output with end users.
* Resolved the issues identified during testing.
* After receiving end-user confirmation, deployed the application to the live environment.

## 6. Project Outcome

* Automated email notifications for Purchase Orders and AR Invoices.
* Enabled PDF generation and email delivery using Crystal Reports.
* Implemented document email status tracking through SAP Business One UDFs.
* Improved control over PO email processing based on GRPO-related conditions.
* Reduced manual effort involved in distributing business documents to vendors and customers.
* Implemented scheduled execution and validated the solution with end users before live deployment.

## 7. Key Technical Contributions

* SAP Business One add-on and database integration using C# and SAP HANA.
* Crystal Reports PDF generation and troubleshooting.
* Stored procedure modification for document status control.
* SAP UDF creation and update.
* Automated email delivery with PDF attachments.
* Troubleshooting database connectivity, assembly compatibility, and report template issues.
* Test environment validation, Task Scheduler configuration, and production deployment.
