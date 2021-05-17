# RxJava Android example

This is an example Android app which demonstrates how to use RxJava framework to communicate with a Spring Boot web app, which is secured by Okta OICD. 

**Prerequisites:**

* [Android Studio][android-studio]
* [Okta CLI][okta-cli]

> [Okta](https://developer.okta.com/) has Authentication and User Management APIs that reduce development time with instant-on, scalable user infrastructure. Okta's intuitive API and expert support make it easy for developers to authenticate, manage and secure users and roles in any application.

* [Getting Started](#getting-started)
* [Links](#links)
* [Help](#help)
* [License](#license)

## Getting Started

Clone the Spring Boot web app:

```bash
git clone git@github.com:oktadeveloper/okta-spring-webflux-react-example.git reactive-spring-boot
cd reactive-spring-boot/reactive-web
```

Signup with Okta and create your first application:

```bash
okta register
okta apps create
```

Copy your Okta values from `.okta.env` into the `reactive-spring-boot/reactive-web/src/main/resources/application.yml` file.
You can also use the instructions in [this](https://github.com/oktadev/okta-spring-webflux-react-example#getting-started) repo’s getting started section.

Run the server by running the command:

```bash
./mvnw
```

Clone this example's source code:

```bash
git clone https://github.com/oktadeveloper/okta-rx-java-android-example.git
cd okta-rx-java-android-example
```

Signup with Okta and create your first application:

```bash
okta register
okta apps create
```

Select **Native** and the default Redirect URIs. This will result in output like the following:

```bash
Okta application configuration:
okta.oauth2.issuer: https://dev-6974382.okta.com/oauth2/default
okta.oauth2.client-id: 0oa3dzttoa4qslD0T5d6
```

Modify the `app/src/main/java/dev/dbikic/oktaloginexample/OktaManager.kt` to use your settings:

```kotlin
init {
    val config = OIDCConfig.Builder()
        .clientId("{yourClientId}")
        .discoveryUri("https://{yourOktaDomain}")
        .redirectUri("{yourReverseOktaDomain}:/callback")
        .endSessionRedirectUri("{yourReverseOktaDomain}:/")
        .scopes("openid", "profile", "offline_access")
        .create()
    ...
}
```

You'll also need to update `app/build.gradle` to use your reverse domain name.

```groovy
manifestPlaceholders = [
    "appAuthRedirectScheme": "{yourReverseOktaDomain}"
]
```

Press the play icon in the top right part of Android Studio. You should be able to log in with your Okta credentials and create/update/delete posts.

## Links

This example uses the following open source libraries from Okta:

* [Okta Android SDK](https://github.com/okta/okta-oidc-android)
* [Okta CLI](https://github.com/okta/okta-cli)

## Help

Please post any questions as comments on [this example's blog post][blog], or use our [Okta Developer Forums](https://devforum.okta.com/).

## License
Apache 2.0, see [LICENSE](LICENSE).

[android-studio]: https://developer.android.com/studio
[blog]: https://developer.okta.com/blog/2021/01/06/android-login
[okta-cli]: https://github.com/okta/okta-cli

