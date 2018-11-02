## basic usage tutorial

The Ansible script already provides a basic setup of both a Keycloak realm and client as well as a Tyk API gateway secured using Keycloak as a OpenID Connect provider.

The following steps assume both Keycloak and Tyk have been installed on localhost, a default realm "jetRealm" has been created with a "jetClient" inside, as well as a Tyk API gateway endpoint named "jetapi" has been created.

## 1. Registering a new realm account

Simply go to the following url:
```
http://127.0.0.1:8080/auth/realms/jetRealm/account
```
And click the _registration_ button found on the bottom of the page.
Fill out the requested information and click register.

Lets assume we have made the following user password combination:
```bash
username: admin
password: password
```

## 2. Retrieving the client-secret

In order to authenticate yourself to our OpenID endpoint we need to retrieve the client-secret for the jetClient we have created in Keycloak.

Log into Keycloak and go to the following URL:
```
http://127.0.0.1:8080/auth/admin/master/console/#/realms/jetRealm/clients
```

Select _jetClient_, select the tab _credentials_ and save the value of the _secret_ field somewhere so we can use it later.
Lets assume for this example our client-secret is the following:
```bash
client-secret: 70c4cd88-dd2a-43ba-9e16-ff4560cd049f
```

## 3. Retrieving the oAuth Bearer token

Now that we have everything we need, we can ask KeyCloak to give us a Bearer token that we can use to authenticate ourselves to our API endpoint.

Using curl, the request will look like the following:

```bash
curl \
  -d "client_id=jetClient" \
  -d "client_secret=70c4cd88-dd2a-43ba-9e16-ff4560cd049f" \
  -d "username=admin" \
  -d "password=admin" \
  -d "grant_type=password" \
  "http://127.0.0.1:8080/auth/realms/jetRealm/protocol/openid-connect/token"
  ```

This request should return a json response formatted like below (the access token has been truncated for clarity):
```json
{
  "access_token": "eyJhbGciOiJ...",
  "expires_in": 300,
  "refresh_expires_in": 1800,
  "refresh_token": "eyJhbGciOiJ...",
  "token_type": "bearer",
  "not-before-policy": 0,
  "session_state": "ac66d762-ef96-40f0-870e-d1d562f7e103",
  "scope": "profile email"
}
```

Extract the *access_token* field and we can move on to actually talking to our API.

## 4. Accessing the API

Now that everything is in place, we can finally send a request to our API.
All we need to do is use the access token we have gotten in the previous step and use it as a bearer token. Tyk will validate this token with Keycloak, and, assuming the token is correct, will give you the requested output.

Again, in curl, the command is the following:

```bash
curl --request GET \
  --url http://127.0.0.1:8081/jetapi/posts \
  --header 'authorization: Bearer eyJhbGciOiJ...'
  ```
