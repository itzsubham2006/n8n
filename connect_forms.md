Steps -->

1. First setup the webhook and copy the URL, if you are using n8n on local machine, donot use that localhost:5678, use ngrok http 5678
it will give u some public URL expose to the internet use that.

2. Setup the google form, and click on 3 dot on upper right side and click 'App Script' and write this code


var POST_URL = "";

function onSubmit(e) {
  var form = FormApp.getActiveForm();
  var allResponses = form.getResponses();
  var latestResponse = allResponses[allResponses.length - 1];
  var response = latestResponse.getItemResponses();
  var payload = {};
  for (var i = 0; i < response.length; i++) {
    var question = response[i].getItem().getTitle();
    var answer = response[i].getResponse();
    payload[question] = answer;
  }

  var options = {
    "method": "post",
    "contentType": "application/json",
    "payload": JSON.stringify(payload)
  };
  UrlFetchApp.fetch(POST_URL, options);
}





and in var POST_URL,  paste the link of ngrok (for example = https://pushy-shirt-herring.ngrok-free.dev/webhook-test/cf09b45c-b4af-4f12-ba8e-a483d0f2f7c8)
for production donot use webhook-test, use 'webhook'

3. In App script, also add the triggers seting, onSubmit -> Head -> From form -> On form submit -> Notify me immediately