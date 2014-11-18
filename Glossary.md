##Web services

Hverjir eru kostirnir við vefþjónustur?
* Þær eru cross platform, þ.e. það geta margar tegundir af clientum tengst þeim
* Margir aðilar geta nýtt sér gögnin ef Web-Apin leyfir það, jafnvel selt aðgang að gögnum 
* Býður upp á möguleikan að nýta gögn frá fleiri ein einum Web-Apa og sameina þau, Mass upp consept
* Allri buisness lógík þarf bara að viðhalda á einum stað
* Clientin getur verið mjög léttur og þarf bara að rendera HTML

Hverjir geta verið ókostirnir við vefþjónustur?
* Getur valdið því að þegar smá breytingar verða á html síðu að þá verði client að endurhlaða henni að fullu frá þjónustunni
* Ef clientin er ekki vefur þá getur hann þurft að parsa HTML-ið til að ná í gögnin, það býður villum heim þar sem HTML getur breyst og þá virkar kannski ekki parsing lengur. 

Nefnið 3 algengar gerðir af vefþjónustum og lýsið arkitektúr þeirra stuttlega
* REST (REpresentational State Transfer, Roy Fielding in 2000) þjónustur eru client/server, þær eru stateless, þær eru cachable, og hypertext driven.   
* SOAP (Simple Object Access protocol)
* WCF (Windows Communication Foundation)

Hver eru einkenni REST þjónustu 
* Client/Server
* Stateless - serverinn á að halda utan um client state, state er sent með öllum requestum
* Cacheable - auðlindir(resources) ákveða sjálfar hvort þær eru cachble og hve lengi
* Hypertext driven (í hinum fullkomna heimi)

Teljið upp nokkur HTTP verbs og hvaða tilgangi þau þjóna
* GET (sækir gögn), POST (býr til nýja gögn), PATCH (uppfærir gögn, t.d. eitt svæði í töflu), PUT (uppfærir gögn í heild sinni), DELETE (eyðir eða setur delete flagg á true)
* HTTP verb tilgreina hvaða aðgerð á að framkvæma þegar kallað er í Web-Apa

Lýsið hefbundinni REST þjónustu í dag
* REST er HTTP þjónusta, sækir gögn og skilar JSON, það er lang algengasta útfærsluaðferð á REST í dag.  En REST þjónusta skv. skilgreiningu þarf ekki að nota HTTP.  Með REST er fólk að uppgvöta hvernig HTTP á að virka, þar sem verbin eru notuð mikið í REST þjónustum. 

Nefnið nokkra HTTP villukóða
* 200 aðgerð heppnaðist
* 301 redirect, urlið var fært, líklega ekki mikið notað
* 400 bad request, client gerði eitthvað vitlaust 
* 401 auðkennin ekki í lagi, senda HTTP authrozation header með
* 403 notandi má ekki framkvæma aðgerðina
* 404 gögn fundust ekki 
* 500 server villa, client getur ekkert gert í þessu

Hvernig á að byggja upp URL fyrir REST þjónustu ?
* /api/courses, sækir alla áfanga
* /api/courses/26892, sækir einn tiltekin áfanga
* /api/courses/26892/students, sækir alla nemendur í tilteknum áfanga

Hvernig er hægt að gera URL óhakkanleg
* Mögulega hægt að gera með ólæsanlegum URL-um
* Eða apin muni bara exposa rótar-urlinu og síðan þyrfti að kalla í Apan til að komast að því hvað er hægt að gera, rótarkallið skilar því

Hvernig er hægt að skilgreina hversu mikið þjónusta er REST þjónusta
* Level 0, SOAP, eitt url, allataf gert POST fyrirspurn á SOAP, uppl sendar í requesti um hvaða aðgerð er verið að kalla á
* Level 1, mismuanndi URL búið að bæta við resource með því
* Level 2, búið að bæta við HTTP verb, Post, Get etc. 
* Level 3, eitt rótar-url, notendur verða að kalla á þjónustuna til að komast að því hvað er hægt að gera, hér er möguleiki að hafa url sem er óhakkanleg (HATEOAS)
* Flestar vefþjónustur eru á level 2 í dag

Hvað er HATEOAS
* REST þjónusta á level 3 sem exposar bara einu rótarurli sem hægt er að nálgast all í gegnum
* Á þessu stili er janfvel hægt að hafa URL sem ekki er hægt að hakka 

Hvernig er best að útgáfustýra API-um
* Setja útgáfuna í urlið /api/v1/...  mikið notað
* Clienter bæti vðið custom http header við request sem segir að þeir vilja fá version x, erfitt að prófa með curl eða vafra
* Content type, bæta þessu við í Accept http headerinn 

##ASP.NET Web API
Hvað heitir nýja web apið sem Microsoft er að vinna að núna 
* ASP.NET vNext
* Open source og er á GtiHub
* Sameinar Web Forms, MVC, Web API í eina sæng, eða réttara sagt verið er að endurskrifa þetta
* Getur keyrt á öllum stýrikerfum

Hvernig er arkitektúr Web API 
* Allir controller klasar verða að erfa frá ApiController 
* ValuController sér um að mappa Urlin í kóðanum, ef föll í controller byjra á Get, Put, Post er gengið út frá því að þau höndli þessi atburði, það er líka hægt að skilgreina með attribute fyrir ofan fallið hvaða verb það höndlar [HttpGet] etc
* Annars á Soulutin að skiptast upp í Web-Apan sem inniheldur controllera og routing, Models sem inniheldur alla model og view klasa. Servises sem inniheldur alla buisness lógík og Entities sem inniheldur alla Entity klasa og tengingar við gagnagrunn.   Einnig er hægt að hafa Entities í sér projecti.

Hvernig er það stillt hvort controller skili JSON eða XML t.d. 
* Accept Http Hedar inniheldur Mime type sem segir til um þetta, application/json, applicatoin/xml

Hvað er CORS (Cross-Origin Resource Sharing)?
* Web apar setja Access-Control-Allow-Origin" HTTP header í response til að tilgreina hvað þeir styðja, þ.e. þa er hægt að tilgreina hvaða domain mega kalla í apan, hvaða aðgerðir eru í boði etc. By default þá gengur ekki að kalla í Apa sem er á öðru domain en maður sjálfur. 
* Vafrar (Chorme, Firefox etc.) senda fyrst HTTP Options request til að vita hvað þeir mega gera, fá til baka "Access-Control-Allow-Origin" HTTP header sem tilgreinir hvort þeir mega kalla í Apan og hvaða aðgerðir má nota.   
* var cors = new EnableCorsAttribute("*", "*", "*");  --origin, header and methods 

##Routing
Lýsið default routing í ASP.NET Web API
* URL eiga að stemma við ControllerName/ActionName 

Lýsið attribute routing
* Route prefix er skilgreint fyrir ofan controller klasan [RoutePrefix("api/v1/my")], síðan er hver aðgerð í klasanum tengd við ákveðna http verb aðgerð, [Route("grades")] etc.  Það er líka mögulegt að láta aðgerðirnar heita Get.., Post.. osfrv. 

Hvernig má senda paramert í api call 
* Parametra má skilgreina í routing fyrir fall, [Route("grades/{id:int}")], síðan verður fallið sem hefur þessa routing skilgreiningu að taka inn parameter sem heitir nákvæmlega það sama

Hvernig má bæta við query parameter í api call
* það er gert með spurningamerki /api/v1/12345/grades?semester=20133, þá verður fallið að taka inn parameter sem heitir semester og hann getur verið optional eða ekki

Hvernig er best að senda model eða entity gögn þegar kallað er í Post, Put eða Patch 
* Það er hægt að senda það með sem primative gildi í http header og verður þá að passa að merkja það með [From Body] attribute. 
* Einnig er hægt að senda með json klasa sem er þá mappað beint í dto klasa, og er þetta besta aðferðin til að senda gögn þar sem auðveldlega er hægt að bæta við gildum seinna meir án þess að bæta við parametrum í controllerin. 

Hvernig er best að skjala APA
* Það er nauðsynlegt að hafa skjölun fyrir conrollera og allar public aðgerðir í þeim, model klasa sem er notaðir til að taka við gögnum eða skila í gegnum vefþjóustuna.   Hafa xml skjölun fyrir ofan föll. 
* Það eru til nokkur hjálpartól þarna úti sem generate skjölun fyrir okkur

Hvaða machine redable skjölun er hægt að búa til fyrir vefþjónustur 
* WSDL (Web Services Description Language), SOAP og WCF þjónustum má lýsa með svona skjölun, það er svo hægt að generate forritsbúta út frá þessari skjölun sem auðveldar svo að forrita á móti þjónustunni. 
* WADL er svo til fyrir REST þjónustur, en það er mjög lítið notað

##Web Service Architecture
Hvernig er best að hafa högun, uppbyggingu á web service API projecti
* Web Api Project, sér um http samskipti, kann ekki neina buisness lógík
* Models Project, inniheldur DTO (gagnaklasa) og ViewModel (viðmóts-gagnaklasa) Web Api project skilar
* Service Project, inniheldur alla buisness lógík
* Test Project, inniheldur öll unit test 
* Entities Project, inniheldur gagnamódelið og tengingar við gagnagrunn

##Unit of Work
Lýsið hvað unit of work gerir
* Skilar repositroy fyrir töflu og sér um að commita breytingar í gagnagrunn
* Notar IRepository til að ná í töflur í gagnagrunni, eitt repository mappar eina töflu
* todo 

Lýsið hvað repository gerir
* Mappar gagnagrunnstöflur í kóða
* todo

##Dependency Injection
Hvað er dependency injection
* Það er að rétta objecti sínar instance breytur
* Þegar DI er notað þá er forritari neyddur til að nota Interface, Interface gera kóðan testanlegri þar sem auðveldara er að injecta dependencyum inn í hann 

Hvaða 3 tegundir af dependency injection eru til?
* Construction injection, skaffa instance breytur með því að senda þær í smiðinn
* Setter injection, gert með því að búa til föll sem gilda instance breytur
* Property injection, gera instance breytuna að property í klasanum 

Hvað er NINJET?
* Framework sem sér um DI fyrir okkur, klasar eru búnir til með Kernel.Get<ServiceClass>().   NINJET finnur út hvaða dependency þarf til að búa til instancið og skilar því svo.

##Linq
Hvað þarf til svo að þessi fyrirspurn skili okkur gögnum, var result = _courses.All().Where(c => c.Semester == "20143").OrderBy(c => c.Name);
* Það þarf að kalla á ToList(), result hér er bara query object (IEnumerable) ekki gögnin sjálf

Hvaða föll má nota til að ná í eina röð í færslur eða query objecti
* First(), skilar fyrstu röð úr collection, kastar villu ef collection er tómt
* FirstOrDefault(), skilar fyrstu röð úr collection eða null ef collection er tómt
* Single(), skilar fyrstu röð úr collection, kastar villu ef collection er tómt eða ef fleiri en ein færsla finnast skv. leitarskilyrðum
* SingleOrDefult(), skilar fyrstu röð úr collection eða null ef collection er tómt, kastar villu ef fleiri en ein færsla finnast skv. leitarskilyrðum

Hvernig join-ar maður tvær töflur í linq
* með equals, join ct in _courseTemplates.All() on ci.CourseID equals ct.ID

Hvenær er sniðugt að nota extension methods?
* Þegar það þarf að select oft sömu fyrirspurn, eins og t.d. eftir id í eina töflu, public static TeacherDTO GetTeacherByID(this IRepository<Teacher> repo, int id ) {select ,,,,  return result.ToList()}

##Entity
Hvaða tengsl eru í boði í entity-um
* one to one
* one to many
* many to many

Hvernig er best að skilgreina tengsl í entity-um
* Í entity klösum er hægt að vera með property sem geymir id á entity sem foreign lykill er í
* Eða collection ef tengslin er many to many

Hvaða loading options eru í boði fyrir tengd entity
* Lazy loading.  Tengd entity eru sótt þegar það vantar gögn úr þeim.
* Eager loading.  Tengd entity eru sótt um leið og entity-ið sem verið er að sækja er sótt.
* Explicit loading.  Við tilgreinum nákvæmlega hvenær á að sækja tengd entity. 

Hvað gerir AutoMapper
* Hann sér um að mappa klösum, þ.e. mappa Entity klösum í Dto og vice versa

Hvað er Fluent API og hvað gerir það
* Þetta gerir okkur kleyft að mappa töflum í gagnagrunni yfir í entity klasa og breyta nöfnum á bæði töflunni og dálkum. Þetta er gott í þeim tilfellum þar sem við erum kannski með legacy grunn með nafnagiftum sem ekki passa við það sem við viljum hafa í dag.  

##Unit Tests
Hvaða kóða á fyrst og fremst að einingaprófa 
* Það á fyrst og fremst að testa buisness lógík, mikilvægasti kóðin til að testa

Hvernig er best að setja upp einingapróf í verkefnum og lýsið hvernig að að gera það
* Það er best að hafa sér project fyrir einingaprófin
* Test klasar verða að vera public og hafa [TestClass] á undan klasa-skilgreiningu og [TestMethod] fyrir ofan öll testföll
* Test föll eiga að vera void og ekki taka inn neina parametra
* Hægt er að hafa [TestInitialize] fall sem er keyrt áður en öll test föllin eru keyrð

Hvaða 3 skref eiga að vera í öllum einingaprófanaföllum
* Arrange - býr til eintak af kerfinu sem á að testa, declera og frumstilla breytur, builda test gögn/klasa og bæta við MockUnitOfWork
* Act - yfirleitt bara ein lína, hér er kóðin (fallið) keyrt sem á að testa  
* Assert - hér er testað hvort niðurstöður eru eins og við var búist 

Er hægt að láta einingapróf kasta villu
* Já það er gert með því að bæta við [ExpectedException(typeof(AppObjectNotFoundException))] fyrir ofan fallið sem er verið að testa, þá gerir Test frameworkið ráð fyrir að þetta test skili þessar villu og ef það gerir það ekki þá failar testið
* Einnig er hægt að nota ExpectedExceptionWithMessage og þá er líka tékkað á villuskilaboðum hvort þau innihaldi ákv. skilaboð

Hvað gerir NBuilder fyrir okkur
* Auðveldar okkur að búa til test gagnaklasa og gögn í þá, sérstaklega ef við þurfum af einhverjum ástæðum að generate mikið af gögnum

##Globalization and Localization in ASP.NET
Hvað gengur þetta út á
* Þetta gengur út á að skrifa application sem styður mörg tungumál og birtingu gagna eins og dagsetningar, tíma ofl.

Hvaða cluture value styður Asp.Net
* Culture og UICulture, gildin í þessu ákvarða hvernig result lítur út úr föllum sem eru háð culture, svo sem dagsetningar, tími, tölur og mynt.  Allir þræðir í .net hafa CurrentCulture og CurrentUICulture object og ASP.NET skoðar þessa klasa þegar síður eru renderaðar
* Culture er skilgreint með og án region, t.d. en-US er enskt svæði og bandarísk enska. 
* Í hverri HTTP request er header field sem heitir Accept-Language sem segir til um hvaða tungumál browserinn skilur, Accept-Language: en-us,en;q=0.5 þýðir að browserinn vilji Ensku(United states) en getur tekið við öðrum tegundum af ensku. 

Hvernig má gera Web-Apa þannig úr garði að hann styðji við mörg tungumál 
* Það þarf að bæta við LanguageMessageHandler í Web-Apa-projectið, þar þarf að tilgreina hvaða tungumál eru studd, gott að setja það bara í array. Síðan er þessum handler bætt við gobal configið fyrir Web-Apan
* Síðan er lesið út request header þau tungumál sem browserinn styður
* Síðan er current tread stilltur á það tungumál sem er beðið um að því gefnu að Web-Apin styði það, þ.e. bæði CurrentCulture og CurrentUICulture
* Web-Apin þarf að vera með default localization þannig að ef hann styður ekki tungumál sem borwser biður um þá verður að nota það
* Hægt er að hafa þýðingar á strengjum í resourece skrá sem Web-Apin getur svo sótt úr eftir tungumálum, ein skrá pr. tungumál
* Í view model klasana er svo hægt að bæta við [Required(ErrorMessageResourceType = typeof(Resources.Resources), AllowEmptyStrings = false, ErrorMessageResourceName = "NameRequired")], hér eru þá villuskilaboð sótt eftir tungumáli browser og birt ef þetta property er ekki útfyllt. 
* Magar vefsíður leyfa notanda að velja tungumál, þ.e. yfirskrifa það sem browserinn styður, það er yfirleitt gert með því að setja valið tungumál í köku

Hvað er data annotation og Model state
* Í Asp.Net er hægt að nota attribute frá System.ComponentModel.DataAnnotations til að validatea Model klasa, það er gert með við því að bæta við [Required(ErrorMessage = "Það vantar að velja ....")]
* Í Controller klösum er svo hægt að tékka á því hvort ModelState.IsValid sé true, og ef ekki skila þá bad request með villuskilaboðum, ath það skilast ekki sjálfraka villa þó validation klikki það verður að forrita það

Hvernig má meðhöndla villur sem koma m.a. frá Model state eða af öðrum ástæðum
* Það má búa til klasa sem erfir ExceptionFilterAttribute eða ActionFilterAttribute, þennan klasa er svo hægt að setja inn í WebApiConfig klasan í Register fallið og þá virkar hann fyrir alla controllera, config.Filters.Add(..
* Síðan má setja þetta attribute fyrir ofan controller föll: [AddExceptionFilter] og þá virkar filterinn bara á það tiltekna fall, og þá er líka sleppt að bæta exception klasanum við Web-Api config
* ATH það má bara vera með einn

Hvaða 3 leiðir eru í boði til að tengja ExceptionFilter inn í WebApi
* By action, fyrir ofan controller föll: [AddExceptionFilter] 
* By controller, fyrir ofan controller klasa: [AddExceptionFilter]
* Globally, bæta við í Web-Api config

Hvernig má kasta villum á mismunandi tungumálum
* Það er einmitt gert með því að útfæra klasa sem erfir frá ExceptionFilterAttribute, sá klasi overridar OnException fallið, tekur við villuskilaboðum og parsar þau, flettir svo upp í resorce skrá eftir réttum villuboðum og endurkastar villunni

Hvernig má kasta HTTP villum með ákv. error kóða
* Það er hægt að nota: throw new HttpResponseException(HttpStatusCode.NotFound), og tilgreina þar villukóða sem á að kasta, 
* Það er einnig hægt að smíða bara HttpError frá grunni, HttpError error = new HttpError(); error.Add(...

Hvað villur ná ExceptionFilters ekki að höndla 
* Exceptions sem koma frá smiðum controllera
* Exceptions sem koma fra message handlers
* Exceptions sem koma v. routing
* Exceptions sem koma þegar það er verið að serializa response content 

Hvernig má höndla þessar villur sem ExceptionFilter grípur ekki
* Það má búa til klasa sem erfir frá ExceptionLogger sem útæfrir IExceptionLogger og yfirskrifa föll þar 
* Síðan þarf bara að bæta þessu við í global config fyrir Web-Apan, config.Services.Add(typeof(IExceptionLogger), new TraceExceptionLogger());
* Það má vera með fleiri en einn svona logger

Hvernig má höndla villur sem ekki eru gripnar af ExceptionFilter (Global error handling) 
* Það má búa til klasa sem erfir frá ExceptionHandler og replace-a í config default ExceptionHandlerinn
* Síðan má yfirskrifa Handler fallið og grípa villuna þar og parsa hana, smíða svo skiljanleg villuboð að skila til clients, public override void Handle(ExceptionHandlerContext context)
* Þennan handler þarf að virkja í global config, config.Services.Replace(typeof(IExceptionHandler), new CourseAPIExceptionHandler());
* Ath það má bara vera með einn svona handler pr. forrit

Hvernig er best að bæta við tracing í Web-Api
* Það þarf að installa Microsoft.AspNet.WebApi.Tracing
* Síðan þarf að setja þetta í Global config, SystemDiagnosticsTraceWriter traceWriter = config.EnableSystemDiagnosticsTracing();
* Til að stilla trace level má setja, traceWriter.IsVerbose = true; og fá villu detail, og svo má stilla trace level,    traceWriter.MinimumLevel = TraceLevel.Debug; þetta er gert í global config
* Síðan þarf að kalla í tracing í þeim föllum sem á að trace, Configuration.Services.GetTraceWriter().Info(Request, "Get", "Get the list of LanguageViewModel.");

Hvernig má búa til custom trace writer
* Það þarf að útfæra klasa sem útfærir ITraceWriter.   
* Með því að gera þetta sjálfur má ma. skrifa trace result í skrá
* Í global config þarf að replace default tracer, config.Services.Replace(typeof(ITraceWriter), new CourseAPITracer());
* ATH það er bara hægt að hafa einn trace writer virkan í einu Web-Api forriti

##Authentication
Hvað er OAuth
* Open authorization, þessi protocol gerir notendum kleyft að gefa aðgengi að private upplýsingum um sig á einni vefsíðu til annarar vefsíðu án þess að deila usernafni og passwordi yfir á hina síðuna.  Það er ss. hægt að nota sama identity til að logga sig inn á margar síður.  Sbr. login with Facebook :)

Hvaða breytingar eru í OAuth 1.0
* Hér kemur til sögunar resource owner, þ.e. auðkenningar-þjónusta.   Clientin þarf því að biðja um aðgang að gögnum í gegnum þennan resource þjón, fær til baka token og matching shared-secret sem hann getur svo notað til að nálgast upplýsingar.  Markmiðið með þessu er að þurfa ekki að senda notenda-upplýsingar á clientin, hægt er að gefa út tóka sem hafa ákveðin gildistíma og takmarkaðar aðgangsheimildir 

Hvaða kemur svo nýtt í OAuth 2.0
* Þetta er víst gölluð útgáfa og ekki mælt með að nota hana

Hver er munurinn á OAuth og OpenId
* OAuth skilgreinir access toka sem gefa aðgang að providerum, OpenId býr til identity toka sem eru bara til þess að auðkenna notedur og þessir tókar eru notaðir til að fá aðgang að clientum
* OpenId byggir á OAuth 2.0 

Lýsið hvernig notandi tengist með OpenId
* The Client sends a request to the OpenID Provider.
* The OpenID Provider authenticates the End-User and obtains authorization.
* The OpenID Provider responds with an ID Token and usually an Access Token.
* The Client can send a request with the Access Token to the UserInfo Endpoint.
* The UserInfo Endpoint returns Claims about the End-User.

OpenId skilar upplýsingum um notenda í form token sem inniheldur scopes og claims þegar notandi er búin að auðkenni sig, það eru 3 megin aðferðir sem eru skilgreindar sem Flow til að gera þetta, lýsið þeim
* Code Flow:
  * The client sends an authentication request to the OpenID provider.
  * The OpenID provider authenticates the user (on behalf of the client) and responds with an authorization code to the client.
  * The client requests an id token with the authorization code.
  * The client validates the token and retrives the user information.
* Implicit Fow:
  * The client sends an authentication request to the OpenID provider.
  * The OpenID provider authenticates the user (on behalf of the client) and redirects him/her to the client with an id token.
  * The client validates the token and retrieves the user information.
* Hybrid Flow: This flow is basically a mix of the other two, which means that in some cases the authorization process is return to the client with a code and sometimes with an id token directly.

Á hvaða formati eru Id token
* JSON Web Token

##OData
Hvað er OData?
* OData er protocol sem lýsir samræmdri aðferð fyrir REST þjónustur til að skila gögnum frá sér, einnig er hægt að breyta gögnum í gegnum þennan protocol
* Það er hægt að gera fyrirspurnir á gögn, OD styður nokkur query options, dæmi:
  * search, finnum "cool beer" http://.../odata/Products?$search="ee"  -- leitar að öllum strengum með "ee"
  * filter, finnum öll verð sem eru minna en 10 http://.../odata/Products?$filter=Price lt 10.00
  * count, http://.../odata/Products?$count=true virkar eins og sql fyrirspurn, grúppar og telur 
  * select, selectar ákveðnar færslur, http://../odata/Products?$select=Price  -- hér er það "Price"
  * svo er top, skip, expand (gefur tengdar færslur líka), format (fromatar outputið)
  * svo má chaina þessum leitarskylirðum saman

##ETags
Hvað er ETag og hvað gerir það
* Þetta er einkvæmt auðkenni pr. url eða resource, ef urlið breytist þá þarf að gefa því nýtt ETag
* ETag er notað þegar gögn eru geymd í minni (chace) á serverum til að flýta fyrirspurnum og einnig til að koma í veg fyrir að það þurfi að fara margoft í gagnagrunn til að sækja sömu gögn
* Client fær ETag til baka með niðurstöðum úr fyrirspurn frá server 
* Þegar Client gerir svo sömu fyrirspurn þá sendir hann ETagið með ásamt "If-None-Match" header, ef gögn eru til í chace þá fær hann þau ásamt http status kóða 304 HTTP response (Not modified), ath serverinn ber ETagið saman við síðustu fyrirspurn (url) frá client til að athuga hvort hún hafi eitthvað breyst. 
* Þegar Client ætlar að uppfæra gögn þá sendir hann "If-Match" header með, og ef ETag matchar ekki við nýjustu útgáfu af gögnum þá skilar server 412 HTTP response (Precondition Failed), þ.e í ETag-i er version númer á gögnum sem verið er að ná í
* stundum eru ETags með prefix /w, það þýðir að það sé week og er bara geymt í minni á server 

##CacheCow
Hvað gerir ChaceChow library 
* Það útfærir caching bæði á client og server, notar message handlers og in-memory database til að halda utan um þetta
* Til að bæta þessu við Web-Apa þá þarf að adda þessu í config fallið, var cacheCowCacheHandler = new CachingHandler(config); config.MessageHandlers.Add(cacheCowCacheHandler)

##CacheOutput
Hvað notar þetta library til að cacha gögn
* Það nota attribute
* Hægt að stilla ClientTimeSpan og ServerTimeSpan, sett fyrir ofan fall [ChacheOutput(ClientTimeSpan = 20, ServerTimeSpan = 30)]
* Það eru fleiri property sem hægt er að stilla, MustRevalidate, ExcludeQueryStringFromCacheKey, AnonymousOnly
* Notar líka ETags

##Vefþjónustur af hverju?
* Leyfa öðrum forriturum að nálgast gögn frá okkur
* Aðskilur betur bakenda og framenda á veflausnum
* Vefþjónustur er hægt að skrifa á mismuanndi1 forritunarmálum, en front endin breytist ekki við það getur verið í allt öðru umhverfi
* Aðrir forritara gætu fundið leiðir til að sýna gögnin á nýjan og spennandi hátt

##Python og bakendaforritun
Af hverju er bakendin svona mikilvægur
* Hann er jú hjartað í lausninni
* Bakendi þarf að vera skilvirkur, Öruggur, Skalanlegur, Vel aðgengilegur, Viðhaldanlegur, Rekstrarlega hagkvæmur og Kostnaður í lágmarki
* Það þarf að hanna kerfið þannig frá upphafi svo hægt sé að stækka það
* Flest tólin sem við notum eru skalanleg og geta orðið að klusterum

Hvað er virtualenv í Linux og Mac?
* Virtualenv er tól sem gerir okkur kleyft að setja upp alls kona pakka og dót í sýndar umhverfi(möppu) fyrir lausn sem við erum að forrita án þess að menga stýrikerfið okkar af þessu dóti, þ.e. pökkum er installað locally í ákv. folder en ekki globaly á stýrikerfinu.   Virtualenv sér svo um að loda þessum pökkum fyrir okkur þegar við virkjum það, source ./venv/bin/activate

Hvað er PIP?
* Það er tók sem við getum notað sem downloda og installar Python pökkum
* pip Freeze > requierments.txt, skrifar dependency's í skrá sem svo er hægt að nota til að installa forritinu seinna meir
* pip install -r requierments.txt, setur upp allt sem er í þessari skrá

Hvað er Flask
* Það er lightweight web framework fyrir Python, 
* Flask er svokallað micro framework, góður kjarni, routing, meðhöndlun á HTTP protocol, og auðvelt að bæta við extensionum
* Í Flask er engin stuðningur við database, eða form validation, hins vegar er hægt að bæta þessu við með því að installa add-inum
* Í fyrstu var þetta aprílgabb frá einum gæja, en það tóku það margir vel í þetta að þetta varð að veruleika
* Flask byggir á Werkzeug (HTTP og WSGI library fyrir Python) og Jinja1 (Template framework fyrir Python) 

Hvað er Flask Restuful
* Extension á Flask sem gerir það auðvelt að búa til Rest þjónustur í Flask

Hver er munurinn á Flask og .Net Web Apa
* ??

Hvað er Curl og hvað gerir það
* Með Curl er hægt að krafta köll í API og testa þær, hægt að nota Post, Get, Put, Patch ofl.
* Gamalt og gott Linux tól sem engin fær leið á

Hvernig skrifar maður Flask Restful service, hvernig er uppbyggingin?
* app.py - er með meðhöndlun á routing og grípur POST, GET etc, skrifar í database eða sækir og renderar html með gögnum
* db.py - keyrir upp database instance, í þessu tilfelli SQL Alchemy
* manage.py - er með fall til að búa til gagnagrunn og keyra upp Rest þjónustuna (main fall)
* models.py - geymir entity klasa og tengingu við database töflur
* templates - mappa sem geymir öll html skjöl

Hvað er Memcached ?
* Er caching kerfi sem er hægt að nota fyrir flest forrit sem þurfa að geyma og sækja gögn í database
* Memchace er þá notað til geyma gögn í minni til að forðast það að þurfa að fara í gagnagrunn og þar með hraða fyrirspurnum margfalt
* Memcache er með risa stóra hash töflu sem hægt er að dreifa á margar vélar, þegar hash taflan er full þá er eldri gögnum ýtt á annað minnissvæði LRU, least recently used.  Forrit sem nota þessa lausn bæta við gögnum og fyrirspurnum í RAM áður en það er skráð í gagnagrunn. 
* Oft er stræð hash töflunar mikil, og getur memchace grunnur farið í mörg GB, Memchace er jafn góð lausn þar sem fyrirspurnatíðni er há eða kostnaður við að sækja gögn er mikill (tími)

Hvað er Node.js?
* Þetta er open source, cross-platform umhverfi fyrir service forrit og vef þjóna.    Node.js er skrifað í JavaScript, og er keyrt með Node.js runtime.  
* Node.js is single threaded and asynchronous
* Node.js forrit munu alltaf keyra án þess að stoppa, jafnvel þó að TimeOutFunction sé implementuð, þá keyrir kóðin á eftir henni fyrst en umhverfið býr bara til task úr TimeOutFunction og stilla biðtíma, eftir bíðtíman fær forritið interrupt og keyrir þetta fall.  Ástæðan fyrir þessu er sú að Node.js er single threaded. 
* Node.js byggir á V8 virtual vél Google.  Java script keyrir alltaf í umhverfi node.js keyrir server side. 
* Node.js leggur áhersu á network forritun

Ef Node.js er single threaded hvernig höndlar það þá margar fyrirspurnir ?
* The first client connects and asks for data from the database. Nodejs sends a request to the database and while it waits for the response from the database it handles other clients requests. When the database is finished getting the data and sends the response back to nodejs. Nodejs gets an interrupt signal, receives the data and gives it to the first client that connected and was asking for this data.

Hvað er MongoDB?
* NpSql database, gögn eru geymd í skrám (document based db)
* Gögn eru geymd í collection, gögn eru geymd á JSON like formati, e.g. binary json string kallað BISON.
* Forritarar eru ekki bundnir af því að geyma eins BISON object í sama collection, þar af leiðandi geta gögn í einu collection oft orðið ansi sundurleit
* Kosturinn er sá að BISON er mjög líkt JSON svo gögn eru geymd svo gott sem á sama formati og þeim er skilað í client
* Data integrity er ekki mikið þar sem engin tengsl eru á milli collection-a og í höndum forritara að tryggj að gögn séu í lagi
* Endurtekning á sömu gögnum getur komið oft fyrir þar sem erfitt er að tékka sig af hvort það er búið að vista þau
* MongoDB er mjög hraðvirkur þegar kemur að því að leita og vista og getur í sumum tilfellum verið margfalt hraðari en hefðbundin database
* MongoDB styður Indexa og er hægt að indexa collection á ákv. field
* MongoDB úthlutar einnig Id á colleciton er það field sett sjálfkrafa inn með öllum gögnum sem eru skráð
* MongoDB leyfir ekki að sama id í collection sé vistað tvisvar
* 

Hvað er Sharding í MongoDB
* Það er leið til að geyma gögn á mörgum serverum
* Í MongoDB er mjög auðvelt að geyma gögn dreift, 

Hvað er ElasticSearch og hvernig virkar það ?
* ElasticSearch er leitar server byggður á Lucene, er með öfluga texta leitarvél með RestFul vef viðmóti og schema-free JSON skjölum sem geyma gögnin. 
* Algent er að nota ES til að replicata gögn sem eru geymd í gagnagrunnum og nota leitarvélina til að leita að gögnum sem eru jafnvel geymt í mismunandi skjölum.
* ES er býður upp á mjög hraða texta-leitarvél og hefur sitt eigið fyrispurnarmál Query DSL (Domain Specific Language) til að búa til fyrirspurnir 
* Ef tvö eintök (node) af ES eru sett upp á sama networki þá reyna þau að smeinast, clustring í ES er mjög öflugt. 


