# CVE Monitor

Quick and dirty PHP script that checks [@cvenew](https://twitter.com/CVEnew/) 
stream for new tweets and relays them (cleaned up and pretty-fied) to a list 
of email recepients.

## How it works

When run, cvemon will:

* Fetch @cvenew stream using
[statuses/user_timeline](https://developer.twitter.com/en/docs/tweets/timelines/api-reference/get-statuses-user_timeline)
* For each new tweet it will
  * Lightly parse the tweet to get the CVE ID
  * Retrieve the page from cve.milre.org to get full CVE description
  * Format and send out the email
* Remember the last tweet it saw so to request only newer ones on the next run

## Dependencies

* PHP 5.6 and up, CLI version.
* [TwitterOAauth](https://github.com/abraham/twitteroauth) lib
* Consumer API keys from Twitter, requires opening a [dev account](https://dev.twitter.com) and creating an "app" there.

Tested on Debian distro of Linux only.

## Setting it up

1. Clone this and TwitterOAuth repos
2. Open cvemon.php and setup `the config` part as required.

In particular:

* Change `RECEPIENTS` to the email(s) that will receive CVE updates.
* Change `EMAIL_FROM` to what should be used for `From:` in these emails.
* Change `EMAIL_ALERT` to the email address that will get pinged with any problems.

* `INI_FILE` stores just the ID of the last processed tweet. Change its location if needed.
* `LOG_FILE` by default sits in `/var/log/` so make sure the script is run under the account that can write there.

* `TWITTER_OAUTH_PHP` should point at `oauth.php` from the TwitterOAuth repo.
* `TWITTER_API_...` should be set to "Consumer API keys" from "Keys and tokens" section of your Twitter app.

Then stick `php /path/to/cvemon.php` into your crontab and set it to run every hour. That's it.

## License

BSD, 2-clause

## Author

Alex Pankratov, https://swapped.cc

