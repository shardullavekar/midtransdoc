# Introduction 

At Midtrans, we are committed to offer a seamless integration experience to our developers. 

We are happy to launch Devsupport AI - a bot programmer that integrates Midtrans with your code in few minutes.

At the end of this document, you will integrate Midtrans-SNAP on *Sandbox Environment*.

## What do I need?

* Client_Key

* Server_Key

Get both these keys from [Midtrans Dashboard](https://dashboard.sandbox.midtrans.com)

## PHP Integration

* Download the [Devsupport AI tool](https://github.com/artpar/devsupport/releases/latest). Install the .exe if you are on Windows, mac.zip if you are on Mac and .deb if you are on Linux. You should see a screen below:

![Installation Screen](img/screen1.png)

* Create a folder on your computer and create an index.php or index.html file in the folder.

* Open Devsupport AI tool and drop the folder in the tool when asked for.

* Search for Midtrans when asked for Product you'd like to integrate

* Click on Midtrans PHP Snap Integration

* Enter your Sandbox Client Key and Server Key & Proceed.   *If you enter wrong key combination, the tool will throw an error!*

* The tool will give you three files, which already have your credentials. Host them on your server and keep their URL ready.
	
	* Veritrans.php
	
	* checkout.php
	
	* handle_notification.php


* The tool will also provide you an HTML tag with which you can initiate a payment. The tag looks like this:

```
<button id="pay-button">Pay!</button>
<!-- TODO: Remove ".sandbox" from script src URL for production environment. Also input your client key in "data-client-key" -->
<script src="https://app.sandbox.midtrans.com/snap/snap.js" data-client-key="YOUR_CLIENT_KEY"></script>
<script type="text/javascript">
  document.getElementById('pay-button').onclick = function(){
    // This is minimal request body as example.
    // Please refer to docs for all available options: https://snap-docs.midtrans.com/#json-parameter-request-body
    // TODO: you should change this gross_amount and order_id to your desire. 
    var requestBody = 
    {
      transaction_details: {
        gross_amount: 123000,
        // as example we use timestamp as order ID
        order_id: 'T-'+Math.round((new Date()).getTime() / 1000) 
      }
    }
    
    getSnapToken(requestBody, function(response){
      var response = JSON.parse(response);
      snap.pay(response.token);
    })
  };
  /**
  * Send AJAX POST request to checkout.php, then call callback with the API response
  * @param {object} requestBody: request body to be sent to SNAP API
  * @param {function} callback: callback function to pass the response
  */
  function getSnapToken(requestBody, callback) {
    var xmlHttp = new XMLHttpRequest();
    xmlHttp.onreadystatechange = function() {
      if(xmlHttp.readyState == 4 && xmlHttp.status == 200) {
        callback(xmlHttp.responseText);
      }
    }
    xmlHttp.open("post", "YOUR_CHECKOUT_URL");
    xmlHttp.send(JSON.stringify(requestBody));
  }
</script>
```

*You can modify the amount and order Id as per your logic*


Voila! If everything went well, you can open the page where you copy pasted the HTML tag and test the payments.


## Android Integration

* Start the flow again and select Android Integration this time.

* Enter the client key and PHP checkout URL you configured earlier, and proceed. That's it! 


## Need help?

You can chat with us using the orange icon on the tool or write us an email at support@devsupport.ai - happy to help!