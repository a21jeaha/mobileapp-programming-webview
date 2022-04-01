
# Rapport

Det första som gjordes var att byta namn på applikationen, denna ändring gjordes vid `res/values/strings.xml` där värdet i variabeln ändrades enligt nedan.

```
<resources>
    <string name="WebViewApp">JPWebViewApp</string>              //här byts namnet ut från WebViewApp, till JPWebViewApp
    <string name="action_external_web">External Web Page</string>
    <string name="action_internal_web">Internal Web Page</string>
</resources>
```

För att ge applikationen internet access så har följande rad kod skrivits in i filen `AndroidManifest.xml` 

```
 <uses-permission android:name="android.permission.INTERNET" />
```
Skapade en ny String name resource som sedan användes som namn till webView elementet i filen `content_main.xml`

```
<string name="id">my_webview</string>
```
```
<WebView
android:id="@+id/webview"
android:layout_width="match_parent"
android:layout_height="match_parent"
/>
```
En private member variable av`WebView` skapades sedan och instansierades i metoden `onCreate()`
```
public class MainActivity extends AppCompatActivity {
    private WebView myWebView;

    public MainActivity(){
        myWebView = new WebView(this);
    }
}
```

```
 @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Toolbar toolbar = findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        myWebView = (WebView) findViewById(R.id.webview);  /// här aktiverar vi elementet
}
```


Och skrev sedan in 
**Skriv din rapport här!**

_Du kan ta bort all text som finns sedan tidigare_.

## Följande grundsyn gäller dugga-svar:

- Ett kortfattat svar är att föredra. Svar som är längre än en sida text (skärmdumpar och programkod exkluderat) är onödigt långt.
- Svaret skall ha minst en snutt programkod.
- Svaret skall inkludera en kort övergripande förklarande text som redogör för vad respektive snutt programkod gör eller som svarar på annan teorifråga.
- Svaret skall ha minst en skärmdump. Skärmdumpar skall illustrera exekvering av relevant programkod. Eventuell text i skärmdumpar måste vara läsbar.
- I de fall detta efterfrågas, dela upp delar av ditt svar i för- och nackdelar. Dina för- respektive nackdelar skall vara i form av punktlistor med kortare stycken (3-4 meningar).

Programkod ska se ut som exemplet nedan. Koden måste vara korrekt indenterad då den blir lättare att läsa vilket gör det lättare att hitta syntaktiska fel.

```
function errorCallback(error) {
    switch(error.code) {
        case error.PERMISSION_DENIED:
            // Geolocation API stöds inte, gör något
            break;
        case error.POSITION_UNAVAILABLE:
            // Misslyckat positionsanrop, gör något
            break;
        case error.UNKNOWN_ERROR:
            // Okänt fel, gör något
            break;
    }
}
```

Bilder läggs i samma mapp som markdown-filen.

![](android.png)

Läs gärna:

- Boulos, M.N.K., Warren, J., Gong, J. & Yue, P. (2010) Web GIS in practice VIII: HTML5 and the canvas element for interactive online mapping. International journal of health geographics 9, 14. Shin, Y. &
- Wunsche, B.C. (2013) A smartphone-based golf simulation exercise game for supporting arthritis patients. 2013 28th International Conference of Image and Vision Computing New Zealand (IVCNZ), IEEE, pp. 459–464.
- Wohlin, C., Runeson, P., Höst, M., Ohlsson, M.C., Regnell, B., Wesslén, A. (2012) Experimentation in Software Engineering, Berlin, Heidelberg: Springer Berlin Heidelberg.
