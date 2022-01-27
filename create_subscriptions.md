# playtomic: create subscriptions

## [Optional] Backend: Create a Customer

This step creates a customer with a test Payment Method and sets a default Payment Method that will be used for new subscriptions. 

If the default Payment Method is not set, you need to mention it in the subscription creation. 

```bash
curl -X POST "https://api.stripe.com/v1/customers" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY': 
```

## Backend: Create a Subscription

You will need to use the following parameters: 
- on_behalf_of
- transfer_data[destination]
- application_fee_percent

```bash
curl -X POST "https://api.stripe.com/v1/subscriptions" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY':  \
  -d customer="cus_L2aYMaSHY2dGhk" \
  -d on_behalf_of="acct_1KMKhT4IjuvCUDVm" \
  -d application_fee_percent=5 \
  -d transfer_data[destination]="acct_1KMKhT4IjuvCUDVm" \
  -d items[0][price]="price_1J0isuKSM3YgOnvFsN7Whte9" \
  -d payment_behavior="default_incomplete"
```

```bash
curl "https://api.stripe.com/v1/invoices/{invoice}" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY': 
```

```bash
curl "https://api.stripe.com/v1/payment_intents/{intent}" \
  -u 'REPLACE_WITH_YOUR_SECRET_KEY': 
```
