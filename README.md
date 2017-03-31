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