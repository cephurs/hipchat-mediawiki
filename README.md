This is an extension for MediaWiki that sends notifications into a HipChat room.

## License

MIT (http://en.wikipedia.org/wiki/MIT_License)

## Supported MediaWiki operations to send notifications

- When article is added.
- When article is removed.
- When article is edited.
- When new user is added.
- When user is blocked.

## Requirements

- cURL
- MediaWiki 1.8+ (only tested with as low as version 1.8)
- Apache should have NE (NoEscape) flag on to prevent issues in URLs. By default this is enabled. Check this thread for more information: https://github.com/kulttuuri/hipchat_mediawiki/issues/8

## How to install

1. Send folder HipchatNotifications into your `mediawiki_installation/extensions` folder.
2. Add these settings in your `LocalSettings.php`:

		require_once("$IP/extensions/HipchatNotifications/hipchat_notifications.php");
		// HipChat API token. Create or view your API keys here: https://hipchat.com/admin/api
		$wgHipchatToken = "";
		// HipChat room ID where you want all the notifications to go into. 
		// You can get the room ID by visiting https://api.hipchat.com/v1/rooms/list?format=xml&auth_token=YOUR_AUTH_TOKEN
		// (replace YOUR_AUTH_TOKEN in the end with your own API key, must be an admin api key)
		$wgHipchatRoomID = ;
		// Required. Name the message will appear be sent from. Must be less than 15 characters long. May contain letters, numbers, -, _, and spaces.
		$wgHipchatFromName = "Wiki";
		// URL into your MediaWiki installation with the trailing /.
		$wgWikiUrl		= "http://your_wiki_url/";
		// Wiki script name. If you have URL shortening turned on like Wikipedia you will need the leading `w/`
		$wgWikiUrlEnding = "w/index.php?title=";

3. Enjoy the notifications in your HipChat room!


## Additional Hipchat options

#### Trigger notification
Whether or not this message should trigger a notification for people in the room (change the tab color, play a sound, etc). Each recipient's notification preferences are taken into account.

	$wgHipchatNotification = true;

#### API URL
URL to HipChat rooms/message sent script. Mostly just leave to default value.

	$wgHipchatRoomMessageApiUrl = "https://api.hipchat.com/v1/rooms/message";

#### MediaWiki actions 
Options for what will be sent notifications of into HipChat. Set desired options to false to disable notifications of those actions.

	// New user added into MediaWiki
	$wgHipchatNotificationNewUser = true;
	// User or IP blocked in MediaWiki
	$wgHipchatNotificationBlockedUser = true;
	// Article added to MediaWiki
	$wgHipchatNotificationAddedArticle = true;
	// Article removed from MediaWiki
	$wgHipchatNotificationRemovedArticle = true;
	// Article edited in MediaWiki
	$wgHipchatNotificationEditedArticle = true;
	// File uploaded
	$wgHipchatNotificationFileUpload = true;
	
## Additional MediaWiki settings
### URL endings

	$wgWikiUrlEndingUserRights          = "Special%3AUserRights&user=";
	$wgWikiUrlEndingBlockUser           = "Special:Block/";
	$wgWikiUrlEndingUserPage            = "User:";
	$wgWikiUrlEndingUserTalkPage        = "User_talk:";
	$wgWikiUrlEndingUserContributions   = "Special:Contributions/";
	$wgWikiUrlEndingBlockList           = "Special:BlockList";
	$wgWikiUrlEndingEditArticle         = "action=edit";
	$wgWikiUrlEndingDeleteArticle       = "action=delete";
	$wgWikiUrlEndingHistory             = "action=history";