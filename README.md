# MyneLeaks
MCLeaks and VPN detection service API reference 

## Version 1 Endpoints

**Base URL:** `https://resolve.mynepanel.com/api/v1/<query>?key=<apikey>`

**Method:** `GET`

**Check:**

[`/check/name/<name>`](#check-for-leaked-account)\
[`/check/uuid/<uuid>`](#check-for-leaked-account)\
[`/check/ip/<ip>`](#check-for-vpn-address)

**Resolve:**

[`/resolve/name/<name>`](#get-uuid-for-name)\
[`/resolve/uuid/<uuid>`](#get-name-for-uuid)\
[`/resolve/case/<name>`](#get-correct-case)

**Submit:**

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
		"message": "",
		"reason": "InvalidAPIVersion"
	},
	"success": false
}
```


## Check For Leaked Account

Returns whether the supplied account is in the leaked database

**Path:** `/check/name/<name>` or `/check/uuid/<uuid>`

**Response:**

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

**Response:**

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

**Path:** `/resolve/name/<name>`

**Response:**

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

**Path:** `/resolve/uuid/<uuid>`

**Response:**

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

**Path:** `/resolve/case/<name>`

**Response:**

```json
{
	"result": {
		"name": "CraftyMyner"
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

Returns your quota, requests and plan status

**Path:** `/client/plan/`

**Note:** Requests/Quota array represents:
```json
["minute","hour","day","month"]
```

**Response (Free Plan):**

```json
}
	"result": {
		"expiry": 0.0,
		"plan": "Free",
		"quota": [10, 100, 1000, 10000],
		"requests": [7, 34, 145, 983]
	},
	"success": true
}
```

**Response (Paid Plan):**

```json
}
	"result": {
		"expiry": 0.0,
		"plan": "Standard",
		"quota": [50, 500, 5000, 50000],
		"requests": [49, 456, 789, 8932]
	},
	"success": true
}
```

## API rate limits and aquiring an API Key:

The rate limits set for free users is 10k requests per month (10 per minute, 100 per hour, 1000 per day). If you need to make more requests, you can aquire an API key from me at [owner@craftymynes.com](owner@craftymynes.com)

##
