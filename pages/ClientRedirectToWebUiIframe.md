# Client redirect to WEB UI

If you wish to have an iFrame implementation the approach is pretty similar.

After successfully generating token you should have a valid **authToken** which looks similar to this *"53dsPAquTfKJwnU0TT227BO09GWVCk3Zps5aZej8"*.

The iFrame has to point to the same redirection URL as if you were initiating an HTTP redirect action for your client to [https://ivs.idenfy.com/api/v2/redirect]() by appending a generated token as a url query string parameter. The redirection happens internally in the iFrame.

<center>

|Redirect URL|
|---|
|https://ivs.idenfy.com/api/v2/redirect|

|Query string parameter name|Example value|
|---|---|
|`authToken`|`53dsPAquTfKJwnU0TT227BO09GWVCk3Zps5aZej8`|

</center>


### Examples

An example redirect url:<br>https://ivs.idenfy.com/api/v2/redirect?authToken=53dsPAquTfKJwnU0TT227BO09GWVCk3Zps5aZej8

#### Example code

Example snippet for iFrame implementation with the redirection URL and [iFrame post messages](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage).

```html
<!DOCTYPE html>
<html>
  <body>
  
  <iframe 
    id='iframe' 
    style="width:80%; height:800px;" 
    src="https://ui.idenfy.com/api/v2/redirect?authToken=53dsPAquTfKJwnU0TT227BO09GWVCk3Zps5aZej8"
    allow="camera"
  ></iframe>
  
  <p id='display'></p>
  
  <script>
  window.addEventListener("message", receiveMessage, false);
    function receiveMessage(event) {
    console.log(event);
    // ...
  }
  </script>
  
  </body>
</html>
```
