# Playtomic: Invoice the clubs

## (Optional) Create Customer

This Customer type corresponds to the club and will be used to invoice the application fees. 

```bash
curl -X POST "https://api.stripe.com/v1/customers" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY':  \
  -d description="Tenis Club" \
  -d name="Tenis Club"
```

## (Optional) Create a Tax Rate

```bash
curl -X POST "https://api.stripe.com/v1/tax_rates" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY':  \
  -d display_name="VAT" \
  -d inclusive="true" \
  -d percentage=21
```

## Generate Invoice

### Update Customer Invoice Items

We keep track of the Invoice Items at Customer level.
This step will be triggered by invoice.payment_succeeded.

```bash
curl -X POST "https://api.stripe.com/v1/invoiceitems" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY':  \
  -d customer="cus_L2aqitZYq9t4BX" \
  -d unit_amount=60 \
  -d currency="EUR" \
  -d description="Application fee for Membership" \
  -d quantity=3
```

### Update Customer Balance

We credit the Customer Balance with the total amount of the application_fee_amount.

```bash
curl -X POST "https://api.stripe.com/v1/customers/{customer}" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY':  \
  -d balance=-180
```

### Create Invoice

This step will create a draft invoice. With all the attached invoice items and customer balance.

```bash
curl -X POST "https://api.stripe.com/v1/invoices" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY':  \
  -d customer="cus_L2aqitZYq9t4BX" \
  -d default_tax_rates[0]="txr_1KMLxPKSM3YgOnvF0aKtNsax" \
  -d auto_advance="true" \
  -d collection_method="send_invoice" \
  -d days_until_due=0
```

### Finalize and send invoice

```bash
curl -X POST "https://api.stripe.com/v1/invoices/{invoice}/finalize" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY':  \
  -d auto_advance="true"
```

