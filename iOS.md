# iOS

## Purchase

<https://developer.apple.com/documentation/appstorereceipts/validating_receipts_on_the_device>
<https://medium.com/@ronaldmannak/how-to-validate-ios-and-macos-in-app-purchases-using-storekit-2-and-server-side-swift-98626641d3ea#:~:text=To%20validate%20in-app%20purchases%20on%20your%20server%20without,and%20Transaction%20signed%20data%20that%20your%20app%20obtains>

```python
from appstoreserverlibrary.signed_data_verifier import (
    SignedDataVerifier,
    VerificationException,
)

def verify_apple_transaction(signed_transaction: str):
    with open(ENV.CERTIFICATE_PATH, "rb") as f:
        root_cert = f.read()

    enable_online_checks = True
    bundle_id = ENV.BUNDLE_ID
    environment = ENV.ENVIRONMENT
    app_apple_id = ENV.APP_APPLE_ID
    signed_data_verifier = SignedDataVerifier(
        [root_cert], enable_online_checks, environment, bundle_id, app_apple_id
    )

    try:
        transaction = signed_data_verifier.verify_and_decode_signed_transaction(signed_transaction)
        return transaction.transactionId
    except VerificationException:
        return None
```
