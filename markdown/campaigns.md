# Managing campaigns 

This topic describes creating, launching and monitoring campaigns.

Campaigns are the way your organization enlists its contacts to respond to requests for new or updated data about themselves. You manage these events on the <madcap:variable name="bes.Campaigns page"></madcap:variable> page. It has two sections:

*   My Campaigns lists all campaigns created. Campaigns on the list can be run once or multiple times.
*   Campaign History lists campaigns in progress and completed. A campaign is in progress until the specified end time is reached. A campaign is completed once the configured running time has expired. If contacts respond after time expires, their replies are tabulated even after the status has changed to completed.

## Limitations in this technical preview

The following are limitations of campaigns in this technical preview release.

*   A campaign cannot be edited or deleted.
*   As campaigns cannot be edited or deleted, best practice is to add only campaigns you intend to run. However, there is no limit on the number of campaigns you can add.
*   You can target only all unvalidated or all validated contacts for a campaign. There is no fine-grained selection of contacts as targets.
*   Campaign history only lists data for the last 10 campaigns launched.

## Create a campaign

Click **Create Campaign** to launch the campaign wizard and follow the prompts to add a campaign. The following describes some aspects of adding a campaign.

*   You can specify campaign duration in minutes only, up to 43,200 minutes (720 hours or 30 days). As this is a technical preview release, specifying duration in minutes enables running brief campaigns for tests or demonstrations.
*   Enter only plain text in the subject line and body of the email message. Use of variables is not supported. However, when <madcap:variable name="bes.BES abbreviation"></madcap:variable> sends the message to the contact, it inserts the salutation "Dear [contact first name]." Upon sending, <madcap:variable name="bes.BES abbreviation"></madcap:variable> also appends the message with a button the recipient clicks to open a form in a browser to complete and submit.

Once you click **Save Campaign**, your campaign is listed under My Campaigns. The campaign is ready to launch.

## Launch a campaign

Click **Launch** to start a campaign on the My Campaigns list. Click **Yes** when prompted. If launched successfully, a message is displayed indicating the campaign is live. <madcap:variable name="bes.BES abbreviation"></madcap:variable> sends the campaign's email message to all targeted contacts.

## Monitor a campaign

Follow the status of in-progress and completed campaigns under the Campaign History section.