# Payment Webservice for Dolibarr

This is a simple script to create payments using the Dolibarr SOAP API.

## Usage

	$client = new \nusoap_client("https://your.crm/webservices/server_payment.php");
	$ns = 'http://www.dolibarr.org/ns/';
	$auth = array(
        "dolibarrkey"       => "abcdef",
        "login"             => "username",
        "password"          => "p455w0rD",
        "sourceapplication" => "MyWonderfulApp",
        "entity"            => "1"
    );
    
    $payload = array(
    	"amount"          => 123.45,
    	"invoice_id"      => 123,
    	"payment_mode_id" => 123,
    	"thirdparty_id"   => 123,
    	"num_paiement"    => "",
    	"bank_account"    => 1,
    	"int_label"       => "CB123456",
    	"bank_source"     => "LCL",
    	"emitter"         => "John Doe"
	);
    
    $response = $client->call('createPayment', array("authentication" => $auth, "payment" => $payload), $ns, '');
    
### Request

Field | Type | Description
----- | ---- | -----------
`amount` | double | The payment's amount
`invoice_id` | integer | The ID of the invoice you want to pay
`payment_mode_id`| integer | ID of the payment method (see DB table `llx_c_paiement`)
`thirdparty_id`| integer | ID of the third party emitting the payment
`num_paiement`| string | Label used on the customer's invoice (payment reference)
`bank_account`| integer | ID of the bank account to report the writing on
`int_label` | string | Internal label used in the "Bank" section of Dolibarr
`bank_source`| string | The bank emitting the payment (i.e. your customer's bank)
`emitter` | string | Your customer's name

## Compatibility

Dolibarr Version | Hosting Provider | Status
---------------- | --------- | ------
3.9.1			 | [O2Switch](http://www.o2switch.net) | OK

Feel free to edit this list :-) ...

## Disclaimer

This element is provided **as is**. I created this project to add a missing function I needed in the SOAP API. If you have any issue with it, I will try to help whenever I can. Do not hesitate to fill in an issue on GitHub to explain your issue. 

## FAQ

**Why using the SOAP API when Dolibarr provides now a JSON/REST API?**

This is a question I asked to myself at the premises of the project. At the moment, the REST API looks more like a draft, a PoC, rather than a reliable solution. Also, it really lacks of a structured documentation.
