# Aerobatic form-submit plugin demo

See this demo live at [https://form-submit-demo.aerobatic.io](https://form-submit-demo.aerobatic.io). Read the complete [form-submit plugin docs](https://www.aerobatic.com/docs/plugins/form-submit).

### Running this demo yourself

* Clone this repo
* From root of repo run `aero create -n your-site-name`
* Visit [https://www.google.com/recaptcha/admin](https://www.google.com/recaptcha/admin) and register a reCAPTCHA. In the **Domains** box, enter `aerobatic.io`.
* Expand the **Keys**, copy the **Site key**, and paste into both `standard-form.html` and `ajax-form.html` here:
  ~~~html
  <div class="g-recaptcha"
    data-sitekey="PASTE HERE"
    data-callback="recaptchaOnSubmit"
    data-size="invisible">
  </div>
  ~~~
* Copy the **Secret key** and use the value to run:
  ~~~sh
  aero env -n RECAPTCHA_SECRET_KEY -v <your secret>
  ~~~
* Uncomment the email target section in `aerobatic.yml` and replace the test email with your own.
  ~~~yaml
  targets:
    email:
      subject: Demo contact-form submission
      recipients: [your-email@email.com]
  ~~~
* Run `aero deploy` and wait for it to complete
* Go see your site at `https://your-site-name.aerobatic.io`
* Fill out the form and you should receive an email with the form values.

## Testing the Google Sheets integration
* Create an account on Zapier and login
* Create a new Zap and select "Webhooks by Zapier" as the trigger.
* Copy the provided webhook URL and set it as an environment variable using the command:
  ~~~sh
  aero env set -n ZAP_GSHEET_WEBHOOK_URL -v <YOUR_WEBHOOK_URL>
  ~~~
* Make sure the following section is uncommented in your `aerobatic.yml`:
  ~~~yaml
  targets:
    - name: webhook
      url: $ZAP_GSHEET_WEBHOOK_URL
  ~~~
* In Zapier, click "Ok, I did this" to advance to the test step. Zapier will wait for an incoming webhook to confirm the integration is working.
* To test it out, deploy your site with `aero deploy` and submit the form with some test inputs. Back in Zapier, it should report that the test action was received successfully.
* Now you can configure the Google Sheet you want to add new rows to. Link your Google account to Zapier, then proceed to the next step where you select the Google Sheets document and Worksheet.
* Then you can determine how the columns in your spreadsheet will be bound to the data fields in the webhook body. Aerobatic appends several `X-` fields with additional metadata including the submitted date, the end user's IP address, and approximate physical location.
* Finish out the Zapier wizard including proving a name for your integration and turning your Zap to the "ON" state.
* Now every form submission on your Aerobatic contact form will automagically show up in Google Sheets!
