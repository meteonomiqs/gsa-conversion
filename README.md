# {TODO: PRODUCT NAME} - conversion tag

Google Tag Manager (GTM) Solution for improving Google Search adwords conversions using high quality weather
provided by https://wetter.com

The solution consists of two tags:
* the adwords tag, see https://github.com/meteonomiqs/gsa-adwords
* this conversion tag

** Note: To be able to use this solution you must register for an API key at {TODO: landing page}**


## Setup

We describe how weather is integrated into Google Ads. The overall idea is to use Google Tag Manager and Google Ads with Smart Bidding to improve the performance of the campaigns.

The installation and configuration consists of the following steps

### Step 1: Setup Google Ads {TODO: exact wording?}
In Google Ads, go to Tools & Settings / Measurement / Conversions.
Create 5 new conversion actions (e.g. good, decent, bad, unknown and weather_test), 4 are used as weather conversions and one conversion (weather_test) is for the AB-test.
The setting for each conversion should fit your business and can be used from your already used conversions.
In case you do not have a conversion, you can use the following set of parameters:
- Value: Use different values for each conversion
- Count: Every
- Click-through conversion window: 7 days
- Engaged-view conversion window: 3 days
- View-through conversion window: 1 day
- Attribution model: Linear

In the Tag setup select Use Google Tag Manager. Write down the conversion labels for each conversion action and the Conversion ID:
good: ZAB12CDefg....
decent: YAB12CDefg....
bad: XAB12CDefg....
unknown: WAB12CDefg....
weather_test: VAB12CDefg....
Conversion ID: 123456789

Create a new custom goal ("weather_conversion") by selecting the 4 weather conversion actions.

### Step 2: Register at {TODO: landing page}
Register on Meteonomiqs by providing the Conversion ID and the 5 conversion labels.

### Step 3: Integrate with your Consent Management
<- Dhivya for details

### Step 4: Configure adwords tag
Add the adwords template to your Google Tag Manager.
<- Dhivya for details

### Step 5: Configure conversion tag
Add the conversion template similar to your current conversion tracking in Google Tag Manager. For testing, we recommend to keep the current conversion tracking.
<- Dhivya for details

## Usage
In Google Ads open an existing campaign or create a new one.
Create an AB-Test for this campaign by clicking on Show more and select Drafts & Experiments.
In Campaign drafts, create a new draft and then create a new experiment based on the draft.
Finally select in Settings the Goals of the campaign to weather_test (for the reference group) and to weather_test (for the test group) and start the test.
