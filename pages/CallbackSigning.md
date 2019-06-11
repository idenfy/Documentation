# Callback signing

Callback signing is a simple method to secure your callback endpoints from
foreign requests.

To check callbacks you need to compute SHA-256 HMAC of content with API secret
as a key, and compare that with `Idnefy-Signature` header.

For example if your code previously looked like this:
```python
@app.route('/idenfy-callback)
def callback():
    handle_request(request)

```

It should now look like this:

```python
import hmac

API_SECRET = "Agegb..." 

@app.route('/idenfy-callback)
def callback():
    signature = hmac.new(
        API_SECRET.encode(),
        request.get_data(),
        "sha256"
    ).hexdigest()
    request_signature = request.headers.get("Idenfy-Signature")
    if request_signature:
        if hmac.compare_digest(signature, request_signature):
            handle_request(request)
```

Note: You should not use standard `==` operator to avoid timing attacks. You
should use hmac.compare_digest or equivalent constant time string comparison.