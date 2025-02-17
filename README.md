# Sensfrx Flutter SDK

![Sensfrx Logo](https://sensfrx.ai/assets/image/footer-logo-white.png)

The **Sensfrx Flutter SDK** is a comprehensive solution that helps companies combat fraudulent activity and protect against compromised accounts. By integrating Sensfrx into your Flutter application, you can detect suspicious behavior, identify potential security threats, and maintain the integrity of user accounts. With its robust features and real-time notifications, Sensfrx provides a seamless and powerful security solution for your app, ensuring a secure environment for your users.

[Know more about us](https://sensfrx.ai)

## Installation

To install the Sensfrx Flutter SDK in your Flutter project, follow these simple steps:

1. Open your project's `pubspec.yaml` file.
2. Add the following dependency under the `dependencies` section:

    ```yaml
    dependencies:
      sensfrx_flutter: ^1.0.0
    ```

    Make sure to replace `^1.0.0` with the latest version of the Sensfrx Flutter SDK.

3. Save the `pubspec.yaml` file.
4. Run the following command in your terminal:

    ```bash
    flutter pub get
    ```

    This command will fetch and download the Sensfrx Flutter SDK package into your project.

5. Import the Sensfrx Flutter SDK in your Dart code:

    ```dart
    import 'package:sensfrx_flutter/sensfrx_flutter.dart';
    ```

You're now ready to start using the Sensfrx Flutter SDK in your application.

> **Note:** Ensure that your Flutter SDK is up to date and compatible with the Sensfrx Flutter SDK version you are installing. For more detailed installation instructions or troubleshooting, refer to the official documentation or reach out to the Sensfrx support team.

### Implementation

For implement Sensfrx SDK in your `main.dart` file you need property and secret.

To Get Your Property Secret
- Register on the [Sensfrx Dashboard](https://sensfrx.ai).
- After registration, log in to your dashboard.
- Generate your Property ID and Property Secret from the dashboard. These credentials are required to configure the SDK in your app.

#### sandboxMode Parameter
sandboxMode (boolean):
- true: Use this mode for testing. In sandbox mode, the SDK will simulate interactions and data without affecting your production environment.
- false: Set this mode to false when you are ready to deploy the app in a live production environment. This ensures the SDK works with real data and integrates with the live backend services.


```dart
@override
void initState() {

 if (Platform.isAndroid) {
      SensfrxFlutter.configure(sandboxMode : true, "6291856998352997:6GXgaUaU4LBep0ka");
    } else if (Platform.isIOS) {
      //dev
      SensfrxFlutter.configure(sandboxMode: true, "6291856998352997:6GXgaUaU4LBep0ka");
    }
  super.initState();
}
```

Make sure to replace `6291856998352997:6GXgaUaU4LBep0ka` with the Property Secret you obtained from the [Sensfrx Dashboard](https://sensfrx.ai).



##  Event Monitoring
Sensfrx provides multiple event tracking mechanisms:


### Click Events
Monitor user interactions with the app by tracking button clicks or any other view clicks. Click events help us read the behavioral data of users, providing insights into how users interact with different elements of your app.


```
SensfrxFlutter.trackClickEvent(context, position);

Example:

import 'package:sensfrx_flutter/sensfrx_flutter.dart';
import 'package:flutter/material.dart';

class ClickEventTestPage extends StatefulWidget {
  const ClickEventTestPage({Key? key}) : super(key: key);

  @override
  State<ClickEventTestPage> createState() => _ClickEventTestPageState();
}

class _ClickEventTestPageState extends State<ClickEventTestPage> {
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTapDown: (position) {
        setState(() {
          SensfrxFlutter.trackClickEvent(context, position);
        });
      },
      child: Scaffold(
        appBar: AppBar(
          title: const Text('Click Event Test Page'),
        ),
        body: Padding(
          padding: const EdgeInsets.all(16.0),
          child: SingleChildScrollView(
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.stretch,
              children: [
                const SizedBox(height: 16.0),
                const Text(
                  'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
                  style: TextStyle(fontSize: 18.0),
                ),
                const SizedBox(height: 32.0),
                ElevatedButton(
                  onPressed: () {},
                  child: const Text('Button 1'),
                ),
                const SizedBox(height: 16.0),
                ElevatedButton(
                  onPressed: () {},
                  child: const Text('Button 2'),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

```


### Login Event
The Login Event is critical for tracking and protecting user logins. By monitoring login attempts and associated behaviors, Sensfrx can detect abnormal patterns that may indicate fraud, such as multiple failed login attempts, IP location changes, and device fingerprint mismatches.

Benefits of Tracking Login Events:

- Account Takeover (ATO) Detection: Identifies fraudulent login attempts and potential account takeovers.
- Fraud Prevention: Detects patterns indicative of credential stuffing, password spraying, or other automated attack techniques.
- Risk Analysis: Provides actionable insights into login behaviors and risks, improving security measures.

Implementation Example

```dart
//_currentPosition is location here
// Create a login request and send it to your backend
String? deviceFingerprints =
        await SensfrxFlutter.getDeviceFingerprintsPayload(_currentPosition);

    String? token = await SensfrxFlutter.getRequestToken();
    String? package = await getPackageName();
    if (token != null) {
      final body = jsonEncode({
        'email': email,
        'password': password,
        'package': package,
        'request_token': token,
        'd_f': deviceFingerprints,
      });

```


Fore more details checkout the demo application or connect with our [support team](https://sensfrx.ai).

### Registration Event Tracking
The Registration Event helps track new user registrations. This is essential for preventing fraudulent account creation, such as fake registrations or bot-driven sign-ups. By tracking registration behaviors, Sensfrx can detect suspicious activities like repeated sign-ups from the same IP address, unusual device fingerprints, or unverified user information.

Benefits of Tracking Registration Events:
- Fake Registration Detection: Identifies automated or bot-driven sign-ups that don't match typical user behavior.
- Fraud Prevention: Prevents fake account creation by detecting patterns such as multiple sign-ups with the same email or device fingerprint.
- Risk Analysis: Provides insights into registration behaviors, helping to prevent fraud and improve account security from the start.

Implementation Example

```dart

//_currentPosition is location here
 String? token = await SensfrxFlutter.getRequestToken();
    String? package = await getPackageName();

String? deviceFingerprints =
        await SensfrxFlutter.getDeviceFingerprintsPayload(_currentPosition);

    if (token != null) {
      print("clicked : $token");

      final body = jsonEncode({
        'rfs': {
          'name': name,
          'email': email,
          'phone': mobile,
          'password': password,
        },
        'request_token': token,
         'd_f': deviceFingerprints,
        'package': package,
      });


```
Fore more details checkout the demo application or connect with our [support team](https://sensfrx.ai).


### Transaction Event Tracking
The Transaction Event provides insights into user purchases and financial transactions. By monitoring transaction data, Sensfrx can help detect suspicious activities like payment fraud, stolen credit cards, and transaction manipulation, ensuring secure and reliable financial interactions.

Benefits of Tracking Transaction Events:
- Payment Fraud Detection: Identifies abnormal transaction patterns such as high-value transactions, unusual payment methods, or frequent payment failures.
- Risk Management: Helps businesses assess transaction risks and detect compromised accounts or fraudulent payment methods.
- Transaction Integrity: Ensures that only legitimate purchases are processed, protecting both users and merchants from fraud.


```dart

  Map<String, dynamic> jsonObject = {
    "transaction_id": "TXN123456",
    "transaction_type": "purchase",
    "email": "dummy@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "username": "john_doe123",
    "payment_mode": "Credit Card",
    "payment_provider": "Visa",
    "card_fullname": "John Doe",
    "card_bin": "411111",
    "card_expire": "12/2026",
    "card_last": "1234",
    "cvv": "999",
    "phone_no": "9998887777",
    "transaction_amount": "1500",
    "transaction_currency": "INR",
    "items": [
      {
        "item_id": "101",
        "item_name": "Wireless Headphones",
        "item_category": "Electronics",
        "item_quantity": "1",
        "item_price": "1200",
        "item_url": "https://example.com/item101"
      },
      {
        "item_id": "102",
        "item_name": "USB-C Charger",
        "item_category": "Accessories",
        "item_quantity": "1",
        "item_price": "300",
        "item_url": "https://example.com/item102"
      }
    ],
    "shipping_cost": "50",
    "shipping_country": "India",
    "shipping_state": "Maharashtra",
    "shipping_city": "Mumbai",
    "shipping_zip": "400001",
    "shipping_phone": "9998887777",
    "shipping_fullname": "John Doe",
    "shipping_method": "Express",
    "billing_country": "India",
    "billing_state": "Maharashtra",
    "billing_city": "Mumbai",
    "billing_zip": "400001",
    "billing_phone": "9998887777",
    "merchant_name": "Gadget World",
    "merchant_category": "Electronics",
    "merchant_id": "M123456",
    "merchant_country": "India",
    "ev": "attempt_succeeded",
    "card_type": "Visa",
    "tax_amount": "100",
    "discount_amount": "50",
    "invoice_id": "INV98765",
    "d_f": "device_fingerprint_abc123",
    "request_token": "token_xyz789",
    "user_id": "user_987654"
  };

  String jsonString = jsonEncode(jsonObject);
 
// Track the transaction event
Sensfrx.trackTransactionEvent(jsonObject)
```

### Transaction Success/Failure Handling
After initiating the payment process with your payment SDK, you can track whether the transaction was successful or failed by utilizing Sensfrx.trackTransactionEvent in your onPaymentSuccess and onPaymentError methods. This helps in tracking the transaction's outcome and improves fraud detection.

#### Java
```java
// Called when payment is successful
@Override
public void onPaymentSuccess(String s) {
    // Set the event to transaction_succeeded
    jsonObject.addProperty("ev", "transaction_succeeded");

    // Send the complete transaction details jsonrequest again with updated flag
    Sensfrx.trackTransactionEvent(jsonObject);
}

// Called when payment fails
@Override
public void onPaymentError(int i, String s) {
    // Set the event to transaction_failed
    jsonObject.addProperty("ev", "transaction_failed");

    // Send the complete transaction details jsonrequest again with updated flag
    Sensfrx.trackTransactionEvent(jsonObject);
}
```

```dart
// Called when payment is successful
 fun onPaymentSuccess(s: String) {
    // Set the event to transaction_succeeded
    jsonObject.addProperty("ev", "transaction_succeeded")

    // Send the complete transaction details jsonrequest again with updated flag
    Sensfrx.trackTransactionEvent(jsonObject)
}

// Called when payment fails
 fun onPaymentError(i: Int, s: String) {
    // Set the event to transaction_failed
    jsonObject.addProperty("ev", "transaction_failed")

    // Send the complete transaction details jsonrequest again with updated flag
    Sensfrx.trackTransactionEvent(jsonObject)
}

```
###  Application Event
Tracking the app's state allows you to monitor when your app is opened, closed, or moved to the background. This information is crucial for detecting unusual app usage patterns, improving user engagement, and strengthening security measures.
Sensfrx manages application events itself. If, for some reason, the app event is not getting generated, you can use the following method:
```
SensfrxFlutter.trackAppEvent(appState);
```

### Screen Change Events
Tracking screen transitions allows you to monitor how users navigate through your app, helping you understand their behavior and detect potential fraud. Sensfrx automatically tracks screen changes and provides valuable insights into user journeys, such as how many screens a user visits and how long they stay on each.
Capture screen transitions:

- User Behavior Analysis: Understanding user navigation patterns allows us to identify normal and abnormal behavior, improving user experience and fraud detection.
- Fraud Detection: Unusual screen change patterns, such as rapid or unexpected transitions, could indicate suspicious activity or attempts to bypass security.

---
```dart
navigatorObservers: [SensfrxFlutter.trackScreenChangeEvent()],

Example:
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      navigatorObservers: [SensfrxFlutter.trackScreenChangeEvent()],
      home: const MainScreen(),
      routes: {
        'main': (context) => const MainScreen(),
        'login': (context) => const LoginScreen(),
        'register': (context) => const RegisterScreen(),
        'location': (context) => const LocationPage(),
        'click_event': (context) => const ClickEventTestPage(),
        'screen_one': (context) => const ScreenOne(),
        'screen_two': (context) => const ScreenTwo(),
        'screen_three': (context) => const ScreenThree(),
        'screen_four': (context) => const ScreenFour(),
      },
    );
  }
}

OR, if your project doesn’t support navigatorObservers, use the custom method:

SensfrxFlutter.trackScreenChangeEvent(currentScreenName);

```


## Analytics and Dashboard
After integrating Sensfrx into your app, you can view real-time fraud detection analytics, user behavior, and transaction logs directly on the Sensfrx Dashboard. This allows you to monitor suspicious activities and make data-driven decisions for fraud prevention.

Access your [Sensfrx Dashboard](https://sensfrx.ai)

---

## Support
For assistance, contact our support team at [info@sensfrx.com](mailto:info@Sensfrx.com) or visit our developer portal.

## License
This project is licensed under the Apache License 2.0 - see the LICENSE file for details.

<p>
  <a href="https://sensfrx.ai" target="_blank">
    <img src="https://forthebadge.com/images/badges/built-with-love.svg" alt="Built with Love">
    <img src="https://forthebadge.com/images/badges/built-for-android.svg" alt="Built for Android">
  </a>
</p>







