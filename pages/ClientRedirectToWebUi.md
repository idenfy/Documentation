# Client redirect to WEB UI

After successfully generating token you should have a valid **authToken** which looks similar to this *"3FA5TFPA2ZE3LMPGGS1EGOJNJE"*.

### Redirect action

You may initiate a HTTP redirect action for your client to [https://ivs.idenfy.com/api/v2/redirect]() by appending a generated token as a url query string parameter.

<center>

|Redirect URL                          |
|--------------------------------------|
|https://ivs.idenfy.com/api/v2/redirect|

|Query string parameter name           |Example value               |
|--------------------------------------|----------------------------|
|`authToken`                           |`3FA5TFPA2ZE3LMPGGS1EGOJNJE`|

</center>

### Examples

An example redirect url looks like this:<br>https://ivs.idenfy.com/api/v2/redirect?authToken=3FA5TFPA2ZE3LMPGGS1EGOJNJE

#### PHP example

```php
<?php
  header("Location: https://ivs.idenfy.com/api/v2/redirect?authToken=3FA5TFPA2ZE3LMPGGS1EGOJNJE");
  exit;
?>
```

#### Python Flask example

```python
from flask import Flask, redirect

app = Flask(__name__)

@app.route('/')
def redirect_to_idenfy():
    return redirect("https://ivs.idenfy.com/api/v2/redirect?authToken=3FA5TFPA2ZE3LMPGGS1EGOJNJE", code=302)
```