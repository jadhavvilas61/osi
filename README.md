String paytmChecksum = OMSAI INTERNET ;

/* Create a TreeMap from the parameters received in POST */
TreeMap<String, String> paytmParams = new TreeMap<String, String>();
for (Entry<String, String[]> requestParamsEntry : request.getParameterMap().entrySet()) {
    if ("CHECKSUMHASH".equalsIgnoreCase(requestParamsEntry.getKey())){
        paytmChecksum = requestParamsEntry.getValue()[0];
    } else {
        paytmParams.put(requestParamsEntry.getKey(), requestParamsEntry.getValue()[0]);
    }
}

/**
* Verify checksum
* Find your Merchant Key in your Paytm Dashboard at https://dashboard.paytm.com/next/apikeys 
*/
boolean isValidChecksum = CheckSumServiceHelper.getCheckSumServiceHelper().verifycheckSum("YOUR_KEY_HERE", paytmParams, paytmChecksum);
if (isValidChecksum) {
	System.out.append("Checksum Matched");
} else {
	System.out.append("Checksum Mismatched");
}
JSON Response
Pass complete response body as a string to the checksum utility to validate checksum.

JAVA
NODE
PHP
PYTHON
.NET
/* string we need to verify against checksum */
String body = "{\"mid\":\"YOUR_MID_HERE\",\"orderId\":\"YOUR_ORDER_ID_HERE\"}";

/* checksum that we need to verify */
String checksum = "CHECKSUM_VALUE";

/**
* Verify Checksum
* Find your Merchant Key in your Paytm Dashboard at https://dashboard.paytm.com/next/apikeys 
*/
boolean isValidChecksum = CheckSumServiceHelper.getCheckSumServiceHelper().verifycheckSum("YOUR_KEY_HERE", body, checksum);
if (isValidChecksum) {
    System.out.append("Checksum Matched");
} else {
    System.out.append("Checksum Mismatched");
