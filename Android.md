# Android

## Google Play Billing

<https://developer.android.com/google/play/billing/integrate>
<https://developer.android.com/google/play/billing/security#verify>

```python
from google.oauth2 import service_account

def verify_google_purchase(product_id: str, purchase_token: str):
    credentials = service_account.Credentials.from_service_account_file(
        ENV.SERVICE_ACCOUNT_FILE,
        scopes=["https://www.googleapis.com/auth/androidpublisher"],
    )

    base_url = "https://androidpublisher.googleapis.com/androidpublisher/v3/applications"
    url = f"{base_url}/{ENV.PACKAGE_NAME}/purchases/products/{product_id}/tokens/{purchase_token}"

    response = requests.get(
        url, headers={"Authorization": f"Bearer {credentials.token}"}
    )
    return response
```

```python
from google.oauth2 import service_account

def consume_google_purchase(product_id: str, purchase_token: str):
    credentials = service_account.Credentials.from_service_account_file(
        ENV.SERVICE_ACCOUNT_FILE,
        scopes=["https://www.googleapis.com/auth/androidpublisher"],
    )

    base_url = "https://androidpublisher.googleapis.com/androidpublisher/v3/applications"
    url = f"{base_url}/{ENV.PACKAGE_NAME}/purchases/products/{product_id}/tokens/{purchase_token}:consume"

    response = requests.get(
        url, headers={"Authorization": f"Bearer {credentials.token}"}
    )
    return response
```
