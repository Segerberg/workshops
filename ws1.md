# workshops

## Webarkivering

### molndal.se

Mölndals stad har en sitemap vilket är väldigt användbart 

https://www.molndal.se/sitemap.xml

<pre>
&lt;sitemapindex xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/siteindex.xsd"&gt;
&lt;sitemap&gt;
&lt;loc&gt;https://www.molndal.se/sitemap1.xml.gz&lt;/loc&gt;
&lt;lastmod&gt;2021-10-30T06:40:02+02:00&lt;/lastmod&gt;
&lt;/sitemap&gt;
&lt;/sitemapindex&gt;
</pre>

sitemappen länkar till en zippad fil (gz) vilken innehåller en sitemap xml som listar alla url:er på webbplatsen, när de senast uppdaterades samt en liten blänkare till sökmotorer vilken prioritet de har. 
  
<pre>
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;urlset xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"
        xmlns="http://www.sitemaps.org/schemas/sitemap/0.9"&gt;
   &lt;url&gt;
      &lt;loc&gt;https://www.molndal.se/images/18.73f6f4121600a42c7a79bd/1553599864230/flerfackskarl_fluglock_oppen855x641vanmac.jpg&lt;/loc&gt;
      &lt;lastmod&gt;2017-12-06T17:28:32+01:00&lt;/lastmod&gt;
      &lt;priority&gt;0.5&lt;/priority&gt;
   &lt;/url&gt;
   &lt;url&gt;
      &lt;loc&gt;https://www.molndal.se/images/18.32712b5a15ea18e59ad309b/1553599713490/flerfackskarl_glasbergsgatan855x641.jpg&lt;/loc&gt;
      &lt;lastmod&gt;2017-10-04T13:06:30+02:00&lt;/lastmod&gt;
      &lt;priority&gt;0.5&lt;/priority&gt;
   &lt;/url&gt;
   &lt;/urlset&gt; 
   ...
   ....
</pre>

Vi kan skapa ett enkelt script som extraherar alla länkar som ändrats sedan ett visst datum 



### Verktyg

#### Collect

##### Wget

wget finns installerat i de flesta större linux-distrubutioner. Wget finns även för windows men saknar tyvärr warc-output

Exempel på hur man kan ladda ner en (1) sida med alla dess resurser (bilder,javascript, css)
<pre>
<code>
wget -H -k -K -p --warc-file="molndal_se" --no-warc-compression https://molndal.se
</code>
</pre>



##### Access

##### pywb
Fullständig dokumentation finns på https://pywb.readthedocs.io/en/latest/


Med python installerat kan pywb hämtas med PIP 
<pre><code>pip install wayback</code></pre>

För att initiera en "samling" kör man 

<pre>
<code>
wb-manger init molndal 
</code>
</pre>

En katalogstrruktur kommer då att skapas enligt nedan
<pre>
collections
└── molndal
    ├── archive
    │ └── en_warcfil.warc
    ├── indexes
    ├── static
    └── templates
</pre>

warc-filer placeras under katalogen "archive" 

För att starta och servera warcfilerna kör man sedan: 
Där "-a" innebär att man vill autoindexera warc-filerna och --auto-interval är med den frekevens man önskar att kolla efter nya warcfiler och indexera dem. I exemplet nedan kollar vi alltså efter nya filer var 10:de sekund.

<pre>
<code>
wayback -a --auto-interval 10
</code>
</pre>

Pywb har en annan fiffig funkttion som lämpar sig bra för att arkivera sidor som annars skulle vara i princip omöjliga att arkivera. 
t.ex. Facebook, instagram osv. Det kräver dock lite mer manuellt arbete. 

Om man startar pywb med följande options: 

<pre>
<code>
wayback --live --record -a --auto-interval 10
</code>
</pre>  

och sedan navigerar till http://127.0.0.1:8080/molndal/record/ (om man kör lokalt på sin egen burk alltså)
följt av den sida man vill arkivera. t.ex. http://127.0.0.1:8080/molndal/record/https://www.facebook.com/molndalsstad

All trafik mellan din webbläsare och internet kommer nu att sparas genom en proxy.

Det lite jobbiga med t.ex. facebook är attt man måste scrolla för att ladda fler inlägg. Ett sätt att hantera detta är att köra lite javascript direkt i webläsarens konsol som man vanligen kommer åt 
genoom att högerklicka någonstans på webbsidan och välja "inspektera". Man kan också trycka på F12. 

Exempel på enkelt script som autoscrollar en sida.  
<pre>
<code>
function Skrollan() {
    window.scrollBy(0,20);
    scrolldelay = setTimeout(pageScroll,5);
}
Skrrollan()
</code>
</pre>


# Webbsidor vi besökt

* https://oldweb.today/
* https://www.httrack.com/
* https://github.com/webrecorder/webrecorder-player
* https://github.com/palewire/savepagenow
* https://www.gnu.org/software/wget/
