# Anypass SDK

「Anypass SDK」は、電話番号とSMSの認証、電話番号の変更機能を備えたアプリを簡単に作成できるようにするSDKです。 これらの機能を使用するための低レベル APIを提供しています。

目次
=================

<!--ts-->
   * [機能](#機能)
	   * [Androidの機能](#androidの機能)
	   * [IOSの機能](#iosの機能)
	   * [一般的な機能](#一般的な機能)
   * [リリース](#リリース)
   * [インストール](#インストール)
      * [要件](#要件)
      * [構成](#構成)
	      * [Android構成](#android構成)
	      * [IOS構成](#ios構成)
   * [入門](#入門)
	   * [パブリックAPI](#パブリックapi)
		   * [Android](#android)
			   * [Kotlin](#kotlin)
			   * [Java](#java)
		   * [IOS](#ios)
			   *  [Swift](#swift)
			   * [Objective C](#objective-c)
   * [参考例](#参考例)
<!--te-->

## 機能

### Androidの機能
**電話番号認証**: ユーザーが許可した場合、デバイスの電話番号を自動的に取得し、この電話番号を認証して結果を返します。

### IOSの機能
**SMS認証**: SMSを送信することで電話番号を認証します。

### 一般的な機能
**引継ぎ(電話番号変更なし)**: 電話番号を変更せずにアカウントを移行します。

**引継ぎ(電話番号変更あり)**: アカウントを移行して電話番号を変更します。

## リリース
* [変更ログ](CHANGELOG.md) では、各リリースの変更概要について説明します。
* [移行ガイド](MIGRATING.md) では、旧バージョンからのアップグレードを行う手順について説明します。

## インストール

### 要件
#### Android
* Android 6.0 (API レベル 23) 以降

#### IOS
* IOS 11 以降
* Swift 5.0 以降又は Objective C

### 構成
#### Android構成
anypass_sdk.jar を案件にインポートします。

- 例: (app-debug.aar)
1. ファイルを app/libsフォルダー に追加します。
![Import Module](https://lh3.googleusercontent.com/drive-viewer/AFGJ81qzW-tXiX6I-6s0ag03QIGlnZfcX9qHHaibREpa21D_tLpxMW3ewmWBwatRd4afbdJeBgW9ISUR9RWHTCMAhdBB1e66=s2560)
2. アプリの [build.gradle](https://developer.android.com/studio/build/dependencies#using-native-dependencies)ファイルに依存関係を追加します。
![Import Module](https://lh3.googleusercontent.com/drive-viewer/AFGJ81rd9S-----xqPj4pS3GJkEvTpsymu2rIf-L7fNaixgnUXlFvYEuW00A6z5UDWQJ9fEtnBElbv36dFdtzlO-G6ZqOHFTFQ=s2560)
 
#### IOS構成
作成した xcframework ファイルを Frameworks、ライブラリ、および埋め込みコンテンツでドラッグ＆ドロップ操作で追加します。
![Import Module](https://drive.google.com/uc?id=1kxWl4cZiNyFGd4cOHtsiF6IIhbEu7ORk)


## 入門

### パブリックAPI

> #### Android

| 関数 |説明<div style="width:2990px">property</div>|  入力  |
|--|--|--|
| verifyAndroidPhoneNumber | 電話番号を認証します。| Domain, DomainApiVerifyPhone |
| transferAccountWithoutChangePhoneNumber | 電話番号を変更せずにアカウントを移行します。 |Domain, DomainApiVerifyPhone|
| transferAccountWithChangePhoneNumber | 電話番号を変更してアカウントを移行します。 |Domain, DomainApiVerifyPhone|

### Java

1.  SDKの起動用ランチャーを作成します。

```java
ActivityResultLauncher<Intent> startActivityIntent = AnyPassSDK.createResultLauncher(this);

```

2.  SDK ビルダーを作成し、SDK を起動します。

```java
new AnyPassSDK.AnyPassSDKBuilder(this) // Set your callback listener here
                    .setDomain("") // Set your domain here
                    .setDomainApiVerifyPhone("") // Set your ApiVerifyPhone here
                    .start(startActivityIntent, this); // start with launcher and activity

```

3.  WebViewURLを読み込みます。

-   Android の電話番号を認証します。

```java
AnyPassSDK.verifyAndroidPhoneNumber();

```

-   電話番号を変更せずにアカウントを移行します。

```java
AnyPassSDK.transferAccountWithoutChangePhoneNumber();

```

-   電話番号を変更してアカウントを移行します。

```java
AnyPassSDK.transferAccountWithChangePhoneNumber();

```

4.  コールバック リスナー

```java
public class MainActivity extends AppCompatActivity implements AnyPassSDK.ClientEventListener

		@Override
    public void didAuthFail(String sdkCode, String msg) {
	
		}

		@Override
    public void didAuthSuccess(String sdkCode, String msg) {
	
		}
}

```

### Kotlin

1.  SDKの起動用ランチャーを作成します。

```kotlin
private val launcher = AnyPassSDK.createResultLauncher(this)

```

2.  SDK ビルダーを作成し、SDK を起動します。

```kotlin
AnyPassSDKBuilder(this) // Set your callback listener here
                      .setDomain("") // Set your domain here
                      .setApiVerifyPhone("") // Set your ApiVerifyPhone here
                      .setMaxUUID("") // Set max UUID here (Optional) 
                      .start(launcher, this) // start with launcher and activity

```

3. WebView URLを読み込みます。

-   Android の電話番号を確認します。

```kotlin
AnyPassSDK.verifyAndroidPhoneNumber()

```

-   電話番号を変更せずにアカウントを移行します。

```kotlin
AnyPassSDK.transferAccountWithoutChangePhoneNumber()

```

-   電話番号を変更してアカウントを移行します。

```kotlin
AnyPassSDK.transferAccountWithChangePhoneNumber()

```

4.  コールバック リスナー

```java
class MainActivity : AppCompatActivity(), ClientEventListener {

		override fun didAuthFail(sdkCode: String, msg: String) {

		}

		override fun didAuthSuccess(sdkCode: String?, msg: String?) {

		}
}

```

 <br /> <br />

> #### IOS
| 関数 | 説明 |  入力  |
|--|--|--|
| verifyIosSms | SMSを送信することで電話番号を認証します。 | domainURL |
| transferAccountWithoutChangePhoneNumber | 電話番号を変更せずにアカウントを移行します。 |domainURL|
| transferAccountWithChangePhoneNumber | アカウントを移行して電話番号を変更します。 |domainURL|

**Swift**

1.  SDK の初期化

```swift
let config = AnyPassConfig(viewController: self, domainURL: "")
let authentication = AnyPassAuthentication(with: config)
authentication.delegate = self

```

2.  機能

-   SMS を認証します。

```swift
authentication.verifyIosSms()

```

-   電話番号を変更せずにアカウントを移行します。

```swift
authentication.transferAccountWithoutChangePhoneNumber()

```

-   電話番号を変更してアカウントを移行します。

```swift
authentication.transferAccountWithChangePhoneNumber()

```

3.  デリゲート

```swift
extension ViewController: AnyPassAuthDelegate {
    func didAuthSuccess(userInfo: AnyPassResult) {
        
    }
    
    func didAuthFailure(error: AnyPassResult) {
        
    }
}

```
### Objective C

1.  SDK の初期化

```objectivec
AnyPassConfig * config = [[AnyPassConfig alloc] initWithViewController: self domainURL: @""];
AnyPassAuthentication *authentication = [[AnyPassAuthentication alloc] initWith: config];
authentication.delegate = self;

```

2.  機能

-   SMS を認証します。

```objectivec
(void)authentication.verifyIosSms;

```

-   電話番号を変更せずにアカウントを移行します。

```objectivec
(void)authentication.transferAccountWithoutChangePhoneNumber;

```

-   電話番号を変更してアカウントを移行します。

```objectivec
(void)authentication.transferAccountWithChangePhoneNumber;

```

3.  デリゲート

```objectivec
@interface ViewController : UIViewController<AnyPassAuthDelegate>

- (void)didAuthSuccessWithUserInfo:(AnyPassResult *)userInfo {
    
}
- (void)didAuthFailureWithError:(AnyPassResult *)error {
    
}

```

<br/><br/>

#### `statusCodes`

発生する可能性があるエラーは下記の通りです。説明内容を参考に、どのエラーが発生したか判断できます。

| 名前                          | 説明                                                                                                                                                                                                                                                                                                                                                               |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `NG_ERROR`           | API 関連のエラー                                                                                                                                                                                                                                                                                                                                     |
| `OK_USER_REGISTRATION`                 | 発券用情報の登録が完了しました。|
| `OK_USER_TRANSITION`            | 発券用情報の引継ぎが完了しました。                                                                                                                                                                                                                                                                                                        |
| `NG_NOTHING_TRANSFERER` | 引継ぎ元の登録情報がありません。                                                                                                                                                                                                                                                                                         |
| `NG_SYSTEM_ERROR` | システムエラーが発生しました。                                                                                                                                                                                                                                                                                         |

### 参考例
-  [Kotlin サンプル プロジェクト](example/kotlin) 
-  [Java サンプル プロジェクト](example/java) 
-  [Swift サンプル プロジェクト](example/swift) 
-  [Objective C サンプル プロジェクト](example/object-c) 

## ライセンス

(確認待ち)
