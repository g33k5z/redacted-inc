
### client-invoice-amounts
```sql
-- client-invoice-amounts
SELECT
  Client.Name,
  SUM(Invoice.TotalAmount) AS TotalInvoiced
FROM
  `msds-demos.redacted_inc.clients` Client
JOIN
  `msds-demos.redacted_inc.invoices` Invoice
ON
  Client.ID = Invoice.ClientID
GROUP BY
  Client.Name;
```

### document-review-status
```sql
-- document-review-status
SELECT
  Document.ID,
  Document.DocumentType,
  Document.SubmissionDate,
  Review.ApprovalStatus
FROM
  `msds-demos.redacted_inc.documents` Document
JOIN
  `msds-demos.redacted_inc.reviews` Review
ON
  Document.ID = Review.DocumentID;
```

### invoice-payments
```sql
-- invoice-payments
SELECT
  Invoice.ID AS InvoiceID,
  Client.Name AS ClientName,
  Payment.PaymentDate,
  Payment.Amount,
  Payment.PaymentMethod
FROM
  `msds-demos.redacted_inc.payments` Payment
JOIN
  `msds-demos.redacted_inc.invoices` Invoice
ON
  Payment.InvoiceID = Invoice.ID
JOIN
  `msds-demos.redacted_inc.clients` Client
ON
  Invoice.ClientID = Client.ID;
```

### overdue-invoices
```sql
-- overdue-invoices
SELECT 
    Client.Name,
    Invoice.InvoiceDate,
    Invoice.DueDate,
    Invoice.TotalAmount
FROM 
    `msds-demos.redacted_inc.clients` Client
JOIN 
    `msds-demos.redacted_inc.invoices` Invoice 
    ON Client.ID = Invoice.ClientID
WHERE 
    Invoice.PaymentStatus = 'Overdue';

```

### pending-invoices
```sql
-- pending-invoices
SELECT
  Client.Name,
  Invoice.InvoiceDate,
  InvoiceItem.Description,
  InvoiceItem.Amount,
  InvoiceItem.Quantity,
  Invoice.TotalAmount,
  Invoice.PaymentStatus
FROM
  `msds-demos.redacted_inc.invoices` Invoice
JOIN
  `msds-demos.redacted_inc.clients` Client
ON
  Invoice.ClientID = Client.ID
JOIN
  `msds-demos.redacted_inc.invoiceitems` InvoiceItem
ON
  Invoice.ID = InvoiceItem.InvoiceID
WHERE
  Invoice.PaymentStatus = 'Pending';
```

### redaction-requests
```sql
-- redaction-requests
SELECT
  Document.DocumentType,
  Redaction.RedactionType,
  Redaction.Description,
  Redaction.Status
FROM
  `msds-demos.redacted_inc.documents` Document
JOIN
  `msds-demos.redacted_inc.redactions` Redaction
ON
  Document.ID = Redaction.DocumentID;
```





