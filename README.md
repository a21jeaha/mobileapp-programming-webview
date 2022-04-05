
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
Ett id för webView elementet i filen `content_main.xml` 

```
  <WebView
       android:id="@+id/webview"
       android:layout_width="wrap_content"
       android:layout_height="wrap_content"
       />
```

I filen `MainActivity.java` skapades en private member variable av`WebView` och instansierades i metoden `onCreate()`,
där den hittades med hjälp av `findViewById`
```
public class MainActivity extends AppCompatActivity {
    private WebView myWebView;
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
fortsatt i `onCreate()` skriver vi in dessa rader kod, för att först associera webSettings med instansen av WebView
sedan aktiveras javascript genom att sätta värder till __true__.

```
        WebSettings webSettings = myWebView.getSettings();
        webSettings.setJavaScriptEnabled(true);
```

För att utföra nästa steg (sätta till en html sida som asset) måste först en assets map skapas innehållande en map (som döps till webb_content) där vi sedan skapar html-filen. Denna fil fylls sedan med lite information så det finns något att se när applikationen läses. 

![](assetFolderCreated.jpg)

För att kunna ladda upp url-länkar behöver man använda sig av `myWebView.loadUrl("lämplig url")`, vid tester fungera den externa url-länken utan problem 
meddan den interna enbart fungera om hela sökvägen skrivs in, istället för den relativa sökvägen som rekommenderas i literaturen.
Vid försök vissas ett error meddelande som lyder __ERR_CLEARTEXT_NOT_PERMITTED__ när filen ska läsas in.
```
    myWebView.loadUrl("https://www.youtube.com/watch?v=d8zLGT5upZs&list=PLAxZA8hcpPLLjcktHtsZiACBvfAhUp6AF&index=25&ab_channel=LenaSYS");
    myWebView.loadUrl("file:///android_asset/webbcontent/about.html");
```
Vid testning av koden ovan erhölls ett resultat där innehållet i Webviewn hamnar under meny raden och en bit utanför fönstret,
Den uppdaterade WebView koden ser nu ut såhär, `android:layout_width=""`  har satts som `match_parent`, medan `android:layout_height=""` fick en fast storlek på 670dp.  
Resterande inställningar gjordes via Designvyn där constraints vid applikationens parent fönster på alla kanter bortsätt från toppen.
```
<WebView
       android:id="@+id/webview"
       android:layout_width="match_parent"
       android:layout_height="669dp"

       android:layout_marginBottom="4dp"
       app:layout_constraintBottom_toBottomOf="parent"
       app:layout_constraintEnd_toEndOf="parent"
       app:layout_constraintHorizontal_bias="0.444"
       app:layout_constraintStart_toStartOf="parent" />
```
Skillnaden är att innehållet i Webview fönstret anpassas till det primära applikations fönstret, däremot hittades ingen önskvärd lösning för att begränsa WebViewn så att den inte hamnar under menyraden.   

Efter det placerades url raderna med kod i deras respektive metod (metoderna fanns redan förskrivna, med instruktioner).
```
   public void showExternalWebPage(){
        myWebView.loadUrl("https://www.youtube.com/watch?v=d8zLGT5upZs&list=PLAxZA8hcpPLLjcktHtsZiACBvfAhUp6AF&index=25&ab_channel=LenaSYS");
    }

    public void showInternalWebPage(){
        myWebView.loadUrl("file:///android_asset/webbcontent/about.html");
    }
```
Det sista kravet 
```
@Override
public boolean onOptionsItemSelected(MenuItem item) {

int id = item.getItemId();

        if (id == R.id.action_external_web) {
            Log.d("==>","Will display external web page");
            showExternalWebPage();
            return true;
        }

        if (id == R.id.action_internal_web) {
            Log.d("==>","Will display internal web page");
            showInternalWebPage();
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
```
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



Läs gärna:

- Boulos, M.N.K., Warren, J., Gong, J. & Yue, P. (2010) Web GIS in practice VIII: HTML5 and the canvas element for interactive online mapping. International journal of health geographics 9, 14. Shin, Y. &
- Wunsche, B.C. (2013) A smartphone-based golf simulation exercise game for supporting arthritis patients. 2013 28th International Conference of Image and Vision Computing New Zealand (IVCNZ), IEEE, pp. 459–464.
- Wohlin, C., Runeson, P., Höst, M., Ohlsson, M.C., Regnell, B., Wesslén, A. (2012) Experimentation in Software Engineering, Berlin, Heidelberg: Springer Berlin Heidelberg.
