<h1>Building the Milagro MFA Mobile SDK and App for Android</h1>
<h2>Overview</h2>
<p class="MsoNormal">This page explains how to build the Milagro MFA Mobile SDK and the app for Android with <em>Android Studio</em>.</p>

<h2>Prerequisites</h2>
<p class="Normal">Download and install Android Studio or higher with Android SDK 16 or higher</p>

<h2>Building the mobile SDK</h2>
Download or Clone the project <a href="https://github.com/miracl/mpin-sdk-android"><code>mpin-sdk-android</code></a> with its submodules
<h3>From Android Studio</h3>
<ol>
    <li>Import the project: <em>File -&gt; Open -&gt; &lt;mpin-sdk-android&gt;</em></li>
    <li>From Gradle Tool View select: <em>mpinsdk -&gt; Tasks -&gt; build -&gt; build</em></li>
    <li>The assembled aar's will be located in <code>&lt;mpin-sdk-android&gt;/mpinsdk/build/outputs/aar</code></li>
</ol>
<h3>From a Command Line</h3>
<ol>
    <li>Navigate to <code>&lt;mpin-sdk-android&gt;</code></li>
    <li>Execute <code>./gradlew build</code></li>
    <li>The assembled aar's will be located in <code>&lt;mpin-sdk-android&gt;/mpinsdk/build/outputs/aar</code></li>
</ol>
</div>