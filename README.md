# WeatherTag4Search - conversion tag

**THIS SOLUTION IS CURRENTLY IN CLOSED BETA**

Google Tag Manager (GTM) Solution for improving Google Search adwords conversions using high quality weather
provided by https://wetter.com

The solution consists of two tags:
* the adwords tag, see https://github.com/meteonomiqs/gsa-adwords
* this conversion tag

**Note: To be able to use this solution you must register for an API key at {TODO: landing page}**


## Setup

We describe how weather is integrated into Google Ads. The overall idea is to use Google Tag Manager and Google Ads with Smart Bidding to improve the performance of the campaigns.

The installation and configuration consists of the following steps

### Step 1: Setup Google Ads 
In Google Ads, go to `Tools & Settings / Measurement / Conversions`.
Create 5 new conversion actions (e.g. good, decent, bad, unknown and weather_test), 4 are used as weather conversions and one conversion (base_test) is for the AB-test.
The setting for each conversion should fit your business and can be replicated from your already used conversions.
In case you do not have a conversion, you can use the following set of parameters:
- Value: Use different values for each conversion
- Count: Every
- Click-through conversion window: 7 days
- Engaged-view conversion window: 3 days
- View-through conversion window: 1 day
- Attribution model: Linear

In the Tag setup select `Use Google Tag Manager`. Write down the `conversion labels` for each `conversion action` and the `Conversion ID`:
- good: ZAB12CDefg....
- decent: YAB12CDefg....
- bad: XAB12CDefg....
- unknown: WAB12CDefg....
- weather_test: VAB12CDefg....
- Conversion ID: 123456789

Finally create a `new custom goal` ("weather_conversion") by selecting the 4 weather conversion actions.

### Step 2: Register at {TODO: landing page}
Register on Meteonomiqs by providing the `Conversion ID` and the 5 conversion labels.

### Step 3: Integrate with your Consent Management

What we need consent for:
* The tag sends the Google ClickId from an AdWords click to our backed
* From the request, the IP address is used to derive the location (latitude, longitude) for determining the weather at that location. Then the IP address is discarded
* Google ClickId, location, weather information, and timestamp are stored in our backend
* In case of a later conversion, another request with the Google ClickId and a conversion value is send to our backend, the weather information
* Google ClickID, conversion value and original weather information are sent to Google AdWords and stored in our backend
#### CMP configuration

An easy way is to add wetter.com Gmbh (meteonomiqs is a brand of wetter.com GmbH) as non IAB Vendor to your CMP (TCF2.0).

* Description: **If a user clicks on a Google ad and lands on the customer page, we determine the weather at the location derived from the IP address. If later a conversion happens, the conversion value is sent together with the original weather information to Google AdWords.
  Google ClickID, conversion value and original weather information are sent to Google AdWords and stored in our backend for the retention period defined during registration plus 10 days grace period.**
* Name of processing company: **meteonomiqs.com  / wetter.com  GmbH**
* Address of processing company: **Reichenaustr. 19a, 78467 Konstanz**
* Puposes: **Weather based conversion improvements**
* Data Collected: **Location based on the IP address, Google Click ID, Conversion Value**
* Technologies Used: **server-side storage: AWS DynamoDB**
* Cookie URL: **-**
* Location of Processing: **European Union**
* Retention Period
  * Cookie: **no cookie is set**
  * Server-side: **Google ClickId, weather, location, conversion value, and timestamp: as defined during registration + 10 days grace period** 
* Policy of Procesor : **Data privacy https://www.meteonomiqs.com/data-privacy/**
* Data Protection Officer: **datenschutz@wetter.com**
* Storage information: **-**

If you are using a CMP prior to TCF2.0 or some other consent solution, please include the above information in your privacy statement as needed.

#### Tag configuration for respection user consent

@Dhivya: PLEASE FILL IN HERE


### Step 4: Configure adwords tag

Import the Adwords template manually or from the solutions gallery. Click on 'Save'.



Create a new tag. Choose the above template which will be available under the custom section. Provide the API key you received during registration. Choose the tag firing option to 'Once per page'. Do not add any trigger at this point. Name the tag as 'Search Weather Tag' and click on Save.



Create a new tag. Choose the tag type as 'Conversion linker'. A Conversion linker tag is used to detect the ad click information in your conversion page URL. Fire this tag on any page where your visitors may land after they click your ad or promotion. Leave the tag firing option to 'Once per event'. Click on tag sequencing and select 'Fire a tag after Conversion Linker fires' and add the 'Search Weather Tag' as the clean up tag. This ensures the 'Search Weather Tag' is fired immediately after the conversion linker tag is fired.



Note: If you have a consent management platform, ensure this tag is fired only when there is consent for Google Ads conversion tracking.

### Step 5: Configure conversion tag

Add the conversion template similar to your current conversion tracking in Google Tag Manager. For testing, we recommend to keep the current conversion tracking.

Import the conversion template manually or from the solutions gallery. Click on 'Save'.



Create a new tag. Choose the above template which will be available under the custom section. Provide the API key you received during registration. Provide the conversion value (eg. 1). Triggers for this tag should be added similar to your existing conversion tracking. 


## Usage
In Google Ads open an existing campaign or create a new one.
Create an AB-Test for this campaign by clicking on `Show more` and select `Drafts & Experiments`.
In Campaign drafts, create a new draft and then create a new experiment based on the draft.
Finally select in `Settings` the `Goals` of the campaign to base_test (for the reference group) and to weather_test (for the test group) and start the test.
