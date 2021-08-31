# Hello-Android-DevOps

<h2>Commands</h2>
<ul>
    <li>Generate App Debug <code>./gradlew assembleDebug</code></li>
    <li>Generate App Release <code>./gradlew assembleRelease</code></li>
    <li>Generate App Bundle - AAB format<code>./gradlew bundleRelease</code></li>
</ul>

<h2>Generate Keystore</h2>
<ul>
    <li><code>keytool -genkey -v -keystore hello.jks -alias hello -keyalg RSA -keysize 2048 -validity 10000</code></li>
</ul>

<br/>
<h2><bold><a href="https://developer.android.com/studio/publish/app-signing">Sign your app</a></bold></h2>

<h3><b>keystore.properties</b></h3>
<code>
storePassword=myStorePassword</br>
keyPassword=mykeyPassword</br>
keyAlias=myKeyAlias</br>
storeFile=myStoreFileLocation</br>
</code>
<h3><b>build.gradle</b></h3>
<code>
...

// Create a variable called keystorePropertiesFile, and initialize it to your
// keystore.properties file, in the rootProject folder.
def keystorePropertiesFile = rootProject.file("keystore.properties")

// Initialize a new Properties() object called keystoreProperties.
def keystoreProperties = new Properties()

// Load your keystore.properties file into the keystoreProperties object.
keystoreProperties.load(new FileInputStream(keystorePropertiesFile))

android {
    ...
}
</code>
<p>Step 1 <b>build.gradle</b></p>
<code>
android {
    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile file(keystoreProperties['storeFile'])
            storePassword keystoreProperties['storePassword']
        }
    }
    ...
  }
  </code>

<p>Step 2</p>
<code>
buildTypes {
        release {
            ... <br/>
            signingConfig signingConfigs.release
        }<br/>
    }
</code>
<p>Step 3</p>
<code>./gradlew assembleRelease</code>

<br/><br/>
<h2>Publish App</h2>
<code>https://play.google.com/console/u/0/developers</code>
<h3>Gradle Play Publisher</h3>
<a href="https://github.com/Triple-T/gradle-play-publisher">Gradle Play Publisher</a>
<div>Add project <code>service-account.json</code> create file in Google Cloud Plataform</div>
<div>Setup <code>gradle</code></div>
<h3>Quick Start</h3>
<ol>
    <li>Basic Setup<code>./gradlew bootstrapListing</code></li>
    <li>Generate Release<code>./gradlew bundleRelease</code></li>
    <li>Publishing listings <code>./gradlew publishListing</code></li>
</ol>