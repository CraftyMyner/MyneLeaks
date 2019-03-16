# MyneLeaks
MCLeaks and VPN detection service API reference 

## Version 1 Endpoints

**Base URL:** `https://resolve.mynepanel.com/api/v1/<query>?key=<apikey>`

**Method:** `GET`

**Check:**

[`/check/name/<name>`](#check-for-leaked-account)\
[`/check/uuid/<uuid>`](#check-for-leaked-account)\
[`/check/ip/<ip>`](#check-for-vpn-address)

**Lookup:**

[`/lookup/name/<name>`](#get-uuid-for-name)\
[`/lookup/uuid/<uuid>`](#get-name-for-uuid)\
[`/lookup/case/<name>`](#get-correct-case)\
[`/lookup/alts/<value>`](#lookup-alts)

**Submit:**

[`/submit/login/<uuid>/<address>`](#submit-player-login)
[`/submit/token/<token>`](#submit-mcleaks-token)

**Client:**

[`/client/plan/`](#get-plan-details)


## Sample Success

**Code:** `200 OK`

```json
{
	"result": {
		"leaked": true
	},
	"success": true
}
```


## Sample Error

**Code:** `400 BAD REQUEST`

```json
{
	"result": {
		"message": "The API method supplied is invalid!",
		"reason": "InvalidAPIVersion"
	},
	"success": false
}
```


## Check For Leaked Account

Returns whether the supplied account is in the leaked database

**Path:** `/check/name/<name>` or `/check/uuid/<uuid>`

**Example:** `/check/name/JohnDoe` or `/check/uuid/c4c28f77-f21f-430c-a4e5-2271ad93e69e`

```json
{
	"result": {
		"leaked": true
	},
	"success": true
}
```

## Check For VPN Address

Returns whether the supplied account is in the VPN database

**Path:** `/check/ip/<ip>`

**Example:** `/check/ip/193.251.76.9`

```json
{
	"result": {
		"vpn": true
	},
	"success": true
}
```

## Get UUID for Name

Returns the UUID for the Minecraft Name

**Path:** `/lookup/name/<name>`

**Example:** `/lookup/name/CraftyMyner`

```json
{
	"result": {
		"uuid": "81c99f50-ff1a-480b-ae85-2792af98edae"
	},
	"success": true
}
```

## Get Name for UUID

Returns the UUID for the Minecraft Name

**Path:** `/lookup/uuid/<uuid>`

**Example:** `/lookup/uuid/81c99f50-ff1a-480b-ae85-2792af98edae`

```json
{
	"result": {
		"name": "CraftyMyner"
	},
	"success": true
}
```


## Get Correct Case

Returns the correct case for a Minecraft Name

**Path:** `/lookup/case/<name>`

**Example:** `/lookup/case/cRaFtYmYnEr`

```json
{
	"result": {
		"name": "CraftyMyner"
	},
	"success": true
}
```


## Lookup Alts

Returns the alts for the supplied Name, UUID or IP Address along with Leaked and VPN results.

NOTE: You must have alt lookup enabled on your plan to have access to this feature.

**Path:** `/lookup/alts/<value>`

**Example:** `/lookup/alts/JonDoe`

```json
{
	"result": {
		"uuids": {
			"c4c28f77-f21f-430c-a4e5-2271ad93e69e": 1,
			"54f28671-e51e-430d-a4e5-7871af13e62f": 2
		},
		"ips": {
			"166.13.48.168": 1,
			"54.241.129.53": 2
		},
		"names": {
			"c4c28f77-f21f-430c-a4e5-2271ad93e69e": "JonDoe",
			"54f28671-e51e-430d-a4e5-7871af13e62f": "Jane"
		},
		"leaked": {
			"54f28671-e51e-430d-a4e5-7871af13e62f": true
		},
		"vpns": {
			"54.241.129.53": true
		}
	},
	"success": true
}
```

## Submit Player Login

To resolve players alt's, you must submit players UUID's and IP's. These will be used to correlate players accounts to IP addresses.

**Path:** `/submit/login/<UUID>/<Address>`

**Example:** `/submit/login/c4c28f77-f21f-430c-a4e5-2271ad93e69e/166.13.48.168`

**Response:**

```json
{
	"result": {	
	},
	"success": true
}
```

## Submit MCLeaks Token

We rely on users submitting tokens from [https://mcleaks.net/](https://mcleaks.net/) to build our database of leaked accounts. By solving the captcha and submitting tokens to the service, you will be rewarded by having your rate limit cleared.

**Path:** `/submit/token/<token>`

**Response:**

```json
{
	"result": {
		"name": "drking12"
	},
	"success": true
}
```


## Get Plan Details

Returns your quota, requests and plan expiry in seconds

**Path:** `/client/plan/`

**Response (Free Plan):**

```json
}
	"result": {
		"plan": "Free",
		"quota": {"daily": 1000, "yearly": 10000},
		"requests": {"daily": 145, "yearly": 983}
	},
	"success": true
}
```

**Response (Paid Plan):**

```json
}
	"result": {
		"expiry": 15062.54212,
		"plan": "Standard",
		"quota": {"daily": 1000, "monthly": 10000},
		"requests": {"daily": 145, "monthy": 983}
	},
	"success": true
}
```

## API rate limits and aquiring an API Key:

The rate limits set for free users is 1k requests per day (10k per month). If you need to make more requests, you can aquire an API key from me at [owner@craftymynes.com](owner@craftymynes.com)

##
